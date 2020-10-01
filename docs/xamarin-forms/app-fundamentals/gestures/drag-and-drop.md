---
title: 끌어서 놓기 제스처 인식기 추가
description: 이 문서에서는 Xamarin.Forms를 사용하여 끌어서 놓기 제스처를 인식하는 방법을 설명합니다.
ms.prod: xamarin
ms.assetid: 4CB2F270-908A-4A89-B852-70BC04066E8C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/04/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: d3eb7edbb24c7e28ee375e1de85f6a7597ec63ac
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91561017"
---
# <a name="add-drag-and-drop-gesture-recognizers"></a>끌어서 놓기 제스처 인식기 추가

![시험판 API](~/media/shared/preview.png)

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithgestures-draganddropgesture/)

끌어서 놓기 제스처를 사용하면 한 번의 연속 제스처를 사용하여 항목 및 연결된 데이터 패키지를 화면의 한 위치에서 다른 위치로 끌어올 수 있습니다. 끌어서 놓기는 단일 애플리케이션에서 수행되거나 한 애플리케이션에서 시작하여 다른 애플리케이션에서 끝날 수 있습니다.

> [!IMPORTANT]
> Xamarin.Forms 끌어서 놓기 제스처 인식기는 현재 실험적이며 `DragAndDrop_Experimental` 플래그를 설정해야만 사용할 수 있습니다. 자세한 내용은 [실험적 플래그](~/xamarin-forms/internals/experimental-flags.md)를 참조하세요.
>
> 끌어서 놓기 제스처 인식은 iOS, Android 및 UWP(유니버설 Windows 플랫폼)에서 지원됩니다. 그러나 iOS에서는 최소 iOS 11의 플랫폼이 필요합니다.

끌기 제스처가 시작되는 요소인 끌기 원본은 데이터 패키지 개체를 채워서 전송할 데이터를 제공할 수 있습니다. 끌기 원본이 해제되면 놓기가 발생합니다. 그러면 끌기 원본 아래의 요소인 놓기 대상이 데이터 패키지를 처리합니다.

애플리케이션에서 끌어서 놓기를 사용 설정하는 프로세스는 다음과 같습니다.

1. `DragGestureRecognizer` 개체를 `GestureRecognizers` 컬렉션에 추가하고 `DragGestureRecognizer.CanDrag` 속성을 `true`로 설정하여 특정 요소에 대한 끌기를 사용 설정합니다. 자세한 내용은 [끌기 사용](#enable-drag)을 참조하세요.
1. [선택 사항] 데이터 패키지를 빌드합니다. Xamarin.Forms는 이미지 및 텍스트 컨트롤에 대해 자동으로 데이터 패키지를 채우지만 다른 콘텐츠에 대해서는 자체 데이터 패키지를 빌드해야 합니다. 자세한 내용은 [데이터 패키지 빌드](#build-a-data-package)를 참조하세요.
1. `DropGestureRecognizer` 개체를 `GestureRecognizers` 컬렉션에 추가하고 `DropGestureRecognizer.AllowDrop` 속성을 `true`로 설정하여 특정 요소에 대한 놓기를 사용 설정합니다. 자세한 내용은 [놓기 사용](#enable-drop)을 참조하세요.
1. [선택 사항] `DropGestureRecognizer.DragOver` 이벤트를 처리하여 놓기 대상에서 허용하는 작업 유형을 표시합니다. 자세한 내용은 [DragOver 이벤트 처리](#handle-the-dragover-event)를 참조하세요.
1. [선택 사항] 데이터 패키지를 처리하여 놓인 콘텐츠를 검색합니다. Xamarin.Forms는 자동으로 데이터 패키지에서 이미지 및 텍스트 데이터를 검색하지만 다른 콘텐츠에 대해서는 데이터 패키지를 처리해야 합니다. 자세한 내용은 [데이터 패키지 처리](#process-the-data-package)를 참조하세요.

> [!NOTE]
> [`CollectionView`](xref:Xamarin.Forms.CollectionView) 간의 항목 끌기는 현재 지원되지 않습니다.

## <a name="enable-drag"></a>끌기 사용

Xamarin.Forms에서 끌기 제스처 인식은 `DragGestureRecognizer` 클래스에 의해 제공됩니다. 이 클래스는 다음과 같은 속성을 정의합니다.

- `bool` 형식의 `CanDrag` - 제스처 인식기가 연결된 요소가 끌기 원본이 될 수 있는지 여부를 나타냅니다. 이 속성의 기본값은 `false`입니다.
- `ICommand` 형식의 `DragStartingCommand` - 끌기 제스처가 처음 인식되면 실행됩니다.
- `object` 형식의 `DragStartingCommandParameter` - `DragStartingCommand`에 전달되는 매개 변수입니다.
- `ICommand` 형식의 `DropCompletedCommmand` - 끌기 원본을 놓으면 실행됩니다.
- `object` 형식의 `DropCompletedCommandParameter` - `DropCompletedCommand`에 전달되는 매개 변수입니다.

이러한 속성은 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) 개체에서 지원하며, 따라서 데이터 바인딩의 대상이 될 수 있고 스타일이 지정될 수 있습니다.

`DragGestureRecognizer` 클래스는 `DragStarting` 및 `DropCompleted` 이벤트도 정의합니다. `DragGestureRecognizer` 개체는 끌기 제스처를 감지하면 `DragStartingCommand`를 실행하고 `DragStarting` 이벤트를 호출합니다. 그런 다음 `DragGestureRecognizer` 개체는 놓기 제스처 완료를 감지하면 `DropCompletedCommand`를 실행하고 `DropCompleted` 이벤트를 호출합니다.

`DragStarting` 이벤트와 함께 제공되는 `DragStartingEventArgs` 개체는 다음 속성을 정의합니다.

- `bool` 형식의 `Handled` - 이벤트 처리기가 이벤트를 처리했는지 여부 또는 Xamarin.Forms가 자체 처리를 계속할지 여부를 나타냅니다.
- `bool` 형식의 `Cancel` - 이벤트를 취소할지 여부를 나타냅니다.
- `DataPackage` 형식의 `Data` - 끌기 원본과 함께 제공되는 데이터 패키지를 나타냅니다. 이 속성은 읽기 전용입니다.

`DropCompleted` 이벤트와 함께 제공되는 `DropCompletedEventArgs` 개체에는 `DataPackageOperation` 형식의 읽기 전용 `DropResult` 속성이 있습니다. `DataPackageOperation` 열거형에 대한 자세한 내용은 [DragOver 이벤트 처리](#handle-the-dragover-event)를 참조하세요.

다음 XAML 예제에서는 [`Image`](xref:Xamarin.Forms.Image)에 연결된 `DragGestureRecognizer`를 보여 줍니다.

```xaml
<Image Source="monkeyface.png">
    <Image.GestureRecognizers>
        <DragGestureRecognizer CanDrag="True" />
    </Image.GestureRecognizers>
</Image>
```

이 예제에서는 [`Image`](xref:Xamarin.Forms.Image)에서 끌기 제스처를 시작할 수 있습니다.

> [!TIP]
> iOS, Android 및 UWP에서 끌기 제스처는 길게 누른 다음 끌기로 시작합니다.

## <a name="build-a-data-package"></a>데이터 패키지 빌드

Xamarin.Forms는 다음과 같은 컨트롤에 대해 끌기가 시작되면 자동으로 데이터 패키지를 빌드합니다.

- 텍스트 컨트롤. 텍스트 값은 [`CheckBox`](xref:Xamarin.Forms.CheckBox), [`DatePicker`](xref:Xamarin.Forms.DatePicker), [`Editor`](xref:Xamarin.Forms.Editor), [`Entry`](xref:Xamarin.Forms.Entry), [`Label`](xref:Xamarin.Forms.Label), [`RadioButton`](xref:Xamarin.Forms.RadioButton), [`Switch`](xref:Xamarin.Forms.Switch) 및 [`TimePicker`](xref:Xamarin.Forms.TimePicker) 개체에서 끌어올 수 있습니다.
- 이미지 컨트롤. 이미지는 [`Button`](xref:Xamarin.Forms.Button), [`Image`](xref:Xamarin.Forms.Image) 및 [`ImageButton`](xref:Xamarin.Forms.ImageButton) 컨트롤에서 끌어올 수 있습니다.

다음 표에서는 텍스트 컨트롤에서 끌기가 시작될 때 읽히는 속성과 시도되는 변환을 보여 줍니다.

| 제어 | 속성 | 변환 |
| --- | --- | --- |
| `CheckBox` | `IsChecked` | `bool`가 `string`로 변환됩니다. |
| `DatePicker` | `Date` | `DateTime`가 `string`로 변환됩니다. |
| `Editor` | `Text` ||
| `Entry` | `Text` ||
| `Label` | `Text` ||
| `RadioButton` | `IsChecked` | `bool`가 `string`로 변환됩니다. |
| `Switch` | `IsToggled` | `bool`가 `string`로 변환됩니다. |
| `TimePicker` | `Time` | `TimeSpan`가 `string`로 변환됩니다. |

텍스트 및 이미지 이외의 콘텐츠에 대해서는 데이터 패키지를 직접 빌드해야 합니다.

데이터 패키지는 다음 속성을 정의하는 `DataPackage` 클래스로 표현됩니다.

- `DataPackagePropertySet` 형식의 `Properties` - `DataPackage`에 포함된 데이터를 구성하는 속성의 컬렉션입니다. 이 속성은 읽기 전용 속성입니다.
- [`ImageSource`](xref:Xamarin.Forms.ImageSource) 형식의 `Image` - `DataPackage`에 포함된 이미지입니다.
- `string` 형식의 `Text` - `DataPackage`에 포함된 텍스트입니다.
- `DataPackageView` 형식의 `View` - `DataPackage`의 읽기 전용 버전입니다.

`DataPackagePropertySet` 클래스는 `Dictionary<string,object>`로 저장된 속성 모음을 나타냅니다. `DataPackageView` 클래스에 대한 자세한 내용은 [데이터 패키지 처리](#process-the-data-package)를 참조하세요.

### <a name="store-image-or-text-data"></a>이미지 또는 텍스트 데이터 저장

`DataPackage.Image` 또는 `DataPackage.Text` 속성에 데이터를 저장하여 이미지 또는 텍스트 데이터를 끌기 원본과 연결할 수 있습니다. 이 작업은 `DragStarting` 이벤트에 대한 처리기에서 수행할 수 있습니다.

다음 XAML 예제에서는 `DragStarting` 이벤트에 대한 처리기를 등록하는 `DragGestureRecognizer`를 보여 줍니다.

```xaml
<Path Stroke="Black"
      StrokeThickness="4">
    <Path.GestureRecognizers>
        <DragGestureRecognizer CanDrag="True"
                               DragStarting="OnDragStarting" />
    </Path.GestureRecognizers>
    <Path.Data>
        <!-- PathGeometry goes here -->
    </Path.Data>
</Path>
```

이 예제에서는 `DragGestureRecognizer`가 `Path` 개체에 연결됩니다. `DragStarting` 이벤트는 `OnDragStarting` 이벤트 처리기를 실행하는 `Path`에서 끌기 제스처가 감지되면 발생합니다.

```csharp
void OnDragStarting(object sender, DragStartingEventArgs e)
{
    e.Data.Text = "My text data goes here";
}
```

`DragStarting` 이벤트와 함께 제공되는 `DragStartingEventArgs` 개체에는 `DataPackage` 형식의 `Data` 속성이 있습니다. 이 예제에서는 `DataPackage` 개체의 `Text` 속성이 `string`으로 설정됩니다. 그런 다음 놓기에서 `DataPackage`에 액세스하여 `string`을 검색할 수 있습니다.

### <a name="store-data-in-the-property-bag"></a>속성 모음에 데이터 저장

이미지 및 텍스트를 비롯한 모든 데이터는 `DataPackage.Properties` 컬렉션에 데이터를 저장하여 끌기 원본과 연결할 수 있습니다. 이 작업은 `DragStarting` 이벤트에 대한 처리기에서 수행할 수 있습니다.

다음 XAML 예제에서는 `DragStarting` 이벤트에 대한 처리기를 등록하는 `DragGestureRecognizer`를 보여 줍니다.

```xaml
<Rectangle Stroke="Red"
           Fill="DarkBlue"
           StrokeThickness="4"
           HeightRequest="200"
           WidthRequest="200">
    <Rectangle.GestureRecognizers>
        <DragGestureRecognizer CanDrag="True"
                               DragStarting="OnDragStarting" />
    </Rectangle.GestureRecognizers>
</Rectangle>
```

이 예제에서는 `DragGestureRecognizer`가 `Rectangle` 개체에 연결됩니다. `DragStarting` 이벤트는 `OnDragStarting` 이벤트 처리기를 실행하는 `Rectangle`에서 끌기 제스처가 감지되면 발생합니다.

```csharp
void OnDragStarting(object sender, DragStartingEventArgs e)
{
    Shape shape = (sender as Element).Parent as Shape;
    e.Data.Properties.Add("Square", new Square(shape.Width, shape.Height));
}
```

`DragStarting` 이벤트와 함께 제공되는 `DragStartingEventArgs` 개체에는 `DataPackage` 형식의 `Data` 속성이 있습니다. `Dictionary<string, object>` 컬렉션인 `DataPackage` 개체의 `Properties` 컬렉션을 수정하여 필요한 데이터를 저장할 수 있습니다. 이 예제에서는 `Properties` 사전이 "Square" 키에 대해 `Rectangle` 크기를 나타내는 `Square` 개체를 저장하도록 수정됩니다.

## <a name="enable-drop"></a>놓기 사용

Xamarin.Forms에서 놓기 제스처 인식은 `DropGestureRecognizer` 클래스에서 제공합니다. 이 클래스는 다음과 같은 속성을 정의합니다.

- `bool` 형식의 `AllowDrop` - 제스처 인식기가 연결된 요소가 놓기 대상이 될 수 있는지 여부를 나타냅니다. 이 속성의 기본값은 `false`입니다.
- `ICommand` 형식의 `DragOverCommand` - 끌기 원본을 놓기 대상으로 끌면 실행됩니다.
- `object` 형식의 `DragOverCommandParameter` - `DragOverCommand`에 전달되는 매개 변수입니다.
- `ICommand` 형식의 `DropCommand` - 끌기 원본을 놓기 대상 위에 놓으면 실행됩니다.
- `object` 형식의 `DropCommandParameter` - `DropCommand`에 전달되는 매개 변수입니다.

이러한 속성은 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) 개체에서 지원하며, 따라서 데이터 바인딩의 대상이 될 수 있고 스타일이 지정될 수 있습니다.

`DropGestureRecognizer` 클래스는 `DragOver` 및 `Drop` 이벤트도 정의합니다. `DropGestureRecognizer`는 놓기 대상 위에서 끌기 원본을 인식하면 `DragOverCommand`를 실행하고 `DragOver` 이벤트를 호출합니다. 그런 다음 `DropGestureRecognizer`는 놓기 대상 위에서 놓기 제스처를 인식하면 `DropCommand`를 실행하고 `Drop` 이벤트를 호출합니다.

`DragOver` 이벤트와 함께 제공되는 `DragEventArgs` 클래스는 다음 속성을 정의합니다.

- `DataPackage` 형식의 `Data` - 끌기 원본과 연결된 데이터를 포함합니다. 이 속성은 읽기 전용입니다.
- `DataPackageOperation` 형식의 `AcceptedOperation` - 놓기 대상에서 허용하는 작업 유형을 지정합니다.

`DataPackageOperation` 열거형에 대한 자세한 내용은 [DragOver 이벤트 처리](#handle-the-dragover-event)를 참조하세요.

`Drop` 이벤트와 함께 제공되는 `DropEventArgs` 클래스는 다음 속성을 정의합니다.

- `DataPackageView` 형식의 `Data` - 데이터 패키지의 읽기 전용 버전입니다.
- `bool` 형식의 `Handled` - 이벤트 처리기가 이벤트를 처리했는지 여부 또는 Xamarin.Forms가 자체 처리를 계속할지 여부를 나타냅니다.

다음 XAML 예제에서는 [`Image`](xref:Xamarin.Forms.Image)에 연결된 `DropGestureRecognizer`를 보여 줍니다.

```xaml
<Image BackgroundColor="Silver"
       HeightRequest="300"
       WidthRequest="250">
    <Image.GestureRecognizers>
        <DropGestureRecognizer AllowDrop="True" />
    </Image.GestureRecognizers>
</Image>
```

이 예제에서는 끌기 원본이 [`ImageSource`](xref:Xamarin.Forms.ImageSource)인 경우 끌기 원본을 [`Image`](xref:Xamarin.Forms.Image) 놓기 대상 위에 놓으면 끌기 원본이 놓기 대상에 복사됩니다. 이는 Xamarin.Forms가 끌어온 이미지 및 텍스트를 호환되는 놓기 대상에 자동으로 복사하기 때문입니다.

## <a name="handle-the-dragover-event"></a>DragOver 이벤트 처리

필요에 따라 `DropGestureRecognizer.DragOver` 이벤트를 처리하여 놓기 대상에서 허용하는 작업 유형을 표시할 수 있습니다. 이 작업을 수행하려면 `DragOver` 이벤트와 함께 제공되는 `DragEventArgs` 개체의 `AcceptedOperation` 속성(`DataPackageOperation` 형식)을 설정합니다.

`DataPackageOperation` 열거형은 다음 멤버를 정의합니다.

- `None` - 수행할 작업이 없음을 나타냅니다.
- `Copy` - 끌기 원본 콘텐츠가 놓기 대상에 복사됨을 나타냅니다.

> [!IMPORTANT]
> `DragEventArgs` 개체가 만들어지면 `AcceptedOperation` 속성은 기본적으로 `DataPackageOperation.Copy`로 설정됩니다.

다음 XAML 예제에서는 `DragOver` 이벤트에 대한 처리기를 등록하는 `DropGestureRecognizer`를 보여 줍니다.

```xaml
<Image BackgroundColor="Silver"
       HeightRequest="300"
       WidthRequest="250">
    <Image.GestureRecognizers>
        <DropGestureRecognizer AllowDrop="True"
                               DragOver="OnDragOver" />
    </Image.GestureRecognizers>
</Image>
```

이 예제에서는 `DropGestureRecognizer`가 [`Image`](xref:Xamarin.Forms.Image) 개체에 연결됩니다. `DragOver` 이벤트는 끌기 원본을 놓기 대상 위로 끌었지만 아직 놓지 않은 경우 발생합니다(놓으면 `OnDragOver` 이벤트 처리기가 실행됨).

```csharp
void OnDragOver(object sender, DragEventArgs e)
{
    e.AcceptedOperation = DataPackageOperation.None;
}
```

이 예제에서는 `DragEventArgs` 개체의 `AcceptedOperation` 속성이 `DataPackageOperation.None`으로 설정됩니다. 이렇게 하면 끌기 원본이 놓기 대상 위에 놓일 때 아무 동작도 수행되지 않습니다.

## <a name="process-the-data-package"></a>데이터 패키지 처리

`Drop` 이벤트는 끌기 원본을 놓기 대상 위에서 해제하면 발생합니다. 이 경우 Xamarin.Forms는 다음과 같은 컨트롤 위에 끌기 원본이 놓이면 자동으로 데이터 패키지에서 데이터를 검색하려고 시도합니다.

- 텍스트 컨트롤. 텍스트 값은 [`CheckBox`](xref:Xamarin.Forms.CheckBox), [`DatePicker`](xref:Xamarin.Forms.DatePicker), [`Editor`](xref:Xamarin.Forms.Editor), [`Entry`](xref:Xamarin.Forms.Entry), [`Label`](xref:Xamarin.Forms.Label), [`RadioButton`](xref:Xamarin.Forms.RadioButton), [`Switch`](xref:Xamarin.Forms.Switch) 및 [`TimePicker`](xref:Xamarin.Forms.TimePicker) 개체 위에 놓을 수 있습니다.
- 이미지 컨트롤. 이미지는 [`Button`](xref:Xamarin.Forms.Button), [`Image`](xref:Xamarin.Forms.Image) 및 [`ImageButton`](xref:Xamarin.Forms.ImageButton) 컨트롤 위에 놓을 수 있습니다.

다음 표에서는 텍스트 기반 끌기 원본이 텍스트 컨트롤 위에 놓일 때 설정되는 속성과 시도되는 변환을 보여 줍니다.

| 제어 | 속성 | 변환 |
| --- | --- | --- |
| `CheckBox` | `IsChecked` | `string`이 `bool`로 변환됩니다. |
| `DatePicker` | `Date` | `string`이 `DateTime`으로 변환됩니다. |
| `Editor` | `Text` ||
| `Entry` | `Text` ||
| `Label` | `Text` ||
| `RadioButton` | `IsChecked` | `string`이 `bool`로 변환됩니다. |
| `Switch` | `IsToggled` | `string`이 `bool`로 변환됩니다. |
| `TimePicker` | `Time` | `string`이 `TimeSpan`으로 변환됩니다. |

텍스트 및 이미지 이외의 콘텐츠에 대해서는 데이터 패키지를 직접 처리해야 합니다.

`Drop` 이벤트와 함께 제공되는 `DropEventArgs` 클래스는 `DataPackageView` 형식의 `Data` 속성을 정의합니다. 이 속성은 데이터 패키지의 읽기 전용 버전을 나타냅니다.

### <a name="retrieve-image-or-text-data"></a>이미지 또는 텍스트 데이터 검색

`Drop` 이벤트에 대한 처리기에서 `DataPackageView` 클래스에 정의된 메서드를 사용하여 데이터 패키지에서 이미지 또는 텍스트 데이터를 검색할 수 있습니다.

`DataPackageView` 클래스에는 `GetImageAsync` 및 `GetTextAsync` 메서드가 포함됩니다. `GetImageAsync` 메서드는 `DataPackage.Image` 속성에 저장된 데이터 패키지에서 이미지를 검색하고 `Task<ImageSource>`를 반환합니다. 마찬가지로 `GetTextAsync` 메서드는 `DataPackage.Text` 속성에 저장된 데이터 패키지에서 텍스트를 검색하고 `Task<string>`을 반환합니다.

다음 예제에서는 `Path`에 대한 데이터 패키지에서 텍스트를 검색하는 `Drop` 이벤트 처리기를 보여 줍니다.

```csharp
async void OnDrop(object sender, DropEventArgs e)
{
    string text = await e.Data.GetTextAsync();

    // Perform logic to take action based on the text value.
}
```

이 예제에서는 `GetTextAsync` 메서드를 사용하여 데이터 패키지에서 텍스트 데이터를 검색합니다. 그런 다음 텍스트 값을 기반으로 하는 작업을 수행할 수 있습니다.

### <a name="retrieve-data-from-the-property-bag"></a>속성 모음에서 데이터 검색

`Drop` 이벤트에 대한 처리기에서 데이터 패키지의 `Properties` 컬렉션에 액세스하여 데이터 패키지에서 데이터를 검색할 수 있습니다.

`DataPackageView` 클래스는 `DataPackagePropertySetView` 형식의 `Properties` 속성을 정의합니다. `DataPackagePropertySetView` 클래스는 `Dictionary<string, object>`로 저장된 읽기 전용 속성 모음을 나타냅니다.

다음 예제에서는 `Rectangle`에 대한 데이터 패키지의 속성 모음에서 데이터를 검색하는 `Drop` 이벤트 처리기를 보여 줍니다.

```csharp
void OnDrop(object sender, DropEventArgs e)
{
    Square square = (Square)e.Data.Properties["Square"];

    // Perform logic to take action based on retrieved value.
}
```

이 예제에서는 "Square" 사전 키를 지정하여 데이터 패키지의 속성 모음에서 `Square` 개체를 검색합니다. 그런 다음 검색된 값을 기반으로 하는 작업을 수행할 수 있습니다.

## <a name="related-links"></a>관련 링크

- [끌어서 놓기 제스처(샘플)](/samples/xamarin/xamarin-forms-samples/workingwithgestures-draganddropgesture/)
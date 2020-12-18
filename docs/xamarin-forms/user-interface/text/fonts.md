---
title: 글꼴 Xamarin.Forms
description: 이 문서에서는 응용 프로그램에 텍스트를 표시 하는 컨트롤에 대 한 글꼴 정보를 지정 하는 방법을 설명 합니다 Xamarin.Forms .
ms.prod: xamarin
ms.assetid: 49DD2249-C575-41AE-AE06-08F890FD6031
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 11/04/2020
ms.custom: contperf-fy21q2
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 146c67655c420611b2a0901efa6cc22ef780713e
ms.sourcegitcommit: c5e72d2ca4152b62ab6583f0dbe84b3ba29d8283
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97677541"
---
# <a name="fonts-in-no-locxamarinforms"></a>글꼴 Xamarin.Forms

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](/samples/xamarin/xamarin-forms-samples/workingwithfonts)

기본적으로에서는 Xamarin.Forms 각 플랫폼에서 정의 된 시스템 글꼴을 사용 합니다. 그러나 텍스트를 표시 하는 컨트롤은이 글꼴을 변경 하는 데 사용할 수 있는 속성을 정의 합니다.

- `FontAttributes`. 형식의 이며,, `FontAttributes` 및 라는 세 개의 멤버가 포함 된 열거형입니다. `None` `Bold` `Italic` 이 속성의 기본값은 `None`입니다.
- `double` 형식의 `FontSize`
- `string` 형식의 `FontFamily`

이러한 속성은 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) 개체에서 지원하며, 따라서 데이터 바인딩의 대상이 될 수 있고 스타일이 지정될 수 있습니다.

## <a name="set-font-attributes"></a>글꼴 특성 설정

텍스트를 표시 하는 컨트롤은 `FontAttributes` 속성을 설정 하 여 글꼴 특성을 지정할 수 있습니다.

```xaml
<Label Text="Italics"
       FontAttributes="Italic" />
<Label Text="Bold and italics"
       FontAttributes="Bold, Italic" />
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
Label label1 = new Label
{
    Text = "Italics",
    FontAttributes = FontAttributes.Italic
};

Label label2 = new Label
{
    Text = "Bold and italics",
    FontAttributes = FontAttributes.Bold | FontAttributes.Italic
};    
```

## <a name="set-the-font-size"></a>글꼴 크기 설정

텍스트를 표시 하는 컨트롤은 `FontSize` 속성을 설정 하 여 글꼴 크기를 지정할 수 있습니다. `FontSize`속성은 `double` 값을 직접 또는 열거형 값으로 설정할 수 있습니다 [`NamedSize`](xref:Xamarin.Forms.NamedSize) .

```xaml
<Label Text="Font size 24"
       FontSize="24" />
<Label Text="Large font size"
       FontSize="Large" />
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
Label label1 = new Label
{
    Text = "Font size 24",
    FontSize = 24
};

Label label2 = new Label
{
    Text = "Large font size",
    FontSize = Device.GetNamedSize(NamedSize.Large, typeof(Label))
};
```

또는 메서드는 `Device.GetNamedSize` 두 번째 인수를로 지정 하는 재정의를 포함 합니다 [`Element`](xref:Xamarin.Forms.Element) .

```csharp
Label myLabel = new Label
{
    Text = "Large font size",
};
myLabel.FontSize = Device.GetNamedSize(NamedSize.Large, myLabel);
```

> [!NOTE]
> `FontSize`로 지정 된 값은 `double` 장치 독립적 단위로 측정 됩니다. 자세한 내용은 [측정 단위](~/xamarin-forms/user-interface/controls/common-properties.md#units-of-measurement)를 참조 하세요.

명명 된 글꼴 크기에 대 한 자세한 내용은 [명명 된 글꼴 크기 이해](#understand-named-font-sizes)를 참조 하세요.

## <a name="set-the-font-family"></a>글꼴 패밀리 설정

텍스트를 표시 하는 컨트롤은 `FontFamily` 속성을 글꼴 패밀리 이름 (예: "Times Roman")으로 설정할 수 있습니다. 그러나이는 특정 플랫폼에서 해당 글꼴 패밀리가 지원 되는 경우에만 작동 합니다.

플랫폼에서 사용할 수 있는 글꼴을 파생 시키는 데 사용할 수 있는 여러 가지 기술이 있습니다. 그러나 .TTF (True 형식 형식) 글꼴 파일의 존재는 반드시 글꼴 패밀리를 의미 하는 것은 아니며 응용 프로그램에서 사용 하기에 적합 하지 않은 경우가 많습니다. 또한 플랫폼에 설치 된 글꼴은 플랫폼 버전으로 변경 될 수 있습니다. 따라서 글꼴 패밀리를 지정 하는 가장 안정적인 방법은 사용자 지정 글꼴을 사용 하는 것입니다.

추가 작업 없이 사용자 지정 글꼴을 Xamarin.Forms 공유 프로젝트에 추가 하 고 플랫폼 프로젝트에서 사용할 수 있습니다. 이 작업을 수행하는 프로세스는 다음과 같습니다.

1. 공유 프로젝트에 글꼴을 Xamarin.Forms 포함 리소스로 추가 합니다 (**빌드 작업: EmbeddedResource**).
1. 특성을 사용 하 여 어셈블리에 **AssemblyInfo.cs** 와 같은 파일에 글꼴 파일을 등록 합니다 `ExportFont` . 선택적 별칭을 지정할 수도 있습니다.

다음 예제에서는 별칭과 함께 어셈블리에 등록 되는 Lobster-Regular 글꼴을 보여 줍니다.

```csharp
using Xamarin.Forms;

[assembly: ExportFont("Lobster-Regular.ttf", Alias = "Lobster")]
```

> [!NOTE]
> 글꼴은 어셈블리에 글꼴을 등록할 때 폴더 이름을 지정 하지 않고도 공유 프로젝트의 모든 폴더에 있을 수 있습니다.
>
> Windows에서는 글꼴 파일 이름과 글꼴 이름이 다를 수 있습니다. Windows에서 글꼴 이름을 검색 하려면 .ttf 파일을 마우스 오른쪽 단추로 클릭 하 고 **미리 보기** 를 선택 합니다. 그런 다음 미리 보기 창에서 글꼴 이름을 확인할 수 있습니다.

그런 다음 파일 확장명 없이 이름을 참조 하 여 각 플랫폼에서 글꼴을 사용할 수 있습니다.

```xaml
<!-- Use font name -->
<Label Text="Hello Xamarin.Forms"
       FontFamily="Lobster-Regular" />
```

또는 해당 별칭을 참조 하 여 각 플랫폼에서 사용 될 수 있습니다.

```xaml
<!-- Use font alias -->
<Label Text="Hello Xamarin.Forms"
       FontFamily="Lobster" />
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
// Use font name
Label label1 = new Label
{
    Text = "Hello Xamarin.Forms!",
    FontFamily = "Lobster-Regular"
};

// Use font alias
Label label2 = new Label
{
    Text = "Hello Xamarin.Forms!",
    FontFamily = "Lobster"
};
```

다음 스크린샷은 사용자 지정 글꼴을 보여 줍니다.

[![IOS 및 Android의 사용자 지정 글꼴](fonts-images/custom-sml.png "사용자 지정 글꼴 예")](fonts-images/custom.png#lightbox "사용자 지정 글꼴 예")

> [!IMPORTANT]
> Windows의 릴리스 빌드의 경우 사용자 지정 글꼴이 포함 된 어셈블리가 메서드 호출에서 인수로 전달 되도록 합니다 `Forms.Init` . 자세한 내용은 [문제 해결](~/xamarin-forms/platform/windows/installation/index.md#troubleshooting)을 참조하세요.

## <a name="set-font-properties-per-platform"></a>플랫폼 당 글꼴 속성 설정

[`OnPlatform`](xref:Xamarin.Forms.OnPlatform`1)및 [`On`](xref:Xamarin.Forms.On) 클래스는 XAML에서 플랫폼 당 글꼴 속성을 설정 하는 데 사용할 수 있습니다. 아래 예제에서는 각 플랫폼에서 다양 한 글꼴 패밀리와 크기를 설정 합니다.

```xaml
<Label Text="Different font properties on different platforms"
       FontSize="{OnPlatform iOS=20, Android=Medium, UWP=24}">
    <Label.FontFamily>
        <OnPlatform x:TypeArguments="x:String">
            <On Platform="iOS" Value="MarkerFelt-Thin" />
            <On Platform="Android" Value="Lobster-Regular" />
            <On Platform="UWP" Value="ArimaMadurai-Black" />
        </OnPlatform>
    </Label.FontFamily>
</Label>
```

[`Device.RuntimePlatform`](~/xamarin-forms/platform/device.md#provide-platform-specific-values)속성은 코드에서 플랫폼 당 글꼴 속성을 설정 하는 데 사용할 수 있습니다.

```csharp
Label label = new Label
{
    Text = "Different font properties on different platforms"
};

label.FontSize = Device.RuntimePlatform == Device.iOS ? 20 :
    Device.RuntimePlatform == Device.Android ? Device.GetNamedSize(NamedSize.Medium, label) : 24;
label.FontFamily = Device.RuntimePlatform == Device.iOS ? "MarkerFelt-Thin" :
   Device.RuntimePlatform == Device.Android ? "Lobster-Regular" : "ArimaMadurai-Black";
```

플랫폼 특정 값을 제공 하는 방법에 대 한 자세한 내용은 [플랫폼별 값 제공](~/xamarin-forms/platform/device.md#provide-platform-specific-values)을 참조 하세요. 태그 확장에 대 한 자세한 내용은 `OnPlatform` [onplatform 태그 확장](~/xamarin-forms/xaml/markup-extensions/consuming.md#onplatform-markup-extension)을 참조 하세요.

## <a name="understand-named-font-sizes"></a>명명 된 글꼴 크기 이해

Xamarin.Forms[`NamedSize`](xref:Xamarin.Forms.NamedSize)특정 글꼴 크기를 나타내는 열거형의 필드를 정의 합니다. 다음 표에서는 `NamedSize` 구성원 및 iOS, Android 및 유니버설 Windows 플랫폼 (UWP)의 기본 크기를 보여 줍니다.

| 멤버 | iOS | Android | UWP |
| --- | --- | --- | --- |
| `Default` | 16 | 14 | 14 |
| `Micro` | 11 | 10 | 15.667 |
| `Small` | 13 | 14 | 18.667 |
| `Medium` | 16 | 17 | 22.667 |
| `Large` | 20 | 22 | 32 |
| `Body` | 17 | 16 | 14 |
| `Header` | 17 | 96 | 46 |
| `Title` | 28 | 24 | 24 |
| `Subtitle` | 22 | 16 | 20 |
| `Caption` | 12 | 12 | 12 |

크기 값은 장치 독립적 단위로 측정 됩니다. 자세한 내용은 [측정 단위](~/xamarin-forms/user-interface/controls/common-properties.md#units-of-measurement)를 참조 하세요.

> [!NOTE]
> IOS 및 Android에서 명명 된 글꼴 크기는 운영 체제의 내게 필요한 옵션에 따라 자동으로 크기를 조정 합니다. 이 동작은 플랫폼별로 iOS에서 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 [iOS의 명명 된 글꼴 크기에 대 한 접근성 크기 조정](~/xamarin-forms/platform/ios/named-font-size-scaling.md)을 참조 하세요.

## <a name="display-font-icons"></a>글꼴 아이콘 표시

Xamarin.Forms개체의 글꼴 아이콘 데이터를 지정 하 여 응용 프로그램에서 글꼴 아이콘을 표시할 수 있습니다 `FontImageSource` . 클래스에서 파생 되는이 클래스에 [`ImageSource`](xref:Xamarin.Forms.ImageSource) 는 다음과 같은 속성이 있습니다.

- `Glyph` –로 지정 된 글꼴 아이콘의 유니코드 문자 값입니다 `string` .
- `Size` – `double` 렌더링 된 글꼴 아이콘의 크기 (장치 독립적 단위)를 나타내는 값입니다. 기본값은 30입니다. 또한이 속성은 명명 된 글꼴 크기로 설정할 수 있습니다.
- `FontFamily` – `string` 글꼴 아이콘이 속한 글꼴 패밀리를 나타내는입니다.
- `Color` – [`Color`](xref:Xamarin.Forms.Color) 글꼴 아이콘을 표시할 때 사용 되는 선택적 값입니다.

이 데이터는를 표시할 수 있는 보기에서 표시할 수 있는 PNG를 만드는 데 사용 됩니다 `ImageSource` . 이 접근 방식을 사용 하면 글꼴 아이콘 표시를 같은 단일 텍스트 (예:)로 제한 하는 것과 달리 여러 뷰에 표시 되는 emojis와 같은 글꼴 아이콘을 사용할 수 있습니다 [`Label`](xref:Xamarin.Forms.Label) .

> [!IMPORTANT]
> 글꼴 아이콘은 현재 유니코드 문자 표시로만 지정할 수 있습니다.

다음 XAML 예제에는 뷰에서 표시 되는 단일 글꼴 아이콘이 있습니다 [`Image`](xref:Xamarin.Forms.Image) .

```xaml
<Image BackgroundColor="#D1D1D1">
    <Image.Source>
        <FontImageSource Glyph="&#xf30c;"
                         FontFamily="{OnPlatform iOS=Ionicons, Android=ionicons.ttf#}"
                         Size="44" />
    </Image.Source>
</Image>
```

이 코드는 아이콘 글꼴 패밀리의 보기에서 XBox 아이콘을 표시 [`Image`](xref:Xamarin.Forms.Image) 합니다. 이 아이콘의 유니코드 문자는 이지만 `\uf30c` XAML에서 이스케이프 되어야 하므로가 됩니다 `&#xf30c;` . 해당하는 C# 코드는 다음과 같습니다.

```csharp
Image image = new Image { BackgroundColor = Color.FromHex("#D1D1D1") };
image.Source = new FontImageSource
{
    Glyph = "\uf30c",
    FontFamily = Device.RuntimePlatform == Device.iOS ? "Ionicons" : "ionicons.ttf#",
    Size = 44
};
```

[바인딩](/samples/xamarin/xamarin-forms-samples/userinterface-bindablelayouts) 가능한 레이아웃 샘플에서 다음 스크린샷에는 바인딩 가능한 레이아웃에 의해 표시 되는 몇 가지 글꼴 아이콘이 표시 됩니다.

![IOS 및 Android에서 표시 되는 글꼴 아이콘의 스크린샷](fonts-images/font-image-source.png "이미지 뷰에 표시 되는 글꼴 아이콘")

## <a name="related-links"></a>관련 링크

- [FontsSample](/samples/xamarin/xamarin-forms-samples/workingwithfonts)
- [텍스트 (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-text)
- [바인딩 가능한 레이아웃 (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-bindablelayouts)
- [플랫폼별 값 제공](~/xamarin-forms/platform/device.md#provide-platform-specific-values)
- [OnPlatform 태그 확장](~/xamarin-forms/xaml/markup-extensions/consuming.md#onplatform-markup-extension)
- [바인딩 가능한 레이아웃](~/xamarin-forms/user-interface/layouts/bindable-layouts.md)

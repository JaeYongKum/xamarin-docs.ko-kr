---
title: 'Xamarin.Forms브러시: 단색'
description: Xamarin.FormsSystem.windows.media.solidcolorbrush> 클래스는 단색으로 영역을 그립니다.
ms.prod: xamarin
ms.assetid: 4225D40A-16C1-40E1-ACBE-23E321E7FDE4
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/27/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 04e882f9b64d0e1f56e1170d353af4e13b079933
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919142"
---
# <a name="no-locxamarinforms-brushes-solid-colors"></a>Xamarin.Forms브러시: 단색

![API 미리 보기](~/media/shared/preview.png "이 API는 현재 시험판임")

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

클래스는 `SolidColorBrush` 클래스에서 파생 `Brush` 되며 단색으로 영역을 그리는 데 사용 됩니다. 의 색을 지정 하는 방법에는 여러 가지가 있습니다 `SolidColorBrush` . 예를 들어 값을 사용 [`Color`](xref:Xamarin.Forms.Color) 하거나 `SolidColorBrush` 클래스에서 제공 하는 미리 정의 된 개체 중 하나를 사용 하 여 색을 지정할 수 있습니다 `Brush` .

`SolidColorBrush`클래스는 `Color` 브러시의 색을 나타내는 형식의 속성을 정의 합니다 [`Color`](xref:Xamarin.Forms.Color) . 이 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉, 데이터 바인딩의 대상이 될 수 있고 스타일을 지정할 수 있습니다.

`SolidColorBrush`또한 클래스에 `IsEmpty` 는 브러시에 색이 할당 되었는지 여부를 나타내는을 반환 하는 메서드가 있습니다 `bool` .

## <a name="create-a-solidcolorbrush"></a>System.windows.media.solidcolorbrush> 만들기

을 만드는 세 가지 주요 기술이 있습니다 `SolidColorBrush` . 에서을 만들거나 `SolidColorBrush` [`Color`](xref:Xamarin.Forms.Color) 미리 정의 된 브러시를 사용 하거나 `SolidColorBrush` 16 진수 표기법을 사용 하 여을 만들 수 있습니다.

### <a name="use-a-predefined-color"></a>미리 정의 된 색 사용

Xamarin.Forms값에서를 만드는 형식 변환기를 포함 `SolidColorBrush` [`Color`](xref:Xamarin.Forms.Color) 합니다. XAML에서이를 사용 하면 `SolidColorBrush` 미리 정의 된 값에서을 만들 수 있습니다 `Color` .

```xaml
<Frame Background="DarkBlue"
       BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120" />
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) 진한 파란색으로 그려집니다 `SolidColorBrush` .

![미리 정의 된 색으로 그린 프레임](solidcolor-images/predefined-color.png)

또는 [`Color`](xref:Xamarin.Forms.Color) 속성 태그 구문을 사용 하 여 값을 지정할 수 있습니다.

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
       <Frame.Background>
           <SolidColorBrush Color="DarkBlue" />
       </Frame.Background>
</Frame>
```

이 예제에서는 [`Frame`](xref:Xamarin.Forms.Frame) `SolidColorBrush` 속성을 설정 하 여 색이 지정 된를 사용 하 여의 배경을 그립니다 `SolidColorBrush.Color` .

### <a name="use-a-predefined-brush"></a>미리 정의 된 브러시 사용

`Brush`클래스는 일반적으로 사용 되는 개체의 집합을 정의 `SolidColorBrush` 합니다. 다음 예제에서는 미리 정의 된 개체 중 하나를 사용 합니다 `SolidColorBrush` .

```xaml
<Frame Background="{x:Static Brush.Indigo}"
       BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120" />       
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
Frame frame = new Frame
{
    Background = Brush.Indigo,
    BorderColor = Color.LightGray,
    // ...
};
```

이 예제에서는 indigo를 사용 하 여의 배경을 [`Frame`](xref:Xamarin.Forms.Frame) 그립니다 `SolidColorBrush` .

![미리 정의 된 System.windows.media.solidcolorbrush>로 그린 프레임](solidcolor-images/predefined-brush.png)

클래스에서 제공 하는 미리 정의 된 `SolidColorBrush` 개체 목록은 `Brush` [단색 브러시](#solid-color-brushes)를 참조 하세요.

### <a name="use-hexadecimal-notation"></a>16 진수 표기법 사용

`SolidColorBrush`16 진수 표기법을 사용 하 여 개체를 만들 수도 있습니다. 이 방법을 사용 하는 경우 색은 빨강, 녹색 및 파랑의 양으로 단일 색으로 결합 하 여 지정 됩니다. 16 진수 표기법을 사용 하 여 색을 지정 하는 기본 형식은입니다 `#rrggbb` .

- `rr`는 빨강의 상대적 크기를 지정 하는 두 자리 16 진수입니다.
- `gg`는 상대 크기의 녹색을 지정 하는 두 자리 16 진수입니다.
- `bb`는 파란색의 상대적 크기를 지정 하는 두 자리 16 진수입니다.

또한 색은에서 `#aarrggbb` `aa` 색의 알파 값 또는 투명도를 지정 하는으로 지정할 수 있습니다. 이 방법은 사용하면 부분적으로 투명한 색을 만들 수 있습니다.

다음 예제에서는 `SolidColorBrush` 16 진수 표기법을 사용 하 여의 색 값을 설정 합니다.

```xaml
<Frame Background="#FF9988"
       BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120" />
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) 연어 색으로 그려집니다 `SolidColorBrush` .

![16 진수 표기법을 사용 하 여 만든 System.windows.media.solidcolorbrush>로 그린 프레임](solidcolor-images/hex.png)

색을 설명 하는 다른 방법은 [의 Xamarin.Forms 색 ](~/xamarin-forms/user-interface/colors.md)을 참조 하세요.

## <a name="solid-color-brushes"></a>단색 브러시

편의 위해 합니다 `Brush` 클래스에서는 일반적으로 사용 되는 집합이 `SolidColorBrush` 같은 개체 `AliceBlue` 및 `YellowGreen`합니다. 다음 이미지에서는 미리 정의 된 각 브러시의 색, 해당 이름 및 해당 16 진수 값을 보여 줍니다.

[![색 견본, 색 이름 및 16 진수 값을 포함 하는 색 표](solidcolor-images/solidcolorbrushes.png)](solidcolor-images/solidcolorbrushes-large.png#lightbox)

## <a name="related-links"></a>관련 링크

- [BrushesDemos (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [색의Xamarin.Forms](~/xamarin-forms/user-interface/colors.md)

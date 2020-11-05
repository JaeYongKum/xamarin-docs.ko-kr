---
title: 'Xamarin.Forms 브러시: 방사형 그라데이션'
description: Xamarin.FormsRadialGradientBrush 클래스는 방사형 그라데이션으로 영역을 그립니다.
ms.prod: xamarin
ms.assetid: 099BA530-3B38-4005-9B19-A0EB4D4DEEFC
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 10645e12b81b1ca4ee8e0790ed3a673a23a4ba26
ms.sourcegitcommit: ebdc016b3ec0b06915170d0cbbd9e0e2469763b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93366934"
---
# <a name="no-locxamarinforms-brushes-radial-gradients"></a>Xamarin.Forms 브러시: 방사형 그라데이션

![API 미리 보기](~/media/shared/preview.png "이 API는 현재 시험판임")

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

클래스는 `RadialGradientBrush` 클래스에서 파생 `GradientBrush` 되 고 방사형 그라데이션을 사용 하 여 영역을 그리며,이는 원에서 두 개 이상의 색을 혼합 합니다. `GradientStop` 개체는 그라데이션의 색과 위치를 지정 하는 데 사용 됩니다. 개체에 대 한 자세한 내용은 `GradientStop` [ Xamarin.Forms 브러시: 그라데이션](gradient.md)을 참조 하세요.

`RadialGradientBrush` 클래스는 다음과 같은 속성을 정의합니다.

- `Center`[`Point`](xref:Xamarin.Forms.Point)방사형 그라데이션에 대 한 원의 중심점을 나타내는 형식의입니다. 이 속성의 기본값은 (0.5, 0.5)입니다.
- `Radius``double`방사형 그라데이션에 대 한 원의 반경을 나타내는 형식의입니다. 이 속성의 기본값은 0.5입니다.

이러한 속성은 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) 개체에서 지원하며, 따라서 데이터 바인딩의 대상이 될 수 있고 스타일이 지정될 수 있습니다.

클래스에는 `RadialGradientBrush` 브러시에 `IsEmpty` 개체가 할당 되었는지 여부를 나타내는을 반환 하는 메서드도 포함 되어 있습니다 `bool` `GradientStop` .

> [!NOTE]
> 방사형 그라데이션은 CSS 함수를 사용 하 여 만들 수도 있습니다 `radial-gradient()` .

## <a name="create-a-radialgradientbrush"></a>RadialGradientBrush 만들기

방사형 그라데이션 브러시의 그라데이션 중지점은 원에서 정의한 그라데이션 축을 따라 배치 됩니다. 그라데이션 축은 원의 중심에서 원주로 radiates. 브러시의 및 속성을 사용 하 여 원의 위치와 크기를 변경할 수 있습니다 `Center` `Radius` . 원은 그라데이션의 끝점을 정의 합니다. 따라서 1.0에서 그라데이션 중지점은 원의 원주 색을 정의 합니다. 0.0에서 그라데이션 중지점은 원의 중심에 있는 색을 정의 합니다.

방사형 그라데이션을 만들려면 개체를 만들고 `RadialGradientBrush` 해당 `Center` 및 속성을 설정 `Radius` 합니다. 그런 다음 두 개 이상의 `GradientStop` 개체를 컬렉션에 추가 `RadialGradientBrush.GradientStops` 하 여 그라데이션의 색과 위치를 지정 합니다.

다음 XAML 예제에서는의 `RadialGradientBrush` 로 설정 된를 보여 줍니다 `Background` [`Frame`](xref:Xamarin.Forms.Frame) .

```xaml    
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- Center defaults to (0.5,0.5)
             Radius defaults to (0.5) -->
        <RadialGradientBrush>
            <GradientStop Color="Red"
                          Offset="0.1" />
            <GradientStop Color="DarkBlue"
                          Offset="1.0" />
        </RadialGradientBrush>
    </Frame.Background>
</Frame>
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) `RadialGradientBrush` 빨강에서 진한 파랑으로 보간 되는를 사용 하 여 그려집니다. 방사형 그라데이션 중심은의 가운데에 배치 됩니다 `Frame` .

![가운데 맞춤 된 RadialGradientBrush로 그린 프레임](radialgradient-images/center.png)

다음 XAML 예제에서는 방사형 그라데이션의 중심을의 왼쪽 위 모퉁이로 이동 합니다 [`Frame`](xref:Xamarin.Forms.Frame) .

```xaml
<!-- Radius defaults to (0.5) -->
<RadialGradientBrush Center="0.0,0.0">
    <GradientStop Color="Red"
                  Offset="0.1" />
    <GradientStop Color="DarkBlue"
                  Offset="1.0" />
</RadialGradientBrush>
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) `RadialGradientBrush` 빨강에서 진한 파랑으로 보간 되는를 사용 하 여 그려집니다. 방사형 그라데이션 중심은의 왼쪽 위에 배치 됩니다 `Frame` .

![왼쪽 위 RadialGradientBrush로 그린 프레임](radialgradient-images/top-left.png)

다음 XAML 예제에서는 방사형 그라데이션의 중심을의 오른쪽 아래 모퉁이로 이동 합니다 [`Frame`](xref:Xamarin.Forms.Frame) .

```xaml
<!-- Radius defaults to (0.5) -->
<RadialGradientBrush Center="1.0,1.0">
    <GradientStop Color="Red"
                  Offset="0.1" />
    <GradientStop Color="DarkBlue"
                  Offset="1.0" />
</RadialGradientBrush>            
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) `RadialGradientBrush` 빨강에서 진한 파랑으로 보간 되는를 사용 하 여 그려집니다. 방사형 그라데이션 중심은의 오른쪽 아래에 배치 됩니다 `Frame` .

![오른쪽 아래 RadialGradientBrush로 그린 프레임](radialgradient-images/bottom-right.png)

## <a name="related-links"></a>관련 링크

- [BrushesDemos (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [Xamarin.Forms 브러시: 그라데이션](gradient.md)
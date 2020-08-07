---
title: 'Xamarin.Forms브러시: 선형 그라데이션'
description: Xamarin.FormsSystem.windows.media.lineargradientbrush.startpoint 클래스는 선형 그라데이션으로 영역을 그립니다.
ms.prod: xamarin
ms.assetid: BEA2B3F5-96B0-4E39-88A6-0FAFE95C3DCD
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 734ecae4fdafd71f0c88ddc5e4b4ed0c672f2019
ms.sourcegitcommit: 579ec4f2884fa391e5e214a3952cd6004c521eb8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919634"
---
# <a name="no-locxamarinforms-brushes-linear-gradients"></a>Xamarin.Forms브러시: 선형 그라데이션

![API 미리 보기](~/media/shared/preview.png "이 API는 현재 시험판임")

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/BrushDemos)

클래스는 `LinearGradientBrush` 클래스에서 파생 `GradientBrush` 되 고 선형 그라데이션으로 영역을 그리며 그라데이션 축 이라고 하는 선을 따라 둘 이상의 색을 혼합 합니다. `GradientStop`개체는 그라데이션의 색과 위치를 지정 하는 데 사용 됩니다. 개체에 대 한 자세한 내용은 `GradientStop` [ Xamarin.Forms 브러시: 그라데이션](gradient.md)을 참조 하세요.

`LinearGradientBrush` 클래스는 다음과 같은 속성을 정의합니다.

- `StartPoint`는 [`Point`](xref:Xamarin.Forms.Point) 선형 그라데이션의 시작 2 차원 좌표를 나타내는 형식의입니다. 이 속성의 기본값은 (0, 0)입니다.
- `EndPoint`[`Point`](xref:Xamarin.Forms.Point)-선형 그라데이션의 끝 2 차원 좌표를 나타내는 형식의입니다. 이 속성의 기본값은 (1, 1)입니다.

이러한 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉, 데이터 바인딩의 대상 및 스타일을 지정할 수 있습니다.

`LinearGradientBrush`클래스는 `IsEmpty` `bool` 브러시에 개체가 할당 되었는지 여부를 나타내는을 반환 하는 메서드 이기도 합니다 `GradientStop` .

> [!NOTE]
> CSS 함수를 사용 하 여 선형 그라데이션을 만들 수도 있습니다 `linear-gradient()` .

## <a name="create-a-lineargradientbrush"></a>System.windows.media.lineargradientbrush.startpoint 만들기

선형 그라데이션 브러시의 그라데이션 중지점은 그라데이션 축을 따라 배치 됩니다. 브러시의 및 속성을 사용 하 여 그라데이션 축의 방향과 크기를 변경할 수 `StartPoint` 있습니다 `EndPoint` . 이러한 속성을 조작 하 여 가로, 세로 및 대각선 그라데이션을 만들고, 그라데이션 방향을 반전 하 고, 그라데이션 확산을 축소할 수 있습니다.

`StartPoint`및 `EndPoint` 속성은 그리고 있는 영역을 기준으로 합니다. (0, 0)은 그리고 있는 영역의 왼쪽 위 모퉁이를 나타내고 (1, 1)은 그리고 있는 영역의 오른쪽 아래 모퉁이를 나타냅니다. 다음 다이어그램에서는 대각선 선형 그라데이션 브러시의 그라데이션 축을 보여 줍니다.

![대각선 그라데이션 축이 있는 프레임](lineargradient-images/gradient-axis.png)

이 다이어그램에서 파선은 그라데이션 축을 보여 줍니다. 그라데이션 축은 시작점에서 끝점 까지의 그라데이션의 보간 경로를 강조 표시 합니다.

### <a name="create-a-horizontal-linear-gradient"></a>가로 선형 그라데이션 만들기

가로 선형 그라데이션을 만들려면 개체를 만들고이 `LinearGradientBrush` `StartPoint` 를 (0, 0)으로 설정 하 고를 `EndPoint` (1, 0)으로 설정 합니다. 그런 다음 두 개 이상의 `GradientStop` 개체를 컬렉션에 추가 `LinearGradientBrush.GradientStops` 하 여 그라데이션의 색과 위치를 지정 합니다.

다음 XAML 예제에서는 `LinearGradientBrush` 의로 설정 된 가로를 보여 줍니다 `Background` [`Frame`](xref:Xamarin.Forms.Frame) .

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- StartPoint defaults to (0,0) -->
        <LinearGradientBrush EndPoint="1,0">
            <GradientStop Color="Yellow"
                          Offset="0.1" />
            <GradientStop Color="Green"
                          Offset="1.0" />
        </LinearGradientBrush>
    </Frame.Background>
</Frame>  
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) `LinearGradientBrush` 노랑에서 녹색 가로로 보간 되는로 그려집니다.

![수평 System.windows.media.lineargradientbrush.startpoint로 그린 프레임](lineargradient-images/horizontal.png)

### <a name="create-a-vertical-linear-gradient"></a>세로 선형 그라데이션 만들기

세로 선형 그라데이션을 만들려면 개체를 만들고이 `LinearGradientBrush` `StartPoint` 를 (0, 0)으로 설정 하 고를 `EndPoint` (0, 1)로 설정 합니다. 그런 다음 두 개 이상의 `GradientStop` 개체를 컬렉션에 추가 `LinearGradientBrush.GradientStops` 하 여 그라데이션의 색과 위치를 지정 합니다.

다음 XAML 예제에서는 `LinearGradientBrush` 의로 설정 된 세로를 보여 줍니다 `Background` [`Frame`](xref:Xamarin.Forms.Frame) .

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- StartPoint defaults to (0,0) -->    
        <LinearGradientBrush EndPoint="0,1">
            <GradientStop Color="Yellow"
                          Offset="0.1" />
            <GradientStop Color="Green"
                          Offset="1.0" />
        </LinearGradientBrush>
    </Frame.Background>
</Frame>
```

이 예제에서의 배경은 [`Frame`](xref:Xamarin.Forms.Frame) `LinearGradientBrush` 노랑에서 녹색 세로 방향으로 보간 되는를 사용 하 여 그려집니다.

![세로 System.windows.media.lineargradientbrush.startpoint를 사용 하 여 그린 프레임](lineargradient-images/vertical.png)

### <a name="create-a-diagonal-linear-gradient"></a>대각선 선형 그라데이션 만들기

대각선 선형 그라데이션을 만들려면 개체를 만들고 `LinearGradientBrush` 해당 개체 `StartPoint` 를 (0, 0)으로 설정 하 고를 `EndPoint` (1, 1)로 설정 합니다. 그런 다음 두 개 이상의 `GradientStop` 개체를 컬렉션에 추가 `LinearGradientBrush.GradientStops` 하 여 그라데이션의 색과 위치를 지정 합니다.

다음 XAML 예제에서는 `LinearGradientBrush` 의로 설정 된 대각선을 보여 줍니다 `Background` [`Frame`](xref:Xamarin.Forms.Frame) .

```xaml
<Frame BorderColor="LightGray"
       HasShadow="True"
       CornerRadius="12"
       HeightRequest="120"
       WidthRequest="120">
    <Frame.Background>
        <!-- StartPoint defaults to (0,0)      
             Endpoint defaults to (1,1) -->
        <LinearGradientBrush>
            <GradientStop Color="Yellow"
                          Offset="0.1" />
            <GradientStop Color="Green"
                          Offset="1.0" />
        </LinearGradientBrush>
    </Frame.Background>
</Frame>
```

이 예제에서는 [`Frame`](xref:Xamarin.Forms.Frame) `LinearGradientBrush` 노란색에서 녹색 대각선 방향으로 보간 하는를 사용 하 여의 배경을 그립니다.

![대각선으로 그린 프레임 System.windows.media.lineargradientbrush.startpoint](lineargradient-images/diagonal.png)

## <a name="related-links"></a>관련 링크

- [BrushesDemos (샘플)](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/BrushDemos)
- [Xamarin.Forms브러시: 그라데이션](gradient.md)

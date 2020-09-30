---
title: 'Xamarin.Forms 브러시: 그라데이션'
description: Xamarin.FormsGradientbrush가 아니며 클래스는 그라데이션 중지점으로 구성 된 그라데이션을 설명 하는 추상 클래스입니다.
ms.prod: xamarin
ms.assetid: 24763E56-74EC-4082-897B-E4EAACCADFEE
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/27/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 08a423830ee3db55cb0ec7facfa5630c8832885b
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91562940"
---
# <a name="no-locxamarinforms-brushes-gradients"></a>Xamarin.Forms 브러시: 그라데이션

![API 미리 보기](~/media/shared/preview.png "이 API는 현재 시험판임")

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)

`GradientBrush`클래스는 클래스에서 파생 `Brush` 되며 그라데이션 중지점으로 구성 된 그라데이션을 설명 하는 추상 클래스입니다. 그라데이션 브러시는 축을 따라 서로 혼합되는 여러 색으로 영역을 그립니다. 에서 파생 되는 클래스는 `GradientBrush` 그라데이션 중지점을 해석 하는 다양 한 방법을 설명 하 고 Xamarin.Forms 다음과 같은 그라데이션 브러시를 제공 합니다.

- `LinearGradientBrush`-선형 그라데이션으로 영역을 그립니다. 자세한 내용은 [ Xamarin.Forms 브러시: 선형 그라데이션](lineargradient.md)을 참조 하세요.
- `RadialGradientBrush`-방사형 그라데이션으로 영역을 그립니다. 자세한 내용은 [ Xamarin.Forms 브러시: 방사형 그라데이션](radialgradient.md)을 참조 하세요.

클래스는 브러시의 그라데이션 `GradientBrush` `GradientStops` `GradientStopsCollection` 축을 따라 색 및 오프셋을 지정 하는 브러시의 그라데이션 중지점을 나타내는 형식의 속성을 정의 합니다. 는 `GradientStopsCollection` `ObservableCollection` 개체의입니다 `GradientStop` . `GradientStops`속성은 개체에 의해 지원 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) 됩니다. 즉, 데이터 바인딩의 대상이 될 수 있고 스타일을 지정할 수 있습니다.

> [!NOTE]
> `GradientStops`속성은 `ContentProperty` 클래스의입니다 `GradientBrush` . 따라서 XAML에서 명시적으로 설정할 필요가 없습니다.

## <a name="gradient-stops"></a>그라데이션 중지점

그라데이션 중지점은 그라데이션 브러시의 빌딩 블록이 며 그라데이션 축을 따라 그라데이션 및 해당 위치에 있는 색을 지정 합니다. 그라데이션 중지점은 개체를 사용 하 여 지정 `GradientStop` 합니다.

`GradientStop` 클래스는 다음과 같은 속성을 정의합니다.

- `Color`[`Color`](xref:Xamarin.Forms.Color)-그라데이션 중지점의 색을 나타내는 형식의입니다. 이 속성의 기본값은 `Color.Default`입니다.
- `Offset``float`-그라데이션 벡터 내에서 그라데이션 중지점의 위치를 나타내는 형식의입니다. 이 속성의 기본값은 0이 고 유효한 값은 0.0-1.0 범위에 있습니다. 이 값이 0에 가까울수록 색이 그라데이션의 시작 부분에 가깝습니다. 마찬가지로이 값이 1에 가까울수록 색이 그라데이션의 끝에 가까울수록 좋습니다.

이러한 속성은 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) 개체에서 지원하며, 따라서 데이터 바인딩의 대상이 될 수 있고 스타일이 지정될 수 있습니다.

> [!IMPORTANT]
> 그라데이션에 사용 되는 좌표계는 출력 영역에 대 한 경계 상자를 기준으로 합니다. 0은 경계 상자의 0%를 나타내고 1은 경계 상자의 100%를 나타냅니다. 따라서 (0.5, 0.5)는 경계 상자 가운데에 있는 점을 설명 하 고 (1, 1)은 경계 상자의 오른쪽 아래에 있는 점을 설명 합니다.

다음 XAML 예제에서는 `LinearGradientBrush` 네 가지 색으로 대각선을 만듭니다.

```xaml
<LinearGradientBrush StartPoint="0,0"
                     EndPoint="1,1">
    <GradientStop Color="Yellow"
                  Offset="0.0" />
    <GradientStop Color="Red"
                  Offset="0.25" />
    <GradientStop Color="Blue"
                  Offset="0.75" />             
    <GradientStop Color="LimeGreen"
                  Offset="1.0" />
</LinearGradientBrush>                                                       
```

그라데이션 중지점 사이에 있는 각 지점의 색은 두 경계 그라데이션 중지점에서 지정 된 색의 조합으로 보간됩니다. 다음 다이어그램에서는 이전 예제의 그라데이션 중지점을 보여 줍니다.

![대각선으로 그린 프레임 System.windows.media.lineargradientbrush.startpoint](gradient-images/gradient-stops.png)

이 다이어그램에서 원은 그라데이션 중지점의 위치를 표시 하 고 파선은 그라데이션 축을 표시 합니다. 첫 번째 그라데이션 중지점은 0.0 오프셋에서 노란색 색을 지정 합니다. 두 번째 그라데이션 중지점은 오프셋 0.25에서 빨강을 지정 합니다. 그라데이션 축을 따라 왼쪽에서 오른쪽으로 이동 하는 경우 이러한 두 그라데이션 사이의 점은 점차적으로 노란색에서 빨강으로 변경 됩니다. 세 번째 그라데이션 중지점은 0.75 오프셋에서 파란색을 지정 합니다. 두 번째 및 세 번째 그라데이션 중지점 사이에 있는 점들은 빨간색에서 파란색으로 서서히 변경됩니다. 네 번째 그라데이션 중지점은 오프셋 1.0의에서 황록색 색을 지정 합니다. 세 번째 및 네 번째 그라데이션 중지점 사이에 있는 점들은 파란색에서 라임 녹색으로 서서히 변경됩니다.

## <a name="related-links"></a>관련 링크

- [BrushesDemos (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-brushdemos/)
- [Xamarin.Forms 브러시: 선형 그라데이션](lineargradient.md)
- [Xamarin.Forms 브러시: 방사형 그라데이션](radialgradient.md)
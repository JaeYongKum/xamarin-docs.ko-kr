---
title: 'Xamarin.Forms도형: 선'
description: Xamarin.Forms줄 클래스를 사용 하 여 선을 그릴 수 있습니다.
ms.prod: xamarin
ms.assetid: 384F1A72-6D3B-4FD3-BC40-E00A73A463EC
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/20/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 9d79f232a77972b6abbce23ba65d9c277b090311
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86935449"
---
# <a name="xamarinforms-shapes-line"></a>Xamarin.Forms도형: 선

![시험판 API](~/media/shared/preview.png "이 API는 현재 시험판임")

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-shapesdemos/)

`Line`클래스는 클래스에서 파생 `Shape` 되며 선을 그리는 데 사용할 수 있습니다. 클래스가 클래스에서 상속 하는 속성에 대 한 자세한 내용은 `Line` `Shape` [ Xamarin.Forms 셰이프](index.md)를 참조 하세요.

`Line`는 다음 속성을 정의합니다.

- `X1`double 형식의은 선 시작점의 x 좌표를 나타냅니다. 이 속성의 기본값은 0.0입니다.
- `Y1`double 형식의는 선 시작점의 y 좌표를 나타냅니다. 이 속성의 기본값은 0.0입니다.
- `X2`double 형식의는 선 끝점의 x 좌표를 나타냅니다. 이 속성의 기본값은 0.0입니다.
- `Y2`double 형식의는 선 끝점의 y 좌표를 나타냅니다. 이 속성의 기본값은 0.0입니다.

이러한 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉, 데이터 바인딩의 대상 및 스타일을 지정할 수 있습니다.

줄 끝을 그리는 방법을 제어 하는 방법에 대 한 자세한 내용은 [줄 끝 제어](index.md#control-line-ends)를 참조 하세요.

## <a name="create-a-line"></a>선 만들기

선을 그리려면 개체를 만들고 `Line` 해당 및 속성을 시작 지점으로 설정 하 고 및 속성을 해당 끝점으로 설정 `X1` `Y1` `X2` `Y` 합니다. 또한 `Stroke` [`Color`](xref:Xamarin.Forms.Color) 스트로크가 없는 줄은 보이지 않으므로 해당 속성을로 설정 합니다.

> [!NOTE]
> `Fill`의 속성을 설정 `Line` 해도 아무 효과가 없습니다.

다음 XAML 예제에서는 선을 그리는 방법을 보여 줍니다.

```xaml
<Line X1="40"
      Y1="0"
      X2="0"
      Y2="120"
      Stroke="Red" />
```

이 예제에서는 (40, 0)에서 (0120)까지 빨간색 대각선을 그립니다.

![Line](line-images/line.png "줄")

,, `X1` `Y1` `X2` 및 `Y2` 속성의 기본값은 0 이므로 최소한의 구문을 사용 하 여 줄을 그릴 수 있습니다.

```xaml
<Line Stroke="Red"
      X2="200" />
```

이 예제에서는 200 장치 독립적 단위 길이의 가로 줄이 정의 됩니다. 다른 속성은 기본적으로 0 이므로 (0, 0)에서 (200, 0)까지 줄이 그려집니다.

다음 XAML 예제에서는 파선을 그리는 방법을 보여 줍니다.

```xaml
<Line X1="40"
      Y1="0"
      X2="0"
      Y2="120"
      Stroke="DarkBlue"
      StrokeDashArray="1,1"
      StrokeDashOffset="6" />
```

이 예에서 진한 파란색 파선 대각선은 (40, 0)에서 (0120)로 그려집니다.

![파선](line-images/dashed-line.png "파선")

파선을 그리는 방법에 대 한 자세한 내용은 [파선 도형 그리기](index.md#draw-dashed-shapes)를 참조 하세요.

## <a name="related-links"></a>관련 링크

- [ShapeDemos (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-shapesdemos/)
- [Xamarin.Forms셰이프도](index.md)

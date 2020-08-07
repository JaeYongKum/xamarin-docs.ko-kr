---
title: Xamarin.Forms브러시
description: Xamarin.Forms브러시 클래스는 영역을 출력으로 칠하는 추상 클래스입니다.
ms.prod: xamarin
ms.assetid: 44420FC2-304C-4175-8654-76769F79A813
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 4f1f56103b20eac84ce6106c0955acebf974cfe3
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87919148"
---
# <a name="no-locxamarinforms-brushes"></a>Xamarin.Forms브러시

![API 미리 보기](~/media/shared/preview.png "이 API는 현재 시험판임")

브러시를 사용 하면 다른 방법을 사용 하 여 컨트롤의 배경과 같은 영역을 그릴 수 있습니다. 의 브러시 지원은 Xamarin.Forms `Xamarin.Forms` IOS, Android, macos, 유니버설 WINDOWS 플랫폼 (UWP) 및 WINDOWS PRESENTATION FOUNDATION (WPF)의 네임 스페이스에서 사용할 수 있습니다.

> [!IMPORTANT]
> 의 브러시 지원은 Xamarin.Forms 현재 실험적 이며 플래그를 설정 하는 방법 으로만 사용할 수 있습니다 `Brush_Experimental` . 자세한 내용은 [실험적 플래그](~/xamarin-forms/internals/experimental-flags.md)를 참조 하세요.

`Brush`클래스는 영역을 출력으로 칠하는 추상 클래스입니다. 에서 파생 되는 클래스는 `Brush` 영역을 그리는 여러 가지 방법을 설명 합니다. 다음 목록에서는에서 사용할 수 있는 다양 한 브러시 유형을 설명 합니다 Xamarin.Forms .

- `SolidColorBrush`는 단색으로 영역을 그립니다. 자세한 내용은 [ Xamarin.Forms 브러시: 단색](solidcolor.md)을 참조 하세요.
- `LinearGradientBrush`-선형 그라데이션으로 영역을 그립니다. 자세한 내용은 [ Xamarin.Forms 브러시: 선형 그라데이션](lineargradient.md)을 참조 하세요.
- `RadialGradientBrush`-방사형 그라데이션으로 영역을 그립니다. 자세한 내용은 [ Xamarin.Forms 브러시: 방사형 그라데이션](radialgradient.md)을 참조 하세요.

이러한 브러시 형식의 인스턴스는의 `Stroke` 및 `Fill` 속성과 `Shape` `Background` 의 속성 [`VisualElement`](xref:Xamarin.Forms.VisualElement) 에 할당할 수 있습니다.

> [!NOTE]
> `VisualElement.Background`속성을 사용 하면 모든 컨트롤의 배경으로 브러시를 사용할 수 있습니다.

`Brush`또한 클래스에는 `IsNullOrEmpty` `bool` 브러시가 정의 되었는지 여부를 나타내는을 반환 하는 메서드가 있습니다.

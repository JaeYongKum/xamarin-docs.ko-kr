---
title: Xamarin.Forms 이중 화면
description: 이 가이드에서는 이중 화면 디바이스용 Xamarin.Forms 앱을 만드는 방법을 설명합니다.
ms.prod: xamarin
ms.assetid: f9906e83-f8ae-48f9-997b-e1540b96ee8e
ms.technology: xamarin-forms
author: davidortinau
ms.author: daortin
ms.date: 02/08/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: a414127c01d26db6bf7b462d6fc5a7f9ae44dddc
ms.sourcegitcommit: 69bd0fdc698c9b0c0d73217776d7084f32ae88ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90832282"
---
# <a name="no-locxamarinforms-dual-screen"></a>Xamarin.Forms 이중 화면

Microsoft Surface Duo와 같은 이중 화면 디바이스는 애플리케이션에 대한 새로운 사용자 환경 가능성을 용이하게 합니다. Xamarin.Forms에는 `TwoPaneView` 및 `DualScreenInfo` 클래스가 포함되어 있으므로, 이중 화면 디바이스용 앱을 개발할 수 있습니다.

## <a name="get-started"></a>시작

Xamarin.Forms 앱에 이중 화면 기능을 추가하려면 다음 단계를 따르세요.

1. 솔루션에 대해 **NuGet 패키지 관리자** 대화 상자를 엽니다.
2. **찾아보기** 탭에서 `Xamarin.Forms.DualScreen`을 검색합니다.
3. `Xamarin.Forms.DualScreen` 패키지를 솔루션에 설치합니다.
4. `OnCreate` 이벤트에서 Android 프로젝트의 `MainActivity` 클래스에 다음 초기화 메서드 호출을 추가합니다.

    ```csharp
    Xamarin.Forms.DualScreen.DualScreenService.Init(this);
    ```

    이 메서드는 앱이 두 화면에 걸쳐 배치되는 것과 같이 앱 상태의 변경을 감지하는 데 필요합니다.

5. Android 프로젝트의 `MainActivity` 클래스에서 `Activity` 특성을 업데이트하여 다음 `ConfigurationChanges` 옵션이 ‘모두’ 포함되도록 합니다.

    ```@csharp
    ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation
        | ConfigChanges.ScreenLayout | ConfigChanges.SmallestScreenSize | ConfigChanges.UiMode
    ```

    해당 값은 구성 변경 및 범위 상태를 보다 신뢰도 높게 보고할 수 있게 하는 데 필요합니다. 기본적으로 두 개만 Xamarin.Forms 프로젝트에 추가되므로, 신뢰할 수 있는 이중 화면 지원을 위해 나머지를 직접 추가해야 합니다.

## <a name="troubleshooting"></a>문제 해결

`DualScreenInfo` 클래스 또는 `TwoPaneView` 레이아웃이 예상대로 작동하지 않는 경우 이 페이지의 설정 지침을 다시 확인하세요. `Init` 메서드나 `ConfigurationChanges` 특성 값을 생략하거나 잘못 구성하는 것이 오류의 일반적인 원인입니다.

추가 지침 및 참조 구현에 대한 자세한 내용은 [Xamarin.Forms 이중 화면 샘플](https://docs.microsoft.com/dual-screen/xamarin/samples)을 검토하세요.

## <a name="next-steps"></a>다음 단계

NuGet을 추가한 후에는 다음 지침에 따라 앱에 이중 화면 기능을 추가합니다.

- [이중 화면 디자인 패턴](design-patterns.md) - 이중 화면 디바이스에서 다중 화면을 최대한 활용하는 방법을 고려할 때는 패턴 지침을 참조하여 애플리케이션 인터페이스에 적합한 패턴을 찾으세요.
- [TwoPaneView 레이아웃](twopaneview.md) - 같은 이름의 UWP 컨트롤에서 영감을 받아 만들어진 Xamarin.Forms `TwoPaneView` 클래스는 이중 화면 디바이스에 최적화된 교차 플랫폼 레이아웃입니다.
- [DualScreenInfo 도우미 클래스](dual-screen-info.md) - `DualScreenInfo` 클래스를 사용하면 보기가 표시된 창과 그 크기, 디바이스의 방향, 힌지 각도 등을 확인할 수 있습니다.
- [이중 화면 트리거](triggers.md) - [`Xamarin.Forms.DualScreen`](xref:Xamarin.Forms.DualScreen) 네임스페이스에는 연결된 레이아웃 또는 창의 보기 모드가 변경될 때 [`VisualState`](xref:Xamarin.Forms.VisualState) 변경을 트리거하는 두 개의 상태 트리거가 포함되어 있습니다.

자세한 내용은 [이중 화면 개발자 문서](https://docs.microsoft.com/dual-screen/)를 참조하세요.

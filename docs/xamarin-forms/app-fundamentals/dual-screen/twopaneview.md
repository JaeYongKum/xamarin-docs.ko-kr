---
title: Xamarin.Forms 이중 화면 레이아웃
description: 이 가이드에서는 Xamarin.Forms TwoPaneView를 사용하여 Surface Duo 및 Surface Neo와 같은 이중 화면 디바이스의 앱 환경을 최적화하는 방법을 설명합니다.
ms.prod: xamarin
ms.assetid: 17ee8afa-5e7c-4a4f-a9b6-2aca03f30fe3
ms.technology: xamarin-forms
author: davidortinau
ms.author: daortin
ms.date: 02/08/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 734dea456af56f4103691e0368ae72202bce9556
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87918236"
---
# <a name="no-locxamarinforms-twopaneview-layout"></a>Xamarin.Forms TwoPaneView 레이아웃

![시험판 API](~/media/shared/preview.png)

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-dualscreendemos/)

`TwoPaneView` 클래스는 사용 가능한 공간에서 나란히 또는 위아래로 콘텐츠의 크기와 위치를 지정하는 2개의 보기가 있는 컨테이너를 나타냅니다. `TwoPaneView`는 `Grid`에서 상속되므로 속성이 그리드에 적용되는 것이라고 생각하면 쉽습니다.

## <a name="set-up-twopaneview"></a>TwoPaneView 설정

앱에서 이중 화면 레이아웃을 만들려면 다음 지침을 따르세요.

1. [시작](index.md) 지침에 따라 NuGet을 추가하고 Android `MainActivity` 클래스를 구성합니다.
1. 다음 XAML을 사용하여 기본 `TwoPaneView`를 시작합니다.

    ```xaml
    <ContentPage
        xmlns:dualScreen="clr-namespace:Xamarin.Forms.DualScreen;assembly=Xamarin.Forms.DualScreen">
        <dualScreen:TwoPaneView>
            <dualScreen:TwoPaneView.Pane1>
                <StackLayout>
                    <Label Text="Pane1 Content" />
                </StackLayout>
            </dualScreen:TwoPaneView.Pane1>
            <dualScreen:TwoPaneView.Pane2>
                <StackLayout>
                    <Label Text="Pane2 Content" />
                </StackLayout>
            </dualScreen:TwoPaneView.Pane2>
        </dualScreen:TwoPaneView>
    </ContentPage>
    ```

> [!TIP]
> 위의 XAML은 `ContentPage` 요소에서 많은 공통 특성을 생략합니다. `TwoPaneView`를 앱에 추가할 때는 표시된 대로 `xmlns:dualScreen` 네임스페이스를 선언해야 합니다.

## <a name="understand-twopaneview-modes"></a>TwoPaneView 모드 이해

다음 모드 중 하나만 활성화할 수 있습니다.

- `SinglePane` - 현재 창 하나만 볼 수 있습니다.
- `Wide` - 두 창이 가로로 배치됩니다. 한 창은 왼쪽에, 다른 창은 오른쪽에 있습니다. 두 개 화면에서는 이것이 디바이스가 세로 방향일 때의 모드입니다.
- `Tall` - 두 창이 세로로 배치됩니다. 한 창은 위쪽에, 다른 창은 아래쪽에 있습니다. 두 개 화면에서는 이것이 디바이스가 가로 방향일 때의 모드입니다.

## <a name="control-twopaneview-when-its-only-on-one-screen"></a>한 화면에만 표시될 때 TwoPaneView 제어

다음 속성은 `TwoPaneView`가 하나의 화면을 차지하고 있는 경우에 적용됩니다.

- `MinTallModeHeight`는 컨트롤이 세로 모드가 되려면 필요한 최소 높이를 나타냅니다.
- `MinWideModeWidth`는 컨트롤이 가로 모드가 되려면 필요한 최소 너비를 나타냅니다.
- `Pane1Length`는 가로 모드에서 Pane1의 너비를, 세로 모드에서 Pane1의 높이를 설정하며 SinglePane 모드에서는 적용되지 않습니다.
- `Pane2Length`는 가로 모드에서 Pane2의 너비를, 세로 모드에서 Pane2의 높이를 설정하며 SinglePane 모드에서는 적용되지 않습니다.

> [!IMPORTANT]
> `TwoPaneView`가 두 개 화면에 걸쳐 있는 경우 이들 속성은 적용되지 않습니다.

## <a name="properties-that-apply-when-on-one-screen-or-two"></a>한 화면 또는 두 화면에 표시될 때 적용되는 속성

다음 속성은 `TwoPaneView`가 하나의 화면 또는 두 개의 화면을 차지하고 있는 경우에 적용됩니다.

- `TallModeConfiguration`은 세로 모드일 때 위쪽/아래쪽 정렬을 나타내거나 TwoPaneViewPriority에서 정의한 대로 단일 창만 표시할지 여부를 나타냅니다.
- `WideModeConfiguration`은 가로 모드일 때 왼쪽/오른쪽 정렬을 나타내거나 TwoPaneViewPriority에서 정의한 대로 단일 창만 표시할지 여부를 나타냅니다.
- `PanePriority`는 SinglePane 모드일 경우 Pane1와 Pane2 중 어느 것을 표시할지를 정합니다.

## <a name="related-links"></a>관련 링크

- [DualScreen(sample)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-dualscreendemos/)(DualScreen(샘플))

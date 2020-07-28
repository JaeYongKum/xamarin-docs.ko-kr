---
title: Xamarin.Forms 이중 화면 트리거
description: 이 문서에서는 Xamarin.Forms 이중 화면 트리거를 사용하여 XAML에서 사용자 인터페이스 변경에 응답하는 방법을 설명합니다.
ms.prod: xamarin
ms.assetid: 2181715D-3995-4E71-9A21-6B892F0B3B59
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/28/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 2e4d85077e1047f4158164d0c752570519c8ecdc
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86936840"
---
# <a name="xamarinforms-dual-screen-triggers"></a>Xamarin.Forms 이중 화면 트리거

![시험판 API](~/media/shared/preview.png "이 API는 현재 시험판임")

[`Xamarin.Forms.DualScreen`](xref:Xamarin.Forms.DualScreen) 네임스페이스에는 다음 두 가지 상태 트리거가 포함되어 있습니다.

- [`SpanModeStateTrigger`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger)는 연결된 레이아웃의 보기 모드가 변경될 때 [`VisualState`](xref:Xamarin.Forms.VisualState) 변경을 트리거합니다.
- `WindowSpanModeStateTrigger`는 창의 보기 모드가 변경될 때 [`VisualState`](xref:Xamarin.Forms.VisualState) 변경을 트리거합니다.

상태 트리거에 대한 자세한 내용은 [상태 트리거](~/xamarin-forms/app-fundamentals/triggers.md#state-triggers)를 참조하세요.

## <a name="span-mode-state-trigger"></a>범위 모드 상태 트리거

[`SpanModeStateTrigger`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger)는 연결된 레이아웃의 범위 모드가 변경될 때 [`VisualState`](xref:Xamarin.Forms.VisualState) 변경을 트리거합니다. 이 트리거에는 바인딩 가능한 속성이 하나 있습니다.

- [`SpanMode`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger.SpanMode) - [`VisualState`](xref:Xamarin.Forms.VisualState)가 적용되어야 하는 범위 모드를 나타내며 [`TwoPaneViewMode`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger.SpanMode) 형식입니다.

> [!NOTE]
> [`SpanModeStateTrigger`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger)는 [`StateTriggerBase`](xref:Xamarin.Forms.StateTriggerBase) 클래스에서 파생되며 이벤트 처리기를 [`IsActiveChanged`](xref:Xamarin.Forms.StateTriggerBase.IsActiveChanged) 이벤트에 연결할 수 있습니다.

다음 XAML 예제에서는 `SpanModeStateTrigger` 개체를 포함하는 [`Grid`](xref:Xamarin.Forms.Grid)을 보여 줍니다.

```xaml
<Grid>
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup>
            <VisualState x:Name="GridSingle">
                <VisualState.StateTriggers>
                    <dualScreen:SpanModeStateTrigger SpanMode="SinglePane"/>
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Green" />
                </VisualState.Setters>
            </VisualState>
            <VisualState x:Name="GridWide">
                <VisualState.StateTriggers>
                    <dualScreen:SpanModeStateTrigger SpanMode="Wide" />
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Red" />
                </VisualState.Setters>
            </VisualState>
            <VisualState x:Name="GridTall">
                <VisualState.StateTriggers>
                    <dualScreen:SpanModeStateTrigger SpanMode="Tall" />
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Purple" />
                </VisualState.Setters>
            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
    ...
</Grid>
```

이 예제에서 시각적 상태는 [`Grid`](xref:Xamarin.Forms.Grid) 개체에 설정됩니다. 하나의 창만 표시되는 경우 `Grid`의 배경색이 녹색이고, 창이 나란히 표시되는 경우 빨간색이며, 창이 위아래로 표시되는 경우 자주색입니다.

## <a name="window-span-mode-state-trigger"></a>창 범위 모드 상태 트리거

`WindowSpanModeStateTrigger`는 창의 범위 모드가 변경될 때 [`VisualState`](xref:Xamarin.Forms.VisualState) 변경을 트리거합니다. 이 트리거에는 바인딩 가능한 속성이 하나 있습니다.

- [`SpanMode`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger.SpanMode) - [`VisualState`](xref:Xamarin.Forms.VisualState)가 적용되어야 하는 범위 모드를 나타내며 [`TwoPaneViewMode`](xref:Xamarin.Forms.DualScreen.SpanModeStateTrigger.SpanMode) 형식입니다.

> [!NOTE]
> `WindowSpanModeStateTrigger`는 [`StateTriggerBase`](xref:Xamarin.Forms.StateTriggerBase) 클래스에서 파생되므로 이벤트 처리기를 [`IsActiveChanged`](xref:Xamarin.Forms.StateTriggerBase.IsActiveChanged) 이벤트에 연결할 수 있습니다.

다음 XAML 예제에서는 `WindowSpanModeStateTrigger` 개체를 포함하는 [`Grid`](xref:Xamarin.Forms.Grid)을 보여 줍니다.

```xaml
<Grid>
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup>
            <VisualState x:Name="NotSpanned">
                <VisualState.StateTriggers>
                    <dualScreen:WindowSpanModeStateTrigger SpanMode="SinglePane"/>
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Red" />
                </VisualState.Setters>
            </VisualState>
            <VisualState x:Name="Spanned">
                <VisualState.StateTriggers>
                    <dualScreen:WindowSpanModeStateTrigger SpanMode="Wide" />
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Green" />
                </VisualState.Setters>
            </VisualState>
                <VisualState x:Name="Tall">
                    <VisualState.StateTriggers>
                        <dualScreen:WindowSpanModeStateTrigger SpanMode="Tall" />
                    </VisualState.StateTriggers>
                    <VisualState.Setters>
                        <Setter Property="BackgroundColor" Value="Yellow" />
                    </VisualState.Setters>
                </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
    ...
</Grid>    
```

이 예제에서 시각적 상태는 [`Grid`](xref:Xamarin.Forms.Grid) 개체에 설정됩니다. 하나의 창만 표시되는 경우 `Grid`의 배경색이 빨간색이고, 창이 나란히 표시되는 경우 녹색이며, 창이 위아래로 표시되는 경우 노란색입니다.

## <a name="related-links"></a>관련 링크

- [Xamarin.Forms 트리거](~/xamarin-forms/app-fundamentals/triggers.md)
- [Xamarin.Forms Visual State Manager](~/xamarin-forms/user-interface/visual-state-manager.md)

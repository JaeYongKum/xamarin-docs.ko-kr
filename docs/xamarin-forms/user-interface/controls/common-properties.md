---
title: Xamarin.Forms공용 컨트롤 속성, 메서드 및 이벤트
description: 이 문서에서는 파생 클래스에서 일반적으로 사용 되는 VisualElement 클래스에 정의 된 공용 속성, 메서드 및 이벤트에 대해 설명 합니다.
ms.prod: xamarin
ms.assetId: 85A0CCF5-C1D8-40BB-927F-A4D944E5534D
ms.technology: xamarin-forms
author: profexorgeek
ms.author: jusjohns
ms.date: 07/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: b4c0ef44f528e3cbc56a27e98a1c38246736ff8c
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87918351"
---
# <a name="no-locxamarinforms-common-control-properties-methods-and-events"></a>Xamarin.Forms공용 컨트롤 속성, 메서드 및 이벤트

Xamarin.Forms `VisualElement` 클래스는 응용 프로그램에서 사용 되는 대부분의 컨트롤에 대 한 기본 클래스입니다 Xamarin.Forms . `VisualElement`클래스는 클래스 파생에 사용 되는 여러 [속성](#properties), [메서드](#methods)및 [이벤트](#events) 를 정의 합니다.

## <a name="properties"></a>속성

개체에서 사용할 수 있는 속성은 다음과 같습니다 [`VisualElement`](xref:Xamarin.Forms.VisualElement) .

### [`AnchorX`](xref:Xamarin.Forms.VisualElement.AnchorX)

`AnchorX`속성은 `double` 눈금 및 회전과 같은 변환에 대 한 X 축의 중심점을 정의 하는 값입니다. 기본값은 0.5입니다.

### [`AnchorY`](xref:Xamarin.Forms.VisualElement.AnchorY)

`AnchorY`속성은 `double` 눈금 및 회전과 같은 변환에 대 한 X 축의 중심점을 정의 하는 값입니다. 기본값은 0.5입니다.

### `Background`

`Background`속성은 `Brush` 모든 컨트롤에서 브러시를 배경으로 사용할 수 있도록 하는 값입니다. 기본값은 `Brush.Default`입니다.

### [`BackgroundColor`](xref:Xamarin.Forms.VisualElement.BackgroundColor)

`BackgroundColor`속성은 `Color` 컨트롤의 배경색을 결정 하는입니다. 설정 하지 않으면 배경이 `Color` 투명으로 렌더링 되는 기본 개체가 됩니다.

### [`Behaviors`](xref:Xamarin.Forms.VisualElement.Behaviors)

`Behaviors`속성은 `List` 개체의입니다 `Behavior` . 동작을 사용 하면 다시 사용 가능한 기능을 목록에 추가 하 여 요소에 연결할 수 있습니다 `Behaviors` . 클래스에 대 한 자세한 내용은 `Behavior` [ Xamarin.Forms 동작](~/xamarin-forms/app-fundamentals/behaviors/index.md)을 참조 하세요.

### [`Bounds`](xref:Xamarin.Forms.VisualElement.Bounds)

`Bounds`속성은 `Rectangle` 컨트롤이 차지 하는 공간을 나타내는 읽기 전용 개체입니다. `Bounds`속성 값은 레이아웃 주기 동안 할당 됩니다. 에는 `Rectangle` `struct` 사각형의 교차 및 포함을 테스트 하는 데 유용한 속성과 메서드가 포함 되어 있습니다. 자세한 내용은 [ Xamarin.Forms 사각형 API](xref:Xamarin.Forms.Rectangle)를 참조 하세요.

### `Clip`

`Clip`속성은 `Geometry` 요소의 내용에 대 한 개요를 정의 하는 개체입니다. 클립을 정의 하려면 `Geometry` 와 같은 개체를 사용 `EllipseGeometry` 하 여 요소의 속성을 설정 `Clip` 합니다. 기 하 도형 영역에 있는 영역만 표시 됩니다. 자세한 내용은 [Geometry를 사용 하 여 클리핑](~/xamarin-forms/user-interface/shapes/geometries.md#clip-with-a-geometry)을 참조 하세요.

### [`Effects`](xref:Xamarin.Forms.Element.Effects)

`Effects`속성은 `List` `Effect` `Element` (f:)에서 상속 되는 개체의입니다 Xamarin.Forms . Element) 클래스 효과를 사용 하면 네이티브 컨트롤을 사용자 지정할 수 있으며, 일반적으로 작은 스타일 변경에 사용 됩니다. 클래스에 대 한 자세한 내용은 `Effect` [ Xamarin.Forms 효과](~/xamarin-forms/app-fundamentals/effects/index.md)를 참조 하세요.

### [`FlowDirection`](xref:Xamarin.Forms.VisualElement.FlowDirection)

`FlowDirection`속성은 `FlowDirection` 열거형 값입니다. 흐름 방향은, 또는로 설정 될 수 있으며 `MatchParent` `LeftToRight` `RightToLeft` 레이아웃 순서와 방향을 결정 합니다. `FlowDirection`속성은 일반적으로 오른쪽에서 왼쪽으로 읽는 언어를 지 원하는 데 사용 됩니다.

### [`Height`](xref:Xamarin.Forms.VisualElement.Height)

`Height`속성은 `double` 컨트롤의 렌더링 된 높이를 설명 하는 읽기 전용 값입니다. `Height`속성은 레이아웃 주기 동안 계산 되며 직접 설정할 수 없습니다. [HeightRequest 속성](#heightrequest)을 사용 하 여 컨트롤의 높이를 요청할 수 있습니다.

### [`HeightRequest`](xref:Xamarin.Forms.VisualElement.HeightRequest)

`HeightRequest`속성은 `double` 컨트롤의 원하는 높이를 결정 하는 값입니다. 컨트롤의 절대 높이가 요청 된 값과 일치 하지 않을 수 있습니다. 자세한 내용은 [요청 속성](#request-properties)을 참조 하세요.

### [`InputTransparent`](xref:Xamarin.Forms.VisualElement.InputTransparent)

`InputTransparent`속성은 `bool` 컨트롤에서 사용자 입력을 받을지 여부를 결정 하는입니다. 기본값은 `false` 로, 요소가 입력을 받도록 합니다. 이 속성은 설정 될 때 자식 요소로 전송 됩니다. `InputTransparent`레이아웃 클래스에서 속성을로 설정 `true` 하면 레이아웃 내의 모든 요소가 입력을 받지 않게 됩니다.

### [`IsEnabled`](xref:Xamarin.Forms.VisualElement.IsEnabled)

`IsEnabled`속성은 `bool` 컨트롤이 사용자 입력에 반응 하는지 여부를 결정 하는 값입니다. 기본값은 `true`입니다. 이 속성을 false로 설정 하면 컨트롤에서 사용자 입력을 허용 하지 않습니다.

### [`IsFocused`](xref:Xamarin.Forms.VisualElement.IsFocused)

`IsFocused`속성은 `bool` 컨트롤이 현재 포커스가 있는 개체 인지 여부를 설명 하는 값입니다. [`Focus`](#focus)컨트롤에서 메서드를 호출 하면 `IsFocused` 값이 true로 설정 됩니다. 메서드를 호출 [`Unfocus`](#unfocus) 하면이 속성이 false로 설정 됩니다.

### [`IsTabStop`](xref:Xamarin.Forms.VisualElement.IsTabStop)

`IsTabStop`속성은 `bool` 사용자가 tab 키를 사용 하 여 컨트롤을 이동할 때 컨트롤이 포커스를 받을 수 있는지 여부를 정의 하는 값입니다. 이 속성이 false 이면 `TabIndex` 속성이 적용 되지 않습니다.

### [`IsVisible`](xref:Xamarin.Forms.VisualElement.IsVisible)

`IsVisible`속성은 `bool` 컨트롤이 렌더링 되는지 여부를 결정 하는 값입니다. `IsVisible`속성이 false로 설정 된 컨트롤은 표시 되지 않으며, 레이아웃 주기 중에 공간 계산에 대 한 고려 되지 않으며 사용자 입력을 허용할 수 없습니다.

### [`MinimumHeightRequest`](xref:Xamarin.Forms.VisualElement.MinimumHeightRequest)

`MinimumHeightRequest`속성은 `double` 두 요소가 제한 된 공간에 대해 경쟁 하는 경우 오버플로를 처리 하는 방법을 결정 하는 값입니다. 속성을 설정 하면 `MinimumHeightRequest` 레이아웃 프로세스에서 요소를 요청 된 최소 차원까지 축소할 수 있습니다. 을 지정 하지 않으면 `MinimumHeightRequest` 기본값은-1이 고, 레이아웃 프로세스는를 최소값으로 간주 합니다 `HeightRequest` . 즉, 값이 없는 요소는 `MinimumHeightRequest` 확장 가능한 높이를 갖지 않습니다.

자세한 내용은 [최소 요청 속성](#minimum-request-properties)을 참조 하세요.

### [`MinimumWidthRequest`](xref:Xamarin.Forms.VisualElement.MinimumWidthRequest)

`MinimumWidthRequest`속성은 `double` 두 요소가 제한 된 공간에 대해 경쟁 하는 경우 오버플로를 처리 하는 방법을 결정 하는 값입니다. 속성을 설정 하면 `MinimumWidthRequest` 레이아웃 프로세스에서 요소를 요청 된 최소 차원까지 축소할 수 있습니다. 을 지정 하지 않으면 `MinimumWidthRequest` 기본값은-1이 고, 레이아웃 프로세스는를 최소값으로 간주 합니다 `WidthRequest` . 즉, 값이 없는 요소는 `MinimumWidthRequest` 확장 가능한 너비를 갖지 않습니다.

자세한 내용은 [최소 요청 속성](#minimum-request-properties)을 참조 하세요.

### [`Opacity`](xref:Xamarin.Forms.VisualElement.Opacity)

`Opacity`속성은 `double` 렌더링 중에 컨트롤의 불투명도를 결정 하는 0에서 1 사이의 값입니다. 이 속성의 기본값은 1.0입니다. 0에서 1 사이의 범위 밖의 값은 고정입니다. 속성은 `Opacity` 속성이 인 경우에만 적용 됩니다 [`IsVisible`](#isvisible) `true` . 불투명은 반복적으로 적용 됩니다. 따라서 부모 컨트롤의 불투명도가 0.5이 고 자식에 0.5 불투명도가 있는 경우 자식은 효과적인 0.25 불투명도 값을 사용 하 여 렌더링 됩니다. `Opacity`입력 컨트롤의 속성을 0으로 설정 하면 정의 되지 않은 동작이 발생 합니다.

### [`Parent`](xref:Xamarin.Forms.Element.Parent)

`Parent` 속성은 `Element` 클래스에서 상속됩니다. 이 속성은 `Element` 컨트롤의 부모인 개체입니다. `Parent`속성은 일반적으로 요소에서 다른 요소의 자식으로 추가 될 때 자동으로 설정 됩니다.

### [`Resources`](xref:Xamarin.Forms.VisualElement.Resources)

`Resources`속성은 `ResourceDictionary` 일반적으로 XAML에서 런타임에 채워지는 키/값 쌍으로 채워지는 인스턴스입니다. 이 사전을 사용 하면 응용 프로그램 개발자가 컴파일 시간과 런타임에 XAML에 정의 된 개체를 다시 사용할 수 있습니다. 사전의 키는 `x:Key` XAML 태그의 특성에서 채워집니다. XAML에서 만든 개체가 `ResourceDictionary` 지정 된 키에 대 한에 삽입 됩니다. 초기화 된 후

자세한 내용은 [리소스 사전](~/xamarin-forms/xaml/resource-dictionaries.md)을 참조 하세요.

### [`Rotation`](xref:Xamarin.Forms.VisualElement.Rotation)

`Rotation`속성은 `double` Z 축에 대 한 회전 (도)을 정의 하는 0에서 360 사이의 값입니다. 이 속성의 기본값은 0입니다. 회전은 및 값을 기준으로 적용 됩니다 [`AnchorX`](#anchorx) [`AnchorY`](#anchory) .

### [`RotationX`](xref:Xamarin.Forms.VisualElement.RotationX)

`RotationX`속성은 `double` X 축에 대 한 회전 (도)을 정의 하는 0에서 360 사이의 값입니다. 이 속성의 기본값은 0입니다. 회전은 및 값을 기준으로 적용 됩니다 [`AnchorX`](#anchorx) [`AnchorY`](#anchory) .

### [`RotationY`](xref:Xamarin.Forms.VisualElement.RotationY)

`RotationY`속성은 `double` Y 축에 대 한 회전 (도)을 정의 하는 0에서 360 사이의 값입니다. 이 속성의 기본값은 0입니다. 회전은 및 값을 기준으로 적용 됩니다 [`AnchorX`](#anchorx) [`AnchorY`](#anchory) .

### [`Scale`](xref:Xamarin.Forms.VisualElement.Scale)

`Scale`속성은 `double` 컨트롤의 소수 자릿수를 정의 하는 값입니다. 이 속성의 기본값은 1.0입니다. 소수 자릿수는 및 값을 기준으로 적용 됩니다 [`AnchorX`](#anchorx) [`AnchorY`](#anchory) .

### [`ScaleX`](xref:Xamarin.Forms.VisualElement.ScaleX)

`ScaleX`속성은 `double` X 축을 따라 컨트롤의 소수 자릿수를 정의 하는 값입니다. 이 속성의 기본값은 1.0입니다. `ScaleX`속성은 값을 기준으로 적용 됩니다 [`AnchorX`](#anchorx) .

### [`ScaleY`](xref:Xamarin.Forms.VisualElement.ScaleY)

`ScaleY`속성은 `double` Y 축을 따라 컨트롤의 소수 자릿수를 정의 하는 값입니다. 이 속성의 기본값은 1.0입니다. `ScaleY`속성은 값을 기준으로 적용 됩니다 [`AnchorY`](#anchory) .

### [`Style`](xref:Xamarin.Forms.NavigableElement.Style)

`Style` 속성은 `NavigableElement` 클래스에서 상속됩니다. 이 속성은 클래스의 인스턴스입니다 `Style` . 클래스에는 `Style` 시각적 요소의 모양 및 동작을 정의 하는 트리거, setter 및 동작이 포함 되어 있습니다. 자세한 내용은 [ Xamarin.Forms XAML 스타일](~/xamarin-forms/user-interface/styles/xaml/index.md)을 참조 하세요.

### [`StyleClass`](xref:Xamarin.Forms.NavigableElement.StyleClass)

`StyleClass`속성은 `string` 클래스의 이름을 나타내는 개체의 목록입니다 `Style` . 이 속성은 `NavigableElement` 클래스에서 상속됩니다. `StyleClass`속성을 사용 하면 여러 스타일 특성을 인스턴스에 적용할 수 있습니다 `VisualElement` . 자세한 내용은 [ Xamarin.Forms 스타일 클래스](~/xamarin-forms/user-interface/styles/xaml/style-class.md)를 참조 하세요.

### [`TabIndex`](xref:Xamarin.Forms.VisualElement.TabIndex)

`TabIndex`속성은 `int` tab 키를 사용 하 여 컨트롤을 이동할 때 제어 순서를 정의 하는 값입니다. `TabIndex`속성은 `ITabStopElement` 클래스에서 구현 하는 인터페이스에 정의 된 속성에 대 한 구현입니다 `VisualElement` .

### [`TranslationX`](xref:Xamarin.Forms.VisualElement.TranslationX)

`TranslationX`속성은 `double` X 축에 적용할 델타 변환을 정의 하는 값입니다. 변환은 레이아웃 후에 적용 되며 일반적으로 애니메이션을 적용 하는 데 사용 됩니다. 요소를 부모 컨테이너의 범위 밖으로 변환 하면 입력이 작동 하지 않습니다.

자세한 내용은 [의 Xamarin.Forms 애니메이션 ](~/xamarin-forms/user-interface/animation/index.md)을 참조 하세요.

### [`TranslationY`](xref:Xamarin.Forms.VisualElement.TranslationY)

`TranslationY`속성은 `double` Y 축에 적용할 델타 변환을 정의 하는 값입니다. 변환은 레이아웃 후에 적용 되며 일반적으로 애니메이션을 적용 하는 데 사용 됩니다. 요소를 부모 컨테이너의 범위 밖으로 변환 하면 입력이 작동 하지 않습니다.

자세한 내용은 [의 Xamarin.Forms 애니메이션 ](~/xamarin-forms/user-interface/animation/index.md)을 참조 하세요.

### [`Triggers`](xref:Xamarin.Forms.VisualElement.Triggers)

`Triggers`속성은 개체의 읽기 전용입니다 `List` `TriggerBase` . 트리거를 사용 하면 응용 프로그램 개발자가 이벤트 또는 속성 변경에 대 한 응답으로 컨트롤의 시각적 모양을 변경 하는 작업을 XAML로 표현할 수 있습니다. 자세한 내용은 [ Xamarin.Forms 트리거](~/xamarin-forms/app-fundamentals/triggers.md)를 참조 하세요.

### [`Visual`](xref:Xamarin.Forms.VisualElement.Visual)

`Visual`속성은 `IVisual` 렌더러를 만들고 선택적으로 인스턴스에 적용할 수 있도록 하는 인스턴스입니다 `VisualElement` . `Visual`속성은 부모와 일치 하도록 설정 되므로 구성 요소에 대 한 렌더러를 정의 하면 해당 구성 요소의 모든 자식에도 적용 됩니다. 컨트롤이 나 해당 상위 항목에 사용자 지정 렌더러를 설정 하지 않은 경우 기본 Xamarin.Forms 렌더러가 사용 됩니다. 자세한 내용은 [ Xamarin.Forms 시각적 개체](~/xamarin-forms/user-interface/visual/index.md)를 참조 하세요.

### [`Width`](xref:Xamarin.Forms.VisualElement.Width)

`Width`속성은 `double` 컨트롤의 렌더링 된 너비를 설명 하는 읽기 전용 값입니다. `Width`속성은 레이아웃 주기 동안 계산 되며 직접 설정할 수 없습니다. 컨트롤의 너비는 너비 [요청 속성](#widthrequest)을 사용 하 여 요청할 수 있습니다.

### [`WidthRequest`](xref:Xamarin.Forms.VisualElement.WidthRequest)

`WidthRequest`속성은 `double` 컨트롤의 원하는 너비를 결정 하는 값입니다. 컨트롤의 절대 너비가 요청 된 값과 일치 하지 않을 수 있습니다. 자세한 내용은 [요청 속성](#request-properties)을 참조 하세요.

### [`X`](xref:Xamarin.Forms.VisualElement.X)

`X`속성은 `double` 컨트롤의 현재 X 위치를 설명 하는 읽기 전용 값입니다.

### [`Y`](xref:Xamarin.Forms.VisualElement.Y)

`Y`속성은 `double` 컨트롤의 현재 Y 위치를 설명 하는 읽기 전용 값입니다.

## <a name="methods"></a>메서드

클래스에서 사용할 수 있는 메서드는 다음과 같습니다 `VisualElement` . 전체 목록은 [Visualelement API 메서드](xref:Xamarin.Forms.VisualElement#methods)를 참조 하세요.

### [`FindByName`](xref:Xamarin.Forms.Element.FindByName*)

`FindByName`메서드는 클래스에서 상속 되며 `Element` 다음과 같은 시그니처가 있습니다.

```csharp
public object FindByName (string name)
```

이 메서드는 제공 된 인수에 대 한 모든 자식 요소를 검색 `name` 하 여 지정 된 이름을 가진 요소를 반환 합니다. 일치하는 항목이 없으면 `null`이 반환됩니다.

### [`Focus`](xref:Xamarin.Forms.VisualElement.Focus)

`Focus`메서드는 요소에 포커스를 설정 하려고 시도 합니다. 이 메서드의 서명은 다음과 같습니다.

```csharp
public bool Focus ()
```

`Focus`이 메서드는 `true` 키보드 포커스가 성공적으로 설정 된 경우를 반환 하 고, `false` 메서드 호출로 인해 포커스가 변경 되지 않은 경우를 반환 합니다. 이 메서드가 작동 하려면 요소가 포커스를 받을 수 있어야 합니다. `Focus`화면에 있거나 지정 되지 않은 요소에 대해 메서드를 호출 하면 정의 되지 않은 동작이 발생 합니다.

### [`Unfocus`](xref:Xamarin.Forms.VisualElement.Unfocus)

`Unfocus`메서드는 요소에서 포커스를 제거 하려고 시도 합니다. 이 메서드의 서명은 다음과 같습니다.

```csharp
public void Unfocus ()
```

이 메서드가 작동 하려면 요소에 이미 포커스가 있어야 합니다.

## <a name="events"></a>이벤트

클래스에서 사용할 수 있는 이벤트는 다음과 같습니다 `VisualElement` . 전체 목록은 [ Xamarin.Forms Visualelement 이벤트](xref:Xamarin.Forms.VisualElement#events)를 참조 하세요.

### [`Focused`](xref:Xamarin.Forms.VisualElement.Focused)

`Focused`인스턴스가 포커스를 받을 때마다 이벤트가 발생 합니다 `VisualElement` . 이 이벤트는 스택을 통해 버블링 되지 않으며 Xamarin.Forms 네이티브 컨트롤에서 직접 수신 됩니다. 이 이벤트는 [`IsFocused`](#isfocused) 속성 setter에서 내보냅니다.

### [`SizeChanged`](xref:Xamarin.Forms.VisualElement.SizeChanged)

`SizeChanged`이 이벤트는 `VisualElement` 인스턴스 `Height` 또는 속성이 변경 될 때마다 발생 합니다 `Width` . 개발자가 변경 후 이벤트에 응답 하는 대신 크기 변경에 직접 응답 하려는 경우 가상 메서드를 대신 구현 해야 합니다 [`OnSizeAllocated`](xref:Xamarin.Forms.VisualElement.OnSizeAllocated*) .

### [`Unfocused`](xref:Xamarin.Forms.VisualElement.Unfocused)

`Unfocused`인스턴스가 포커스를 잃을 때마다 이벤트가 발생 합니다 `VisualElement` . 이 이벤트는 스택을 통해 버블링 되지 않으며 Xamarin.Forms 네이티브 컨트롤에서 직접 수신 됩니다. 이 이벤트는 [`IsFocused`](#isfocused) 속성 setter에서 내보냅니다.

## <a name="units-of-measurement"></a>측정 단위

Android, iOS 및 UWP 플랫폼에는 장치에 따라 다를 수 있는 여러 단위가 있습니다. Xamarin.Forms장치 및 플랫폼에서 단위를 정규화 하는 플랫폼 독립적인 측정 단위를 사용 합니다. 에는 인치당 160 단위 또는 센티미터 당 64 단위가 있습니다 Xamarin.Forms .

## <a name="request-properties"></a>요청 속성

이름에 "request"가 포함 된 속성은 실제 렌더링 된 값과 일치 하지 않을 수 있는 원하는 값을 정의 합니다. 예를 들어,가 `HeightRequest` 150로 설정 되어 있지만 레이아웃에서 100 단위에 대 한 공간을 허용 하는 경우 `Height` 컨트롤의 렌더링은 100만 됩니다. 렌더링 된 크기는 사용 가능한 공간 및 포함 된 구성 요소의 영향을 받습니다.

## <a name="minimum-request-properties"></a>최소 요청 속성

최소 요청 속성에는 `MinimumHeightRequest` 및 `MinimumWidthRequest` 가 포함 되며,는 요소가 서로를 기준으로 오버플로를 처리 하는 방식을 보다 정확 하 게 제어할 수 있도록 하기 위한 것입니다. 그러나 이러한 속성과 관련 된 레이아웃 동작에는 몇 가지 중요 한 고려 사항이 있습니다.

### <a name="unspecified-minimum-property-values"></a>지정 되지 않은 최소 속성 값

최소값을 설정 하지 않으면 최소 속성의 기본값은-1입니다. 레이아웃 프로세스에서는이 값을 무시 하 고 절대 값을 최소값으로 간주 합니다. 이 동작의 실제 결과는 최소 값이 지정 되지 않은 요소가 축소 **되지** 않는 것입니다. 최소값이 지정 된 요소가 축소 **됩니다** .

다음 XAML에서는 가로의 두 요소를 보여 줍니다 `BoxView` `StackLayout` .

```xaml
<StackLayout Orientation="Horizontal">
    <BoxView HeightRequest="100" BackgroundColor="Purple" WidthRequest="500"></BoxView>
    <BoxView HeightRequest="100" BackgroundColor="Green" WidthRequest="500" MinimumWidthRequest="250"></BoxView>
</StackLayout>
```

첫 번째 `BoxView` 인스턴스는 500의 너비를 요청 하 고 최소 너비를 지정 하지 않습니다. 두 번째 `BoxView` 인스턴스는 너비 500 및 최소 너비 250를 요청 합니다. 부모 요소의 너비가 `StackLayout` 요청 된 너비의 두 구성 요소를 모두 포함 하도록 충분 하지 않은 경우 첫 번째 `BoxView` 인스턴스는 지정 된 다른 최소값이 없으므로 레이아웃 프로세스에서 최소 너비 500을 갖는 것으로 간주 됩니다. 두 번째 `BoxView` 인스턴스는 250로 축소 될 수 있으며 너비가 250 단위까지 감소할 수 있습니다.

첫 번째 `BoxView` 인스턴스가 최소 너비로 축소 되도록 하려면 원하는 동작을 `MinimumWidthRequest` 0과 같은 유효한 값으로 설정 해야 합니다.

### <a name="minimum-and-absolute-property-values"></a>최소 및 절대 속성 값

최 솟 값이 절대값 보다 크면 동작이 정의 되지 않습니다. 예를 들어 `WidthRequest` 가 100로 설정 된 경우 속성은 100을 초과 하면 안 됩니다 `MinimumWidthRequest` . 최소 속성 값을 지정 하는 경우 절대 값이 최소값 보다 큰지 항상 절대값을 지정 해야 합니다.

### <a name="minimum-properties-within-a-grid"></a>그리드 내의 최소 속성

`Grid`레이아웃에는 행과 열의 상대적인 크기 조정을 위한 고유한 시스템이 있습니다. `MinimumWidthRequest` `MinimumHeightRequest` 레이아웃 내에서 또는를 사용 `Grid` 하면 효과가 없습니다. 자세한 내용은 [ Xamarin.Forms 표](~/xamarin-forms/user-interface/layouts/grid.md)를 참조 하세요.

## <a name="related-links"></a>관련 링크

- [VisualElement API](xref:Xamarin.Forms.VisualElement)

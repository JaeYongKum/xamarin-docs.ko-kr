---
title: 연결된 속성
description: 이 문서에서는 Attached Properties에 대한 소개와 어떻게 만들고 사용하는지에 대해 알아봅니다.
ms.prod: xamarin
ms.assetid: 6E9DCDC3-A0E4-46A6-BAA9-4FEB6DF8A5A8
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/02/2016
ms.openlocfilehash: 78dd2d3a63cd0e2b6ab1e6876dd82f49f5580f0b
ms.sourcegitcommit: d0e6436edbf7c52d760027d5e0ccaba2531d9fef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75489975"
---
# <a name="attached-properties"></a>연결된 속성

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/effects-shadoweffect)


연결 자체 클래스를 정의 하지 않는 속성에 대 한 값을 할당 하는 개체 속성을 사용 합니다. 예를 들어, 자식 요소를 사용할 수 있습니다를 연결 된 속성의 사용자 인터페이스에 표시 되는 방식을 부모 요소에 알림을 보내야 합니다. 합니다 [ `Grid` ](xref:Xamarin.Forms.Grid) 행과 열을 설정 하 여 지정할 수는 자식 컨트롤을 사용 하는 `Grid.Row` 및 `Grid.Column` 연결 된 속성입니다. `Grid.Row` 및 `Grid.Column` 은 자식 요소에 설정 되므로 연결 된 속성을 `Grid`, 대신에 `Grid` 자체.

바인딩 가능한 속성 다음과 같은 시나리오에서 연결 된 속성으로 구현 해야 합니다.

- 속성 설정 메커니즘을 사용할 수 있는 클래스에 대 한 이외의 필요한 경우 클래스를 정의 합니다.
- 경우 클래스는 다른 클래스와 손쉽게 통합할 수 해야 하는 서비스를 나타냅니다.

바인딩 가능한 속성에 대 한 자세한 내용은 참조 하세요. [바인딩 가능한 속성](~/xamarin-forms/xaml/bindable-properties.md)합니다.

## <a name="create-an-attached-property"></a>연결 된 속성 만들기

연결된 된 속성을 만드는 프로세스는 다음과 같습니다.

1. 만들기는 [ `BindableProperty` ](xref:Xamarin.Forms.BindableProperty) 중 하나를 사용 하 여 인스턴스를 [ `CreateAttached` ](xref:Xamarin.Forms.BindableProperty.CreateAttached*) 메서드 오버 로드 합니다.
1. 제공할 `static` `Get` *PropertyName* 하 고 `Set` *PropertyName* 연결된 된 속성에 대 한 접근자 메서드.

### <a name="create-a-property"></a>속성 만들기

다른 형식에서 사용 하 여 연결된 된 속성을 만들 때 속성 만들어지는 클래스에서 파생 않아도 [ `BindableObject` ](xref:Xamarin.Forms.BindableObject)합니다. 그러나 합니다 *대상* 접근자에 대 한 속성의 수 또는 컨트롤에서 파생 해야 [ `BindableObject` ](xref:Xamarin.Forms.BindableObject)합니다.

연결된 된 속성을 선언 하 여 만들 수 있습니다는 `public static readonly` 형식의 속성 [ `BindableProperty` ](xref:Xamarin.Forms.BindableProperty)합니다. 반환된 된 값 중 하나에 바인딩할 수 있는 속성을 설정 해야 합니다 [ `BindableProperty.CreateAttached` ](xref:Xamarin.Forms.BindableProperty.CreateAttached(System.String,System.Type,System.Type,System.Object,Xamarin.Forms.BindingMode,Xamarin.Forms.BindableProperty.ValidateValueDelegate,Xamarin.Forms.BindableProperty.BindingPropertyChangedDelegate,Xamarin.Forms.BindableProperty.BindingPropertyChangingDelegate,Xamarin.Forms.BindableProperty.CoerceValueDelegate,Xamarin.Forms.BindableProperty.CreateDefaultValueDelegate)) 메서드 오버 로드 합니다. 소유 하는 클래스의 이지만 멤버 정의 외부 본문 내에서 선언 해야 합니다.

다음 코드는 연결된 된 속성의 예를 보여 줍니다.

```csharp
public static readonly BindableProperty HasShadowProperty =
  BindableProperty.CreateAttached ("HasShadow", typeof(bool), typeof(ShadowEffect), false);
```

명명 된 연결된 된 속성을 이렇게 `HasShadow`, 형식의 `bool`합니다. 속성을 소유 하는 `ShadowEffect` 클래스 및 기본 값 `false`합니다. 연결 된 속성에 대 한 명명 규칙은 연결 된 속성 식별자에 지정 된 속성 이름과 일치 해야 하는 `CreateAttached` 메서드를 추가 하는 "Property"를 사용 하 여 합니다. 따라서 위의 예제에서는 연결 된 속성 식별자의 `HasShadowProperty`합니다.

생성 중에 지정할 수 있는 매개 변수를 포함 하 여 바인딩 가능한 속성을 만드는 방법에 대 한 자세한 내용은 [바인딩 가능한 속성 만들기](~/xamarin-forms/xaml/bindable-properties.md#consume-a-bindable-property)를 참조 하세요.

### <a name="create-accessors"></a>접근자 만들기

정적 `Get` *PropertyName* 하 고 `Set` *PropertyName* 메서드는 필요한 연결된 된 속성의 접근자로, 그렇지 않으면 속성 시스템의 사용할 수 없습니다 됩니다는 연결 된 속성입니다. 합니다 `Get` *PropertyName* 접근자는 다음 서명을 준수 해야 합니다.

```csharp
public static valueType GetPropertyName(BindableObject target)
```

합니다 `Get` *PropertyName* 접근자 해당 포함 된 값을 반환 해야 `BindableProperty` 연결된 된 속성에 대 한 필드입니다. 이 호출 하 여 수행할 수 있습니다 합니다 [ `GetValue` ](xref:Xamarin.Forms.BindableObject.GetValue(Xamarin.Forms.BindableProperty)) 메서드 값을 가져올를 바인딩 가능 속성 식별자에 전달 하 고 다음 결과 값을 필요한 형식으로 캐스팅 합니다.

합니다 `Set` *PropertyName* 접근자는 다음 서명을 준수 해야 합니다.

```csharp
public static void SetPropertyName(BindableObject target, valueType value)
```

합니다 `Set` *PropertyName* 접근자는 해당 값을 설정 해야 `BindableProperty` 연결된 된 속성에 대 한 필드입니다. 이 호출 하 여 수행할 수 있습니다 합니다 [ `SetValue` ](xref:Xamarin.Forms.BindableObject.SetValue(Xamarin.Forms.BindableProperty,System.Object)) 값 및 설정할 값을 설정 하는 바인딩 가능한 속성 식별자를 전달 하는 메서드.

두 접근자에 대해 합니다 *대상* 개체의 수 또는 컨트롤에서 파생 해야 [ `BindableObject` ](xref:Xamarin.Forms.BindableObject)합니다.

다음 코드 예제에서는 대 한 접근자를 `HasShadow` 연결 된 속성:

```csharp
public static bool GetHasShadow (BindableObject view)
{
  return (bool)view.GetValue (HasShadowProperty);
}

public static void SetHasShadow (BindableObject view, bool value)
{
  view.SetValue (HasShadowProperty, value);
}
```

### <a name="consume-an-attached-property"></a>연결 된 속성 사용

연결된 된 속성을 만든 후에 XAML 또는 코드에서 사용할 수 있습니다. XAML, 공용 언어 런타임 (CLR) 네임 스페이스 이름이 고 필요에 따라 어셈블리 이름이 나타내는 네임 스페이스 선언을 사용 하 여 접두사를 사용 하 여 네임 스페이스를 선언 하 여 작업을 수행 합니다. 자세한 내용은 [XAML 네임 스페이스](~/xamarin-forms/xaml/namespaces.md)합니다.

다음 코드 예제에서는 사용자 지정 형식을 참조 하는 응용 프로그램 코드와 동일한 어셈블리 내에 정의 된 연결된 된 속성을 포함 하는 사용자 지정 형식에 대 한 XAML 네임 스페이스를 보여 줍니다.

```xaml
<ContentPage ... xmlns:local="clr-namespace:EffectsDemo" ...>
  ...
</ContentPage>
```

다음 XAML 코드 예제에서 설명한으로 특정 컨트롤에 연결된 된 속성을 설정 하는 경우에 다음 네임 스페이스 선언을 사용 됩니다.

```xaml
<Label Text="Label Shadow Effect" local:ShadowEffect.HasShadow="true" />
```

동등한 C# 코드는 다음 코드 예제와 같습니다.

```csharp
var label = new Label { Text = "Label Shadow Effect" };
ShadowEffect.SetHasShadow (label, true);
```

### <a name="consume-an-attached-property-with-a-style"></a>스타일을 사용 하 여 연결 된 속성 사용

또한 연결 된 속성 스타일으로 컨트롤을 추가할 수 있습니다. 다음 XAML 코드 예제는 *명시적* 스타일을 사용 하는 `HasShadow` 연결 된 속성에 적용할 수 있는 [ `Label` ](xref:Xamarin.Forms.Label) 컨트롤:

```xaml
<Style x:Key="ShadowEffectStyle" TargetType="Label">
  <Style.Setters>
    <Setter Property="local:ShadowEffect.HasShadow" Value="true" />
  </Style.Setters>
</Style>
```

다음 코드 예제에 설명된 대로 `StaticResource` 태그 확장을 사용하여 해당 [`Style`](xref:Xamarin.Forms.NavigableElement.Style) 속성을 `Style` 인스턴스로 설정하면 [`Style`](xref:Xamarin.Forms.Style)을 [`Label`](xref:Xamarin.Forms.Label)에 적용할 수 있습니다.

```xaml
<Label Text="Label Shadow Effect" Style="{StaticResource ShadowEffectStyle}" />
```

스타일에 대한 자세한 내용은 [스타일](~/xamarin-forms/user-interface/styles/index.md)을 참조하세요.

## <a name="advanced-scenarios"></a>고급 시나리오

연결된 된 속성을 만들 때 연결 된 속성을 고급 시나리오를 사용 하도록 설정할 수 있는 선택적 매개 변수는 여러 가지가 있습니다. 여기에 속성 변경 내용 감지 속성 값의 유효성을 검사 하 고 속성 값을 강제 변환 합니다. 자세한 내용은 [고급 시나리오](~/xamarin-forms/xaml/bindable-properties.md#advanced-scenarios)를 참조 하십시오.

## <a name="related-links"></a>관련 링크

- [바인딩 가능한 속성](~/xamarin-forms/xaml/bindable-properties.md)
- [XAML 네임스페이스](~/xamarin-forms/xaml/namespaces.md)
- [그림자 효과(샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/effects-shadoweffect)
- [BindableProperty API](xref:Xamarin.Forms.BindableProperty)
- [BindableObject API](xref:Xamarin.Forms.BindableObject)

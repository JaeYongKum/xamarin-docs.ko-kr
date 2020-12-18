---
title: Xamarin.Forms RelativeLayout
description: Xamarin.FormsRelativeLayout는 레이아웃 또는 형제 요소의 속성을 기준으로 위치 및 크기 자식에 사용 됩니다.
ms.prod: xamarin
ms.assetid: 2530BCB8-01B8-4C4F-BF14-CA53659F1B5A
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/13/2020
ms.custom: contperf-fy21q1
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 22e7611cbe9aaad00f3b512cbe1a44bcc3f3541b
ms.sourcegitcommit: c5e72d2ca4152b62ab6583f0dbe84b3ba29d8283
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97677540"
---
# <a name="no-locxamarinforms-relativelayout"></a>Xamarin.Forms RelativeLayout

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](/samples/xamarin/xamarin-forms-samples/userinterface-relativelayoutdemos)

[![::: no loc (Xamarin.ios)::: RelativeLayout](relativelayout-images/layouts.png)](relativelayout-images/layouts-large.png#lightbox)

는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 레이아웃이 나 형제 요소의 속성을 기준으로 자식을 배치 하 고 크기를 조정 하는 데 사용 됩니다. 이를 통해 장치 크기에 비례하여 크기를 조정 하는 Ui를 만들 수 있습니다. 또한 다른 레이아웃 클래스와 달리는 `RelativeLayout` 겹칠 수 있도록 자식을 배치할 수 있습니다.

[`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)클래스는 다음 속성을 정의 합니다.

- [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty). 형식의 이며, [`Constraint`](xref:Xamarin.Forms.Constraint) 자식의 X 위치에 대 한 제약 조건을 나타내는 연결 된 속성입니다.
- [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty). 형식의 이며, [`Constraint`](xref:Xamarin.Forms.Constraint) 자식의 Y 위치에 대 한 제약 조건을 나타내는 연결 된 속성입니다.
- [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty). 형식의 이며, [`Constraint`](xref:Xamarin.Forms.Constraint) 자식의 너비에 대 한 제약 조건을 나타내는 연결 된 속성입니다.
- [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty). 형식의 이며, [`Constraint`](xref:Xamarin.Forms.Constraint) 자식의 높이에 대 한 제약 조건을 나타내는 연결 된 속성입니다.
- [`BoundsConstraint`](xref:Xamarin.Forms.RelativeLayout.BoundsConstraintProperty). 형식의 이며, [`BoundsConstraint`](xref:Xamarin.Forms.BoundsConstraint) 자식의 위치와 크기에 대 한 제약 조건을 나타내는 연결 된 속성입니다. 이 속성은 XAML에서 쉽게 사용할 수 없습니다.

이러한 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉, 속성이 데이터 바인딩 및 스타일의 대상이 될 수 있습니다. 연결 된 속성에 대 한 자세한 내용은 [ Xamarin.Forms 연결 된 속성](~/xamarin-forms/xaml/attached-properties.md)을 참조 하세요.

> [!NOTE]
> [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) `WidthRequest` `HeightRequest` 및 연결 된 속성 대신 자식의 및 속성을 통해의 자식에 대 한 너비와 높이를 지정할 수도 있습니다 [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) .

[`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)클래스는 `Layout<T>` 형식의 속성을 정의 하는 클래스에서 파생 `Children` `IList<T>` 됩니다. `Children`속성은 `ContentProperty` 클래스의입니다 `Layout<T>` . 따라서 XAML에서 명시적으로 설정할 필요는 없습니다.

> [!TIP]
> 가능한 경우 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)을 사용하지 마세요. 그러면 CPU가 훨씬 더 많은 작업을 수행해야 합니다.

## <a name="constraints"></a>제약 조건

내에서 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 자식의 위치와 크기는 절대 값 또는 상대 값을 사용 하 여 제약 조건으로 지정 됩니다. 제약 조건이 지정 되지 않은 경우 자식은 레이아웃의 왼쪽 위 모퉁이에 배치 됩니다.

다음 표에서는 XAML 및 c #에서 제약 조건을 지정 하는 방법을 보여 줍니다.

|     | XAML | C# |
| --- | ---- | -- |
| **절대값** | 절대 제약 조건은 연결 된 속성을 값으로 설정 하 여 지정 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) `double` 합니다. | 절대 제약 조건은 [`Constraint.Constant`](xref:Xamarin.Forms.Constraint.Constant*) 메서드에서 지정 하거나 `Children.Add` 인수를 필요로 하는 오버 로드를 사용 하 여 지정 합니다 `Func<Rectangle>` . |
| **상대 값** | [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)연결 된 속성을 [`Constraint`](xref:Xamarin.Forms.Constraint) 태그 확장에서 반환 되는 개체로 설정 하 여 상대 제약 조건을 지정 합니다 `ConstraintExpression` . | 상대 제약 조건은 [`Constraint`](xref:Xamarin.Forms.Constraint) 클래스의 메서드에서 반환 되는 개체에 의해 지정 됩니다 `Constraint` . |

절대값을 사용 하 여 제약 조건 지정에 대 한 자세한 내용은 [절대 위치 지정 및 크기 조정](#absolute-positioning-and-sizing)을 참조 하세요. 상대 값을 사용 하 여 제약 조건 지정에 대 한 자세한 내용은 [상대 위치 지정 및 크기 조정](#relative-positioning-and-sizing)을 참조 하세요.

C #에서는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 세 개의 오버 로드를 통해 자식을 추가할 수 있습니다 `Add` . 첫 번째 오버 로드에서는 `Expression<Func<Rectangle>>` 자식의 위치와 크기를 지정 하기 위해가 필요 합니다. 두 번째 오버 로드에는,, `Expression<Func<double>>` 및 인수에 대 한 선택적 개체가 필요 `x` `y` `width` `height` 합니다. 세 번째 오버 로드에는,, `Constraint` 및 인수에 대 한 선택적 개체가 필요 `x` `y` `width` `height` 합니다.

에서,, 및 메서드를 사용 하 여 자식의 위치와 크기를 변경할 수 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) [`SetXConstraint`](xref:Xamarin.Forms.RelativeLayout.SetXConstraint*) [`SetYConstraint`](xref:Xamarin.Forms.RelativeLayout.SetYConstraint*) [`SetWidthConstraint`](xref:Xamarin.Forms.RelativeLayout.SetWidthConstraint*) [`SetHeightConstraint`](xref:Xamarin.Forms.RelativeLayout.SetHeightConstraint*) 있습니다. 이러한 각 메서드에 대 한 첫 번째 인수는 자식 이며, 두 번째 인수는 [`Constraint`](xref:Xamarin.Forms.Constraint) 개체입니다. 또한 [`SetBoundsConstraint`](xref:Xamarin.Forms.RelativeLayout.SetBoundsConstraint*) 메서드를 사용 하 여 자식의 위치와 크기를 변경할 수도 있습니다. 이 메서드의 첫 번째 인수는 자식 이며, 두 번째 인수는 [`BoundsConstraint`](xref:Xamarin.Forms.BoundsConstraint) 개체입니다.

## <a name="absolute-positioning-and-sizing"></a>절대 위치 지정 및 크기 조정

는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 레이아웃에서 자식을 배치 해야 하는 위치를 명시적으로 정의 하는 장치 독립적 단위에 지정 된 절대 값을 사용 하 여 자식을 배치 하 고 크기를 지정할 수 있습니다. 이는의 컬렉션에 자식을 추가 `Children` `RelativeLayout` 하 고 [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) 각 자식의,, 및 연결 된 속성을 [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) 절대 위치 및/또는 크기 값으로 설정 하 여 수행 됩니다.

> [!WARNING]
> 여러 장치의 화면 크기와 해상도가 다르기 때문에 자식을 배치 하 고 크기를 조정 하는 데 절대값을 사용 하면 문제가 발생할 수 있습니다. 따라서 한 장치에서 화면 중심의 좌표는 다른 장치에서 오프셋 될 수 있습니다.

다음 XAML은 절대값을 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 사용 하 여 해당 자식을 배치 하는을 보여 줍니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="RelativeLayoutDemos.Views.StylishHeaderDemoPage"
             Title="Stylish header demo">
    <RelativeLayout Margin="20">
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="0"
                 RelativeLayout.YConstraint="10"
                 RelativeLayout.WidthConstraint="200"
                 RelativeLayout.HeightConstraint="5" />
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="0"
                 RelativeLayout.YConstraint="20"
                 RelativeLayout.WidthConstraint="200"
                 RelativeLayout.HeightConstraint="5" />
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="10"
                 RelativeLayout.YConstraint="0"
                 RelativeLayout.WidthConstraint="5"
                 RelativeLayout.HeightConstraint="65" />
        <BoxView Color="Silver"
                 RelativeLayout.XConstraint="20"
                 RelativeLayout.YConstraint="0"
                 RelativeLayout.WidthConstraint="5"
                 RelativeLayout.HeightConstraint="65" />
        <Label Text="Stylish header"
               FontSize="24"
               RelativeLayout.XConstraint="30"
               RelativeLayout.YConstraint="25" />
    </RelativeLayout>
</ContentPage>
```

이 예에서는 [`BoxView`](xref:Xamarin.Forms.BoxView) 및 연결 된 속성에 지정 된 값을 사용 하 여 각 개체의 위치를 정의 합니다 [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) . 각의 크기는 `BoxView` 및 연결 된 속성에 지정 된 값을 사용 하 여 정의 됩니다 [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) . 또한 개체의 위치는 [`Label`](xref:Xamarin.Forms.Label) 및 연결 된 속성에 지정 된 값을 사용 하 여 정의 됩니다 `XConstraint` `YConstraint` . 그러나 크기 값은에 대해 지정 되지 않으므로 `Label` 제한 되지 않으며 크기 자체입니다. 모든 경우에서 절대 값은 장치 독립적 단위를 나타냅니다.

다음 스크린샷은 결과 레이아웃을 보여줍니다.

![절대값을 사용 하 여 RelativeLayout에 배치 된 자식](relativelayout-images/absolute-values.png)

해당하는 C# 코드는 다음과 같습니다.

```csharp
public class StylishHeaderDemoPageCS : ContentPage
{
    public StylishHeaderDemoPageCS()
    {
        RelativeLayout relativeLayout = new RelativeLayout
        {
            Margin = new Thickness(20)
        };

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(0, 10, 200, 5));

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(0, 20, 200, 5));

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(10, 0, 5, 65));

        relativeLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, () => new Rectangle(20, 0, 5, 65));

        relativeLayout.Children.Add(new Label
        {
            Text = "Stylish Header",
            FontSize = 24
        }, Constraint.Constant(30), Constraint.Constant(25));

        Title = "Stylish header demo";
        Content = relativeLayout;
    }
}
```

이 예제에서는 [`BoxView`](xref:Xamarin.Forms.BoxView) [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 를 사용 하 여 `Add` `Expression<Func<Rectangle>>` 각 자식의 위치와 크기를 지정 하는 오버 로드를 사용 하 여 개체를에 추가 합니다. 의 위치는 [`Label`](xref:Xamarin.Forms.Label) `Add` 메서드에 의해 생성 된 선택적 개체가 필요한 오버 로드를 사용 하 여 정의 됩니다 [`Constraint`](xref:Xamarin.Forms.Constraint) [`Constraint.Constant`](xref:Xamarin.Forms.Constraint.Constant*) .

> [!NOTE]
> [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)절대 값을 사용 하는는 레이아웃의 범위 내에 들어가지 않도록 자식을 배치 하 고 크기를 조정할 수 있습니다.

## <a name="relative-positioning-and-sizing"></a>상대 위치 지정 및 크기 조정

는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 레이아웃의 속성 또는 형제 요소를 기준으로 하는 값을 사용 하 여 자식을 배치 하 고 크기를 지정할 수 있습니다. 이렇게 하려면의 컬렉션에 자식을 추가 하 `Children` `RelativeLayout` 고 [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) 개체를 [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) 사용 하 여 각 자식의,, 및 연결 된 속성을 상대 값으로 [`Constraint`](xref:Xamarin.Forms.Constraint) 설정 합니다.

제약 조건은 부모를 기준으로 하는 상수 이거나 형제를 기준으로 할 수 있습니다. 제약 조건의 형식은 다음 멤버를 정의 하는 열거형으로 표현 됩니다 [`ConstraintType`](xref:Xamarin.Forms.ConstraintType) .

- `RelativeToParent`-부모에 상대적인 제약 조건을 나타냅니다.
- `RelativeToView`-뷰 (또는 형제)에 상대적인 제약 조건을 나타냅니다.
- `Constant`-상수 제약 조건을 나타냅니다.

### <a name="constraint-markup-extension"></a>제약 조건 태그 확장

XAML에서 개체는 [`Constraint`](xref:Xamarin.Forms.Constraint) 태그 확장을 통해 만들 수 있습니다 [`ConstraintExpression`](xref:Xamarin.Forms.ConstraintExpression) . 이 태그 확장은 일반적으로 내에 있는 자식의 위치와 크기를 부모 또는 형제에 연결 하는 데 사용 됩니다 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) .

[`ConstraintExpression`](xref:Xamarin.Forms.ConstraintExpression)클래스는 다음 속성을 정의 합니다.

- [`Constant`](xref:Xamarin.Forms.ConstraintExpression.Constant)`double`제약 조건 상수 값을 나타내는 형식의입니다.
- [`ElementName`](xref:Xamarin.Forms.ConstraintExpression.ElementName)`string`제약 조건을 계산할 원본 요소의 이름을 나타내는 형식의입니다.
- [`Factor`](xref:Xamarin.Forms.ConstraintExpression.Factor)`double`원본 요소를 기준으로 제한 된 차원의 크기를 조정 하는 인수를 나타내는 형식의입니다. 이 속성의 기본값은 1입니다.
- [`Property`](xref:Xamarin.Forms.ConstraintExpression.Property)`string`제약 조건 계산에 사용할 소스 요소의 속성 이름을 나타내는 형식의입니다.
- [`Type`](xref:Xamarin.Forms.ConstraintExpression.Type)[`ConstraintType`](xref:Xamarin.Forms.ConstraintType)제약 조건의 형식을 나타내는 형식의입니다.

Xamarin.Forms 태그 확장에 대한 자세한 내용은 [XAML 태그 확장](~/xamarin-forms/xaml/markup-extensions/index.md)을 참조하세요.

다음 XAML에서는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 자식이 태그 확장에 의해 제한 되는을 보여 줍니다 [`ConstraintExpression`](xref:Xamarin.Forms.ConstraintExpression) .

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="RelativeLayoutDemos.Views.RelativePositioningAndSizingDemoPage"
             Title="RelativeLayout demo">
    <RelativeLayout>
        <BoxView Color="Red"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=Constant, Constant=0}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=Constant, Constant=0}" />
        <BoxView Color="Green"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Constant=-40}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=Constant, Constant=0}" />
        <BoxView Color="Blue"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=Constant, Constant=0}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Constant=-40}" />
        <BoxView Color="Yellow"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Constant=-40}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Constant=-40}" />

        <!-- Centered and 1/3 width and height of parent -->
        <BoxView x:Name="oneThird"
                 Color="Silver"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.33}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0.33}"
                 RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.33}"
                 RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0.33}" />

        <!-- 1/3 width and height of previous -->
        <BoxView Color="Black"
                 RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=X}"
                 RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=Y}"
                 RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=Width, Factor=0.33}"
                 RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToView, ElementName=oneThird, Property=Height, Factor=0.33}" />
    </RelativeLayout>
</ContentPage>
```

이 예에서는 [`BoxView`](xref:Xamarin.Forms.BoxView) 및 연결 된 속성을 설정 하 여 각 개체의 위치를 정의 합니다 [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) . 첫 번째에는 `BoxView` `XConstraint` `YConstraint` 상수 (절대값)로 설정 된 및 연결 된 속성이 있습니다. 나머지 `BoxView` 개체는 모두 하나 이상의 상대 값을 사용 하 여 해당 위치를 설정 합니다. 예를 들어, 노란색 `BoxView` 개체는 `XConstraint` 연결 된 속성을 해당 부모의 너비 ()에서 40을 뺀 값으로 설정 합니다 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) . 마찬가지로,이는 `BoxView` `YConstraint` 연결 된 속성을 부모의 높이로 설정 하 고 40을 뺀 값입니다. 이렇게 하면 `BoxView` 화면의 오른쪽 아래 모퉁이에 노란색이 표시 됩니다.

> [!NOTE]
> [`BoxView`](xref:Xamarin.Forms.BoxView) 크기를 지정 하지 않는 개체의 크기는 자동으로 4 0x40으로 조정 됩니다 Xamarin.Forms .

이라는 은색 [`BoxView`](xref:Xamarin.Forms.BoxView) 은 `oneThird` 부모를 기준으로 중앙에 배치 됩니다. 부모를 기준으로 크기를 조정 하 여 너비와 높이의 1/3을 지정 하기도 합니다. 이렇게 [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) 하려면 및 연결 된 속성을 [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) 부모 ()의 너비 (0.33)로 설정 합니다 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) . 마찬가지로 [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) 및 연결 된 [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) 속성은 부모의 높이로 설정 되며 0.33를 곱합니다.

검정은에 [`BoxView`](xref:Xamarin.Forms.BoxView) 상대적으로 배치 되 고 크기가 지정 됩니다 `oneThird` `BoxView` . 이렇게 [`XConstraint`](xref:Xamarin.Forms.RelativeLayout.XConstraintProperty) 하려면 및 연결 된 속성을 [`YConstraint`](xref:Xamarin.Forms.RelativeLayout.YConstraintProperty) `X` `Y` 각각 형제 요소의 및 값으로 설정 합니다. 마찬가지로 크기는 해당 형제 요소의 너비와 높이 중 1/3로 설정 됩니다. 이를 [`WidthConstraint`](xref:Xamarin.Forms.RelativeLayout.WidthConstraintProperty) [`HeightConstraint`](xref:Xamarin.Forms.RelativeLayout.HeightConstraintProperty) 위해 및 연결 된 속성을 `Width` 각각 형제 요소의 및 값으로 설정 하 고이를 `Height` 0.33에 곱합니다.

다음 스크린샷은 결과 레이아웃을 보여 줍니다.

![상대 값을 사용 하 여 RelativeLayout에 배치 된 자식](relativelayout-images/relative-values.png)

### <a name="constraint-objects"></a>제약 조건 개체

[`Constraint`](xref:Xamarin.Forms.Constraint)클래스는 개체를 반환 하는 다음과 같은 공용 정적 메서드를 정의 합니다 `Constraint` .

- [`Constant`](xref:Xamarin.Forms.Constraint.Constant*)-자식을로 지정 된 크기로 제한 합니다 `double` .
- [`FromExpression`](xref:Xamarin.Forms.Constraint.FromExpression*)는 람다 식을 사용 하 여 자식을 제한 합니다.
- [`RelativeToParent`](xref:Xamarin.Forms.Constraint.RelativeToParent*)-부모 크기를 기준으로 자식을 제한 합니다.
- [`RelativeToView`](xref:Xamarin.Forms.Constraint.RelativeToView*)-뷰의 크기를 기준으로 자식을 제한 합니다.

또한 [`BoundsConstraint`](xref:Xamarin.Forms.BoundsConstraint) 클래스는 [`FromExpression`](xref:Xamarin.Forms.BoundsConstraint.FromExpression*) `BoundsConstraint` 자식의 위치와 크기를로 제한 하는을 반환 하는 단일 메서드인를 정의 합니다 `Expression<Func<Rectangle>>` . 이 메서드를 사용 하 여 연결 된 속성을 설정할 수 있습니다 [`BoundsConstraint`](xref:Xamarin.Forms.RelativeLayout.BoundsConstraintProperty) .

다음 c # 코드는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 자식 개체가 개체에 의해 제한 되는을 보여 줍니다 [`Constraint`](xref:Xamarin.Forms.Constraint) .

```csharp
public class RelativePositioningAndSizingDemoPageCS : ContentPage
{
    public RelativePositioningAndSizingDemoPageCS()
    {
        RelativeLayout relativeLayout = new RelativeLayout();

        // Four BoxView's
        relativeLayout.Children.Add(
            new BoxView { Color = Color.Red },
            Constraint.Constant(0),
            Constraint.Constant(0));

        relativeLayout.Children.Add(
            new BoxView { Color = Color.Green },
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width - 40;
            }), Constraint.Constant(0));

        relativeLayout.Children.Add(
            new BoxView { Color = Color.Blue },
            Constraint.Constant(0),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height - 40;
            }));

        relativeLayout.Children.Add(
            new BoxView { Color = Color.Yellow },
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width - 40;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height - 40;
            }));

        // Centered and 1/3 width and height of parent
        BoxView silverBoxView = new BoxView { Color = Color.Silver };
        relativeLayout.Children.Add(
            silverBoxView,
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width * 0.33;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height * 0.33;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Width * 0.33;
            }),
            Constraint.RelativeToParent((parent) =>
            {
                return parent.Height * 0.33;
            }));

        // 1/3 width and height of previous
        relativeLayout.Children.Add(
            new BoxView { Color = Color.Black },
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.X;
            }),
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.Y;
            }),
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.Width * 0.33;
            }),
            Constraint.RelativeToView(silverBoxView, (parent, sibling) =>
            {
                return sibling.Height * 0.33;
            }));

        Title = "RelativeLayout demo";
        Content = relativeLayout;
    }
}
```

이 예제에서는 [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) `Add` ,, `Constraint` `x` `y` `width` 및 `height` 인수에 대 한 선택적 개체가 필요한 오버 로드를 사용 하 여에 자식을 추가 합니다.

> [!NOTE]
> [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout)상대 값을 사용 하는는 레이아웃의 범위 내에 들어가지 않도록 자식을 배치 하 고 크기를 조정할 수 있습니다.

## <a name="related-links"></a>관련 링크

- [RelativeLayout 데모 (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-relativelayoutdemos)
- [Xamarin.Forms 연결 된 속성](~/xamarin-forms/xaml/attached-properties.md)
- [XAML 태그 확장](~/xamarin-forms/xaml/markup-extensions/index.md)
- [레이아웃 선택 Xamarin.Forms](choose-layout.md)
- [Xamarin.Forms앱 성능 향상](~/xamarin-forms/deploy-test/performance.md)

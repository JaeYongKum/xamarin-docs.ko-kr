---
title: Xamarin.Forms AbsoluteLayout
description: Xamarin.FormsAbsoluteLayout는 명시적 값 또는 레이아웃 크기에 비례 하는 값을 사용 하 여 요소를 배치 하 고 크기를 조정 하는 데 사용 됩니다.
ms.prod: xamarin
ms.assetid: 01A5CCE0-AD45-4806-84FD-72C007005B38
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/07/2020
ms.custom: contperfq1
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 0468d132ee6e75ab75c0150f1f5c9e0af6dfde40
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91557779"
---
# <a name="no-locxamarinforms-absolutelayout"></a>Xamarin.Forms AbsoluteLayout

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-absolutelayoutdemos)

[![::: no loc (Xamarin.ios)::: AbsoluteLayout](absolutelayout-images/layouts.png)](absolutelayout-images/layouts-large.png#lightbox)

는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 명시적 값을 사용 하 여 자식을 배치 하 고 크기를 조정 하는 데 사용 됩니다. 위치는의 왼쪽 위 모퉁이를 기준으로 하는 자식의 왼쪽 위 모퉁이 `AbsoluteLayout` (장치 독립적 단위)로 지정 됩니다. 또한 `AbsoluteLayout`은 비례 위치 지정 및 크기 조정 기능을 구현합니다. 또한 다른 레이아웃 클래스와 달리 `AbsoluteLayout` 는 겹칠 수 있도록 자식을 배치할 수 있습니다.

는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 자식에 크기를 적용할 수 있거나 요소의 크기가 다른 자식의 위치 지정에 영향을 주지 않는 경우에만 사용 되는 특수 한 용도의 레이아웃으로 간주 되어야 합니다.

[`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout)클래스는 다음 속성을 정의 합니다.

- [`LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty). 형식의 이며, [`Rectangle`](xref:Xamarin.Forms.Rectangle) 자식의 위치와 크기를 나타내는 연결 된 속성입니다. 이 속성의 기본값은 (0, 0, AutoSize, AutoSize)입니다.
- [`LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty). 형식의 이며, [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) 자식의 위치와 크기를 조정 하는 데 사용 되는 레이아웃 경계의 속성이 비례적으로 해석 되는지 여부를 나타내는 연결 된 속성입니다. 이 속성의 기본값은 `AbsoluteLayoutFlags.None`입니다.

이러한 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉, 속성이 데이터 바인딩 및 스타일의 대상이 될 수 있습니다. 연결 된 속성에 대 한 자세한 내용은 [ Xamarin.Forms 연결 된 속성](~/xamarin-forms/xaml/attached-properties.md)을 참조 하세요.

[`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout)클래스는 `Layout<T>` 형식의 속성을 정의 하는 클래스에서 파생 `Children` `IList<T>` 됩니다. `Children`속성은 `ContentProperty` 클래스의입니다 `Layout<T>` . 따라서 XAML에서 명시적으로 설정할 필요는 없습니다.

> [!TIP]
> 가능한 최상의 레이아웃 성능을 얻으려면 [레이아웃 성능 최적화](~/xamarin-forms/deploy-test/performance.md#optimize-layout-performance)의 지침을 따르세요.

## <a name="position-and-size-children"></a>자식 위치 및 크기 조정

에서 자식의 위치와 크기는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) 절대 값 또는 비례 값을 사용 하 여 각 자식의 연결 된 속성을 설정 하 여 정의 됩니다. Position의 크기를 조정 해야 하는 경우 자식에 대해 절대 및 비례 값을 혼합할 수 있지만 크기는 고정 되어 있거나 그 반대의 경우도 마찬가지입니다. 절대 값에 대 한 자세한 내용은 [절대 위치 지정 및 크기 조정](#absolute-positioning-and-sizing)을 참조 하세요. 비례 값에 대 한 자세한 내용은 [비례 위치 지정 및 크기 조정](#proportional-positioning-and-sizing)을 참조 하세요.

[`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty)절대값 또는 비례 값의 사용 여부에 관계 없이 두 가지 형식을 사용 하 여 연결 된 속성을 설정할 수 있습니다.

- `x, y`. 이 형식을 사용 하는 경우 `x` 및 `y` 값은 부모를 기준으로 자식의 왼쪽 위 모퉁이의 위치를 표시 합니다. 자식은 제한 되지 않으며 크기 자체입니다.
- `x, y, width, height`. 이 형식을 사용 하는 경우 및 값은 `x` `y` 부모를 기준으로 자식의 왼쪽 위 모퉁이의 위치를 나타내고 `width` , 및 `height` 값은 자식의 크기를 표시 합니다.

자식 크기를 가로 또는 세로로 지정 하거나 둘 다 지정 하려면 `width` 및/또는 `height` 값을 속성으로 설정 합니다 [`AbsoluteLayout.AutoSize`](xref:Xamarin.Forms.AbsoluteLayout.AutoSize) . 그러나이 속성을 과도 하 게 사용할 경우 레이아웃 엔진이 추가 레이아웃 계산을 수행 하기 때문에 응용 프로그램 성능이 저하 될 수 있습니다.

> [!IMPORTANT]
> [`HorizontalOptions`](xref:Xamarin.Forms.View.HorizontalOptions)및 [`VerticalOptions`](xref:Xamarin.Forms.View.VerticalOptions) 속성은의 자식에는 영향을 주지 않습니다 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) .

## <a name="absolute-positioning-and-sizing"></a>절대 위치 지정 및 크기 조정

기본적으로는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 레이아웃에서 자식을 배치 해야 하는 위치를 명시적으로 정의 하는 장치 독립적 단위로 지정 된 절대 값을 사용 하 여 자식 위치 및 크기를 지정 합니다. 이는의 컬렉션에 자식을 추가 하 `Children` `AbsoluteLayout` 고 [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) 각 자식의 연결 된 속성을 절대 위치 및/또는 크기 값으로 설정 하 여 수행 됩니다.

> [!WARNING]
> 여러 장치의 화면 크기와 해상도가 다르기 때문에 자식을 배치 하 고 크기를 조정 하는 데 절대값을 사용 하면 문제가 발생할 수 있습니다. 따라서 한 장치에서 화면 중심의 좌표는 다른 장치에서 오프셋 될 수 있습니다.

다음 XAML은 절대값을 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 사용 하 여 해당 자식을 배치 하는을 보여 줍니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="AbsoluteLayoutDemos.Views.StylishHeaderDemoPage"
             Title="Stylish header demo">
    <AbsoluteLayout Margin="20">
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="0, 10, 200, 5" />
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="0, 20, 200, 5" />
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="10, 0, 5, 65" />
        <BoxView Color="Silver"
                 AbsoluteLayout.LayoutBounds="20, 0, 5, 65" />
        <Label Text="Stylish Header"
               FontSize="24"
               AbsoluteLayout.LayoutBounds="30, 25" />
    </AbsoluteLayout>
</ContentPage>
```

이 예제에서 각 개체의 위치는 [`BoxView`](xref:Xamarin.Forms.BoxView) 연결 된 속성에 지정 된 처음 두 개의 절대 값을 사용 하 여 정의 됩니다 [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) . 각의 크기는 `BoxView` 세 번째와 그 사이의 값을 사용 하 여 정의 됩니다. 개체의 위치는 [`Label`](xref:Xamarin.Forms.Label) 연결 된 속성에 지정 된 두 개의 절대 값을 사용 하 여 정의 됩니다 `AbsoluteLayout.LayoutBounds` . 크기 값은에 대해 지정 되지 않으므로 `Label` 제한 되지 않으며 크기 자체입니다. 모든 경우에서 절대 값은 장치 독립적 단위를 나타냅니다.

다음 스크린샷은 결과 레이아웃을 보여 줍니다.

![절대값을 사용 하 여 AbsoluteLayout에 배치 된 자식](absolutelayout-images/absolute-values.png)

해당 c # 코드는 다음과 같습니다.

```csharp
public class StylishHeaderDemoPageCS : ContentPage
{
    public StylishHeaderDemoPageCS()
    {
        AbsoluteLayout absoluteLayout = new AbsoluteLayout
        {
            Margin = new Thickness(20)
        };

        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver,
        }, new Rectangle(0, 10, 200, 5));
        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, new Rectangle(0, 20, 200, 5));
        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, new Rectangle(10, 0, 5, 65));
        absoluteLayout.Children.Add(new BoxView
        {
            Color = Color.Silver
        }, new Rectangle(20, 0, 5, 65));

        absoluteLayout.Children.Add(new Label
        {
            Text = "Stylish Header",
            FontSize = 24
        }, new Point(30,25));                    

        Title = "Stylish header demo";
        Content = absoluteLayout;
    }
}
```

이 예제에서 각의 위치와 크기는 [`BoxView`](xref:Xamarin.Forms.BoxView) 개체를 사용 하 여 정의 됩니다 [`Rectangle`](xref:Xamarin.Forms.Rectangle) . 의 위치는 [`Label`](xref:Xamarin.Forms.Label) 개체를 사용 하 여 정의 됩니다 [`Point`](xref:Xamarin.Forms.Point) .

C #에서는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) `Children` 메서드를 사용 하 여 컬렉션에 추가 된 후의 자식에 대 한 위치와 크기를 설정할 수 있습니다 [`AbsoluteLayout.SetLayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.SetLayoutBounds*) . 이 메서드의 첫 번째 인수는 자식 이며, 두 번째 인수는 [`Rectangle`](xref:Xamarin.Forms.Rectangle) 개체입니다.

> [!NOTE]
> [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout)절대 값을 사용 하는는 레이아웃의 범위 내에 들어가지 않도록 자식을 배치 하 고 크기를 조정할 수 있습니다.

## <a name="proportional-positioning-and-sizing"></a>비례 위치 지정 및 크기 조정

는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 가변 값을 사용 하 여 자식을 배치 하 고 크기를 지정할 수 있습니다. 이는의 컬렉션에 자식을 추가 하 `Children` `AbsoluteLayout` 고 [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) 각 자식의 연결 된 속성을 0-1 범위의 비례 위치 및/또는 크기 값으로 설정 하 여 수행 됩니다. 위치 및 크기 값은 [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) 각 자식에서 연결 된 속성을 설정 하 여 비례에 따라 결정 됩니다.

[`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty)형식의 연결 된 속성을 [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) 사용 하면 자식의 레이아웃 범위 위치 및 크기 값이의 크기에 비례하여 표시 되는 플래그를 설정할 수 있습니다 `AbsoluteLayout` . 자식을 레이아웃할 때 `AbsoluteLayout` 위치 및 크기 값을 적절 하 게 확장 하 여 장치 크기에 맞게 조정 합니다.

[`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags)열거형은 다음 멤버를 정의 합니다.

- `None`는 값이 절대 값으로 해석 됨을 나타냅니다. 이 값은 연결 된 속성의 기본값입니다 [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) .
- `XProportional`는 `x` 값이 비례로 해석 되는 반면 다른 모든 값은 절대값으로 간주 함을 나타냅니다.
- `YProportional`는 `y` 값이 비례로 해석 되는 반면 다른 모든 값은 절대값으로 간주 함을 나타냅니다.
- `WidthProportional`는 `width` 값이 비례로 해석 되는 반면 다른 모든 값은 절대값으로 간주 함을 나타냅니다.
- `HeightProportional`는 `height` 값이 비례로 해석 되는 반면 다른 모든 값은 절대값으로 간주 함을 나타냅니다.
- `PositionProportional`는 `x` 및 `y` 값이 비례로 해석 되는 반면 크기 값은 절대 값으로 해석 됨을 나타냅니다.
- `SizeProportional`는 `width` 및 `height` 값이 비례로 해석 되는 반면 위치 값은 절대 값으로 해석 됨을 나타냅니다.
- `All`는 모든 값이 비례하여 해석 됨을 나타냅니다.

> [!TIP]
> 열거형은 열거형 [`AbsoluteLayoutFlags`](xref:Xamarin.Forms.AbsoluteLayoutFlags) `Flags` 멤버를 결합할 수 있음을 의미 하는 열거형입니다. 이는 XAML에서 쉼표로 구분 된 목록을 사용 하 고 c #에서는 비트 OR 연산자를 사용 하 여 수행 됩니다.

예를 들어, 플래그를 사용 하 `SizeProportional` 고 자식의 너비를 0.25로 설정 하 고 높이를 0.1로 설정 하는 경우 자식은의 너비 중 1 사분기이 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 고 높이는 1/10입니다. `PositionProportional`플래그는 유사 합니다. (0, 0)의 위치는 자식를 왼쪽 위 모퉁이에 배치 하 고, (1, 1)의 위치는 자식를 오른쪽 아래 모퉁이에 배치 하 고 (0.5, 0.5)의 위치는 내에서 자식을 가운데에 맞춥니다 `AbsoluteLayout` .

다음 XAML에서는 [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 비례 값을 사용 하 여 해당 자식을 배치 하는을 보여 줍니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="AbsoluteLayoutDemos.Views.ProportionalDemoPage"
             Title="Proportional demo">
    <AbsoluteLayout>
        <BoxView Color="Blue"
                 AbsoluteLayout.LayoutBounds="0.5,0,100,25"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <BoxView Color="Green"
                 AbsoluteLayout.LayoutBounds="0,0.5,25,100"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <BoxView Color="Red"
                 AbsoluteLayout.LayoutBounds="1,0.5,25,100"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <BoxView Color="Black"
                 AbsoluteLayout.LayoutBounds="0.5,1,100,25"
                 AbsoluteLayout.LayoutFlags="PositionProportional" />
        <Label Text="Centered text"
               AbsoluteLayout.LayoutBounds="0.5,0.5,110,25"
               AbsoluteLayout.LayoutFlags="PositionProportional" />
    </AbsoluteLayout>
</ContentPage>
```

이 예제에서 각 자식은 비례 값을 사용 하 여 배치 되지만 절대 값을 사용 하 여 크기가 지정 됩니다. 이렇게 [`AbsoluteLayout.LayoutFlags`](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty) 하려면 각 자식의 연결 된 속성을로 설정 `PositionProportional` 합니다. 각 자식에 대해 연결 된 속성에 지정 된 처음 두 값은 [`AbsoluteLayout.LayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) 비례 값을 사용 하 여 위치를 정의 합니다. 각 자식의 크기는 장치 독립적 단위를 사용 하 여 세 번째와 그 사이의 절대값으로 정의 됩니다.

다음 스크린샷은 결과 레이아웃을 보여 줍니다.

![비례 위치 값을 사용 하 여 AbsoluteLayout에 배치 된 자식](absolutelayout-images/proportional-position.png)

해당 c # 코드는 다음과 같습니다.

```csharp
public class ProportionalDemoPageCS : ContentPage
{
    public ProportionalDemoPageCS()
    {
        BoxView blue = new BoxView { Color = Color.Blue };
        AbsoluteLayout.SetLayoutBounds(blue, new Rectangle(0.5, 0, 100, 25));
        AbsoluteLayout.SetLayoutFlags(blue, AbsoluteLayoutFlags.PositionProportional);

        BoxView green = new BoxView { Color = Color.Green };
        AbsoluteLayout.SetLayoutBounds(green, new Rectangle(0, 0.5, 25, 100));
        AbsoluteLayout.SetLayoutFlags(green, AbsoluteLayoutFlags.PositionProportional);

        BoxView red = new BoxView { Color = Color.Red };
        AbsoluteLayout.SetLayoutBounds(red, new Rectangle(1, 0.5, 25, 100));
        AbsoluteLayout.SetLayoutFlags(red, AbsoluteLayoutFlags.PositionProportional);

        BoxView black = new BoxView { Color = Color.Black };
        AbsoluteLayout.SetLayoutBounds(black, new Rectangle(0.5, 1, 100, 25));
        AbsoluteLayout.SetLayoutFlags(black, AbsoluteLayoutFlags.PositionProportional);

        Label label = new Label { Text = "Centered text" };
        AbsoluteLayout.SetLayoutBounds(label, new Rectangle(0.5, 0.5, 110, 25));
        AbsoluteLayout.SetLayoutFlags(label, AbsoluteLayoutFlags.PositionProportional);

        Title = "Proportional demo";
        Content = new AbsoluteLayout
        {
            Children = { blue, green, red, black, label }
        };
    }
}
```

이 예제에서는 메서드를 사용 하 여 각 자식의 위치와 크기를 설정 합니다 [`AbsoluteLayout.SetLayoutBounds`](xref:Xamarin.Forms.AbsoluteLayout.SetLayoutBounds*) . 메서드의 첫 번째 인수는 자식 이며, 두 번째 인수는 [`Rectangle`](xref:Xamarin.Forms.Rectangle) 개체입니다. 각 자식의 위치는 비례 값을 사용 하 여 설정 되지만 각 자식의 크기는 장치 독립적 단위를 사용 하 여 절대 값으로 설정 됩니다.

> [!NOTE]
> [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout)비례 값을 사용 하는는 0-1 범위를 벗어난 값을 사용 하 여 레이아웃의 범위 내에 들어가지 않도록 자식을 배치 하 고 크기를 조정할 수 있습니다.

## <a name="related-links"></a>관련 링크

- [AbsoluteLayout 데모 (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-absolutelayoutdemos)
- [Xamarin.Forms 연결 된 속성](~/xamarin-forms/xaml/attached-properties.md)
- [레이아웃 선택 Xamarin.Forms](choose-layout.md)
- [Xamarin.Forms앱 성능 향상](~/xamarin-forms/deploy-test/performance.md)
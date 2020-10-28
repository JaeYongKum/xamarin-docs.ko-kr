---
title: Xamarin.Forms CollectionView 데이터
description: CollectionView는 System.windows.controls.itemscontrol.itemssource 속성을 IEnumerable을 구현 하는 컬렉션으로 설정 하 여 데이터로 채워집니다.
ms.prod: xamarin
ms.assetid: E1783E34-1C0F-401A-80D5-B2BE5508F5F8
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/27/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 77f47af2ed2cce787cf0f66e524c2314ef4c9452
ms.sourcegitcommit: 1550019cd1e858d4d13a4ae6dfb4a5947702f24b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92897507"
---
# <a name="no-locxamarinforms-collectionview-data"></a>Xamarin.Forms CollectionView 데이터

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-collectionviewdemos/)

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 에는 표시할 데이터 및 모양을 정의 하는 다음 속성이 포함 되어 있습니다.

- [`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource)형식의는 `IEnumerable` 표시 될 항목의 컬렉션을 지정 하 고 기본값은 `null` 입니다.
- [`ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate)형식의는 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 표시할 항목 컬렉션의 각 항목에 적용할 템플릿을 지정 합니다.

이러한 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉, 속성은 데이터 바인딩의 대상이 될 수 있습니다.

> [!NOTE]
> [`CollectionView`](xref:Xamarin.Forms.CollectionView)`ItemsUpdatingScrollMode`새 항목이 추가 될 때의 스크롤 동작을 나타내는 속성을 정의 `CollectionView` 합니다. 이 속성에 대 한 자세한 내용은 [새 항목이 추가 될 때 스크롤 위치 제어](scrolling.md#control-scroll-position-when-new-items-are-added)를 참조 하세요.

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 사용자가 스크롤하면 증분 데이터 가상화를 지원 합니다. 자세한 내용은 [데이터를 증분 로드](#load-data-incrementally)를 참조 하세요.

## <a name="populate-a-collectionview-with-data"></a>데이터를 사용 하 여 CollectionView 채우기

는 [`CollectionView`](xref:Xamarin.Forms.CollectionView) 속성을를 [`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource) 구현 하는 컬렉션으로 설정 하 여 데이터로 채워집니다 `IEnumerable` . 기본적으로는 [`CollectionView`](xref:Xamarin.Forms.CollectionView) 세로 목록에 항목을 표시 합니다.

> [!IMPORTANT]
> [`CollectionView`](xref:Xamarin.Forms.CollectionView)기본 컬렉션에서 항목이 추가, 제거 또는 변경 될 때를 새로 고쳐야 하는 경우 기본 컬렉션은 `IEnumerable` 와 같은 속성 변경 알림을 보내는 컬렉션 이어야 합니다 `ObservableCollection` .

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 데이터 바인딩을 사용 하 여 속성을 컬렉션에 바인딩하면 데이터를 데이터로 채울 수 있습니다 [`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource) `IEnumerable` . XAML에서이 작업은 태그 확장을 사용 하 여 구현 됩니다 `Binding` .

```xaml
<CollectionView ItemsSource="{Binding Monkeys}" />
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
CollectionView collectionView = new CollectionView();
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Monkeys");
```

이 예제에서 [`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource) 속성 데이터는 `Monkeys` 연결 된 viewmodel의 속성에 바인딩됩니다.

> [!NOTE]
> 컴파일된 바인딩을 사용 하면 응용 프로그램에서 데이터 바인딩 성능을 향상 시킬 수 있습니다 Xamarin.Forms . 자세한 내용은 [컴파일된 바인딩](~/xamarin-forms/app-fundamentals/data-binding/compiled-bindings.md)을 참조하세요.

레이아웃을 변경 하는 방법에 대 한 자세한 내용은 [`CollectionView`](xref:Xamarin.Forms.CollectionView) [ Xamarin.Forms CollectionView layout](layout.md)을 참조 하세요. 에서 각 항목의 모양을 정의 하는 방법에 대 한 자세한 내용은 `CollectionView` [항목 모양 정의](#define-item-appearance)를 참조 하세요. 데이터 바인딩에 대한 자세한 내용은 [Xamarin.Forms 데이터 바인딩](~/xamarin-forms/app-fundamentals/data-binding/index.md)을 참조하세요.

> [!WARNING]
> [`CollectionView`](xref:Xamarin.Forms.CollectionView)[`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource)가 UI 스레드에서 업데이트 되 면에서 예외를 throw 합니다.

## <a name="define-item-appearance"></a>항목 모양 정의

에서 각 항목의 모양은 속성을 [`CollectionView`](xref:Xamarin.Forms.CollectionView) 로 설정 하 여 정의할 수 있습니다 [`CollectionView.ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate) [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) .

```xaml
<CollectionView ItemsSource="{Binding Monkeys}">
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <Grid Padding="10">
                <Grid.RowDefinitions>
                    <RowDefinition Height="Auto" />
                    <RowDefinition Height="Auto" />
                </Grid.RowDefinitions>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="Auto" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <Image Grid.RowSpan="2"
                       Source="{Binding ImageUrl}"
                       Aspect="AspectFill"
                       HeightRequest="60"
                       WidthRequest="60" />
                <Label Grid.Column="1"
                       Text="{Binding Name}"
                       FontAttributes="Bold" />
                <Label Grid.Row="1"
                       Grid.Column="1"
                       Text="{Binding Location}"
                       FontAttributes="Italic"
                       VerticalOptions="End" />
            </Grid>
        </DataTemplate>
    </CollectionView.ItemTemplate>
    ...
</CollectionView>
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
CollectionView collectionView = new CollectionView();
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Monkeys");

collectionView.ItemTemplate = new DataTemplate(() =>
{
    Grid grid = new Grid { Padding = 10 };
    grid.RowDefinitions.Add(new RowDefinition { Height = GridLength.Auto });
    grid.RowDefinitions.Add(new RowDefinition { Height = GridLength.Auto });
    grid.ColumnDefinitions.Add(new ColumnDefinition { Width = GridLength.Auto });
    grid.ColumnDefinitions.Add(new ColumnDefinition { Width = GridLength.Auto });

    Image image = new Image { Aspect = Aspect.AspectFill, HeightRequest = 60, WidthRequest = 60 };
    image.SetBinding(Image.SourceProperty, "ImageUrl");

    Label nameLabel = new Label { FontAttributes = FontAttributes.Bold };
    nameLabel.SetBinding(Label.TextProperty, "Name");

    Label locationLabel = new Label { FontAttributes = FontAttributes.Italic, VerticalOptions = LayoutOptions.End };
    locationLabel.SetBinding(Label.TextProperty, "Location");

    Grid.SetRowSpan(image, 2);

    grid.Children.Add(image);
    grid.Children.Add(nameLabel, 1, 0);
    grid.Children.Add(locationLabel, 1, 1);

    return grid;
});
```

에서 지정 된 요소는 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 목록에 있는 각 항목의 모양을 정의 합니다. 이 예제에서 내의 레이아웃 `DataTemplate` 은를 통해 관리 됩니다 [`Grid`](xref:Xamarin.Forms.Grid) . 는 `Grid` [`Image`](xref:Xamarin.Forms.Image) [`Label`](xref:Xamarin.Forms.Label) 모두 클래스의 속성에 바인딩되는 개체와 두 개의 개체를 포함 합니다 `Monkey` .

```csharp
public class Monkey
{
    public string Name { get; set; }
    public string Location { get; set; }
    public string Details { get; set; }
    public string ImageUrl { get; set; }
}
```

다음 스크린샷에는 목록의 각 항목에 대 한 템플릿 결과가 나와 있습니다.

[![IOS 및 Android에서 각 항목이 템플릿 인 CollectionView의 스크린샷](populate-data-images/datatemplate.png "CollectionView의 템플릿 항목")](populate-data-images/datatemplate-large.png#lightbox "CollectionView의 템플릿 항목")

데이터 템플릿에 대한 자세한 내용은 [Xamarin.Forms 데이터 템플릿](~/xamarin-forms/app-fundamentals/templates/data-templates/index.md)을 참조하세요.

## <a name="choose-item-appearance-at-runtime"></a>런타임에 항목 모양 선택

에서 각 항목의 모양은 속성을 [`CollectionView`](xref:Xamarin.Forms.CollectionView) 개체로 설정 하 여 항목 값에 따라 런타임에 선택할 수 있습니다 [`CollectionView.ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate) [`DataTemplateSelector`](xref:Xamarin.Forms.DataTemplateSelector) .

```xaml
<ContentPage ...
             xmlns:controls="clr-namespace:CollectionViewDemos.Controls">
    <ContentPage.Resources>
        <DataTemplate x:Key="AmericanMonkeyTemplate">
            ...
        </DataTemplate>

        <DataTemplate x:Key="OtherMonkeyTemplate">
            ...
        </DataTemplate>

        <controls:MonkeyDataTemplateSelector x:Key="MonkeySelector"
                                             AmericanMonkey="{StaticResource AmericanMonkeyTemplate}"
                                             OtherMonkey="{StaticResource OtherMonkeyTemplate}" />
    </ContentPage.Resources>

    <CollectionView ItemsSource="{Binding Monkeys}"
                    ItemTemplate="{StaticResource MonkeySelector}" />
</ContentPage>
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
CollectionView collectionView = new CollectionView
{
    ItemTemplate = new MonkeyDataTemplateSelector { ... }
};
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Monkeys");
```

[`ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate)속성은 개체로 설정 됩니다 `MonkeyDataTemplateSelector` . 다음 예제에서는 클래스를 보여 줍니다 `MonkeyDataTemplateSelector` .

```csharp
public class MonkeyDataTemplateSelector : DataTemplateSelector
{
    public DataTemplate AmericanMonkey { get; set; }
    public DataTemplate OtherMonkey { get; set; }

    protected override DataTemplate OnSelectTemplate(object item, BindableObject container)
    {
        return ((Monkey)item).Location.Contains("America") ? AmericanMonkey : OtherMonkey;
    }
}
```

`MonkeyDataTemplateSelector`클래스는 `AmericanMonkey` `OtherMonkey` [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 다른 데이터 템플릿으로 설정 된 및 속성을 정의 합니다. `OnSelectTemplate`재정의는 `AmericanMonkey` 원숭이 이름 및 위치를 청록색으로 표시 하는 템플릿 (원숭이 이름에 "아메리카"가 포함 된 경우)을 반환 합니다. 원숭이 이름에 "아메리카"가 포함 되어 있지 않으면 `OnSelectTemplate` 재정의는 `OtherMonkey` 다음의 원숭이 이름과 위치를 은색에 표시 하는 템플릿을 반환 합니다.

[![IOS 및 Android에서 CollectionView 런타임 항목 템플릿 선택의 스크린샷](populate-data-images/datatemplateselector.png "CollectionView의 런타임 항목 템플릿 선택")](populate-data-images/datatemplateselector-large.png#lightbox "CollectionView의 런타임 항목 템플릿 선택")

데이터 템플릿 선택기에 대 한 자세한 내용은 [Create a Xamarin.Forms DataTemplateSelector](~/xamarin-forms/app-fundamentals/templates/data-templates/selector.md)을 참조 하세요.

> [!IMPORTANT]
> 를 사용 하는 경우 [`CollectionView`](xref:Xamarin.Forms.CollectionView) 개체의 루트 요소를으로 설정 하지 마십시오 [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) `ViewCell` . 이로 인해에는 셀 개념이 없기 때문에 예외가 throw 됩니다 `CollectionView` .

## <a name="context-menus"></a>상황에 맞는 메뉴

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 는 `SwipeView` 살짝 밀기 제스처를 사용 하 여 상황에 맞는 메뉴를 표시 하는를 통해 데이터 항목의 상황에 맞는 메뉴를 지원 합니다. 는 `SwipeView` 콘텐츠 항목 주위에 래핑하는 컨테이너 컨트롤이 며 해당 콘텐츠 항목에 대 한 상황에 맞는 메뉴 항목을 제공 합니다. 따라서가 `CollectionView` `SwipeView` 래핑하는 콘텐츠를 정의 하는 `SwipeView` 및 살짝 밀기 제스처로 표시 되는 상황에 맞는 메뉴 항목을 정의 하는을 만들어에 대해 상황에 맞는 메뉴를 구현할 수 있습니다. 이 작업은의 `SwipeView` [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) 각 데이터 항목의 모양을 정의 하는의 루트 뷰로를 설정 하 여 `CollectionView` 수행 됩니다.

```xaml
<CollectionView x:Name="collectionView"
                ItemsSource="{Binding Monkeys}">
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <SwipeView>
                <SwipeView.LeftItems>
                    <SwipeItems>
                        <SwipeItem Text="Favorite"
                                   IconImageSource="favorite.png"
                                   BackgroundColor="LightGreen"
                                   Command="{Binding Source={x:Reference collectionView}, Path=BindingContext.FavoriteCommand}"
                                   CommandParameter="{Binding}" />
                        <SwipeItem Text="Delete"
                                   IconImageSource="delete.png"
                                   BackgroundColor="LightPink"
                                   Command="{Binding Source={x:Reference collectionView}, Path=BindingContext.DeleteCommand}"
                                   CommandParameter="{Binding}" />
                    </SwipeItems>
                </SwipeView.LeftItems>
                <Grid BackgroundColor="White"
                      Padding="10">
                    <!-- Define item appearance -->
                </Grid>
            </SwipeView>
        </DataTemplate>
    </CollectionView.ItemTemplate>
</CollectionView>
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
CollectionView collectionView = new CollectionView();
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Monkeys");

collectionView.ItemTemplate = new DataTemplate(() =>
{
    // Define item appearance
    Grid grid = new Grid { Padding = 10, BackgroundColor = Color.White };
    // ...

    SwipeView swipeView = new SwipeView();
    SwipeItem favoriteSwipeItem = new SwipeItem
    {
        Text = "Favorite",
        IconImageSource = "favorite.png",
        BackgroundColor = Color.LightGreen
    };
    favoriteSwipeItem.SetBinding(MenuItem.CommandProperty, new Binding("BindingContext.FavoriteCommand", source: collectionView));
    favoriteSwipeItem.SetBinding(MenuItem.CommandParameterProperty, ".");

    SwipeItem deleteSwipeItem = new SwipeItem
    {
        Text = "Delete",
        IconImageSource = "delete.png",
        BackgroundColor = Color.LightPink
    };
    deleteSwipeItem.SetBinding(MenuItem.CommandProperty, new Binding("BindingContext.DeleteCommand", source: collectionView));
    deleteSwipeItem.SetBinding(MenuItem.CommandParameterProperty, ".");

    swipeView.LeftItems = new SwipeItems { favoriteSwipeItem, deleteSwipeItem };
    swipeView.Content = grid;    
    return swipeView;
});
```

이 예제에서 콘텐츠는 `SwipeView` [`Grid`](xref:Xamarin.Forms.Grid) 에 있는 각 항목의 모양을 정의 하는입니다 [`CollectionView`](xref:Xamarin.Forms.CollectionView) . 살짝 밀기 항목은 콘텐츠에 대 한 작업을 수행 하는 데 사용 되며 `SwipeView` , 컨트롤이 왼쪽에서 스와이프 때 표시 됩니다.

[![IOS 및 Android에서 CollectionView 상황에 맞는 메뉴 항목의 스크린샷](populate-data-images/swipeview.png "SwipeView 상황에 맞는 메뉴 항목을 사용 하는 CollectionView")](populate-data-images/swipeview-large.png#lightbox "SwipeView 상황에 맞는 메뉴 항목을 사용 하는 CollectionView")

`SwipeView` 는 개체를 추가할 방향 컬렉션에 의해 정의 되는 살짝 밀기 방향을 사용 하 여 네 가지 살짝 밀기 방향을 지원 `SwipeItems` `SwipeItems` 합니다. 기본적으로 사용자가 탭 할 때 살짝 밀기 항목이 실행 됩니다. 또한 살짝 밀기 항목이 실행 된 후에는 살짝 밀기 항목이 숨겨지고 `SwipeView` 콘텐츠가 다시 표시 됩니다. 그러나 이러한 동작은 변경할 수 있습니다.

컨트롤에 대 한 자세한 내용은 `SwipeView` [ Xamarin.Forms SwipeView](~/xamarin-forms/user-interface/swipeview.md)를 참조 하세요.

## <a name="pull-to-refresh"></a>당겨서 새로 고침

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 는를 통해 기능을 새로 고칠 수 있도록 지원 합니다 `RefreshView` . 그러면 항목 목록에서 아래로 당겨 데이터를 새로 고칠 수 있습니다. 는 `RefreshView` 자식에서 스크롤 가능한 콘텐츠를 지 원하는 경우 해당 자식에 대 한 기능을 새로 고치는 끌어오기를 제공 하는 컨테이너 컨트롤입니다. 따라서를 `CollectionView` 의 자식으로 설정 하 여에 대 한 끌어오기를 새로 고쳐 구현 합니다 `RefreshView` .

```xaml
<RefreshView IsRefreshing="{Binding IsRefreshing}"
             Command="{Binding RefreshCommand}">
    <CollectionView ItemsSource="{Binding Animals}">
        ...
    </CollectionView>
</RefreshView>
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
RefreshView refreshView = new RefreshView();
ICommand refreshCommand = new Command(() =>
{
    // IsRefreshing is true
    // Refresh data here
    refreshView.IsRefreshing = false;
});
refreshView.Command = refreshCommand;

CollectionView collectionView = new CollectionView();
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Animals");
refreshView.Content = collectionView;
// ...
```

사용자가 새로 고침을 시작 하면 `ICommand` 속성으로 정의 된가 `Command` 실행 되어 표시 되는 항목을 새로 고쳐야 합니다. 새로 고침이 발생 하는 동안 애니메이션 처리 원으로 구성 된 새로 고침 시각화가 표시 됩니다.

[![IOS 및 Android에서 CollectionView 끌어오기-새로 고침의 스크린샷](populate-data-images/pull-to-refresh.png "CollectionView 가져오기-새로 고침")](populate-data-images/pull-to-refresh-large.png#lightbox "CollectionView 가져오기-새로 고침")

속성의 값은 `RefreshView.IsRefreshing` 의 현재 상태를 나타냅니다 `RefreshView` . 사용자가 새로 고침을 트리거하는 경우이 속성은 자동으로로 전환 됩니다 `true` . 새로 고침이 완료 되 면 속성을로 다시 설정 해야 합니다 `false` .

에 대 한 자세한 내용은 `RefreshView` [ Xamarin.Forms refreshview](~/xamarin-forms/user-interface/refreshview.md)를 참조 하세요.

## <a name="load-data-incrementally"></a>증분 방식으로 데이터 로드

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 사용자가 스크롤하면 증분 데이터 가상화를 지원 합니다. 이렇게 하면 사용자가 스크롤할 때 웹 서비스에서 데이터 페이지를 비동기적으로 로드 하는 등의 시나리오를 사용할 수 있습니다. 또한 더 많은 데이터를 로드 하는 지점은 사용자가 빈 공간을 보거나 스크롤에서 중지 되도록 구성할 수 있습니다.

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 데이터의 증분 로드를 제어 하는 다음 속성을 정의 합니다.

- `RemainingItemsThreshold`형식의, `int` 이벤트가 발생 되는 목록에 아직 표시 되지 않는 항목의 임계값입니다 `RemainingItemsThresholdReached` .
- `RemainingItemsThresholdReachedCommand`에 `ICommand` 도달할 때 실행 되는 형식의입니다 `RemainingItemsThreshold` .
- `object` 형식의 `RemainingItemsThresholdReachedCommandParameter` - `RemainingItemsThresholdReachedCommand`에 전달되는 매개 변수입니다.

[`CollectionView`](xref:Xamarin.Forms.CollectionView) 또한 `RemainingItemsThresholdReached` `CollectionView` `RemainingItemsThreshold` 항목이 표시 되지 않을 정도로가 충분히 스크롤 될 때 발생 하는 이벤트를 정의 합니다. 이 이벤트를 처리 하 여 더 많은 항목을 로드할 수 있습니다. 또한 `RemainingItemsThresholdReached` 이벤트가 발생 하면 `RemainingItemsThresholdReachedCommand` 이 실행 되어 viewmodel에서 증분 데이터 로드가 발생 하도록 할 수 있습니다.

속성의 기본값은 `RemainingItemsThreshold` -1 이며이는 `RemainingItemsThresholdReached` 이벤트가 발생 하지 않음을 나타냅니다. 속성 값이 0 이면의 `RemainingItemsThresholdReached` 마지막 항목이 표시 될 때 이벤트가 발생 합니다 [`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource) . 0 보다 큰 값의 경우에 `RemainingItemsThresholdReached` `ItemsSource` 아직 스크롤되지 않는 항목 수가에 포함 되어 있으면 이벤트가 발생 합니다.

> [!NOTE]
> [`CollectionView`](xref:Xamarin.Forms.CollectionView) 속성의 `RemainingItemsThreshold` 값이 항상-1 보다 크거나 같도록 속성의 유효성을 검사 합니다.

다음 XAML 예제에서는 데이터를 [`CollectionView`](xref:Xamarin.Forms.CollectionView) 증분 로드 하는을 보여 줍니다.

```xaml
<CollectionView ItemsSource="{Binding Animals}"
                RemainingItemsThreshold="5"
                RemainingItemsThresholdReached="OnCollectionViewRemainingItemsThresholdReached">
    ...
</CollectionView>
```

해당하는 C# 코드는 다음과 같습니다.

```csharp
CollectionView collectionView = new CollectionView
{
    RemainingItemsThreshold = 5
};
collectionView.RemainingItemsThresholdReached += OnCollectionViewRemainingItemsThresholdReached;
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Animals");
```

이 코드 예제에서 이벤트는 `RemainingItemsThresholdReached` 5 개의 항목이 아직 스크롤되지 않고 이벤트 처리기를 실행 하는 경우에 발생 합니다 `OnCollectionViewRemainingItemsThresholdReached` .

```csharp
void OnCollectionViewRemainingItemsThresholdReached(object sender, EventArgs e)
{
    // Retrieve more data here and add it to the CollectionView's ItemsSource collection.
}
```

> [!NOTE]
> 를 `RemainingItemsThresholdReachedCommand` viewmodel의 구현에 바인딩하여 데이터를 증분 로드할 수도 있습니다 `ICommand` .

## <a name="related-links"></a>관련 링크

- [CollectionView (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-collectionviewdemos/)
- [Xamarin.Forms RefreshView](~/xamarin-forms/user-interface/refreshview.md)
- [Xamarin.Forms SwipeView](~/xamarin-forms/user-interface/swipeview.md)
- [Xamarin.Forms 데이터 바인딩](~/xamarin-forms/app-fundamentals/data-binding/index.md)
- [Xamarin.Forms 데이터 템플릿](~/xamarin-forms/app-fundamentals/templates/data-templates/index.md)
- [DataTemplateSelector 만들기 Xamarin.Forms](~/xamarin-forms/app-fundamentals/templates/data-templates/selector.md)

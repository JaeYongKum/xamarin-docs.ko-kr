---
title: ListView 모양
description: 이 문서에서는 Xamarin.Forms 헤더, 바닥글, 그룹 및 가변 높이 셀을 사용 하 여 응용 프로그램에서 listview을 사용자 지정 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: DC8009B0-4371-4D60-885A-5362FC7EE3E5
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/13/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 415c10706252b11cc2ec009137feab1d6d7d90ba
ms.sourcegitcommit: ebdc016b3ec0b06915170d0cbbd9e0e2469763b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93365946"
---
# <a name="listview-appearance"></a>ListView 모양

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](/samples/xamarin/xamarin-forms-samples/userinterface-listview-grouping)

를 사용 하면 목록의 Xamarin.Forms [`ListView`](xref:Xamarin.Forms.ListView) [`ViewCell`](xref:Xamarin.Forms.ViewCell) 각 행에 대 한 인스턴스와 함께 목록의 표시를 사용자 지정할 수 있습니다.

## <a name="grouping"></a>그룹화

연속 스크롤 목록에서 많은 데이터 집합을 표시 하는 것이 어려울 수 있습니다. 그룹화를 사용 하면 데이터를 더 쉽게 탐색할 수 있도록 콘텐츠를 구성 하 고 플랫폼별 컨트롤을 활성화 하 여 이러한 경우에서 사용자 환경을 향상 시킬 수 있습니다.

에 대해 그룹화가 활성화 되 면 `ListView` 각 그룹에 대해 머리글 행이 추가 됩니다.

그룹화를 사용 하도록 설정 하려면:

- 목록 목록 (그룹 목록, 각 그룹이 요소 목록)을 만듭니다.
- 을 `ListView` `ItemsSource` 해당 목록으로 설정 합니다.
- `IsGroupingEnabled`를 true로 설정합니다.
- [`GroupDisplayBinding`](xref:Xamarin.Forms.ListView.GroupDisplayBinding)그룹의 제목으로 사용 되는 그룹의 속성에 바인딩하려면 설정 합니다.
- 필드 [`GroupShortNameBinding`](xref:Xamarin.Forms.ListView.GroupShortNameBinding) 그룹의 짧은 이름으로 사용 되는 그룹의 속성에 바인딩하려면 설정 합니다. 짧은 이름은 점프 목록 (iOS의 오른쪽 열)에 사용 됩니다.

먼저 그룹에 대 한 클래스를 만듭니다.

```csharp
public class PageTypeGroup : List<PageModel>
    {
        public string Title { get; set; }
        public string ShortName { get; set; } //will be used for jump lists
        public string Subtitle { get; set; }
        private PageTypeGroup(string title, string shortName)
        {
            Title = title;
            ShortName = shortName;
        }

        public static IList<PageTypeGroup> All { private set; get; }
    }
```

위의 코드에서 `All` 는 ListView에 바인딩 소스로 제공 되는 목록입니다. `Title` 및는 `ShortName` 그룹 제목에 사용 되는 속성입니다.

이 단계에서 `All` 는 빈 목록입니다. 프로그램이 시작 될 때 목록이 채워지도록 정적 생성자를 추가 합니다.

```csharp
static PageTypeGroup()
{
    List<PageTypeGroup> Groups = new List<PageTypeGroup> {
            new PageTypeGroup ("Alpha", "A"){
                new PageModel("Amelia", "Cedar", new switchCellPage(),""),
                new PageModel("Alfie", "Spruce", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Ava", "Pine", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Archie", "Maple", new switchCellPage(), "grapefruit.jpg")
            },
            new PageTypeGroup ("Bravo", "B"){
                new PageModel("Brooke", "Lumia", new switchCellPage(),""),
                new PageModel("Bobby", "Xperia", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Bella", "Desire", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Ben", "Chocolate", new switchCellPage(), "grapefruit.jpg")
            }
        };
        All = Groups; //set the publicly accessible list
}
```

위의 코드에서 `Add` 형식의 인스턴스인의 요소에 대해를 호출할 수도 있습니다 `Groups` `PageTypeGroup` . 는에서 상속 되므로이 메서드는 가능 `PageTypeGroup` `List<PageModel>` 합니다.

그룹화 된 목록을 표시 하는 XAML은 다음과 같습니다.

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="DemoListView.GroupingViewPage"
    <ContentPage.Content>
        <ListView  x:Name="GroupedView"
                   GroupDisplayBinding="{Binding Title}"
                   GroupShortNameBinding="{Binding ShortName}"
                   IsGroupingEnabled="true">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}"
                              Detail="{Binding Subtitle}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </ContentPage.Content>
</ContentPage>
```

이 XAML은 다음 작업을 수행 합니다.

- `GroupShortNameBinding` `ShortName` 그룹 클래스에 정의 된 속성으로 설정 합니다.
- `GroupDisplayBinding` `Title` 그룹 클래스에 정의 된 속성으로 설정 합니다.
- `IsGroupingEnabled`True로 설정
- 를 `ListView` 그룹화 된 `ItemsSource` 목록으로 변경

다음 스크린샷은 결과 UI를 보여 줍니다.

![ListView 그룹화 예](customizing-list-appearance-images/grouping-depth.png)

### <a name="customizing-grouping"></a>그룹화 사용자 지정

목록에서 그룹화를 사용 하도록 설정한 경우 그룹 머리글도 사용자 지정할 수 있습니다.

`ListView` `ItemTemplate` 행이 표시 되는 방식을 정의 하기 위한가 있는 방법과 마찬가지로에가 있습니다 `ListView` `GroupHeaderTemplate` .

XAML에서 그룹 헤더를 사용자 지정 하는 예제는 다음과 같습니다.

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="DemoListView.GroupingViewPage">
    <ContentPage.Content>
        <ListView x:Name="GroupedView"
                  GroupDisplayBinding="{Binding Title}"
                  GroupShortNameBinding="{Binding ShortName}"
                  IsGroupingEnabled="true">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}"
                              Detail="{Binding Subtitle}"
                              TextColor="#f35e20"
                              DetailColor="#503026" />
                </DataTemplate>
            </ListView.ItemTemplate>
            <!-- Group Header Customization-->
            <ListView.GroupHeaderTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}"
                              Detail="{Binding ShortName}"
                              TextColor="#f35e20"
                              DetailColor="#503026" />
                </DataTemplate>
            </ListView.GroupHeaderTemplate>
            <!-- End Group Header Customization -->
        </ListView>
    </ContentPage.Content>
</ContentPage>
```

## <a name="headers-and-footers"></a>머리글 및 바닥글

ListView가 목록의 요소로 스크롤되는 머리글 및 바닥글을 표시할 수 있습니다. 머리글과 바닥글은 텍스트 문자열 또는 보다 복잡 한 레이아웃 일 수 있습니다. 이 동작은 [섹션 그룹과](#grouping)구분 됩니다.

`Header`및/또는를 값으로 설정 `Footer` `string` 하거나 보다 복잡 한 레이아웃으로 설정할 수 있습니다. 또한 `HeaderTemplate` 및 속성을 `FooterTemplate` 사용 하 여 데이터 바인딩을 지 원하는 머리글 및 바닥글에 대해 더 복잡 한 레이아웃을 만들 수 있습니다.

기본 머리글/바닥글을 만들려면 머리글 또는 바닥글 속성을 표시 하려는 텍스트로 설정 하면 됩니다. 코드

```csharp
ListView HeaderList = new ListView()
{
    Header = "Header",
    Footer = "Footer"
};
```

XAML에서:

```xaml
<ListView x:Name="HeaderList" 
          Header="Header"
          Footer="Footer">
    ...
</ListView>
```

![머리글 및 바닥글이 있는 ListView](customizing-list-appearance-images/header-default.png)

사용자 지정 된 머리글 및 바닥글을 만들려면 머리글 및 바닥글 뷰를 정의 합니다.

```xaml
<ListView.Header>
    <StackLayout Orientation="Horizontal">
        <Label Text="Header"
               TextColor="Olive"
               BackgroundColor="Red" />
    </StackLayout>
</ListView.Header>
<ListView.Footer>
    <StackLayout Orientation="Horizontal">
        <Label Text="Footer"
               TextColor="Gray"
               BackgroundColor="Blue" />
    </StackLayout>
</ListView.Footer>
```

![사용자 지정 된 머리글 및 바닥글이 있는 ListView](customizing-list-appearance-images/header-custom.png)

## <a name="scrollbar-visibility"></a>스크롤 표시 유형

[`ListView`](xref:Xamarin.Forms.ListView)클래스에는 `HorizontalScrollBarVisibility` `VerticalScrollBarVisibility` [`ScrollBarVisibility`](xref:Xamarin.Forms.ScrollBarVisibility) 가로 또는 세로 스크롤 막대가 표시 될 때를 나타내는 값을 가져오거나 설정 하는 및 속성이 있습니다. 두 속성은 모두 다음 값으로 설정할 수 있습니다.

- [`Default`](xref:Xamarin.Forms.ScrollBarVisibility) 플랫폼의 기본 스크롤 막대 동작을 나타내며 및 속성의 기본값입니다 `HorizontalScrollBarVisibility` `VerticalScrollBarVisibility` .
- [`Always`](xref:Xamarin.Forms.ScrollBarVisibility) 뷰가 뷰에 맞는 경우에도 스크롤 막대가 표시 됨을 나타냅니다.
- [`Never`](xref:Xamarin.Forms.ScrollBarVisibility) 콘텐츠가 뷰에 맞지 않는 경우에도 스크롤 막대가 표시 되지 않음을 나타냅니다.

## <a name="row-separators"></a>행 구분 기호

`ListView`기본적으로 iOS 및 Android의 요소 사이에 구분 기호가 표시 됩니다. IOS 및 Android에서 구분선을 숨기려는 경우 `SeparatorVisibility` ListView에서 속성을 설정 합니다. 의 옵션은 `SeparatorVisibility` 다음과 같습니다.

- **기본값** -IOS 및 Android의 구분선을 표시 합니다.
- **없음** -모든 플랫폼에서 구분 기호를 숨깁니다.

기본 표시 유형:

C#:

```csharp
SeparatorDemoListView.SeparatorVisibility = SeparatorVisibility.Default;
```

PAGE.XAML

```xaml
<ListView x:Name="SeparatorDemoListView" SeparatorVisibility="Default" />
```

![기본 행 구분 기호가 있는 ListView](customizing-list-appearance-images/separator-default.png)

없음:

C#:

```csharp
SeparatorDemoListView.SeparatorVisibility = SeparatorVisibility.None;
```

PAGE.XAML

```xaml
<ListView x:Name="SeparatorDemoListView" SeparatorVisibility="None" />
```

![행 구분 기호가 없는 ListView](customizing-list-appearance-images/separator-none.png)

속성을 통해 구분 기호 선의 색을 설정할 수도 있습니다 `SeparatorColor` .

C#:

```csharp
SeparatorDemoListView.SeparatorColor = Color.Green;
```

PAGE.XAML

```xaml
<ListView x:Name="SeparatorDemoListView" SeparatorColor="Green" />
```

![녹색 행 구분 기호가 있는 ListView](customizing-list-appearance-images/separator-custom.png)

> [!NOTE]
> 을 로드 한 후 Android에서 이러한 속성 중 하나 `ListView` 를 설정 하면 성능이 크게 저하 됩니다.

## <a name="row-height"></a>행 높이

ListView의 모든 행은 기본적으로 높이가 같습니다. ListView에는 해당 동작을 변경 하는 데 사용할 수 있는 두 가지 속성이 있습니다.

- `HasUnevenRows`&ndash; `true`/`false` 값으로 설정 된 경우 행의 높이가 달라 집니다 `true` . 기본값은 `false`입니다.
- `RowHeight`&ndash;가 일 때 각 행의 높이를 설정 합니다 `HasUnevenRows` `false` .

에서 속성을 설정 하 여 모든 행의 높이를 설정할 수 있습니다 `RowHeight` `ListView` .

### <a name="custom-fixed-row-height"></a>사용자 지정 고정 행 높이

C#:

```csharp
RowHeightDemoListView.RowHeight = 100;
```

PAGE.XAML

```xaml
<ListView x:Name="RowHeightDemoListView" RowHeight="100" />
```

![고정 행 높이가 있는 ListView](customizing-list-appearance-images/height-custom.png)

### <a name="uneven-rows"></a>불균형 행

개별 행의 높이가 서로 다른 경우 속성을로 설정할 수 있습니다 `HasUnevenRows` `true` . `HasUnevenRows` `true` 높이가에 의해 자동으로 계산 되기 때문에 행 높이를 수동으로 설정 하지 않아도 됩니다 Xamarin.Forms .

C#:

```csharp
RowHeightDemoListView.HasUnevenRows = true;
```

PAGE.XAML

```xaml
<ListView x:Name="RowHeightDemoListView" HasUnevenRows="true" />
```

![행이 균등 하지 않은 ListView](customizing-list-appearance-images/height-uneven.png)

### <a name="resize-rows-at-runtime"></a>런타임에 행 크기 조정

`ListView`속성이로 설정 된 경우 개별 행은 런타임에 프로그래밍 방식으로 크기를 조정할 수 있습니다 `HasUnevenRows` `true` . [`Cell.ForceUpdateSize`](xref:Xamarin.Forms.Cell.ForceUpdateSize)메서드는 다음 코드 예제에서 보여 주는 것 처럼 현재 표시 되지 않는 경우에도 셀의 크기를 업데이트 합니다.

```csharp
void OnImageTapped (object sender, EventArgs args)
{
    var image = sender as Image;
    var viewCell = image.Parent.Parent as ViewCell;

    if (image.HeightRequest < 250) {
        image.HeightRequest = image.Height + 100;
        viewCell.ForceUpdateSize ();
    }
}
```

`OnImageTapped`이벤트 처리기는 탭 하는 셀의에 대 한 응답으로 실행 되며 [`Image`](xref:Xamarin.Forms.Image) `Image` 쉽게 볼 수 있도록 셀에 표시 되는의 크기를 늘립니다.

![런타임 행 크기 조정을 사용 하는 ListView](customizing-list-appearance-images/dynamic-row-resizing.png)

> [!WARNING]
> 런타임 행 크기 조정을 과도 하 게 사용할 경우 성능이 저하 될 수 있습니다.

## <a name="related-links"></a>관련 링크

- [그룹화 (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-listview-grouping)
- [사용자 지정 렌더러 뷰 (샘플)](/samples/xamarin/xamarin-forms-samples/workingwithlistviewnative)
- [행의 동적 크기 조정 (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-listview-dynamicunevenlistcells)
- [1.4 릴리스 정보](https://forums.xamarin.com/discussion/35451/xamarin-forms-1-4-0-released/)
- [1.3 릴리스 정보](https://forums.xamarin.com/discussion/29934/xamarin-forms-1-3-0-released/)
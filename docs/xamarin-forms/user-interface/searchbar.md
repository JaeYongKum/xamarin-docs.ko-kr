---
title: Xamarin.Forms SearchBar
description: Xamarin.FormsSearchbar는 검색을 시작 하는 데 사용 되는 사용자 입력 컨트롤입니다. SearchBar 컨트롤은 자리 표시자 텍스트, 쿼리 입력, 실행 및 취소를 지원 합니다. 이 문서에서는 XAML 및 코드에서 SearchBar를 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetId: F5EFEA72-CB23-4DD6-9545-D9BB755AF3CB
ms.technology: xamarin-forms
author: profexorgeek
ms.author: jusjohns
ms.date: 07/21/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 66ffbe0f45754517610a2fc2858a00a6185e1d45
ms.sourcegitcommit: ebdc016b3ec0b06915170d0cbbd9e0e2469763b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93369131"
---
# <a name="no-locxamarinforms-searchbar"></a>Xamarin.Forms SearchBar

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](/samples/xamarin/xamarin-forms-samples/userinterface-searchbardemos/)

는 Xamarin.Forms [`SearchBar`](xref:Xamarin.Forms.SearchBar) 검색을 시작 하는 데 사용 되는 사용자 입력 컨트롤입니다. `SearchBar`컨트롤은 자리 표시자 텍스트, 쿼리 입력, 검색 실행 및 취소를 지원 합니다. 다음 스크린샷에서 `SearchBar` 는에 결과가 표시 된 쿼리를 보여 줍니다 `ListView` .

[![IOS 및 Android에 대 한 SearchBar의 스크린샷](searchbar-images/device-searchbars-cropped.png "IOS 및 Android의 SearchBar")](searchbar-images/device-searchbars.png#lightbox "IOS 및 Android의 SearchBar")

`SearchBar` 클래스는 다음과 같은 속성을 정의합니다.

* [`CancelButtonColor`](xref:Xamarin.Forms.SearchBar.CancelButtonColor) 는 `Color` 취소 단추의 색을 정의 하는입니다.
* `double` 형식의 `CharacterSpacing`은 `SearchBar` 텍스트를 구성하는 문자 사이의 간격입니다.
* [`FontAttributes`](xref:Xamarin.Forms.SearchBar.FontAttributes)`FontAttributes` `SearchBar` 글꼴이 굵게, 기울임꼴로 또는 둘 다 인지 여부를 결정 하는 열거형 값입니다.
* [`FontFamily`](xref:Xamarin.Forms.SearchBar.FontFamily) 는에서 `string` 사용 하는 글꼴 패밀리를 결정 하는입니다 `SearchBar` .
* [`FontSize`](xref:Xamarin.Forms.SearchBar.FontSize) 는 `NamedSize` 열거형 값 이거나 `double` 여러 플랫폼에서 특정 글꼴 크기를 나타내는 값일 수 있습니다.
* [`HorizontalTextAlignment`](xref:Xamarin.Forms.SearchBar.HorizontalTextAlignment)`TextAlignment`쿼리 텍스트의 가로 맞춤을 정의 하는 열거형 값입니다.
* `VerticalTextAlignment``TextAlignment`쿼리 텍스트의 세로 맞춤을 정의 하는 열거형 값입니다.
* [`Placeholder`](xref:Xamarin.Forms.InputView.Placeholder) 는 `string` "Search ..."와 같은 자리 표시자 텍스트를 정의 하는입니다.
* [`PlaceholderColor`](xref:Xamarin.Forms.InputView.PlaceholderColor)`Color`자리 표시자 텍스트의 색을 정의 하는입니다.
* [`SearchCommand`](xref:Xamarin.Forms.SearchBar.SearchCommand) 는 `ICommand` 핑거 탭 또는 클릭과 같은 사용자 동작을 viewmodel에 정의 된 명령에 바인딩할 수 있는입니다.
* [`SearchCommandParameter`](xref:Xamarin.Forms.SearchBar.SearchCommandParameter) 는에 `object` 전달 되어야 하는 매개 변수를 지정 하는입니다 `SearchCommand` .
* [`Text`](xref:Xamarin.Forms.InputView.Text) 는의 `string` 쿼리 텍스트를 포함 하는입니다 `SearchBar` .
* [`TextColor`](xref:Xamarin.Forms.InputView.TextColor) 는 `Color` 쿼리 텍스트 색을 정의 하는입니다.
* `TextTransform``TextTransform`텍스트의 대/소문자를 결정 하는 값입니다 `SearchBar` .

이러한 속성은 개체에 의해 지원 됩니다 [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) . 즉,를 `SearchBar` 사용자 지정 하 고 데이터 바인딩의 대상으로 지정할 수 있습니다. 에서 글꼴 속성을 지정 하 `SearchBar` 는 것은 다른 [ Xamarin.Forms 텍스트 컨트롤](~/xamarin-forms/user-interface/text/index.md)에서 텍스트를 사용자 지정 하는 것과 일치 합니다. 자세한 내용은 [의 Xamarin.Forms 글꼴 ](~/xamarin-forms/user-interface/text/fonts.md)을 참조 하십시오.

## <a name="create-a-searchbar"></a>SearchBar 만들기

는 `SearchBar` XAML에서 인스턴스화될 수 있습니다. `Placeholder`쿼리 입력 상자에 힌트 텍스트를 정의 하기 위해 선택적 속성을 설정할 수 있습니다. 의 기본값은 `Placeholder` 빈 문자열 이므로 설정 되지 않은 경우에는 자리 표시 자가 표시 되지 않습니다. 다음 예제에서는 `SearchBar` 선택적 속성 집합을 사용 하 여 XAML에서를 인스턴스화하는 방법을 보여 줍니다 `Placeholder` .

```xaml
<SearchBar Placeholder="Search items..." />
```

`SearchBar`코드에서를 만들 수도 있습니다.

```csharp
SearchBar searchBar = new SearchBar{ Placeholder = "Search items..." };
```

### <a name="searchbar-appearance-properties"></a>SearchBar 모양 속성

컨트롤은 `SearchBar` 컨트롤의 모양을 사용자 지정 하는 다양 한 속성을 정의 합니다. 다음 예제에서는 `SearchBar` 여러 속성을 지정 하 여 XAML에서를 인스턴스화하는 방법을 보여 줍니다.

```xaml
<SearchBar Placeholder="Search items..."
           CancelButtonColor="Orange"
           PlaceholderColor="Orange"
           TextColor="Orange"
           TextTransform="Lowercase"
           HorizontalTextAlignment="Center"
           FontSize="Medium"
           FontAttributes="Italic" />
```

이러한 속성은 코드에서 개체를 만들 때에도 지정할 수 있습니다 `SearchBar` .

```csharp
SearchBar searchBar = new SearchBar
{
    Placeholder = "Search items...",
    PlaceholderColor = Color.Orange,
    TextColor = Color.Orange,
    TextTransform = TextTransform.Lowercase,
    HorizontalTextAlignment = TextAlignment.Center,
    FontSize = Device.GetNamedSize(NamedSize.Medium, typeof(SearchBar)),
    FontAttributes = FontAttributes.Italic
};
```

다음 스크린샷은 결과 컨트롤을 보여 줍니다 `SearchBar` .

[![IOS 및 Android에서 사용자 지정 된 SearchBar의 스크린샷](searchbar-images/device-searchbars-styled-cropped.png "IOS 및 Android의 사용자 지정 된 SearchBar")](searchbar-images/device-searchbars-styled.png#lightbox "IOS 및 Android의 사용자 지정 된 SearchBar")

> [!NOTE]
> IOS에서 클래스는 `SearchBarRenderer` 재정의 가능한 메서드를 포함 `UpdateCancelButton` 합니다. 이 메서드는 취소 단추가 표시 되는 시점을 제어 하 고 사용자 지정 렌더러에서 재정의할 수 있습니다. 사용자 지정 렌더러에 대 한 자세한 내용은 [ Xamarin.Forms 사용자 지정 렌더러](~/xamarin-forms/app-fundamentals/custom-renderer/index.md)를 참조 하세요.

## <a name="perform-a-search-with-event-handlers"></a>이벤트 처리기를 사용 하 여 검색 수행

`SearchBar`다음 이벤트 중 하나에 이벤트 처리기를 연결 하 여 컨트롤을 사용 하 여 검색을 실행할 수 있습니다.

* [`SearchButtonPressed`](xref:Xamarin.Forms.SearchBar.SearchButtonPressed) 사용자가 검색 단추를 클릭 하거나 enter 키를 누를 때 호출 됩니다.
* [`TextChanged`](xref:Xamarin.Forms.InputView.TextChanged) 쿼리 상자의 텍스트가 변경 될 때마다이 호출 됩니다.

다음 예제에서는 XAML의 이벤트에 연결 된 이벤트 처리기를 보여 주고를 사용 하 여 `TextChanged` `ListView` 검색 결과를 표시 합니다.

```xaml
<SearchBar TextChanged="OnTextChanged" />
<ListView x:Name="searchResults" >
```

이벤트 처리기를 코드에서 만든에 연결할 수도 있습니다 `SearchBar` .

```csharp
SearchBar searchBar = new SearchBar {/*...*/};
searchBar.TextChanged += OnTextChanged;
```

`TextChanged`코드 숨김이 `SearchBar` XAML 또는 코드를 통해 생성 되었는지 여부에 관계 없이 코드 숨김이 파일의 이벤트 처리기는 동일 합니다.

```csharp
void OnTextChanged(object sender, EventArgs e)
{
    SearchBar searchBar = (SearchBar)sender;
    searchResults.ItemsSource = DataService.GetSearchResults(searchBar.Text);
}
```

이전 예제에서는 `DataService` `GetSearchResults` 쿼리와 일치 하는 항목을 반환할 수 있는 메서드가 포함 된 클래스가 있음을 의미 합니다. `SearchBar`컨트롤의 `Text` 속성 값이 메서드에 전달 되 `GetSearchResults` 고 결과는 `ListView` 컨트롤의 속성을 업데이트 하는 데 사용 됩니다 `ItemsSource` . 전반적인 효과는 검색 결과가 컨트롤에 표시 되는 것입니다 `ListView` .

샘플 응용 프로그램은 `DataService` 검색 기능을 테스트 하는 데 사용할 수 있는 클래스 구현을 제공 합니다.

## <a name="perform-a-search-using-a-viewmodel"></a>Viewmodel을 사용 하 여 검색 수행

`SearchCommand`및 `SearchCommandParameter` 속성을 구현에 바인딩하여 이벤트 처리기 없이 검색을 실행할 수 있습니다 `ICommand` . 샘플 프로젝트는 MVVM (모델-뷰-ViewModel) 패턴을 사용 하 여 이러한 구현을 보여 줍니다. MVVM를 사용한 데이터 바인딩에 대 한 자세한 내용은 [MVVM를 사용 하 여 데이터 바인딩](~/xamarin-forms/xaml/xaml-basics/data-bindings-to-mvvm.md)을 참조 하세요.

샘플 응용 프로그램의 viewmodel에는 다음 코드가 포함 되어 있습니다.

```csharp
public class SearchViewModel : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void NotifyPropertyChanged([CallerMemberName] string propertyName = "")
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }

    public ICommand PerformSearch => new Command<string>((string query) =>
    {
        SearchResults = DataService.GetSearchResults(query);
    });

    private List<string> searchResults = DataService.Fruits;
    public List<string> SearchResults
    {
        get
        {
            return searchResults;
        }
        set
        {
            searchResults = value;
            NotifyPropertyChanged();
        }
    }
}
```

> [!NOTE]
> Viewmodel은 검색을 수행할 수 있는 클래스의 존재를 가정 합니다 `DataService` . `DataService`예제 데이터를 포함 하는 클래스는 샘플 응용 프로그램에서 사용할 수 있습니다.

다음 XAML은 `SearchBar` 검색 결과를 표시 하는 컨트롤을 사용 하 여를 예제 viewmodel에 바인딩하는 방법을 보여 줍니다 `ListView` .

```xaml
<ContentPage ...>
    <ContentPage.BindingContext>
        <viewmodels:SearchViewModel />
    </ContentPage.BindingContext>
    <StackLayout ...>
        <SearchBar x:Name="searchBar"
                   ...
                   SearchCommand="{Binding PerformSearch}"
                   SearchCommandParameter="{Binding Text, Source={x:Reference searchBar}}"/>
        <ListView x:Name="searchResults"
                  ...
                  ItemsSource="{Binding SearchResults}" />
    </StackLayout>
</ContentPage>
```

이 예제에서는을 `BindingContext` 클래스의 인스턴스로 설정 합니다 `SearchViewModel` . Viewmodel의에 속성을 바인딩하고 속성 `SearchCommand` `PerformSearch` `ICommand` `SearchBar` `Text` 을 속성에 바인딩합니다 `SearchCommandParameter` . `ListView.ItemsSource`속성은 `SearchResults` viewmodel의 속성에 바인딩됩니다.

인터페이스 및 바인딩에 대 한 자세한 내용은 `ICommand` [ Xamarin.Forms 데이터 바인딩](~/xamarin-forms/app-fundamentals/data-binding/index.md) 및 [ICommand 인터페이스](~/xamarin-forms/app-fundamentals/data-binding/commanding.md)를 참조 하세요.

## <a name="related-links"></a>관련 링크

* [SearchBar 데모](/samples/xamarin/xamarin-forms-samples/userinterface-searchbardemos/)
* [Xamarin.Forms 텍스트 컨트롤](~/xamarin-forms/user-interface/text/index.md)
* [글꼴 Xamarin.Forms](~/xamarin-forms/user-interface/text/fonts.md)
* [Xamarin.Forms 데이터 바인딩](~/xamarin-forms/app-fundamentals/data-binding/index.md)
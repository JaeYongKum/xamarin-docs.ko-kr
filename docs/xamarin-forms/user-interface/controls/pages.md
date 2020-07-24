---
title: ':::no-loc(Xamarin.Forms)::: Pages'
description: ':::no-loc(Xamarin.Forms):::페이지는 플랫폼 간 모바일 응용 프로그램 화면을 나타냅니다. 이 문서에서는에 포함 된 페이지를 나열 합니다 :::no-loc(Xamarin.Forms)::: .'
ms.prod: xamarin
ms.assetid: 9C8C710F-E312-420B-9324-A7A20CEDB7EC
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/12/2016
no-loc:
- ':::no-loc(Xamarin.Forms):::'
- ':::no-loc(Xamarin.Essentials):::'
ms.openlocfilehash: ca7e98e4e955ac45a3813a3c1cde97ab0939853a
ms.sourcegitcommit: 952db1983c0bc373844c5fbe9d185e04a87d8fb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86997269"
---
# <a name="no-locxamarinforms-pages"></a>:::no-loc(Xamarin.Forms)::: Pages

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/formsgallery/)

_:::no-loc(Xamarin.Forms):::페이지는 플랫폼 간 모바일 응용 프로그램 화면을 나타냅니다._

아래에서 설명 하는 모든 페이지 형식은 클래스에서 파생 됩니다 :::no-loc(Xamarin.Forms)::: [`Page`](xref::::no-loc(Xamarin.Forms):::.Page) . 이러한 시각적 요소는 대부분의 화면을 차지 합니다. `Page`개체는 `ViewController` iOS의와 `Page` 유니버설 Windows 플랫폼의를 나타냅니다. Android에서 각 페이지는와 같은 화면을 차지 `Activity` 하지만 :::no-loc(Xamarin.Forms)::: 페이지는 개체가 *아닙니다* `Activity` .

[![::: no loc (Xamarin.ios)::: 페이지 형식](pages-images/pages-sml.png)](pages-images/pages.png#lightbox "::: no loc (Xamarin.ios)::: 페이지 형식")

## <a name="pages"></a>페이지

:::no-loc(Xamarin.Forms):::에서는 다음 페이지 형식을 지원 합니다.

| 형식 | 설명 | 모양 |
| --- | --- | --- |
| `ContentPage` | [`ContentPage`](xref::::no-loc(Xamarin.Forms):::.ContentPage)는 가장 간단 하 고 가장 일반적인 페이지 유형입니다. 속성을 [`Content`](xref::::no-loc(Xamarin.Forms):::.ContentPage.Content) 단일 개체로 설정 합니다 [`View`](views.md) .이 개체는 일반적으로 [`Layout`](layouts.md) , 또는와 같은입니다 [`StackLayout`](xref::::no-loc(Xamarin.Forms):::.StackLayout) [`Grid`](xref::::no-loc(Xamarin.Forms):::.Grid) [`ScrollView`](xref::::no-loc(Xamarin.Forms):::.ScrollView) .<br /><br />[API 문서](xref::::no-loc(Xamarin.Forms):::.ContentPage) | [![ContentPage 예제](pages-images/ContentPage.png "ContentPage 예제")](pages-images/ContentPage-Large.png#lightbox "ContentPage 예제")<br />[이 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ContentPageDemoPage.cs)  /  에 대 한 c # 코드 [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ContentPageDemoPage.xaml) |
| `MasterDetailPage` | 는 [`MasterDetailPage`](xref::::no-loc(Xamarin.Forms):::.MasterDetailPage) 두 가지 정보 창을 관리 합니다. 속성을 [`Master`](xref::::no-loc(Xamarin.Forms):::.MasterDetailPage.Master) 일반적으로 목록이 나 메뉴를 표시 하는 페이지로 설정 합니다. 속성을 [`Detail`](xref::::no-loc(Xamarin.Forms):::.MasterDetailPage.Detail) 마스터 페이지에서 선택한 항목을 표시 하는 페이지로 설정 합니다. [`IsPresented`](xref::::no-loc(Xamarin.Forms):::.MasterDetailPage.IsPresented)속성은 마스터 또는 세부 페이지가 표시 되는지 여부를 제어 합니다.<br /><br />[API 설명서](xref::::no-loc(Xamarin.Forms):::.MasterDetailPage)  /  [가이드](~/xamarin-forms/app-fundamentals/navigation/master-detail-page.md)  /  [샘플](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-masterdetailpage) | [![MasterDetailPage 예제](pages-images/MasterDetailPage.png "MasterDetailPage 예제")](pages-images/MasterDetailPage-Large.png#lightbox "MasterDetailPage 예제")<br />[이 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/MasterDetailPageDemoPage.cs)  /  에 대 한 c # 코드 [코드 숨김이](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/MasterDetailPageDemoPage.xaml.cs) 포함 된 [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/MasterDetailPageDemoPage.xaml) |
| `NavigationPage` | 는 [`NavigationPage`](xref::::no-loc(Xamarin.Forms):::.NavigationPage) 스택 기반 아키텍처를 사용 하 여 다른 페이지 간의 탐색을 관리 합니다. 응용 프로그램에서 페이지 탐색을 사용 하는 경우 홈 페이지의 인스턴스를 개체의 생성자에 전달 해야 합니다 `NavigationPage` .<br /><br />[API 설명서](xref::::no-loc(Xamarin.Forms):::.NavigationPage)  /  [가이드](~/xamarin-forms/app-fundamentals/navigation/hierarchical.md)  /  [예제 1](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-hierarchical), [2](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-passingdata), [3](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-loginflow)  | [![NavigationPage 예제](pages-images/NavigationPage.png "NavigationPage 예제")](pages-images/NavigationPage-Large.png#lightbox "NavigationPage 예제")<br />[이 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/NavigationPageDemoPage.cs)  /  에 대 한 c # 코드 [코드 = 숨김으로](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/NavigationPageDemoPage.xaml.cs) [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/NavigationPageDemoPage.xaml) |
| `TabbedPage` | [`TabbedPage`](xref::::no-loc(Xamarin.Forms):::.TabbedPage)추상 클래스에서 파생 되 [`MultiPage`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1) 고 탭을 사용 하 여 자식 페이지 간을 탐색할 수 있도록 합니다. 속성을 [`Children`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1.Children) 페이지 컬렉션으로 설정 하거나, 속성을 데이터 개체 컬렉션으로 설정 하 고, 속성을로 설정 하 여 [`ItemsSource`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1.ItemsSource) [`ItemTemplate`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1.ItemTemplate) [`DataTemplate`](xref::::no-loc(Xamarin.Forms):::.DataTemplate) 각 개체를 시각적으로 표시 하는 방법을 설명 합니다.<br /><br />[API 설명서](xref::::no-loc(Xamarin.Forms):::.TabbedPage)  /  [가이드](~/xamarin-forms/app-fundamentals/navigation/tabbed-page.md)  /  [샘플 1](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-tabbedpage) 및 [2](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-tabbedpagewithnavigationpage) | [![TabbedPage 예제](pages-images/TabbedPage.png "TabbedPage 예제")](pages-images/TabbedPage-Large.png#lightbox "TabbedPage 예제")<br />[이 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/TabbedPageDemoPage.cs)  /  에 대 한 c # 코드 [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/TabbedPageDemoPage.xaml) |
| `CarouselPage` | [`CarouselPage`](xref::::no-loc(Xamarin.Forms):::.CarouselPage)추상 클래스에서 파생 [`MultiPage`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1) 되며 손가락 살짝 밀기를 통해 자식 페이지 간을 탐색할 수 있습니다. 속성을 [`Children`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1.Children) 개체의 컬렉션으로 설정 [`ContentPage`](xref::::no-loc(Xamarin.Forms):::.ContentPage) 하거나, 속성을 데이터 개체 컬렉션으로 설정 하 고, 속성을로 설정 하 여 [`ItemsSource`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1.ItemsSource) [`ItemTemplate`](xref::::no-loc(Xamarin.Forms):::.MultiPage`1.ItemTemplate) [`DataTemplate`](xref::::no-loc(Xamarin.Forms):::.DataTemplate) 각 개체를 시각적으로 표시 하는 방법을 설명 합니다.<br /><br />[API 설명서](xref::::no-loc(Xamarin.Forms):::.CarouselPage)  /  [가이드](~/xamarin-forms/app-fundamentals/navigation/carousel-page.md)  /  [샘플 1](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-carouselpage) 및 [2](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/navigation-carouselpagetemplate) | [![CarouselPage 예제](pages-images/CarouselPage.png "CarouselPage 예제")](pages-images/CarouselPage-Large.png#lightbox "CarouselPage 예제")<br />[이 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/CarouselPageDemoPage.cs)  /  에 대 한 c # 코드 [XAML 페이지](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/CarouselPageDemoPage.xaml) |
| `TemplatedPage` | [`TemplatedPage`](xref::::no-loc(Xamarin.Forms):::.TemplatedPage)컨트롤 템플릿이 있는 전체 화면 콘텐츠를 표시 하 고,의 기본 클래스입니다 [`ContentPage`](xref::::no-loc(Xamarin.Forms):::.ContentPage) .<br /><br />[API 설명서](xref::::no-loc(Xamarin.Forms):::.TemplatedPage)  /  [가이드](~/xamarin-forms/app-fundamentals/templates/control-template.md) | [![TemplatedPage 예제](pages-images/TemplatedPage.png "TemplatedPage 예제")](pages-images/TemplatedPage.png "TemplatedPage 예제") |
|     |     |     |

## <a name="related-links"></a>관련 링크

- [:::no-loc(Xamarin.Forms):::양식 갤러리 샘플](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/formsgallery)
- [:::no-loc(Xamarin.Forms)::: 샘플](https://docs.microsoft.com/samples/browse/?products=xamarin&term=:::no-loc(Xamarin.Forms):::)
- [:::no-loc(Xamarin.Forms):::API 설명서](https://docs.microsoft.com/dotnet/api/xamarin.forms?view=xamarin-forms)

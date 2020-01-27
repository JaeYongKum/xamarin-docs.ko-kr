---
title: Xamarin.Forms 레이아웃
description: Xamarin.Forms 布局用于将用户界面控件组合到可视结构。 本文列出了包含在 Xamarin.Forms 中的布局。
ms.prod: xamarin
ms.assetid: F4180997-BA21-453A-9958-D1E2940DF050
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/21/2018
ms.openlocfilehash: 4747ce6555a6440c687dc3d239d75307f68683ca
ms.sourcegitcommit: db422e33438f1b5c55852e6942c3d1d75dc025c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76724484"
---
# <a name="xamarinforms-layouts"></a>Xamarin.Forms 레이아웃

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/formsgallery)

_Xamarin.Forms 布局用于将用户界面控件组合到可视结构。_

[ `Layout` ](xref:Xamarin.Forms.Layout)并[ `Layout<T>` ](xref:Xamarin.Forms.Layout`1)在 Xamarin.Forms 中的类是专用的视图作为视图和其他布局容器的子类型。 `Layout`类本身派生自[ `View` ](views.md)。 一个`Layout`派生类通常包含在 Xamarin.Forms 应用程序中设置的位置和大小的子元素的逻辑。

[![Xamarin.ios 레이아웃 형식](layouts-images/layouts-sml.png "Xamarin.ios 레이아웃 형식")](layouts-images/layouts.png#lightbox "Xamarin.ios 레이아웃 형식")

派生的类`Layout`可以分为两类：

## <a name="layouts-with-single-content"></a>具有单一内容布局

这些类派生自[ `Layout` ](xref:Xamarin.Forms.Layout)，用于定义[ `Padding` ](xref:Xamarin.Forms.Layout.Padding)并[ `IsClippedToBounds` ](xref:Xamarin.Forms.Layout.IsClippedToBounds)属性。

<a name="contentView" />

### <a name="contentview"></a>ContentView

|     |     |
| --- | --- |
| [`ContentView`](xref:Xamarin.Forms.ContentView) 包含与设置的一个子[ `Content` ](xref:Xamarin.Forms.ContentView.Content)属性。 `Content`属性可以设置为任意`View`派生类，包括其他`Layout`派生类。 `ContentView` 主要用作结构化元素并用作基类[ `Frame` ](#frame)。<br /><br />[API 文档](xref:Xamarin.Forms.ContentView) / [指南](~/xamarin-forms/user-interface/layouts/contentview.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-contentviewdemos/) | [![ContentView 예제](layouts-images/ContentView.png "ContentView 예제")](layouts-images/ContentView-Large.png#lightbox "ContentView 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ContentViewDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ContentViewDemoPage.xaml) |
|     |     |

<a named="frame" />

### <a name="frame"></a>프레임

|     |     |
| --- | --- |
| [`Frame`](xref:Xamarin.Forms.Frame) 클래스는 [`ContentView`](#contentView) 에서 파생 되 고 해당 자식 주위에 테두리 또는 프레임을 표시 합니다. `Frame` 클래스의 기본 [`Padding`](xref:Xamarin.Forms.Layout.Padding) 값은 20 이며 [`BorderColor`](xref:Xamarin.Forms.Frame.BorderColor), [`CornerRadius`](xref:Xamarin.Forms.Frame.CornerRadius)및 [`HasShadow`](xref:Xamarin.Forms.Frame.HasShadow) 속성도 정의 합니다.<br /><br />[API 文档](xref:Xamarin.Forms.Frame) / [指南](~/xamarin-forms/user-interface/layouts/frame.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-frame/) | [![프레임 예제](layouts-images/Frame.png "프레임 예제")](layouts-images/Frame-Large.png#lightbox "프레임 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FrameDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FrameDemoPage.xaml) |
|     |     |

<a name="scrollView" />

### <a name="scrollview"></a>ScrollView

|     |     |
| --- | --- |
| [`ScrollView`](xref:Xamarin.Forms.ScrollView) 它能够滚动其内容。 设置[ `Content` ](xref:Xamarin.Forms.ScrollView.Content)属性设置为要在屏幕上显示的视图或布局太大。 `ScrollView`의 콘텐츠는 [`StackLayout`](#stackLayout)매우 많습니다. [`Orientation`](xref:Xamarin.Forms.ScrollView.Orientation) 속성을 설정 하 여 스크롤이 세로, 가로 또는 둘 다 인지 여부를 표시 합니다.<br /><br />[API 文档](xref:Xamarin.Forms.ScrollView) / [指南](~/xamarin-forms/user-interface/layouts/scroll-view.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-layout) | [![ScrollView 예제](layouts-images/ScrollView.png "ScrollView 예제")](layouts-images/ScrollView-Large.png#lightbox "ScrollView 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ScrollViewDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ScrollViewDemoPage.xaml) |
|     |     |

### <a name="templatedview"></a>TemplatedView

|     |     |
| --- | --- |
| [`TemplatedView`](xref:Xamarin.Forms.TemplatedView) 显示使用控件模板的内容，并为类的基类[ `ContentView` ](#contentView)。<br /><br />[API 文档](xref:Xamarin.Forms.TemplatedView) / [指南](~/xamarin-forms/app-fundamentals/templates/control-template.md) | [![TemplatedView 예제](layouts-images/TemplatedView.png "TemplatedView 예제")](layouts-images/TemplatedView.png#lightbox "TemplatedView 예제") |
|     |     |

### <a name="contentpresenter"></a>ContentPresenter

|     |     |
| --- | --- |
| [`ContentPresenter`](xref:Xamarin.Forms.ContentPresenter) 是模板化中使用的视图的布局管理器[ `ControlTemplate` ](xref:Xamarin.Forms.ControlTemplate)标记呈现内容的显示位置。<br /><br />[API 文档](xref:Xamarin.Forms.ContentPresenter) / [指南](~/xamarin-forms/app-fundamentals/templates/control-template.md) | [![ContentPresenter 예제](layouts-images/ContentPresenter.png "ContentPresenter 예제")](layouts-images/ContentPresenter.png#lightbox "ContentPresenter 예제") |
|     |     |

## <a name="layouts-with-multiple-children"></a>使用多个子级的布局

这些类派生自[ `Layout<View>` ](xref:Xamarin.Forms.Layout`1)。

<a name="stackLayout" />

### <a name="stacklayout"></a>StackLayout

|     |     |
| --- | --- |
| [`StackLayout`](xref:Xamarin.Forms.StackLayout) 将子元素定位在水平或垂直方向上基于堆栈[ `Orientation` ](xref:Xamarin.Forms.StackLayout.Orientation)属性。 [ `Spacing` ](xref:Xamarin.Forms.StackLayout.Spacing)属性控制子级之间的间距和具有默认值为 6。<br /><br />[API 文档](xref:Xamarin.Forms.StackLayout) / [指南](~/xamarin-forms/user-interface/layouts/stack-layout.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-layout)| [![StackLayout 예제](layouts-images/StackLayout.png "StackLayout 예제")](layouts-images/StackLayout-Large.png#lightbox "StackLayout 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/StackLayoutDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/StackLayoutDemoPage.xaml) |
|     |     |

<a name="grid" />

### <a name="grid"></a>모눈

|     |     |
| --- | --- |
| [`Grid`](xref:Xamarin.Forms.Grid) 在行和列的网格中定位其子元素。 使用表示子表位置[附加属性](~/xamarin-forms/xaml/attached-properties.md) [ `Row` ](xref:Xamarin.Forms.Grid.RowProperty)， [ `Column` ](xref:Xamarin.Forms.Grid.ColumnProperty)， [ `RowSpan` ](xref:Xamarin.Forms.Grid.RowSpanProperty)，并[ `ColumnSpan` ](xref:Xamarin.Forms.Grid.ColumnSpanProperty)。<br /><br />[API 文档](xref:Xamarin.Forms.Grid) / [指南](~/xamarin-forms/user-interface/layouts/grid.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-layout) | [![표 예](layouts-images/Grid.png "표 예")](layouts-images/Grid-Large.png#lightbox "표 예")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/GridDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/GridDemoPage.xaml) |
|     |     |

### <a name="absolutelayout"></a>AbsoluteLayout

|     |     |
| --- | --- |
| [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) 相对于其父级的特定位置定位子元素。 使用表示子表位置[附加属性](~/xamarin-forms/xaml/attached-properties.md) [ `LayoutBounds` ](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty)并[ `LayoutFlags` ](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty)。 `AbsoluteLayout`可用于对视图的位置进行动画处理。<br /><br />[API 文档](xref:Xamarin.Forms.AbsoluteLayout) / [指南](~/xamarin-forms/user-interface/layouts/absolute-layout.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-layout) | [![AbsoluteLayout 예제](layouts-images/AbsoluteLayout.png "AbsoluteLayout 예제")](layouts-images/AbsoluteLayout-Large.png#lightbox "AbsoluteLayout 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/AbsoluteLayoutDemoPage.cs) / [XAML 页面](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml)与[代码隐藏](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml.cs) |
|     |     |

### <a name="relativelayout"></a>RelativeLayout

|     |     |
| --- | --- |
| [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) 定位子元素相对于`RelativeLayout`本身或其同级。 使用表示子表位置[附加属性](~/xamarin-forms/xaml/attached-properties.md)设置为的类型的对象[ `Constraint` ](xref:Xamarin.Forms.Constraint)并[ `BoundsConstraint` ](xref:Xamarin.Forms.Constraint)。<br /><br />[API 文档](xref:Xamarin.Forms.RelativeLayout) / [指南](~/xamarin-forms/user-interface/layouts/relative-layout.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-layout) | [![RelativeLayout 예제](layouts-images/RelativeLayout.png "RelativeLayout 예제")](layouts-images/RelativeLayout-Large.png#lightbox "RelativeLayout 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/RelativeLayoutDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/RelativeLayoutDemoPage.xaml) |
|     |     |

### <a name="flexlayout"></a>FlexLayout

|     |     |
| --- | --- |
| [`FlexLayout`](xref:Xamarin.Forms.FlexLayout) 根据 CSS[灵活框布局模块](https://www.w3.org/TR/css-flexbox-1/)，通常称为_flex 布局_或_弹性框_。 `FlexLayout` 定义六种可绑定属性和允许儿童堆积或包装了许多的对齐方式和方向选项的五个附加的可绑定属性。<br /><br />[API 文档](xref:Xamarin.Forms.FlexLayout) / [指南](~/xamarin-forms/user-interface/layouts/flex-layout.md) / [示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-flexlayoutdemos) | [![안 면 레이아웃 예제](layouts-images/FlexLayout.png "안 면 레이아웃 예제")](layouts-images/FlexLayout-Large.png#lightbox "안 면 레이아웃 예제")<br />[此页的 C# 代码](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FlexLayoutDemoPage.cs) / [XAML 页](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FlexLayoutDemoPage.xaml) |
|     |     |

## <a name="related-links"></a>관련 링크

- [Xamarin.Forms FormsGallery 示例](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/formsgallery)
- [Xamarin.Forms 샘플](https://docs.microsoft.com/samples/browse/?products=xamarin&term=Xamarin.Forms)
- [Xamarin.Forms API 설명서](https://docs.microsoft.com/dotnet/api/xamarin.forms?view=xamarin-forms)

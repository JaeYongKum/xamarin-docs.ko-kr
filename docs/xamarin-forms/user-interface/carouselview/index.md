---
title: Xamarin.FormsCarouselView
description: CarouselView는 스크롤 가능한 레이아웃으로 데이터를 표시 하기 위한 뷰입니다. 사용자는 항목 컬렉션을 통해 이동할 수 있습니다.
ms.prod: xamarin
ms.assetid: 5b673347-cdba-4532-820f-fb5f070c86bc
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/08/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 40b918adff523fa446e69c064029311c54d01290
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86935046"
---
# <a name="xamarinforms-carouselview"></a>Xamarin.FormsCarouselView

![시험판 API](~/media/shared/preview.png "이 API는 현재 시험판임")

## <a name="introduction"></a>[소개](introduction.md)

는 [`CarouselView`](xref:Xamarin.Forms.CarouselView) 스크롤 가능한 레이아웃으로 데이터를 표시 하기 위한 뷰입니다. 사용자는 항목 컬렉션을 통해 이동할 수 있습니다.

## <a name="data"></a>[Data](populate-data.md)

는 [`CarouselView`](xref:Xamarin.Forms.CarouselView) 속성을를 [`ItemsSource`](xref:Xamarin.Forms.ItemsView.ItemsSource) 구현 하는 컬렉션으로 설정 하 여 데이터로 채워집니다 `IEnumerable` . 속성을로 설정 하 여 각 항목의 모양을 정의할 수 있습니다 [`ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate) [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) .

## <a name="layout"></a>[레이아웃](layout.md):

기본적으로에는 [`CarouselView`](xref:Xamarin.Forms.CarouselView) 해당 항목이 가로 목록으로 표시 됩니다. 그러나 세로 방향을 포함 하 여 CollectionView와 동일한 레이아웃에도 액세스할 수 있습니다.

## <a name="interaction"></a>[상호 작용](interaction.md)

에 현재 표시 된 항목은 [`CarouselView`](xref:Xamarin.Forms.CarouselView) 및 속성을 통해 액세스할 수 있습니다 `CurrentItem` `Position` .

## <a name="empty-views"></a>[빈 뷰](emptyview.md)

에서 [`CarouselView`](xref:Xamarin.Forms.CarouselView) 데이터를 표시할 수 없는 경우 사용자에 게 피드백을 제공 하는 빈 뷰를 지정할 수 있습니다. 빈 뷰는 문자열, 뷰 또는 여러 뷰가 될 수 있습니다.

## <a name="scrolling"></a>[스크롤](scrolling.md)

사용자가 스크롤을 시작 swipes 면 항목이 완전히 표시 되도록 스크롤의 끝 위치를 제어할 수 있습니다. 또한 [`CarouselView`](xref:Xamarin.Forms.CarouselView) [`ScrollTo`](xref:Xamarin.Forms.ItemsView.ScrollTo*) 는 프로그래밍 방식으로 항목을 뷰로 스크롤 하는 두 가지 메서드를 정의 합니다. 오버 로드 중 하나는 지정 된 인덱스에 있는 항목을 뷰로 스크롤하고 다른 하나는 지정 된 항목을 뷰로 스크롤합니다.

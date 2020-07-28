---
title: Xamarin.Forms 탐색
description: 이 가이드에서는 Xamarin.Forms 앱에서 탐색을 수행하는 방법을 설명합니다. Xamarin.Forms는 사용되는 페이지 형식에 따라 다양한 페이지 탐색 환경을 제공합니다.
ms.prod: xamarin
ms.assetid: BC5D0C6C-D5A9-4B12-A492-ED1F570CEC87
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/01/2017
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 65aa0f060e4d48834017a334d69b2f21645825f3
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86937191"
---
# <a name="xamarinforms-navigation"></a>Xamarin.Forms 탐색

‘Xamarin.Forms는 사용되는 페이지 형식에 따라 다양한 페이지 탐색 환경을 제공합니다.’

![Xamarin.Forms 페이지 유형](images/page-types.png)

또는 Xamarin.Forms Shell 애플리케이션은 설정된 탐색 계층 구조를 적용하지 않는 URI 기반의 탐색 환경을 사용합니다. 자세한 내용은 [Xamarin.Forms Shell 탐색](~/xamarin-forms/app-fundamentals/shell/navigation.md)를 참조하세요.

## <a name="hierarchical-navigation"></a>[계층적 탐색](hierarchical.md)

[`NavigationPage`](xref:Xamarin.Forms.NavigationPage) 클래스는 사용자가 필요에 따라 페이지를 앞뒤로 탐색할 수 있는 계층적 탐색 환경을 제공합니다. 이 모델은 탐색을 [`Page`](xref:Xamarin.Forms.Page) 개체의 LIFO(Last-In, First-Out, 후입선출) 스택으로 구현합니다.

## <a name="tabbedpage"></a>[TabbedPage](tabbed-page.md)

Xamarin.Forms [`TabbedPage`](xref:Xamarin.Forms.TabbedPage)는 탭 목록과 더 큰 세부 정보 영역으로 구성되며 각 탭은 세부 정보 영역으로 콘텐츠를 로드합니다.

## <a name="carouselpage"></a>[CarouselPage](carousel-page.md)

Xamarin.Forms [`CarouselPage`](xref:Xamarin.Forms.CarouselPage)는 사용자가 옆으로 살짝 밀어서 갤러리와 같은 콘텐츠 페이지를 탐색할 수 있는 페이지입니다.

## <a name="masterdetailpage"></a>[MasterDetailPage](master-detail-page.md)

Xamarin.Forms [`MasterDetailPage`](xref:Xamarin.Forms.MasterDetailPage)는 두 개의 관련 정보 페이지를 관리하는 페이지입니다. 이러한 페이지는 항목을 표시하는 마스터 페이지와 이 페이지의 항목에 대한 세부 정보를 표시하는 세부 정보 페이지입니다.

## <a name="modal-pages"></a>[모달 페이지](modal.md)

Xamarin.Forms는 모달 페이지도 지원합니다. 모달 페이지는 사용자가 작업이 완료되거나 취소될 때까지 다른 부분으로 이동할 수 없는 자체 포함된 작업을 완료하도록 권장합니다.

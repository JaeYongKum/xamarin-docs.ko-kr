---
title: Android에서 TabbedPage 페이지 살짝 밀기
description: 플랫폼별를 사용 하면 사용자 지정 렌더러 나 효과를 구현 하지 않고 특정 플랫폼 에서만 사용할 수 있는 기능을 사용할 수 있습니다. 이 문서에서는 TabbedPage의 페이지 간에 가로 손가락 제스처를 사용 하 여 살짝 밀기를 사용 하는 Android 플랫폼별를 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: D1C09CCB-7246-41A4-8BD2-FA6FABCF1C72
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/10/2018
no-loc:
- ':::no-loc(Xamarin.Forms):::'
- ':::no-loc(Xamarin.Essentials):::'
ms.openlocfilehash: 0043d90e631c19a55b766a877a9cd30316f14650
ms.sourcegitcommit: 952db1983c0bc373844c5fbe9d185e04a87d8fb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86997386"
---
# <a name="tabbedpage-page-swiping-on-android"></a>Android에서 TabbedPage 페이지 살짝 밀기

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

이 Android 플랫폼별는의 페이지 간에 가로 손가락 제스처를 사용 하 여 살짝 밀기를 사용 하도록 설정 하는 데 사용 됩니다 [`TabbedPage`](xref::::no-loc(Xamarin.Forms):::.TabbedPage) . 연결 된 속성을 값으로 설정 하 여 XAML에서 사용 됩니다 [`TabbedPage.IsSwipePagingEnabled`](xref::::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific.TabbedPage.IsSwipePagingEnabledProperty) `boolean` .

```xaml
<TabbedPage ...
            xmlns:android="clr-namespace::::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific;assembly=:::no-loc(Xamarin.Forms):::.Core"
            android:TabbedPage.OffscreenPageLimit="2"
            android:TabbedPage.IsSwipePagingEnabled="true">
    ...
</TabbedPage>
```

또는 흐름 API를 사용 하 여 c #에서 사용할 수 있습니다.

```csharp
using :::no-loc(Xamarin.Forms):::.PlatformConfiguration;
using :::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific;
...

On<Android>().SetOffscreenPageLimit(2)
             .SetIsSwipePagingEnabled(true);
```

`TabbedPage.On<Android>`메서드는이 플랫폼별가 Android 에서만 실행 되도록 지정 합니다. [ `TabbedPage.SetIsSwipePagingEnabled` ] (F: :::no-loc(Xamarin.Forms)::: 입니다. PlatformConfiguration. SetIsSwipePagingEnabled ( :::no-loc(Xamarin.Forms)::: . BindableObject, system.string) 메서드는 [`:::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific`](xref::::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific) 네임 스페이스에서의 페이지 사이를 살짝 밀기를 사용 하도록 설정 하는 데 사용 됩니다 [`TabbedPage`](xref::::no-loc(Xamarin.Forms):::.TabbedPage) . 또한 `TabbedPage` 네임 스페이스의 클래스에 `:::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific` 는 [ `EnableSwipePaging` ] (f:)도 :::no-loc(Xamarin.Forms)::: 있습니다. PlatformConfiguration. EnableSwipePaging ( :::no-loc(Xamarin.Forms)::: . IPlatformElementConfiguration { :::no-loc(Xamarin.Forms)::: . PlatformConfiguration. Android, :::no-loc(Xamarin.Forms)::: . TabbedPage}))를 사용 하도록 설정 하는 메서드를 사용 하는 방법을 지정 `DisableSwipePaging` :::no-loc(Xamarin.Forms)::: 합니다. PlatformConfiguration. DisableSwipePaging ( :::no-loc(Xamarin.Forms)::: . IPlatformElementConfiguration { :::no-loc(Xamarin.Forms)::: . PlatformConfiguration. Android, :::no-loc(Xamarin.Forms)::: . TabbedPage}))를 사용 하지 않도록 설정 하는 메서드를 지정 합니다. [`TabbedPage.OffscreenPageLimit`](xref::::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific.TabbedPage.OffscreenPageLimitProperty)연결 된 속성 및 [ `SetOffscreenPageLimit` ] (f:) :::no-loc(Xamarin.Forms)::: PlatformConfiguration. Setoffscreenandpagelimit ( :::no-loc(Xamarin.Forms)::: . BindableObject, System.object) 메서드는 현재 페이지의 한쪽에서 유휴 상태로 유지 해야 하는 페이지 수를 설정 하는 데 사용 됩니다.

결과적으로에 의해 표시 되는 페이지를 통해 살짝 밀기 페이징이 [`TabbedPage`](xref::::no-loc(Xamarin.Forms):::.TabbedPage) 활성화 됩니다.

![TabbedPage를 통해 페이징 살짝 밀기](tabbedpage-page-swiping-images/tabbedpage-swipe.png)

## <a name="related-links"></a>관련 링크

- [PlatformSpecifics (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [플랫폼별 만들기](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [AndroidSpecific API](xref::::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific)
- [AndroidSpecific AppCompat API](xref::::no-loc(Xamarin.Forms):::.PlatformConfiguration.AndroidSpecific.AppCompat)

---
title: Android의 NavigationPage Bar Height
description: 플랫폼별를 사용 하면 사용자 지정 렌더러 나 효과를 구현 하지 않고 특정 플랫폼 에서만 사용할 수 있는 기능을 사용할 수 있습니다. 이 문서에서는 NavigationPage의 탐색 모음 높이를 설정 하는 Android 플랫폼별를 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: C8A73B64-FE70-408A-A72E-8AF147F0C52C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/10/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 5f5e6311c79a88a6018526a2e1c0c06065eefb32
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86929742"
---
# <a name="navigationpage-bar-height-on-android"></a>Android의 NavigationPage Bar Height

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

이 Android 플랫폼별는의 탐색 모음 높이를 설정 [`NavigationPage`](xref:Xamarin.Forms.NavigationPage) 합니다. [`NavigationPage.BarHeight`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.NavigationPage.BarHeightProperty)바인딩 가능한 속성을 정수 값으로 설정 하 여 XAML에서 사용 됩니다.

```xaml
<NavigationPage ...
                xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat;assembly=Xamarin.Forms.Core"
                android:NavigationPage.BarHeight="450">
    ...
</NavigationPage>
```

또는 흐름 API를 사용 하 여 c #에서 사용할 수 있습니다.

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat;
...

public class AndroidNavigationPageCS : Xamarin.Forms.NavigationPage
{
    public AndroidNavigationPageCS()
    {
        On<Android>().SetBarHeight(450);
    }
}
```

`NavigationPage.On<Android>`메서드는이 플랫폼별가 앱 호환 Android 에서만 실행 되도록 지정 합니다. [ `NavigationPage.SetBarHeight` ] (F: Xamarin.Forms 입니다. Platform\roid특정.. a d. Xamarin.Forms IPlatformElementConfiguration { Xamarin.Forms . PlatformConfiguration. Android, Xamarin.Forms . 네임 스페이스의 NavigationPage}, system.string) 메서드는의 [`Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat) 탐색 모음 높이를 설정 하는 데 사용 됩니다 [`NavigationPage`](xref:Xamarin.Forms.NavigationPage) . 또한 [ `NavigationPage.GetBarHeight` ] (f: Xamarin.Forms 입니다. PlatformConfiguration.. b a r a d. Xamarin.Forms IPlatformElementConfiguration { Xamarin.Forms . PlatformConfiguration. Android, Xamarin.Forms . NavigationPage}) 메서드를 사용 하 여에서 탐색 모음의 높이를 반환할 수 있습니다 `NavigationPage` .

그러면의 탐색 모음 높이를 [`NavigationPage`](xref:Xamarin.Forms.NavigationPage) 설정할 수 있습니다.

![NavigationPage 탐색 모음 높이](navigationpage-bar-height-images/navigationpage-barheight.png)

## <a name="related-links"></a>관련 링크

- [PlatformSpecifics (샘플)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [플랫폼별 만들기](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [AndroidSpecific API](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific)
- [AndroidSpecific AppCompat API](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat)

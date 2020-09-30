---
title: IOS의 명명 된 글꼴 크기에 대 한 접근성 크기 조정
description: 플랫폼별를 사용 하면 사용자 지정 렌더러 나 효과를 구현 하지 않고 특정 플랫폼 에서만 사용할 수 있는 기능을 사용할 수 있습니다. 이 문서에서는 명명 된 글꼴 크기에 대 한 접근성 크기 조정을 사용 하지 않도록 설정 하는 iOS 플랫폼별를 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: B443BAF6-E6F6-4A0E-80B5-CAACE6B550EF
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/28/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: e693565bf34b2ab17992aed72d022315a33b87e3
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91563668"
---
# <a name="accessibility-scaling-for-named-font-sizes-on-ios"></a>IOS의 명명 된 글꼴 크기에 대 한 접근성 크기 조정

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

이 iOS 플랫폼별 플랫폼 전용은 명명 된 글꼴 크기에 대 한 접근성 크기 조정을 비활성화 합니다. 바인딩 가능한 속성을로 설정 하 여 XAML에서 사용 됩니다 `Application.EnableAccessibilityScalingForNamedFontSizes` `false` .

```xaml
<Application ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
             ios:Application.EnableAccessibilityScalingForNamedFontSizes="false">
    ...
</Application>
```

또는 흐름 API를 사용 하 여 c #에서 사용할 수 있습니다.

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

Xamarin.Forms.Application.Current.On<iOS>().SetEnableAccessibilityScalingForNamedFontSizes(false);
```

`Application.On<iOS>`메서드는이 플랫폼별가 iOS 에서만 실행 되도록 지정 합니다. `Application.SetEnableAccessibilityScalingForNamedFontSizes`네임 스페이스의 메서드는 [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) iOS 접근성 설정에 따라 크기가 조정 되는 명명 된 글꼴 크기를 사용 하지 않도록 설정 하는 데 사용 됩니다. 또한 `Application.GetEnableAccessibilityScalingForNamedFontSizes` 메서드를 사용 하 여 명명 된 글꼴 크기를 iOS 내게 필요한 옵션 설정으로 조정할지 여부를 반환할 수 있습니다.

## <a name="related-links"></a>관련 링크

- [PlatformSpecifics (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [플랫폼별 만들기](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iOSSpecific API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
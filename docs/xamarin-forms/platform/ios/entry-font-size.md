---
title: IOS의 항목 글꼴 크기
description: 플랫폼별를 사용 하면 사용자 지정 렌더러 나 효과를 구현 하지 않고 특정 플랫폼 에서만 사용할 수 있는 기능을 사용할 수 있습니다. 이 문서에서는 항목의 글꼴 크기를 조정 하는 iOS 플랫폼별를 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: E8881D4E-902B-4397-A43E-916B2885EC87
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: a3f5b920a3717bb70454eb16a5f830e6472413eb
ms.sourcegitcommit: ebdc016b3ec0b06915170d0cbbd9e0e2469763b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93373187"
---
# <a name="entry-font-size-on-ios"></a>IOS의 항목 글꼴 크기

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)

이 iOS 플랫폼별는의 글꼴 크기를 조정 하 여 [`Entry`](xref:Xamarin.Forms.Entry) 입력 텍스트가 컨트롤에 들어가도록 하는 데 사용 됩니다. 연결 된 속성을 값으로 설정 하 여 XAML에서 사용 됩니다 [`Entry.AdjustsFontSizeToFitWidth`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific.Entry.AdjustsFontSizeToFitWidthProperty) `boolean` .

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
    <StackLayout Margin="20">
        <Entry x:Name="entry"
               Placeholder="Enter text here to see the font size change"
               FontSize="22"
               ios:Entry.AdjustsFontSizeToFitWidth="true" />
        ...
    </StackLayout>
</ContentPage>
```

또는 흐름 API를 사용 하 여 c #에서 사용할 수 있습니다.

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

entry.On<iOS>().EnableAdjustsFontSizeToFitWidth();
```

`Entry.On<iOS>`메서드는이 플랫폼별가 iOS 에서만 실행 되도록 지정 합니다. [ `Entry.EnableAdjustsFontSizeToFitWidth` ] (F: Xamarin.Forms 입니다. PlatformConfiguration. iOSSpecific ( Xamarin.Forms . IPlatformElementConfiguration { Xamarin.Forms . PlatformConfiguration. iOS, Xamarin.Forms . Entry})) 메서드를 사용 하 여 [`Xamarin.Forms.PlatformConfiguration.iOSSpecific`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) 에 맞게 입력 텍스트의 글꼴 크기를 조정 [`Entry`](xref:Xamarin.Forms.Entry) 합니다. 또한 [`Entry`](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific.Entry) 네임 스페이스의 클래스에 `Xamarin.Forms.PlatformConfiguration.iOSSpecific` 는 [ `DisableAdjustsFontSizeToFitWidth` ] (f:)도 Xamarin.Forms 있습니다. PlatformConfiguration. iOSSpecific ( Xamarin.Forms . IPlatformElementConfiguration { Xamarin.Forms . PlatformConfiguration. iOS, Xamarin.Forms . Entry}))를 사용 하지 않도록 설정 하는 메서드 `SetAdjustsFontSizeToFitWidth` (f: Xamarin.Forms . PlatformConfiguration. iOSSpecific ( Xamarin.Forms . IPlatformElementConfiguration { Xamarin.Forms . PlatformConfiguration. iOS, Xamarin.Forms . Entry}, system.string) 메서드를 호출 하 여 글꼴 크기 조정을 설정/해제 하는 데 사용할 수 있는 메서드 `AdjustsFontSizeToFitWidth` (f: Xamarin.Forms . PlatformConfiguration. iOSSpecific ( Xamarin.Forms . IPlatformElementConfiguration { Xamarin.Forms . PlatformConfiguration. iOS, Xamarin.Forms . Entry}) 메서드:

```csharp
entry.On<iOS>().SetAdjustsFontSizeToFitWidth(!entry.On<iOS>().AdjustsFontSizeToFitWidth());
```

그 결과,의 글꼴 크기를 [`Entry`](xref:Xamarin.Forms.Entry) 조정 하 여 입력 텍스트가 컨트롤에 맞게 조정 됩니다.

![항목 글꼴 크기 조정 Platform-Specific](entry-font-size-images/entry-font-size.png)

## <a name="related-links"></a>관련 링크

- [PlatformSpecifics (샘플)](/samples/xamarin/xamarin-forms-samples/userinterface-platformspecifics)
- [플랫폼별 만들기](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iOSSpecific API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
---
title: 'Xamarin.Essentials: 전화 걸기'
description: Xamarin.Essentials에서 PhoneDialer 클래스를 사용하면 애플리케이션이 전화 걸기에서 전화 번호를 열 수 있습니다.
ms.assetid: E7457942-4D7B-4195-A2FF-417919B9537F
author: jamesmontemagno
ms.custom: video
ms.author: jamont
ms.date: 07/02/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 9bd281a61fd53ef3f6d0d3d2307f78a218f33cf4
ms.sourcegitcommit: db423d51356cf5a2dfa1b3925204797b1baf3cd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92734776"
---
# <a name="no-locxamarinessentials-phone-dialer"></a>Xamarin.Essentials: 전화 걸기

**PhoneDialer** 클래스를 사용하면 애플리케이션이 전화 걸기에서 전화 번호를 열 수 있습니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

# <a name="android"></a>[Android](#tab/android)

프로젝트의 대상 Android 버전이 **Android 11(R API 30)** 로 설정된 경우 새 [패키지 가시성 요구 사항](https://developer.android.com/preview/privacy/package-visibility)에 사용되는 쿼리로 해당 Android 매니페스트를 업데이트해야 합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<queries>
  <intent>
    <action android:name="android.intent.action.DIAL" />
    <data android:scheme="tel"/>
  </intent>
</queries>
```

# <a name="ios"></a>[iOS](#tab/ios)

추가 설정이 필요하지 않습니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

플랫폼의 차이점이 없습니다.

-----

## <a name="using-phone-dialer"></a>전화 걸기 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

전화 걸기 기능은 전화 걸기를 열기 위해 전화 번호로 `Open` 메서드를 호출하여 작동합니다. `Open`이 요청되면 API는 국가 번호(지정된 경우)에 따라 자동으로 숫자 형식을 지정하려고 합니다.

```csharp
public class PhoneDialerTest
{
    public void PlacePhoneCall(string number)
    {
        try
        {
            PhoneDialer.Open(number);
        }
        catch (ArgumentNullException anEx)
        {
            // Number was null or white space
        }
        catch (FeatureNotSupportedException ex)
        {
            // Phone Dialer is not supported on this device.
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

## <a name="api"></a>API

- [전화 걸기 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/PhoneDialer)
- [전화 걸기 API 문서](xref:Xamarin.Essentials.PhoneDialer)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Phone-Dialer-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

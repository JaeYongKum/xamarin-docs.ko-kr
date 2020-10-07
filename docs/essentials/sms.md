---
title: 'Xamarin.Essentials: SMS'
description: Xamarin.Essentials의 SMS 클래스를 사용하면 애플리케이션이 기본 SMS 애플리케이션에서 수신자에게 보내도록 지정된 메시지를 열 수 있습니다.
ms.assetid: 81A757F2-6F2A-458F-B9BE-770ADEBFAB58
author: jamesmontemagno
ms.custom: video
ms.author: jamont
ms.date: 09/24/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: d981a7ed2bffbbff12cf69ee4d0cda27ce319040
ms.sourcegitcommit: 3a15d9b29d65139b18dcf0871fe00cffb2a56357
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91353384"
---
# <a name="no-locxamarinessentials-sms"></a>Xamarin.Essentials: SMS

**Sms** 클래스를 사용하면 애플리케이션이 기본 SMS 애플리케이션에서 수신자에게 보내도록 지정된 메시지를 열 수 있습니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

**Sms** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

프로젝트의 대상 Android 버전이 **Android 11(R API 30)** 로 설정된 경우 새 [패키지 가시성 요구 사항](https://developer.android.com/preview/privacy/package-visibility)에 사용되는 쿼리로 해당 Android 매니페스트를 업데이트해야 합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<queries>
  <intent>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="smsto"/>
  </intent>
</queries>
```

# <a name="ios"></a>[iOS](#tab/ios)

추가 설정이 필요하지 않습니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

플랫폼의 차이점이 없습니다.

-----

## <a name="using-sms"></a>Sms 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

SMS 기능은 메시지의 수신자와 메시지 본문이 포함된 `SmsMessage`에 대해 `ComposeAsync` 메서드를 호출하여 작동합니다.

```csharp
public class SmsTest
{
    public async Task SendSms(string messageText, string recipient)
    {
        try
        {
            var message = new SmsMessage(messageText, new []{ recipient });
            await Sms.ComposeAsync(message);
        }
        catch (FeatureNotSupportedException ex)
        {
            // Sms is not supported on this device.
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

또한 여러 명의 수신자를 `SmsMessage`에 전달할 수 있습니다.

```csharp
public class SmsTest
{
    public async Task SendSms(string messageText, string[] recipients)
    {
        try
        {
            var message = new SmsMessage(messageText, recipients);
            await Sms.ComposeAsync(message);
        }
        catch (FeatureNotSupportedException ex)
        {
            // Sms is not supported on this device.
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

## <a name="api"></a>API

- [Sms 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Sms)
- [Sms API 문서](xref:Xamarin.Essentials.Sms)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/SMS-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

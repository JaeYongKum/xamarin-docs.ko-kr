---
title: 'Xamarin.Essentials: 전자 메일'
description: Xamarin.Essentials에서 Email 클래스를 사용하면 애플리케이션이 제목, 본문 및 받는 사람(받는 사람, 참조, 숨은 참조)을 포함한 지정된 정보를 사용하여 기본 메일 애플리케이션을 열 수 있습니다.
ms.assetid: 5FBB6FF0-0E7B-4C29-8F06-91642AF12629
author: jamesmontemagno
ms.custom: video
ms.author: jamont
ms.date: 09/24/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 577628237d1e7433c2ad06466a2e804808874108
ms.sourcegitcommit: d8627a500a9b8a07615aef9822c9b1dba2bf6650
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92629638"
---
# <a name="no-locxamarinessentials-email"></a>Xamarin.Essentials: 전자 메일

**Email** 클래스를 사용하면 애플리케이션이 제목, 본문 및 받는 사람(받는 사람, 참조, 숨은 참조)을 포함한 지정된 정보를 사용하여 기본 메일 애플리케이션을 열 수 있습니다.

**이메일** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

프로젝트의 대상 Android 버전이 **Android 11(R API 30)** 로 설정된 경우 새 [패키지 가시성 요구 사항](https://developer.android.com/preview/privacy/package-visibility)에 사용되는 쿼리로 해당 Android 매니페스트를 업데이트해야 합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<queries>
  <intent>
    <action android:name="android.intent.action.SENDTO" />
    <data android:scheme="mailto" />
  </intent>
</queries>
```

# <a name="ios"></a>[iOS](#tab/ios)

iOS 9 이상에서 Apple은 애플리케이션이 쿼리할 수 있는 구성표를 적용합니다. 전자 메일이 유효한 대상인지 쿼리하려면 Info.plist 파일의 LSApplicationQueriesSchemes에서 `mailto` 구성표를 지정해야 합니다.

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>mailto</string>
</array>
```

# <a name="uwp"></a>[UWP](#tab/uwp)

플랫폼의 차이점이 없습니다.

-----

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

> [!TIP]
> iOS에서 Email API를 사용하려면 물리적 디바이스에서 실행해야 하며, 예외는 throw됩니다.

## <a name="using-email"></a>메일 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

메일 기능은 메일에 대한 정보를 포함하는 `ComposeAsync` 메서드 `EmailMessage`를 호출하여 작동합니다.

```csharp
public class EmailTest
{
    public async Task SendEmail(string subject, string body, List<string> recipients)
    {
        try
        {
            var message = new EmailMessage
            {
                Subject = subject,
                Body = body,
                To = recipients,
                //Cc = ccRecipients,
                //Bcc = bccRecipients
            };
            await Email.ComposeAsync(message);
        }
        catch (FeatureNotSupportedException fbsEx)
        {
            // Email is not supported on this device
        }
        catch (Exception ex)
        {
            // Some other exception occurred
        }
    }
}
```

## <a name="file-attachments"></a>첨부 파일

이 기능을 통해 앱이 디바이스의 전자 메일 클라이언트에 있는 파일을 전자 메일로 보낼 수 있습니다. Xamarin.Essentials는 자동으로 파일 형식(MIME)을 검색하고 파일을 첨부 파일로 추가하도록 요청합니다. 모든 전자 메일 클라이언트는 서로 다르며 특정 파일 확장명만 지원하거나 전혀 지원하지 않을 수 있습니다.

다음은 디스크에 텍스트를 쓰고 이메일 첨부 파일로 추가하는 샘플입니다.

```csharp
var message = new EmailMessage
{
    Subject = "Hello",
    Body = "World",
};

var fn = "Attachment.txt";
var file = Path.Combine(FileSystem.CacheDirectory, fn);
File.WriteAllText(file, "Hello World");

message.Attachments.Add(new EmailAttachment(file));

await Email.ComposeAsync(message);
```

## <a name="platform-differences"></a>플랫폼의 차이점

# <a name="android"></a>[Android](#tab/android)

모든 Android용 이메일 클라이언트가 `Html`을 지원하는 것은 아닙니다. 지원 여부를 확인할 방법은 없으므로 이메일을 보낼 때는 `PlainText`를 사용하는 것이 좋습니다.

# <a name="ios"></a>[iOS](#tab/ios)

플랫폼의 차이점이 없습니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

`PlainText`를 `Html`을 보내려는 `BodyFormat`으로 지원하면 `FeatureNotSupportedException`을 throw합니다.

일부 메일 클라이언트는 첨부 파일 보내기를 지원하지 않습니다. 자세한 내용은 [설명서](/windows/uwp/contacts-and-calendar/sending-email)를 참조하세요.

-----

## <a name="api"></a>API

- [메일 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Email)
- [메일 API 문서](xref:Xamarin.Essentials.Email)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Email-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

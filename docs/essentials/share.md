---
title: 'Xamarin.Essentials: 공유'
description: Xamarin.Essentials에서 Share 클래스를 사용하면 디바이스에 있는 다른 Share의 텍스트 및 웹 링크와 같은 데이터를 공유할 수 있습니다.
ms.assetid: B7B01D55-0129-4C87-B515-89F8F4E94665
author: jamesmontemagno
ms.author: jamont
ms.date: 01/06/2020
ms.custom: video
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 0870dd94c15f1bd94d5c6864b3d4caeb96349f32
ms.sourcegitcommit: 83793378b28e8ef8624406309b4ecd41aa1a3a14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94503269"
---
# <a name="no-locxamarinessentials-share"></a>Xamarin.Essentials: 공유

**Share** 클래스를 사용하면 Share이 디바이스에 있는 다른 Share의 텍스트 및 웹 링크와 같은 데이터를 공유할 수 있습니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-share"></a>Share 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

Share 기능은 다른 애플리케이션에 공유할 정보를 포함하는 데이터 요청 페이로드로 `RequestAsync` 메서드를 호출하여 작동합니다. 텍스트 및 URI는 혼합될 수 있으며 각 플랫폼은 콘텐츠를 기반으로 필터링을 처리합니다.

```csharp

public class ShareTest
{
    public async Task ShareText(string text)
    {
        await Share.RequestAsync(new ShareTextRequest
            {
                Text = text,
                Title = "Share Text"
            });
    }

    public async Task ShareUri(string uri)
    {
        await Share.RequestAsync(new ShareTextRequest
            {
                Uri = uri,
                Title = "Share Web Link"
            });
    }
}
```

요청 시 표시되는 외부 애플리케이션에 공유할 사용자 인터페이스:

![공유](images/share.png)

## <a name="file"></a>파일

이 기능을 통해 앱이 디바이스의 다른 애플리케이션과 파일을 공유할 수 있습니다. Xamarin.Essentials는 자동으로 파일 형식(MIME)을 검색하고 공유를 요청합니다. 각 플랫폼은 특정 파일 확장명만 지원할 수 있습니다.

다음은 디스크에 텍스트를 작성하고 다른 앱과 공유하는 샘플입니다.

```csharp
var fn =  "Attachment.txt";
var file = Path.Combine(FileSystem.CacheDirectory, fn);
File.WriteAllText(file, "Hello World");

await Share.RequestAsync(new ShareFileRequest
{
    Title = Title,
    File = new ShareFile(file)
});
```

## <a name="multiple-files"></a>다중 파일

![시험판 API](~/media/shared/preview.png)

여러 파일 공유 사용은 한 번에 여러 파일을 전송할 수 있다는 점만 단일 파일과 다릅니다.

```csharp
var file1 = Path.Combine(FileSystem.CacheDirectory, "Attachment1.txt");
File.WriteAllText(file, "Content 1");
var file2 = Path.Combine(FileSystem.CacheDirectory, "Attachment2.txt");
File.WriteAllText(file, "Content 2");

await Share.RequestAsync(new ShareMultipleFilesRequest
{
    Title = ShareFilesTitle,
    Files = new ShareFile[] { new ShareFile(file1), new ShareFile(file2) }
});
```

## <a name="presentation-location"></a>프레젠테이션 위치

iPadOS에서 공유를 요청하는 경우 팝 오버 컨트롤에 표시할 수 있습니다. 이는 팝업이 표시되고 화살표가 직접 가리키는 위치를 지정합니다. 이 위치는 보통 작업을 시작한 컨트롤입니다. `PresentationSourceBounds` 속성을 사용하여 위치를 지정할 수 있습니다.

```csharp
await Share.RequestAsync(new ShareFileRequest
{
    Title = Title,
    File = new ShareFile(file),
    PresentationSourceBounds = DeviceInfo.Platform== DevicePlatform.iOS && DeviceInfo.Idiom == DeviceIdiom.Tablet
                            ? new System.Drawing.Rectangle(0, 20, 0, 0)
                            : System.Drawing.Rectangle.Empty
});
```

Xamarin.Forms를 사용할 경우 `View`를 전달하고 경계를 계산할 수 있습니다.


```
public static class ViewHelpers
{
    public static Rectangle GetAbsoluteBounds(this Xamarin.Forms.View element)
    {
        Element looper = element;

        var absoluteX = element.X + element.Margin.Top;
        var absoluteY = element.Y + element.Margin.Left;

        // Add logic to handle titles, headers, or other non-view bars

        while (looper.Parent != null)
        {
            looper = looper.Parent;
            if (looper is Xamarin.Forms.View v)
            {
                absoluteX += v.X + v.Margin.Top;
                absoluteY += v.Y + v.Margin.Left;
            }
        }

        return new Rectangle(absoluteX, absoluteY, element.Width, element.Height);
    }

    public static System.Drawing.Rectangle ToSystemRectangle(this Rectangle rect) =>
        new System.Drawing.Rectangle((int)rect.X, (int)rect.Y, (int)rect.Width, (int)rect.Height);
}
```

`RequstAsync` 호출 시 이를 활용할 수 있습니다.

```csharp
public Command<Xamarin.Forms.View> ShareCommand { get; } = new Command<Xamarin.Forms.View>(Share);
async void Share(Xamarin.Forms.View element)
{
    try
    {
        Analytics.TrackEvent("ShareWithFriends");
        var bounds = element.GetAbsoluteBounds();

        await Share.RequestAsync(new ShareTextRequest
        {
            PresentationSourceBounds = bounds.ToSystemRectangle(),
            Title = "Title",
            Text = "Text"
        });
    }
    catch (Exception)
    {
        // Handle exception that share failed
    }
}
```

`Command` 트리거 시 호출하는 요소를 전달할 수 있습니다.

```xml
<Button Text="Share"
        Command="{Binding ShareWithFriendsCommand}"
        CommandParameter="{Binding Source={RelativeSource Self}}"/>
```

## <a name="platform-differences"></a>플랫폼의 차이점

# <a name="android"></a>[Android](#tab/android)

- `Subject` 속성은 메시지의 원하는 제목에 사용됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

- `Subject`이 사용되지 않습니다.
- `Title`이 사용되지 않습니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

- 설정되지 않은 경우 `Title`은 기본적으로 애플리케이션 이름으로 설정됩니다.
- `Subject`이 사용되지 않습니다.

-----

## <a name="api"></a>API

- [Share 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Share)
- [Share API 문서](xref:Xamarin.Essentials.Share)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Share-Essential-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

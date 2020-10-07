---
title: 'Xamarin.Essentials: 스크린 샷'
description: 이 문서에서는 현재 표시된 앱 화면을 캡처할 수 있는 Xamarin.Essentials의 스크린샷 클래스에 대해 설명합니다.
ms.assetid: C52AE99A-0FB3-425D-9106-3DA5777FEFA0
author: jamesmontemagno
ms.author: jamont
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 085da722aa2e893f97efb1c89f20b03da330ac3e
ms.sourcegitcommit: 744f977b0595f489c592e29c8a3ba548fde02b6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414712"
---
# <a name="no-locxamarinessentials-screenshot"></a>Xamarin.Essentials: 스크린 샷

**스크린샷** 클래스는 현재 표시된 앱 화면을 캡처할 수 있습니다.

![시험판 API](~/media/shared/preview.png)


## <a name="get-started"></a>시작하기

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-screenshot"></a>스크린샷 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

그런 다음, `CaptureAsync`를 호출하여 실행 중인 애플리케이션에서 현재 화면의 스크린샷을 만듭니다. 이렇게 하면 만든 스크린샷의 `Width`, `Height` 및 `Stream`을 가져오는 데 사용할 수 있는 `ScreenshotResult`가 반환됩니다.


```csharp
async Task CaptureScreenshot()
{
    var screenshot = await Screenshot.CaptureAsync();
    var stream = await screenshot.OpenReadAsync();

    Image = ImageSource.FromStream(() => stream);
}
```


## <a name="api"></a>API

- [스크린샷 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Screenshot)
- [스크린샷 API 설명서](xref:Xamarin.Essentials.Screenshot)

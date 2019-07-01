---
title: 'Xamarin.Essentials: 클립보드'
description: 이 문서에서는 애플리케이션 간에 텍스트를 복사하여 시스템 클립보드에 붙여넣을 수 있는 Xamarin.Essentials의 Clipboard 클래스를 설명합니다.
ms.assetid: C52AE99A-0FB3-425D-9106-3DA5777FEFA0
author: jamesmontemagno
ms.author: jamont
ms.date: 02/12/2019
ms.custom: video
ms.openlocfilehash: c186f5c61bd2fa3df305be92a03135e57e302d02
ms.sourcegitcommit: 6e04246207aa743820029e8c217a43cfdd24f991
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67352126"
---
# <a name="xamarinessentials-clipboard"></a>Xamarin.Essentials: 클립보드

**Clipboard** 클래스를 사용하여 애플리케이션 간에 텍스트를 복사하여 시스템 클립보드에 붙여넣을 수 있습니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-clipboard"></a>클립보드 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

**클립보드**에 현재 붙여넣을 준비가 된 텍스트가 있는지 확인합니다.

```csharp
var hasText = Clipboard.HasText;
```

**클립보드**의 텍스트를 설정합니다.

```csharp
await Clipboard.SetTextAsync("Hello World");
```

**클립보드**에서 텍스트를 읽습니다.

```csharp
var text = await Clipboard.GetTextAsync();
```

> [!TIP]
> 클립보드에 대한 액세스는 기본 사용자 인터페이스 스레드에서 이루어져야 합니다. 기본 사용자 인터페이스 스레드에서 메서드를 호출하는 방법을 보려면 [MainThread](~/essentials/main-thread.md) API를 참조하세요.

## <a name="api"></a>API

- [클립보드 소스 코드](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Clipboard)
- [클립보드 API 문서](xref:Xamarin.Essentials.Clipboard)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Clipboard-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

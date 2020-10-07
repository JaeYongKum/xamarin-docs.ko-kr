---
title: 'Xamarin.Essentials: 햅틱 피드백'
description: 이 문서에서는 디바이스에서 햅틱 피드백을 제어할 수 있는 Xamarin.Essentials의 HapticFeedback 클래스에 대해 설명합니다.
ms.assetid: 4462936c-4018-443b-906d-d63da6d0ed7d
author: dimonovdd
ms.author: jamont
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: b1bf597874dc22a95ca9a3db239d9c7d2dd5658a
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91436731"
---
# <a name="no-locxamarinessentials-haptic-feedback"></a>Xamarin.Essentials: 햅틱 피드백

**HapticFeedback** 클래스를 사용하여 디바이스에서 햅틱 피드백을 제어할 수 있습니다.

![시험판 API](~/media/shared/preview.png)

## <a name="get-started"></a>시작하기

[!include[](~/essentials/includes/get-started.md)]

**HapticFeedback** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

Vibrate 권한이 필요하며 Android 프로젝트에서 구성해야 합니다. 이 권한은 다음과 같은 방법으로 추가할 수 있습니다.

**속성** 폴더 아래의 **AssemblyInfo.cs** 파일을 열고 다음을 추가합니다.

```csharp
[assembly: UsesPermission(Android.Manifest.Permission.Vibrate)]
```

또는 Android 매니페스트를 업데이트합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<uses-permission android:name="android.permission.VIBRATE" />
```

또는 Android 프로젝트를 마우스 오른쪽 단추로 클릭하고 프로젝트의 속성을 엽니다. **Android 매니페스트** 아래에서 **필요한 권한:** 영역을 찾아 **VIBRATE** 권한을 확인합니다. 그러면 **AndroidManifest.xml** 파일이 자동으로 업데이트됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

추가 설정이 필요하지 않습니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

플랫폼의 차이점이 없습니다.

-----

## <a name="using-haptic-feedback"></a>햅틱 피드백 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

`Click` 또는 `LongPress` 피드백 유형을 사용하여 햅틱 피드백 기능을 수행할 수 있습니다.

```csharp
try
{
    // Perform click feedback
    HapticFeedback.Perform(HapticFeedbackType.Click);

    // Or use long press    
    HapticFeedback.Perform(HapticFeedbackType.LongPress);
}
catch (FeatureNotSupportedException ex)
{
    // Feature not supported on device
}
catch (Exception ex)
{
    // Other error has occurred.
}
```

## <a name="api"></a>API

- [HapticFeedback 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/HapticFeedback)
- [HapticFeedback API 설명서](xref:Xamarin.Essentials.HapticFeedback)

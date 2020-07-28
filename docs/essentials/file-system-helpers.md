---
title: 'Xamarin.Essentials: 파일 시스템 도우미'
description: Xamarin.Essentials의 FileSystem 클래스에는 앱 패키지 내에서 애플리케이션의 캐시 및 데이터와 열린 파일을 찾기 위한 일련의 도우미가 포함되어 있습니다.
ms.assetid: B3EC2DE0-EFC0-410C-AF71-7410AE84CF84
author: jamesmontemagno
ms.custom: video
ms.author: jamont
ms.date: 11/04/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: eb35750372c5ccb878c7b38f9d25898b09fd7f1e
ms.sourcegitcommit: e412858ce431b3280c88241e324fcab33066eb58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86865899"
---
# <a name="xamarinessentials-file-system-helpers"></a>Xamarin.Essentials: 파일 시스템 도우미

**FileSystem** 클래스에는 앱 패키지 내에서 애플리케이션의 캐시 및 데이터와 열린 파일을 찾기 위한 일련의 도우미가 포함되어 있습니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-file-system-helpers"></a>파일 시스템 도우미 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

**캐시 데이터**를 저장할 애플리케이션 디렉터리를 가져옵니다. 캐시 데이터는 임시 데이터보다 오래 지속되어야 하지만. OS에서 이 스토리지를 지우는 시기를 나타내므로 제대로 작동하는 데 필요한 데이터가 아닌 모든 데이터에 사용할 수 있습니다.

```csharp
var cacheDir = FileSystem.CacheDirectory;
```

사용자 데이터 파일이 아닌 파일에 대한 애플리케이션의 최상위 디렉터리를 가져옵니다. 이러한 파일은 운영 체제 동기화 프레임워크를 사용하여 백업됩니다. 아래 플랫폼 구현 관련 정보를 참조하세요.

```csharp
var mainDir = FileSystem.AppDataDirectory;
```

애플리케이션 패키지에 번들로 제공된 파일을 엽니다.

```csharp
 using (var stream = await FileSystem.OpenAppPackageFileAsync(templateFileName))
 {
    using (var reader = new StreamReader(stream))
    {
        var fileContents = await reader.ReadToEndAsync();
    }
 }
```

## <a name="platform-implementation-specifics"></a>플랫폼 구현 관련 정보

# <a name="android"></a>[Android](#tab/android)

- **CacheDirectory** – 현재 컨텍스트의 [CacheDir](https://developer.android.com/reference/android/content/Context.html#getCacheDir)을 반환합니다.
- **AppDataDirectory** – 현재 컨텍스트의 [FilesDir](https://developer.android.com/reference/android/content/Context.html#getFilesDir)을 반환하고 API 23 이상부터 [자동 백업](https://developer.android.com/guide/topics/data/autobackup.html)을 사용하여 백업됩니다.

Android 프로젝트의 **Assets** 폴더에 파일을 추가하고 빌드 작업을 **AndroidAsset**으로 표시하여 `OpenAppPackageFileAsync`와 함께 사용합니다.

# <a name="ios"></a>[iOS](#tab/ios)

- **CacheDirectory** – [Library/Caches](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html) 디렉터리를 반환합니다.
- **AppDataDirectory** – iTunes 및 iCloud를 통해 백업되는 [Library](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html) 디렉터리를 반환합니다.

> [!IMPORTANT]
> iOS 시뮬레이터에서 애플리케이션 ID(디렉터리 이름에 포함됨)는 모든 빌드에서 변경되므로, 시뮬레이터용 애플리케이션을 빌드할 때마다 올바른 ID를 검색해야 합니다.

iOS 프로젝트의 **Resources** 폴더에 파일을 추가하고 빌드 작업을 **BundledResource**로 표시하여 `OpenAppPackageFileAsync`와 함께 사용합니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

- **CacheDirectory** – [LocalCacheFolder](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localcachefolder#Windows_Storage_ApplicationData_LocalCacheFolder) 디렉터리를 반환합니다.
- **AppDataDirectory** - 클라우드에 백업된 [LocalFolder](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder#Windows_Storage_ApplicationData_LocalFolder) 디렉터리를 반환합니다.

UWP 프로젝트의 루트에 파일을 추가하고 빌드 작업을 **Content**로 표시하여 `OpenAppPackageFileAsync`와 함께 사용합니다.

--------------

## <a name="api"></a>API

- [파일 시스템 도우미 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/FileSystem)
- [파일 시스템 API 문서](xref:Xamarin.Essentials.FileSystem)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/File-System-Helpers-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

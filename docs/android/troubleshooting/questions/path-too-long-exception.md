---
title: PathTooLongException 오류를 해결하려면 어떻게 할까요?
description: 이 문서에서는 앱을 빌드하는 동안 발생할 수 있는 PathTooLongException을 해결하는 방법을 설명합니다.
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 60EE1C8D-BE44-4612-B3B5-70316D71B1EA
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 05/29/2018
ms.openlocfilehash: d58cb676b347caac00c39a381de94954219d1865
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91456862"
---
# <a name="how-do-i-resolve-a-pathtoolongexception-error"></a>PathTooLongException 오류를 해결하려면 어떻게 할까요?

## <a name="cause"></a>원인

Xamarin.Android 프로젝트에서 생성된 경로 이름은 매우 길 수 있습니다.
예를 들어 다음과 같은 경로가 빌드 중에 생성될 수 있습니다.

**C:\\Some\\Directory\\Solution\\Project\\obj\\Debug\\__library_projects__\\Xamarin.Forms.Platform.Android\\library_project_imports\\assets**

최대 경로 길이가 [260자](/windows/win32/fileio/naming-a-file)인 Windows에서는 생성된 경로가 최대 길이를 초과하는 경우 프로젝트를 빌드하는 동안 **PathTooLongException**이 생성될 수 있습니다. 

## <a name="fix"></a>문제 해결

`UseShortFileNames` MSBuild 속성은 기본적으로 이 오류를 피하기 위해 `True`로 설정됩니다. 이 속성을 `True`로 설정하면 빌드 프로세스에서 짧은 경로 이름을 사용하여 **PathTooLongException**을 생성할 가능성을 줄입니다.
예를 들어 `UseShortFileNames`를 `True`로 설정하면 위의 경로는 다음과 같은 경로로 줄어듭니다.

**C:\\Some\\Directory\\Solution\\Project\\obj\\Debug\\lp\\1\\jl\\assets**

이 속성을 수동으로 설정하려면 프로젝트 **.csproj** 파일에 다음 MSBuild 속성을 추가합니다.

```xml
<PropertyGroup>
    <UseShortFileNames>True</UseShortFileNames>
</PropertyGroup>
```

이 플래그를 설정해도 **PathTooLongException** 오류가 해결되지 않으면 프로젝트 **.csproj** 파일에서 `IntermediateOutputPath`를 설정하여 솔루션의 프로젝트에 대한 [공통 중간 출력 루트](/archive/blogs/kirillosenkov/using-a-common-intermediate-and-output-directory-for-your-solution)를 지정하는 것이 또 다른 방법입니다. 비교적 짧은 경로를 사용하세요. 예를 들어:

```xml
<PropertyGroup>
    <IntermediateOutputPath>C:\Projects\MyApp</IntermediateOutputPath>
</PropertyGroup>
```

빌드 속성을 설정하는 방법에 대한 자세한 내용은 [빌드 프로세스](~/android/deploy-test/building-apps/build-process.md)를 참조하세요.
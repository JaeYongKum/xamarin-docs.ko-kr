---
title: 빌드 대상
description: 이 문서에서는 Xamarin.Android 빌드 프로세스에서 지원되는 모든 대상을 나열합니다.
ms.prod: xamarin
ms.assetid: 17DE89FF-F316-4620-B865-EF6E0963A29C
ms.technology: xamarin-android
author: jonpryor
ms.author: jopryo
ms.date: 09/17/2020
ms.openlocfilehash: 4482e6c4bfe2a6952d59d896b7c79ca82432b42b
ms.sourcegitcommit: 38496cfd4d30fd40a011011f303a31de639bd699
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91247230"
---
# <a name="build-targets"></a>빌드 대상

Xamarin.Android 프로젝트에는 다음 빌드 대상이 정의됩니다.

## <a name="build"></a>빌드

프로젝트 및 모든 종속성 안에 소스 코드를 빌드합니다.

이 대상은 Android 패키지(`.apk` 파일)를 만들지 *않습니다*.
Android 패키지를 만들려면, 다음을 빌드할 때 [SignAndroidPackage](#signandroidpackage) 대상을 사용*하거나*, [`$(AndroidBuildApplicationPackage)](~/android/deploy-test/building-apps/build-properties.md#androidbuildapplicationpackage) 속성을 True로 설정합니다.

```shell
msbuild /p:AndroidBuildApplicationPackage=True App.sln
```

## <a name="buildandstartaotprofiling"></a>BuildAndStartAotProfiling

포함된 AOT 프로파일러를 사용하여 앱을 빌드하고, 프로파일러 TCP 포트를 [`$(AndroidAotProfilerPort)`](~/android/deploy-test/building-apps/build-properties.md#androidaotprofilerport)로 설정하고, 기본 작업을 시작합니다.

기본 TCP 포트는 `9999`입니다.

Xamarin.Android 10.2에 추가되었습니다.

## <a name="clean"></a>정리

빌드 프로세스에서 생성된 파일을 모두 제거합니다.

## <a name="finishaotprofiling"></a>FinishAotProfiling

[BuildAndStartAotProfiling](#buildandstartaotprofiling) 대상 *이후에* 호출해야 합니다.

TCP 포트 [`$(AndroidAotProfilerPort)`](~/android/deploy-test/building-apps/build-properties.md#androidaotprofilerport)를 통해 디바이스 또는 에뮬레이터에서 AOT 프로파일러 데이터를 수집하여
[`$(AndroidAotCustomProfilePath)`](~/android/deploy-test/building-apps/build-properties.md#androidaotcustomprofilepath)에 씁니다.

포트 및 사용자 지정 프로필의 기본값은 `9999` 및 `custom.aprof`입니다.

`aprofutil`에 추가 옵션을 전달하려면 [`$(AProfUtilExtraOptions)`](~/android/deploy-test/building-apps/build-properties.md#aprofutilextraoptions) 속성에서 해당 항목을 설정합니다.
속성의 값에 따라 달라집니다.

다음 코드와 동일합니다.

```shell
aprofutil $(AProfUtilExtraOptions) -s -v -f -p $(AndroidAotProfilerPort) -o "$(AndroidAotCustomProfilePath)"
```

Xamarin.Android 10.2에 추가되었습니다.

## <a name="install"></a>설치

기본 디바이스 또는 가상 디바이스에 패키지를 [만들고 서명하여](#signandroidpackage) 설치합니다.

[`$(AdbTarget)`](~/android/deploy-test/building-apps/build-properties.md#adbtarget) 속성은 Android 패키지를 설치하거나 제거할 수 있는 Android 대상 디바이스를 지정합니다.

```bash
# Install package onto emulator via -e
# Use `/Library/Frameworks/Mono.framework/Commands/msbuild` on OS X
MSBuild /t:Install ProjectName.csproj /p:AdbTarget=-e
```

## <a name="signandroidpackage"></a>SignAndroidPackage

Android 패키지(`.apk`) 파일을 만들고 서명합니다.

자체 포함 "릴리스" 패키지를 생성하려면 `/p:Configuration=Release`와 함께 사용합니다.

## <a name="startandroidactivity"></a>StartAndroidActivity

디바이스 또는 실행 중 에뮬레이터에서 기본 작업을 시작합니다.

다른 작업을 시작하려면 [`$(AndroidLaunchActivity)`](~/android/deploy-test/building-apps/build-properties.md#androidlaunchactivity)
속성을 활동 이름으로 설정합니다.

다음 코드와 동일합니다.

```shell
adb shell am start @PACKAGE_NAME@/$(AndroidLaunchActivity)
```

Xamarin.Android 10.2에 추가되었습니다.

## <a name="stopandroidpackage"></a>StopAndroidPackage

디바이스 또는 실행 중 에뮬레이터에서 애플리케이션 패키지를 완전히 중지합니다.

다음 코드와 동일합니다.

```shell
adb shell am force-stop @PACKAGE_NAME@
```

Xamarin.Android 10.2에 추가되었습니다.

## <a name="uninstall"></a>제거

기본 디바이스 또는 가상 디바이스에서 Android 패키지를 제거합니다.

[`$(AdbTarget)`](~/android/deploy-test/building-apps/build-properties.md#adbtarget) 속성은 Android 패키지를 설치하거나 제거할 수 있는 Android 대상 디바이스를 지정합니다.

## <a name="updateandroidresources"></a>UpdateAndroidResources

`Resource.designer.cs` 파일을 업데이트합니다.

이 대상은 일반적으로 프로젝트에 새 리소스가 추가될 때 IDE에 의해 호출됩니다.

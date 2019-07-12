---
title: 버전 정보 및 로그는 어디에서 확인할 수 있나요?
description: 이 문서에서는 Xamarin 버전 정보와 로그를 찾는 데 위치를 설명 합니다. 이 정보는 버그 제출 또는 지원 받기 문제를 진단할 때 유용 합니다.
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: CF386485-EAB0-4B9E-AA17-CB1B6462E505
author: asb3993
ms.author: amburns
ms.date: 03/29/2017
ms.openlocfilehash: e389bc33538ec3c3d36eb749c746f5a4723aab3c
ms.sourcegitcommit: 654df48758cea602946644d2175fbdfba59a64f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67830362"
---
# <a name="where-can-i-find-my-version-information-and-logs"></a>버전 정보 및 로그는 어디에서 확인할 수 있나요?

## <a name="outline"></a>윤곽선

- [버전 정보](#version-information)
    - Windows 버전 정보
    - Mac 버전 정보
    - Android SDK Tools, 플랫폼 도구 빌드-도구
- [IDE 및 설치 관리자 로그](#ide-and-installer-logs)
    - [Windows 로그](#windows-logs)
        - Xamarin Studio
        - Visual Studio용 Xamarin
        - Xamarin Universal 설치 관리자
        - 개별 `.msi` 설치 관리자, 자세한 정보 표시 로그
        - Visual Studio 시작, 자세한 정보 표시 로그
    - [Mac 로그](#mac-logs)
        - 빌드 호스트
    - Mac용 Visual Studio
        - Xamarin Studio
        - Xamarin 설치 관리자
- [자세한 빌드 출력](#verbose-build-output-logs)
- [Xamarin.iOS 및 Xamarin.Android 앱에 대 한 로그 디버그](#debug-logs-for-xamarin-apps)
    - Android `adb` logcat 로그
    - iOS 시뮬레이터 로그온 (Mac)
    - iOS 장치 로그온 (Mac)

## <a name="a-idversion-information-nameversion-information-version-information"></a><a id="version-information" name="version-information" />버전 정보

일반적으로 가장 효율적인 전송 다시 정보에 대 한 모든 합니다 **복사 정보** 단추. 그렇지 않은 경우 추가 정보를 요청 해야 경우가 많습니다. 예를 들어 Android API 수준을 설치 하는 운영 체제 버전, Xcode 버전 및.NET 버전 모두 때 중요할 수 있습니다 문제를 해결 하는 데 합니다.

### <a name="a-idwindows-version-information-namewindows-version-information-windows-version-information"></a><a id="windows-version-information" name="windows-version-information" />Windows 버전 정보

#### <a name="xamarin-studio"></a>Xamarin Studio

**도움말 > 정보 > 자세한 정보 표시 > 복사본 정보 [단추]**

#### <a name="visual-studio"></a>Visual Studio

**도움말 > Microsoft Visual Studio 정보 > [단추] 정보 복사**

### <a name="a-idmac-version-information-namemac-version-information-mac-version-information"></a><a id="mac-version-information" name="mac-version-information" />Mac 버전 정보

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**Visual Studio > Visual Studio 정보 > 자세한 정보 표시 > 복사본 정보 [단추]**

### <a name="a-idandroid-sdk-tools-versions-nameandroid-sdk-tools-versions-android-sdk-tools-platform-tools-build-tools"></a><a id="android-sdk-tools-versions" name="android-sdk-tools-versions" />Android SDK Tools, 플랫폼 도구 빌드-도구

Android SDK Manager를 열고 위쪽의 스크린샷의 찍을 **도구** 섹션입니다.

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**도구 > Android SDK Manager 열기**

#### <a name="visual-studio"></a>Visual Studio

**도구 > Android > Android SDK Manager를 열고...**

## <a name="a-idide-and-installer-logs-nameide-and-installer-logs-ide-and-installer-logs"></a><a id="ide-and-installer-logs" name="ide-and-installer-logs" />IDE 및 설치 관리자 로그

각 로그 위치에 대해 해야 압축 하 고 전체 로그 폴더를 연결 합니다.

### <a name="a-idwindows-logs-namewindows-logs-windows-logs"></a><a id="windows-logs" name="windows-logs" />Windows 로그

#### <a name="a-idwindows-logs-xamarin-vs-namewindows-logs-xamarin-vs--visual-studio-tools-for-xamarin"></a><a id="windows-logs-xamarin-vs" name="windows-logs-xamarin-vs" /> Visual Studio Tools for Xamarin

`%LOCALAPPDATA%\Xamarin\Logs`

#### <a name="a-idvs-2017-namevs-2017--visual-studio-2017"></a><a id="vs-2017" name="vs-2017" /> Visual Studio 2017

[Visual Studio 설치 로그를 가져오는 방법](https://docs.microsoft.com/visualstudio/install/troubleshooting-installation-issues#how-to-get-the-visual-studio-installation-logs)

#### <a name="a-idvs-2015-namevs-2015--visual-studio-2015"></a><a id="vs-2015" name="vs-2015" /> Visual Studio 2015

#### <a name="a-idwindows-universal-installer-namewindows-universal-installer--xamarin-universal-installer"></a><a id="windows-universal-installer" name="windows-universal-installer" /> Xamarin "범용" 설치 관리자

`%LOCALAPPDATA%\Xamarin\Universal`

이러한 로그는에서 로그를 `XamarinInstaller.exe` 설치 관리자입니다.

#### <a name="a-idindividual-msi-installers-verbose-logs-nameindividual-msi-installers-verbose-logs-individual-msi-installers-verbose-logs"></a><a id="individual-msi-installers-verbose-logs" name="individual-msi-installers-verbose-logs" />개별 `.msi` 설치 관리자, 자세한 정보 표시 로그

```csharp
msiexec /i Xamarin.msi /l*vx "%USERPROFILE%\Desktop\Xamarin.log"
```

참조: [명령줄 옵션](https://msdn.microsoft.com/library/aa367988.aspx)

#### <a name="a-idvisual-studio-startup-verbose-logs-namevisual-studio-startup-verbose-logs-visual-studio-startup-verbose-logs"></a><a id="visual-studio-startup-verbose-logs" name="visual-studio-startup-verbose-logs" />Visual Studio 시작, 자세한 정보 표시 로그

```csharp
devenv.exe /log "%USERPROFILE%\Desktop\VisualStudio.log"
```

참조: [/Log (devenv.exe)](https://msdn.microsoft.com/library/ms241272.aspx)

### <a name="a-idmac-logs-namemac-logs-mac-logs"></a><a id="mac-logs" name="mac-logs" />Mac 로그

선택할 수 있습니다 합니다 **이동 > 폴더로 이동** 메뉴 항목 Finder에서 복사 하 고 대화 상자에 이러한 경로 붙여 넣습니다.

#### <a name="a-idmac-logs-visual-studio-namemac-logs-visual-studio-visual-studio-for-mac"></a><a id="mac-logs-visual-studio" name="mac-logs-visual-studio" />Mac용 Visual Studio

`~/Library/Logs/VisualStudio/7.0` (이 숫자는 사용 중인 버전에 따라 변경 될 수 있습니다.)

이 폴더를 열 수도 있습니다를 통해 "로그 디렉터리 열기-> Help"입니다.

#### <a name="a-idmac-logs-xamarin-studio-namemac-logs-xamarin-studio-xamarin-studio"></a><a id="mac-logs-xamarin-studio" name="mac-logs-xamarin-studio" />Xamarin Studio

`~/Library/Logs/XamarinStudio-6.0` (이 숫자는 사용 중인 버전에 따라 변경 될 수 있습니다.)

이 폴더를 열 수도 있습니다를 통해 "로그 디렉터리 열기-> Help"입니다.

#### <a name="a-idmac-universal-installer-namemac-universal-installer-xamarin-universal-installer"></a><a id="mac-universal-installer" name="mac-universal-installer" />Xamarin "범용" 설치 관리자

`~/Library/Logs/XamarinInstaller/Universal`

이러한 로그는에서 로그를 `XamarinInstaller.dmg` 설치 관리자입니다.

#### <a name="a-idmac-build-host-namemac-build-host-xamarin-build-host"></a><a id="mac-build-host" name="mac-build-host" />Xamarin 빌드 호스트

`~/Library/Logs/Xamarin-[MAJOR.MINOR]`

## <a name="a-idverbose-build-output-logs-nameverbose-build-output-logs-verbose-build-output"></a><a id="verbose-build-output-logs" name="verbose-build-output-logs" />자세한 빌드 출력

1.  사용 하도록 설정 [진단 MSBuild 출력](~/android/troubleshooting/troubleshooting.md#Diagnostic_MSBuild_Output)합니다.

2.  IOS 앱을 사용 하도록 설정할 수도 **verbose mtouch 출력** 더하여 `-v -v -v -v` 아래 **프로젝트 속성 > iOS 빌드 > 일반 (탭) > 추가 옵션 > 추가 mtouch 인수**합니다.

3.  정리 하 고 프로젝트를 다시 빌드하십시오.

4.  복사 하 여 텍스트 파일에 IDE에서 빌드 출력을 붙여넣습니다.
     - Visual Studio (Windows): **보기 > 출력 >에서 출력 보기: 빌드**
     - Visual Studio for Mac: **보기 > 패드 > 오류 > 빌드 출력 (탭)**

## <a name="a-iddebug-logs-for-xamarin-apps-namedebug-logs-for-xamarin-apps-debug-logs-for-xamarinandroid-and-xamarinios-apps"></a><a id="debug-logs-for-xamarin-apps" name="debug-logs-for-xamarin-apps" />Xamarin.iOS 및 Xamarin.Android 앱에 대 한 로그 디버그

### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**보기 > 패드 > 응용 프로그램 출력**

(Note: 앱 실행 된 후이 메뉴 항목만 표시 됩니다.)

### <a name="visual-studio"></a>Visual Studio

**보기 > 출력 >에서 출력 보기: 디버그**

### <a name="a-idadb-logcat-nameadb-logcat-android-adbhttpsdeveloperandroidcomtoolshelpadbhtml-logcat-logs"></a><a id="adb-logcat" name="adb-logcat" />Android [ `adb` ](https://developer.android.com/tools/help/adb.html) logcat 로그

실행 한 후 합니다 `adb` 명령에 다시 연결 합니다 **android_logcat.txt** 바탕 화면에서 파일입니다. 이러한 지침 연결 된 장치가 하나만 있다고 가정 합니다.

참고 항목의 [Android 디버그 로그](~/android/deploy-test/debugging/android-debug-log.md) 페이지입니다.

#### <a name="visual-studio"></a>Visual Studio

1. **도구 > Android > Android Adb 명령 프롬프트를 시작 합니다.**
2. 로그를 정리 합니다. `adb logcat -c`
3. 문제를 재현 합니다.
4. 로그를 출력 합니다. `adb logcat -vtime -d > "%USERPROFILE%\Desktop\android_logcat.txt"`

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

1. **도구 > Android SDK 명령 프롬프트 열기**
2. 로그를 정리 합니다. `adb logcat -c`
3. 문제를 재현 합니다.
4. 로그를 출력 합니다. `adb logcat -vtime -d > ~/Desktop/android_logcat.txt`

### <a name="a-idios-simulator-logs-nameios-simulator-logs-ios-simulator-logs-on-mac"></a><a id="ios-simulator-logs" name="ios-simulator-logs" />iOS 시뮬레이터 로그온 (Mac)

* 시스템 로그에 액세스 하려면 **디버그 > 시스템 로그 열기...**  iOS 시뮬레이터 앱에서.

* 시뮬레이터에서 크래시 보고서를 보려면 Console.app 열고 이동할 `~/Library/Logs > DiagnosticReports`합니다.

### <a name="a-idios-device-logs-nameios-device-logs-ios-device-logs-on-mac"></a><a id="ios-device-logs" name="ios-device-logs" />iOS 장치 로그온 (Mac)

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**보기 > 패드 > iOS 장치 로그**

#### <a name="xcode"></a>Xcode

**창 > 장치 > ${DeviceName}**

충돌 보고서에서 사용할 수는 **장치 로그 보기** 단추입니다. 장치에 대 한 시스템 로그의 공개 화살표 창의 맨 아래에 나타납니다.

#### <a name="xcode-5"></a>Xcode 5

**창 > 도우미 > 장치 (탭) > ${DeviceName}**

---
title: 버전 정보 및 로그는 어디에서 확인할 수 있나요?
description: 이 문서에서는 Xamarin 버전 정보 및 로그를 찾는 위치를 설명 합니다. 이 정보는 문제를 진단 하거나, 버그를 제출 하거나, 지원을 받을 때 유용 합니다.
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: CF386485-EAB0-4B9E-AA17-CB1B6462E505
author: davidortinau
ms.author: daortin
ms.date: 03/29/2017
ms.openlocfilehash: 997c6398c4cd9c4f4be6fbcd60847d82b0cae13d
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91457837"
---
# <a name="where-can-i-find-my-version-information-and-logs"></a>버전 정보 및 로그는 어디에서 확인할 수 있나요?

## <a name="outline"></a>윤곽선

- [버전 정보](#version-information)
  - Windows 버전 정보
  - Mac 버전 정보
  - Android SDK Tools, 플랫폼 도구, 빌드-도구
- [IDE 및 설치 관리자 로그](#ide-and-installer-logs)
  - [Windows 로그](#windows-logs)
    - Xamarin Studio
    - Visual Studio용 Xamarin
    - Xamarin Universal 설치 관리자
    - 개별 `.msi` 설치 관리자, 자세한 정보 로그
    - Visual Studio 시작, 자세한 정보 로그
  - [Mac 로그](#mac-logs)
    - 빌드 호스트
  - Mac용 Visual Studio
    - Xamarin Studio
    - Xamarin 설치 관리자
- [자세한 정보 표시 빌드 출력](#verbose-build-output-logs)
- [Xamarin Android 및 Xamarin.ios 앱에 대 한 디버그 로그](#debug-logs-for-xamarin-apps)
  - Android `adb` logcat 로그
  - iOS 시뮬레이터 로그 (Mac)
  - iOS 장치 로그 (Mac의 경우)

## <a name="version-information"></a><a id="version-information" name="version-information" />버전 정보

일반적으로 **정보 복사** 단추에서 모든 정보를 다시 전송 하는 것이 가장 좋습니다. 그렇지 않으면 추가 정보를 요청 해야 하는 경우가 많습니다. 예를 들어, 운영 체제 버전, Xcode 버전, 설치 된 Android API 수준 및 .NET 버전은 문제 해결에 도움이 될 수 있습니다.

### <a name="windows-version-information"></a><a id="windows-version-information" name="windows-version-information" />Windows 버전 정보

#### <a name="xamarin-studio"></a>Xamarin Studio

**정보를 > 정보를 표시 하는 방법에 대 한 도움말 > > 복사 정보 [단추]**

#### <a name="visual-studio"></a>Visual Studio

**Microsoft Visual Studio > 정보 복사에 대 한 도움말 > [button]**

### <a name="mac-version-information"></a><a id="mac-version-information" name="mac-version-information" />Mac 버전 정보

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**Visual studio > Visual Studio > 정보 > 복사 정보 표시 [단추]**

### <a name="android-sdk-tools-platform-tools-build-tools"></a><a id="android-sdk-tools-versions" name="android-sdk-tools-versions" />Android SDK Tools, 플랫폼 도구, 빌드-도구

Android SDK 관리자를 열고 최상위 **도구** 섹션의 스크린샷을 찍습니다.

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**Android SDK Manager > 도구를 엽니다.**

#### <a name="visual-studio"></a>Visual Studio

**Android > 도구 > Android SDK 관리자 열기 ...**

## <a name="ide-and-installer-logs"></a><a id="ide-and-installer-logs" name="ide-and-installer-logs" />IDE 및 설치 관리자 로그

각 로그 위치에 대해 전체 로그 폴더를 압축 하 여 연결 해야 합니다.

### <a name="windows-logs"></a><a id="windows-logs" name="windows-logs" />Windows 로그

#### <a name="visual-studio-tools-for-xamarin"></a><a id="windows-logs-xamarin-vs" name="windows-logs-xamarin-vs" />Xamarin용 Visual Studio Tools

`%LOCALAPPDATA%\Xamarin\Logs`

#### <a name="visual-studio-2017"></a><a id="vs-2017" name="vs-2017" /> Visual Studio 2017

[Visual Studio 설치 로그를 가져오는 방법](/visualstudio/install/troubleshooting-installation-issues#how-to-get-the-visual-studio-installation-logs)

#### <a name="visual-studio-2015"></a><a id="vs-2015" name="vs-2015" /> Visual Studio 2015

#### <a name="xamarin-universal-installer"></a><a id="windows-universal-installer" name="windows-universal-installer" /> Xamarin "범용" 설치 관리자

`%LOCALAPPDATA%\Xamarin\Universal`

이러한 로그는 `XamarinInstaller.exe` 설치 관리자의 로그입니다.

#### <a name="individual-msi-installers-verbose-logs"></a><a id="individual-msi-installers-verbose-logs" name="individual-msi-installers-verbose-logs" />개별 `.msi` 설치 관리자, 자세한 정보 로그

```csharp
msiexec /i Xamarin.msi /l*vx "%USERPROFILE%\Desktop\Xamarin.log"
```

참조: [명령줄 옵션](/windows/win32/msi/command-line-options)

#### <a name="visual-studio-startup-verbose-logs"></a><a id="visual-studio-startup-verbose-logs" name="visual-studio-startup-verbose-logs" />Visual Studio 시작, 자세한 정보 로그

```csharp
devenv.exe /log "%USERPROFILE%\Desktop\VisualStudio.log"
```

참조: [/log (devenv.exe)](/visualstudio/ide/reference/log-devenv-exe)

### <a name="mac-logs"></a><a id="mac-logs" name="mac-logs" />Mac 로그

Finder에서 **이동 > 폴더로 이동** 메뉴 항목을 선택 하 고이 경로를 복사 하 여 대화 상자에 붙여 넣을 수 있습니다.

#### <a name="visual-studio-for-mac"></a><a id="mac-logs-visual-studio" name="mac-logs-visual-studio" />Mac용 Visual Studio

`~/Library/Logs/VisualStudio/7.0` 이 번호는 사용 중인 버전에 따라 달라질 수 있습니다.

이 폴더는 "도움말-> 로그 디렉터리 열기"를 통해 열 수도 있습니다.

#### <a name="xamarin-studio"></a><a id="mac-logs-xamarin-studio" name="mac-logs-xamarin-studio" />Xamarin Studio

`~/Library/Logs/XamarinStudio-6.0` 이 번호는 사용 중인 버전에 따라 달라질 수 있습니다.

이 폴더는 "도움말-> 로그 디렉터리 열기"를 통해 열 수도 있습니다.

#### <a name="xamarin-universal-installer"></a><a id="mac-universal-installer" name="mac-universal-installer" />Xamarin "범용" 설치 관리자

`~/Library/Logs/XamarinInstaller/Universal`

이러한 로그는 `XamarinInstaller.dmg` 설치 관리자의 로그입니다.

#### <a name="xamarin-build-host"></a><a id="mac-build-host" name="mac-build-host" />Xamarin 빌드 호스트

`~/Library/Logs/Xamarin-[MAJOR.MINOR]`

## <a name="verbose-build-output"></a><a id="verbose-build-output-logs" name="verbose-build-output-logs" />자세한 정보 표시 빌드 출력

1. [진단 MSBuild 출력](~/android/troubleshooting/troubleshooting.md#Diagnostic_MSBuild_Output)을 사용 하도록 설정 합니다.

2. IOS 앱의 경우, 추가 **verbose mtouch output** `-v -v -v -v` **Mtouch 인수 > 추가 옵션 > ios 빌드 > 일반 (탭) > 프로젝트 속성**에를 추가 하 여 자세한 정보 표시 mtouch 출력을 사용 하도록 설정 합니다.

3. 프로젝트를 정리 하 고 다시 빌드합니다.

4. IDE의 빌드 출력을 복사 하 여 텍스트 파일에 붙여 넣습니다.
     - Visual Studio (Windows): 출력 **> 표시 > 출력: 빌드**
     - Mac용 Visual Studio: **빌드 출력 > > 패드 > 오류 보기 (탭)**

## <a name="debug-logs-for-xamarinandroid-and-xamarinios-apps"></a><a id="debug-logs-for-xamarin-apps" name="debug-logs-for-xamarin-apps" />Xamarin Android 및 Xamarin.ios 앱에 대 한 디버그 로그

### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**응용 프로그램 출력 > > 패드 보기**

이 메뉴 항목은 앱이 시작 된 후에만 표시 됩니다.

### <a name="visual-studio"></a>Visual Studio

**출력 > 표시 > 디버그: 디버그**

### <a name="android-adb-logcat-logs"></a><a id="adb-logcat" name="adb-logcat" />Android [`adb`](https://developer.android.com/tools/help/adb.html) logcat 로그

명령을 실행 한 후 `adb` 바탕 화면에서 **android_logcat.txt** 파일을 다시 연결 합니다. 이 지침에서는 장치가 하나만 연결 되어 있다고 가정 합니다.

[Android 디버그 로그](~/android/deploy-test/debugging/android-debug-log.md) 페이지도 참조 하세요.

#### <a name="visual-studio"></a>Visual Studio

1. **Android > 도구 > Android Adb 명령 프롬프트 시작**
2. 로그를 정리 합니다. `adb logcat -c`
3. 문제를 재현합니다.
4. 로그를 출력 합니다. `adb logcat -vtime -d > "%USERPROFILE%\Desktop\android_logcat.txt"`

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

1. **도구 > Android SDK 명령 프롬프트 열기**
2. 로그를 정리 합니다. `adb logcat -c`
3. 문제를 재현합니다.
4. 로그를 출력 합니다. `adb logcat -vtime -d > ~/Desktop/android_logcat.txt`

### <a name="ios-simulator-logs-on-mac"></a><a id="ios-simulator-logs" name="ios-simulator-logs" />iOS 시뮬레이터 로그 (Mac)

- 시스템 로그에 액세스 하려면 iOS 시뮬레이터 앱에서 **디버그 > 시스템 로그 열기** ...를 선택 합니다.

- 시뮬레이터에서 충돌 보고서를 보려면 Console. 앱을 열고로 이동 `~/Library/Logs > DiagnosticReports` 합니다.

### <a name="ios-device-logs-on-mac"></a><a id="ios-device-logs" name="ios-device-logs" />iOS 장치 로그 (Mac의 경우)

#### <a name="visual-studio-for-mac"></a>Mac용 Visual Studio

**IOS 장치 로그 > > 패드 보기**

#### <a name="xcode"></a>Xcode

**Windows > 장치 > $ {장치 이름}**

충돌 보고서는 **장치 로그 보기** 단추 아래에서 사용할 수 있습니다. 장치의 시스템 로그는 창 아래쪽에 있는 노출 화살표 아래에 나타납니다.

#### <a name="xcode-5"></a>Xcode 5

**창 > 구성 도우미 > 장치 (탭) > $ {장치 이름}**
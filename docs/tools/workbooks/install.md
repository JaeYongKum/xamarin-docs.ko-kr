---
title: 통합 문서 설치 및 요구 사항
description: 이 문서에서는 Xamarin Workbooks를 다운로드 하 고 설치 하는 방법, 지원 되는 플랫폼 및 시스템 요구 사항에 대해 설명 합니다.
ms.prod: xamarin
ms.assetid: 9D4E10E8-A288-4C6C-9475-02969198C119
author: davidortinau
ms.author: daortin
ms.date: 06/19/2018
ms.openlocfilehash: 99ecf661679f02bda6cfffa6093bd4a904676bce
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86939349"
---
# <a name="workbooks-installation-and-requirements"></a>통합 문서 설치 및 요구 사항

<a name="install"></a>

## <a name="download-and-install"></a>다운로드 및 설치

<!-- markdownlint-disable MD001 -->

# <a name="windows"></a>[Windows](#tab/windows)

1. 아래 [요구 사항을](#requirements) 확인 하세요.
2. [Windows 용 Xamarin Workbooks](https://dl.xamarin.com/interactive/XamarinInteractive.msi)를 다운로드 하 고 설치 합니다.
3. 통합 문서를 [재생](~/tools/workbooks/workbook.md) 하기 시작 합니다.

# <a name="macos"></a>[macOS](#tab/macos)

1. 아래 [요구 사항을](#requirements) 확인 하세요.
2. [Mac 용 Xamarin Workbooks](https://dl.xamarin.com/interactive/XamarinInteractive.pkg)를 다운로드 하 고 설치 합니다.
3. [재생](~/tools/workbooks/workbook.md)을 시작 합니다.

-----

## <a name="requirements"></a>요구 사항

#### <a name="supported-operating-systems"></a>지원되는 운영 체제

- **Mac** -OS X 10.11 이상
- **Windows** -windows 7 이상 (Internet Explorer 11 이상 및 .net 4.6.1 이상)

#### <a name="supported-app-platforms"></a>지원 되는 앱 플랫폼

|앱 플랫폼|OS 지원|참고|
|--- |--- |--- |
|Mac|Mac 에서만 지원 됨|
|iOS|Mac 및 Windows에서 지원 됨|Xamarin.ios 11.0 및 Xcode 9.0 이상이 Mac에 설치 되어 있어야 합니다. Windows에서 iOS 통합 문서를 실행 하려면 위의 모든를 실행 하는 Mac 빌드 호스트와 Windows에 [원격 Ios 시뮬레이터](~/tools/ios-simulator/index.md) 가 설치 되어 있어야 합니다.|
|Android|Mac 및 Windows에서 지원 됨|가상 장치 >= 5.0를 사용 하 여 Google, Visual Studio 또는 Xamarin Android emulator를 사용 해야 합니다.|
|WPF|Windows 에서만 지원 됨|
|콘솔 (.NET Framework)|Mac 및 Windows에서 지원 됨|
|콘솔 (.NET Core)|Mac 및 Windows에서 지원 됨|

## <a name="reporting-bugs"></a>버그 보고

[GitHub에서 문제를 보고][bugs]하 고 다음 정보를 모두 포함 하세요.

### <a name="log-files"></a>로그 파일

항상 통합 문서 클라이언트 로그 파일 첨부:

- Mac: `~/Library/Logs/Xamarin/Workbooks/Xamarin Workbooks {date}.log`
- Windows: `%LOCALAPPDATA%\Xamarin\Workbooks\logs\Xamarin Workbooks {date}.log`

1.4. x에는 주 메뉴에서 직접 Finder (macOS) 또는 탐색기 (Windows)의 로그 파일을 선택 하는 기능도 있습니다.

- **로그 파일을 표시 > 도움말**

#### <a name="log-paths-for-workbooks-13-and-earlier"></a>통합 문서 1.3 및 이전 버전에 대 한 로그 경로:

- Mac: `~/Library/Logs/Xamarin/Inspector/Xamarin Inspector {date}.log`
- Windows: `%LOCALAPPDATA%\Xamarin\Inspector\logs\Xamarin Inspector {date}.log`

### <a name="platform-version-information"></a>플랫폼 버전 정보

운영 체제 및 설치 된 Xamarin 제품에 대 한 세부 정보를 파악 하는 것이 매우 유용 합니다.

통합 문서의 주 메뉴에서 다음을 수행 합니다.

- **버전 정보를 복사 > 도움말**

#### <a name="instructions-for-workbooks-13-and-earlier"></a>통합 문서 1.3 및 이전 버전에 대 한 지침:

Mac 용 Visual Studio

- **Visual studio > > 정보를 > 복사 정보를 표시 합니다.**
- 버그 보고서에 붙여넣기

Visual Studio

- **Visual Studio > 정보 복사에 대 한 도움말 >**
- 운영 체제 버전 및 32 비트 또는 64 비트 Windows를 실행 하 고 있는지 여부를 알려주세요.

### <a name="samples"></a>샘플

문제가 있는 **통합 문서** 파일에 연결 하거나 연결할 수 있는 경우 버그를 보다 신속 하 게 해결 하는 데 도움이 될 수 있습니다.

### <a name="devices"></a>디바이스

IOS 또는 Android 통합 문서를 연결 하는 데 문제가 있고 [문제 해결 페이지](~/tools/workbooks/troubleshooting/index.md)를 이미 확인 한 경우 다음 사항을 알고 있어야 합니다.

- 연결 하려는 장치의 이름
- 장치의 OS 버전
- Android: x86 에뮬레이터를 사용 하 고 있는지 확인
- Android: 어떤 에뮬레이터 플랫폼을 사용 하 고 있나요? Google Emulator?
  Visual Studio Android Emulator? Xamarin Android Player?
- Windows의 iOS: 설치 된 Xamarin 원격 iOS 시뮬레이터의 버전 ( **제어판**의 **프로그램 추가/제거** 확인)
- Windows의 iOS: Mac 빌드 호스트에 대 한 플랫폼 버전 정보를 제공 하세요.
- 장치가 네트워크에 연결 되어 있나요 (웹 브라우저를 통해 확인)?

[bugs]: https://github.com/Microsoft/workbooks/issues/new

## <a name="uninstall"></a>제거

### <a name="windows"></a>Windows

통합 문서를 구입한 방법에 따라 두 가지 제거 절차를 수행 해야 할 수 있습니다. 소프트웨어를 완전히 제거 하려면이 두 가지를 모두 확인 하세요.

#### <a name="visual-studio-installer"></a>Visual Studio 설치 관리자

Visual Studio 2017가 있는 경우 **Visual Studio 설치 관리자**를 열고 **Xamarin Workbooks**의 **개별 구성 요소** 를 확인 합니다. 확인란이 선택 되어 있으면 선택을 취소 한 다음 **수정** 을 클릭 하 여 제거 합니다.

#### <a name="system-uninstall"></a>시스템 제거

다운로드 한 설치 관리자를 사용 하 여 통합 문서를 설치한 경우 Windows 10의 **앱 & 기능** 시스템 설정 페이지 또는 이전 버전의 Windows에서 제어판의 **프로그램 추가/제거** 를 통해 제거 해야 합니다.

> **시스템 > 앱 & 기능 > > 설정 시작**

![&quot;앱 기능에 나열 된 &amp; Xamarin Workbooks&quot;](install-images/windows-remove.png)

**Visual Studio 설치 관리자에 대 한 절차를 계속 수행 하 여 사용자 모르게 통합 문서를 다시 설치 하지 않도록 해야 합니다.**

<a name="uninstall-macos"></a>

### <a name="macos"></a>macOS

[1.2.2](https://github.com/xamarin/release-notes-archive/blob/master/release-notes/interactive/interactive-1.2.md)부터를 실행 하 여 터미널에서 Xamarin Workbooks 제거할 수 있습니다.

```bash
sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
```

제거 하는 파일 및 디렉터리에 대 한 세부 정보를 표시 하 고 계속 하기 전에 확인 합니다.

`-help` `uninstall` 더 많은 고급 시나리오를 위해 스크립트에 인수를 전달 합니다.

이전 버전의 경우 다음 항목을 수동으로 제거해야 합니다.

1. `"/Applications/Xamarin Workbooks.app"`에서 Workbooks 앱 삭제
2. `"Applications/Xamarin Inspector.app"`에서 Inspector 앱 삭제
3. `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Interactive"` 및 `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Inspector"` 추가 기능 삭제
4. `/Library/Frameworks/Xamarin.Interactive.framework` 및 `/Library/Frameworks/Xamarin.Inspector.framework`에서 Inspector 및 지원 파일 삭제

## <a name="downgrading"></a>다운

**/Applications/Xamarin 통합 문서** 에 대 한 번들 식별자는 `com.xamarin.Inspector` `com.xamarin.Workbooks` 통합 문서와 검사기가 모두 완전히 분할 되므로 1.4 릴리스의에서로 변경 되었습니다.

이전 설치 관리자의 버그로 인해 1.3.2 또는 이전 설치 관리자를 사용 하 여 1.4 이상의 릴리스를 다운 그레이드할 수 없습니다.

1.4 이상에서 1.3.2 또는 이전 버전으로 다운 그레이드 하려면:

1. [통합 문서 & 검사기를 수동으로 제거](#uninstall-macos)
2. 1.3.2 또는 이전 `.pkg` 설치 관리자 실행

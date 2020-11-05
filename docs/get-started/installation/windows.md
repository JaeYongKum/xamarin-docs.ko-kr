---
title: Visual Studio 2019에 Xamarin 설치
description: 이 문서에서는 Visual Studio 2019에 Xamarin을 설치하는 방법을 설명합니다. 요구 사항, 설치 프로세스 및 설치 확인을 설명합니다.
ms.prod: xamarin
ms.assetid: E20D4463-368E-4B60-A059-F50DB8C5552D
author: conceptdev
ms.author: crdun
ms.date: 08/28/2018
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 255c870407f1657196abd826b46c7e9b114285c9
ms.sourcegitcommit: d1980b2251999224e71c1289e4b4097595b7e261
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2020
ms.locfileid: "91433323"
---
# <a name="installing-xamarin-in-visual-studio-2019"></a>Visual Studio 2019에 Xamarin 설치

<a name="requirements"></a>

시작하기 전에 [시스템 요구 사항](~/cross-platform/get-started/requirements.md)을 확인합니다.

## <a name="installation"></a>설치

[!include[](~/cross-platform/includes/install-xamarin-windows-2019.md)]

Visual Studio 2019에서 **도움말** 메뉴를 클릭하여 Xamarin이 설치되어 있는지 확인합니다. Xamarin이 설치된 경우 이 스크린샷에 표시된 것처럼 **Xamarin** 메뉴 항목이 표시됩니다.

![도움말 메뉴의 Xamarin 메뉴 항목](windows-images/12-xamarin-menu-item.png "도움말 메뉴의 Xamarin 메뉴 항목")

**도움말 > Microsoft Visual Studio 정보** 를 클릭하고 설치된 제품 목록을 스크롤하여 Xamarin이 설치되었는지 확인할 수도 있습니다.

![Visual Studio 2019의 설치 제품 화면](windows-images/13-xamarin-is-installed.png "Visual Studio 2019의 설치 제품 화면")

버전 정보를 찾는 방법에 대한 자세한 내용은 [내 버전 정보와 로그를 어디에서 찾을 수 있습니까?](~/cross-platform/troubleshooting/questions/version-logs.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Visual Studio 2019에 Xamarin을 설치하면 앱에 대한 코드 작성을 시작할 수 있지만, 시뮬레이터, 에뮬레이터 및 디바이스에 앱을 빌드하고 배포하기 위한 추가 설정은 필요하지 않습니다. 다음 가이드를 참조하여 설치를 완료하고 플랫폼 간 앱 빌드를 시작하세요.

### <a name="ios"></a>iOS

자세한 내용은 [Windows에 Xamarin.iOS 설치](~/ios/get-started/installation/windows/index.md) 가이드를 참조하세요.

1. [Mac용 Visual Studio 설치](/visualstudio/mac/installation)
2. [Mac 빌드 호스트에 Visual Studio 연결](~/ios/get-started/installation/windows/connecting-to-mac/index.md)
3. [iOS 개발자 설정](~/ios/get-started/installation/device-provisioning/index.md) - 디바이스에서 애플리케이션을 실행하는 데 필요합니다.
4. [원격 iOS 시뮬레이터](~/tools/ios-simulator/index.md)
5. [Visual Studio용 Xamarin.iOS 소개](~/ios/get-started/installation/windows/introduction-to-xamarin-ios-for-visual-studio.md)

### <a name="android"></a>Android

자세한 내용은 [Windows에 Xamarin.Android 설치](~/android/get-started/installation/windows.md) 가이드를 참조하세요.

1. [Xamarin.Android Configuration](~/android/get-started/installation/windows.md#configuration)
2. [Xamarin Android SDK Manager 사용](~/android/get-started/installation/android-sdk.md?ide=vs)
3. [Android SDK 에뮬레이터](~/android/get-started/installation/android-emulator/index.md)
4. [개발용 디바이스 설정](~/android/get-started/installation/set-up-device-for-development.md)
---
title: 이전 버전의 Xcode 또는 Xamarin.ios를 사용할 수 있나요?
description: 이 가이드에서는 이전 버전의 Xamarin.ios 또는 Xcode 사용과 관련 된 문제를 간략히 설명 합니다 (현재 안정적인 릴리스).
ms.prod: xamarin
ms.assetid: 27CF7EB7-9251-435F-BEA5-F20F8DD7DC17
ms.technology: xamarin-ios
author: chamons
ms.author: chhamo
ms.date: 04/16/2019
ms.openlocfilehash: 6c6a0491f7989f2f76afabc3412e38be74a06da4
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91431577"
---
# <a name="can-i-use-an-older-version-of-xcode-or-xamarinios"></a>이전 버전의 Xcode 또는 Xamarin.ios를 사용할 수 있나요?

Xamarin 설명서에서는 권장 되는 최신 Xamarin.ios 및 Xcode를 사용 하는 것으로 가정 합니다. 그러나 일부 고객은 이전 Xamarin.ios 및/또는 Xcode를 사용 하 고 결과에 대 한 세부 정보를 선호 합니다.

릴리스 정보에는 다음과 같은 경고가 포함 되어 있습니다.

> [!WARNING]
> **이전 Xcode 버전 사용**
>
> 위의 [요구 사항](/xamarin/ios/release-notes/12/12.8#requirements)에서 언급 한 것 보다 오래 된 Xcode 버전을 사용 하는 것이 가능 하지만 일부 기능은 사용 하지 못할 수 있습니다. 또한 다음과 같은 몇 가지 제한 사항을 해결 해야 할 수도 있습니다.
>
> - 정적 등록자는 응용 프로그램을 빌드하기 위한 Xcode 헤더 파일이 필요 하며 [`MT0091`](../mtouch-errors.md#MT0091) [`MT4109`](../mtouch-errors.md#MT4109) api가 없는 경우 오류가 발생 합니다. 대부분의 경우 관리 되는 링커를 사용 하도록 설정 하면 API를 제거 하 여 도움이 됩니다.
> - Xcode 9.0 + 도구 체인를 사용 하지 않는 경우 tvOS 및 watchOS에 대 한 bitcode 빌드는 앱 스토어에 전송 되지 않을 수 있습니다.

## <a name="further-information"></a>추가 정보

응용 프로그램을 개발 하 고 제출할 때 최신 Xcode 및 최신 Xamarin.ios 릴리스를 사용 하는 것이 좋습니다. Apple에서는 응용 프로그램을 제출할 때 최신 Xcode를 사용 해야 합니다.

최신 Xcode를 사용 해도 응용 프로그램이 이전 iOS 버전을 대상으로 하는 것을 방지할 수는 없습니다. 지원 되는 iOS 버전은 **info.plist** 항목 및 응용 프로그램에서 사용 하는 api에 따라 달라 집니다.

**Xcode101** 및 **Xcode102**와 같은 다른 이름을 사용 하 여 여러 버전의 Xcode를 나란히 설치할 수 있습니다. 여러 버전을 사용 하는 경우 [Mac용 Visual Studio 설정](~/ios/troubleshooting/questions/ios-sdk.md) 및 명령줄 도구를 사용 하 여 활성 Xcode를 설정 해야 [`xcode-select`](https://developer.apple.com/library/archive/technotes/tn2339/_index.html#//apple_ref/doc/uid/DTS40014588-CH1-HOW_DO_I_SELECT_THE_DEFAULT_VERSION_OF_XCODE_TO_USE_FOR_MY_COMMAND_LINE_TOOLS_) [command line tool](https://developer.apple.com/library/archive/technotes/tn2339/_index.html#//apple_ref/doc/uid/DTS40014588-CH1-HOW_DO_I_SELECT_THE_DEFAULT_VERSION_OF_XCODE_TO_USE_FOR_MY_COMMAND_LINE_TOOLS_)합니다.

그러나 드문 경우 이지만 이전 구성 요소를 사용 해야 할 수도 있습니다. 이 설명서에서는 최신 버전 보다 오래 된 버전을 사용할 때 직면 하는 일반적인 문제에 대해 설명 합니다.

Apple의 각 릴리스는 고유 하지만 여기에 문서화 되지 않은 다른 문제를 겪을 수 있습니다.

이러한 문제는 종종 해결할 필요가 없는 경우가 있으므로 가능한 경우 최신 Xcode 및 최신 Xamarin.ios의 지원 되는 구성이 될 수 있습니다.

## <a name="use-of-an-old-xamarinios-with-an-old-xcode"></a>이전 Xcode를 사용 하 여 이전 Xamarin.ios 사용

Xamarin.ios 및 Xcode는 최소한 일정 시간 동안 업데이트할 수 없습니다. 이 제한은 특정 시점에 응용 프로그램을 제출 하기 위해 Apple에서 최소 버전의 Xcode가 필요 하다는 것입니다. 이 시점에서 모든 구성 요소 (macOS, Xcode 및 Xamarin.ios)를 최신 버전 (또는 Apple에서 요구 하는 Xcode의 최소 버전 및 일치 하는 Xamarin.ios 릴리스)으로 업데이트 해야 합니다.

일반적으로 점진적으로 업데이트 하 고 작은 변경 내용을 유지 하는 것이 더 쉽습니다. 업데이트가 더 어려울 수 있는 규모가 많은 프로젝트의 경우 알려진 작업 집합을 유지 하는 것이 좋을 수 있습니다.

## <a name="use-of-new-xamarinios-with-older-xcode"></a>이전 Xcode를 사용 하는 새 Xamarin.ios 사용

일반적으로 xamarin.ios는 가능한 경우 이전 Xcode 릴리스를 지원 합니다. 몇 가지 잠재적인 문제는 다음과 같습니다.

- 최신 Xamarin.ios는 선택한 Xcode에 없는 일부 기능과 Api를 지원할 수 있습니다. 
- **정적 등록자** 는 응용 프로그램을 빌드하기 위한 Xcode 헤더 파일이 필요 하며 [`MT0091`](~/ios/troubleshooting/mtouch-errors.md#MT0091) [`MT4109`](~/ios/troubleshooting/mtouch-errors.md#MT4109) api가 없는 경우 오류가 발생 합니다.
  - 대부분의 경우 관리 되는 링커를 사용 하도록 설정 하는 것은 사용 되지 않는 경우 새 API에 대 한 관리 되는 바인딩을 제거 하 여 도움이 됩니다.
- Xcode 9.0 + 도구 체인를 사용 하지 않는 경우 tvOS 및 watchOS에 대 한 bitcode 빌드는 앱 스토어에 전송 되지 않을 수 있습니다.

## <a name="use-of-new-xcode-with-older-xamarinios"></a>이전 Xamarin.ios와 함께 새 Xcode 사용

이 사용 사례는 Xamarin에서 새로운 Xcode의 변화 하는 요구 사항을 예측할 수 없기 때문에 훨씬 더 어렵습니다. MacOS의 업데이트는 문제를 발생 시킬 수 있으며 호환성 패치를 사용 하지 않으면 Xamarin.ios의 많은 부분이 영향을 받을 수 있습니다. 

다음을 비롯 한 여러 가지 잠재적 영역이 있을 수 있습니다.

- 비호환 `mlaunch` :
  - 시뮬레이터 지원이 제대로 작동 하지 않을 수 있습니다 (또는 모두).
  - 장치 지원이 제대로 작동 하지 않을 수 있습니다.
- 에 대 한 알 수 없는 지원 `mtouch` 
  - 새 프레임 워크에 대 한 지원 없음
  - 새 자격에 대 한 지원 없음
  - 신규 또는 업데이트 된 도구에 대 한 지원 없음
    - 코드 서명에도 영향을 줄 수 있습니다.

### <a name="new-appstore-submission-rules"></a>새 AppStore 전송 규칙

Apple은 언제 든 지 AppStore 전송 규칙을 업데이트할 수 있는 권리를 보유 합니다. 이러한 규칙 변경은 종종 미리 발표 됩니다. 이러한 변경 내용 중 일부를 지원 하려면 업데이트 된 Xamarin.ios 구성 요소가 필요한 도구를 변경 해야 합니다.

Apple에서는 규칙 변경 외에도 제출 된 앱에 유효성 검사를 추가 하거나 기존 앱을 tightens 하는 경우가 많습니다. 이러한 도구 중 일부는 도구 (예: 새 블랙 리스트에 기호)를 변경 해야 합니다. 이러한 이러한 대부분은 규칙의 알림 (또는 목록)이 없기 때문에 제출 하는 고객이 가장 먼저 발생 합니다.

## <a name="summary"></a>요약

가능 하면 Apple의 지침을 수행 하 고 앱 스토어에 출시 된 최신 Xcode를 사용 하 여 개발 및 제출 하 여 안전 하 게 재생 하세요.

그리고 마지막으로 릴리스된 Xamarin.ios를 사용 합니다. 이렇게 하면 제출 된 응용 프로그램에 영향을 줄 수 있는 최신 수정 사항을 추적 하 고 최신 규칙 변경 내용을 준수할 수 있습니다.

적절 하지 않은 경우 일치 하는 이전 Xcode 및 Xamarin.ios 릴리스를 사용 하는 것이 좋습니다. 이는 한 번에 작동할 수 있지만 특정 시점에서 Apple은 최신 도구를 사용 하 여 적절 하 게 계획 합니다.
---
title: Xamarin.ios-macOS Sierra 문제 해결
description: 이 문서에서는 Xamarin.ios 앱의 macOS Sierra 작업에 대 한 몇 가지 문제 해결 팁을 제공 합니다. 팁은 Mac 앱 스토어, Apple Pay, 이진 호환성, CFNetwork, CloudKit 등과 관련이 있습니다.
ms.prod: xamarin
ms.assetid: 323DD5EE-87CE-48E4-B234-1CF61B45A019
ms.technology: xamarin-mac
author: davidortinau
ms.author: daortin
ms.date: 09/22/2016
ms.openlocfilehash: d3ec300cbda5d22a285c3f63d3281bde29b94024
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91430052"
---
# <a name="xamarinmac---macos-sierra-troubleshooting"></a>Xamarin.ios-macOS Sierra 문제 해결

_이 문서에서는 Xamarin.ios 앱의 macOS Sierra을 사용 하기 위한 몇 가지 문제 해결 팁을 제공 합니다._

다음 섹션에는 Xamarin.ios 및 해당 문제에 대 한 해결 방법으로 macOS Sierra를 사용 하는 경우 발생할 수 있는 몇 가지 알려진 문제가 나와 있습니다.

- [App Store](#App-Store)
- [Apple Pay](#Apple-Pay)
- [이진 호환성](#Binary-Compatibility)
- [CFNetwork HTTP 프로토콜](#CFNetwork-HTTP-Protocol)
- [CloudKit](#CloudKit)
- [핵심 이미지](#CoreImage)
- [알림](#Notifications)
- [NSUserActivity](#NSUserActivity)
- [Safari](#Safari)

<a name="App-Store"></a>

## <a name="app-store"></a>App Store

알려진 문제:

- 샌드박스 환경에서 앱에서 바로 구매를 테스트할 때 인증 대화 상자가 두 번 표시 될 수 있습니다.
- 샌드박스 환경에서 호스팅된 콘텐츠를 사용 하 여 앱 내 구매를 테스트할 때 콘텐츠 다운로드가 완료 될 때까지 앱이 포그라운드로 전환 될 때마다 암호 대화 상자가 표시 됩니다.

<a name="Apple-Pay"></a>

## <a name="apple-pay"></a>Apple Pay

Apple Pay에 새 지불 카드를 추가할 때 잘못 된 만료 날짜 또는 CW (보안 코드)를 입력 하는 경우 카드 프로 비전 프로세스가 종료 됩니다.

<a name="Binary-Compatibility"></a>

## <a name="binary-compatibility"></a>이진 호환성

알려진 문제:

- 를 호출 `NSObject.ValueForKey` 하면 `null` 키가 예외를 발생 합니다.
- `NSURLSession`및 모두 `NSURLConnection` url에 대 한 TLS 핸드셰이크 중에 더 이상 RC4 암호 그룹을 사용할 필요가 없습니다 `http://` .
- 또는 메서드에서 슈퍼 뷰의 기 하 도형을 수정 하면 앱이 중단 될 수 `ViewWillLayoutSubviews` 있습니다 `LayoutSubviews` .
- 모든 SSL/TLS 연결의 경우 이제 RC4 대칭 암호화가 기본적으로 사용 하지 않도록 설정 됩니다. 또한 보안 전송 API는 더 이상 SSLv3을 지원 하지 않으며, 가능한 한 빨리 SHA-1 및 3DES 암호화를 사용 하 여 앱을 중지 하는 것이 좋습니다.

<a name="CFNetwork-HTTP-Protocol"></a>

## <a name="cfnetwork-http-protocol"></a>CFNetwork HTTP 프로토콜

`HTTPBodyStream` `NSMutableURLRequest` 이후에는 `NSURLConnection` `NSURLSession` 이 요구 사항을 엄격 하 게 적용 하기 때문에 클래스의 속성을 아직 열지 않은 스트림으로 설정 해야 합니다.

<a name="CloudKit"></a>

## <a name="cloudkit"></a>CloudKit

장기 실행 작업은 _"파일을 저장할 수 있는 권한이 없습니다."를 반환 합니다._ error.

<a name="CoreImage"></a>

## <a name="core-image"></a>핵심 이미지

`CIImageProcessor`이제 API는 임의의 입력 이미지 수를 지원 합니다. `CIImageProcessor` MacOS Sierra beta 1에 포함 된 API가 제거 됩니다.

<a name="Notifications"></a>

## <a name="notifications"></a>알림

알림 콘텐츠 확장을 사용 하는 경우 보기 컨트롤러가 올바르게 해제 되지 않으므로 확장 메모리 제한에 도달 하면 충돌이 발생할 수 있습니다.

<a name="NSUserActivity"></a>

## <a name="nsuseractivity"></a>NSUserActivity

전달 작업 후에는 `UserInfo` 개체의 속성이 비어 있을 수 `NSUserActivity` 있습니다. `BecomeCurrent` `NSUserActivity` 현재 해결 방법으로 개체를 명시적으로 호출 합니다.

<a name="Safari"></a>

## <a name="safari"></a>Safari

WebGeolocation 위치에는 `https://` 악의적인 위치 데이터 사용을 방지 하기 위해 iOS 10과 macOS Sierra 모두에서 작동 하는 보안 () URL이 필요 합니다.

## <a name="related-links"></a>관련 링크

- [Mac 샘플](/samples/browse/?products=xamarin&term=Xamarin.Mac)
- [MacOS 10.12의 새로운 기능](https://developer.apple.com/library/prerelease/content/releasenotes/MacOSX/WhatsNewInOSX/Articles/OSXv10.html#//apple_ref/doc/uid/TP40017145-SW1)
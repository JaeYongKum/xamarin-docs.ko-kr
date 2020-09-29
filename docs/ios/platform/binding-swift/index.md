---
title: IOS Swift 라이브러리 바인딩
description: '이 문서에서는 Swift 코드에 c # 바인딩을 만들어 Xamarin.ios 응용 프로그램에서 네이티브 라이브러리 및 CocoaPods를 사용할 수 있도록 하는 방법을 설명 합니다.'
ms.prod: xamarin
ms.assetid: 890EFCCA-A2A2-4561-88EA-30DE3041F61D
ms.technology: xamarin-ios
author: alexeystrakh
ms.author: alstrakh
ms.date: 02/11/2020
ms.openlocfilehash: f678ec02ca5b9b47f6f78eea77547b038274190f
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91435515"
---
# <a name="bind-ios-swift-libraries"></a>IOS Swift 라이브러리 바인딩

> [!IMPORTANT]
> 현재 Xamarin 플랫폼에서 사용자 지정 바인딩 사용을 조사하고 있습니다. [**설문 조사**](https://www.surveymonkey.com/r/KKBHNLT)에 참여하여 향후 개발 작업에 대해 알려 주시기 바랍니다.

IOS 플랫폼은 해당 네이티브 언어 및 도구와 함께 지속적으로 진화 하 고 있으며 최신 제품을 사용 하 여 개발 된 많은 타사 라이브러리도 있습니다. 코드 및 구성 요소 재사용을 최대화하는 것은 플랫폼 간 개발의 주요 목표 중 하나입니다. Swift를 사용 하 여 빌드된 구성 요소를 다시 사용 하는 기능은 개발자의 인기를 지속적으로 성장 하는 Xamarin 개발자에 게 점점 더 중요 해지고 있습니다. 이미 일반 [목표-C](../binding-objective-c/walkthrough.md) 라이브러리를 바인딩하는 프로세스에 대해 잘 알고 있을 수 있습니다. 이제 [Swift 프레임 워크를 바인딩하](walkthrough.md)는 프로세스를 설명 하는 추가 설명서를 사용할 수 있으므로 동일한 방식으로 Xamarin 응용 프로그램에서 사용할 수 있습니다. 이 문서의 목적은 Xamarin에 대 한 Swift 바인딩을 만드는 개략적인 방법을 설명 하는 것입니다.

## <a name="high-level-approach"></a>개략적인 접근법

Xamarin을 사용하면 Xamarin 애플리케이션에서 사용 가능한 타사 네이티브 라이브러리를 빌드할 수 있습니다. Swift는 새 언어 이며이 언어로 작성 된 라이브러리에 대 한 바인딩을 만들려면 몇 가지 추가 단계와 도구가 필요 합니다. 이 방법은 다음 4단계를 포함합니다.

1. 네이티브 라이브러리 빌드
1. Xamarin 도구에서 c # 클래스를 생성할 수 있도록 하는 Xamarin 메타 데이터 준비
1. 네이티브 라이브러리 및 메타 데이터를 사용 하 여 Xamarin 바인딩 라이브러리 빌드
1. Xamarin 응용 프로그램에서 Xamarin 바인딩 라이브러리 사용

다음 섹션에서는 추가 정보를 사용하여 이러한 단계를 간략하게 설명합니다.

### <a name="build-the-native-library"></a>네이티브 라이브러리 빌드

첫 번째 단계는 기본 Swift 프레임 워크를 목표로 준비 하는 것입니다. 이 파일은 원하는 Swift 클래스, 메서드 및 필드를 노출 하 여 Xamarin 바인딩 라이브러리를 통해 목표 C와 궁극적으로 c # 모두에 액세스할 수 있도록 하는 자동 생성 된 헤더입니다. 이 파일은 프레임 워크 내에서 프레임 ** \<FrameworkName> 워크/헤더/ \<FrameworkName> -Swift**경로 아래에 있습니다. 노출 된 인터페이스에 필요한 모든 멤버가 있는 경우 다음 단계로 건너뛸 수 있습니다. 그렇지 않으면 해당 멤버를 노출 하는 데 추가 단계가 필요 합니다. 접근 방식은 Swift framework 소스 코드에 액세스할 수 있는지 여부에 따라 달라 집니다.

- 코드에 액세스할 수 있는 경우 필요한 Swift 멤버를 특성으로 데코레이팅 하 `@objc` 고 몇 가지 추가 규칙을 적용 하 여 Xcode 빌드 도구에서 이러한 멤버를 목표-C 세계 및 헤더에 노출 해야 한다는 것을 알 수 있습니다.
- 소스 코드에 액세스할 수 없는 경우 원래 Swift 프레임 워크를 래핑하고 특성을 사용 하 여 응용 프로그램에 필요한 공용 인터페이스를 정의 하는 프록시 Swift 프레임 워크를 만들어야 `@objc` 합니다.

### <a name="prepare-the-xamarin-metadata"></a>Xamarin 메타데이터 준비

두 번째 단계는 c # 클래스를 생성 하기 위해 바인딩 프로젝트에서 사용 되는 API 정의 인터페이스를 준비 하는 것입니다. 이러한 정의는 [목표 Sharpie](../../../cross-platform/macios/binding/objective-sharpie/index.md) 도구와 앞에서 생성 된 ** \<FrameworkName> Swift** 헤더 파일에서 수동으로 또는 자동으로 만들 수 있습니다. 메타 데이터를 생성 한 후에는 수동으로 확인 하 고 유효성을 검사 해야 합니다.

### <a name="build-the-xamarinios-binding-library"></a>Xamarin.ios 바인딩 라이브러리를 빌드합니다.

세 번째 단계는 특수 프로젝트-Xamarin.ios 바인딩 라이브러리를 만드는 것입니다. 각 프레임 워크의 기반이 되는 추가 종속성과 함께 이전 단계에서 준비한 프레임 워크 및 메타 데이터를 참조 합니다. 또한 사용 중인 Xamarin.ios 응용 프로그램을 사용 하 여 참조 된 네이티브 프레임 워크의 링크를 처리 합니다.

### <a name="consume-the-xamarin-binding-library"></a>Xamarin 바인딩 라이브러리 사용

네 번째 및 마지막 단계는 Xamarin.ios 응용 프로그램에서 바인딩 라이브러리를 참조 하는 것입니다. IOS 12.2 이상을 대상으로 하는 Xamarin.ios 응용 프로그램 내에서 네이티브 라이브러리를 사용 하도록 설정 하는 것은 충분 합니다. 더 낮은 버전을 대상으로 하는 응용 프로그램의 경우 몇 가지 추가 단계가 필요 합니다.

- 런타임 지원에 대 한 Swift dylib 종속성을 추가 합니다. IOS 12.2 및 Swift 5.1부터 언어는 ABI (응용 프로그램 이진 인터페이스) 안정적이 고 호환 가능 합니다. 따라서 더 낮은 iOS 버전을 대상으로 하는 응용 프로그램은 프레임 워크에서 사용 하는 Swift dylibs 종속성을 포함 해야 합니다. [SwiftRuntimeSupport NuGet 패키지](https://www.nuget.org/packages/Xamarin.iOS.SwiftRuntimeSupport/) 를 사용 하 여 필요한 dylib 종속성을 결과 응용 프로그램 패키지에 자동으로 포함 합니다.
- 서명 된 dylibs을 사용 하 여 **SwiftSupport** 폴더를 추가 합니다 .이 폴더는 업로드 프로세스 중에 appstore에서 유효성을 검사 합니다. Xcode 도구를 사용 하 여 패키지에 서명 하 고 AppStore connect에 배포 해야 합니다. 그렇지 않으면 자동으로 거부 됩니다.

## <a name="walkthrough"></a>연습

위의 방법은 Xamarin에 대 한 Swift 바인딩을 만드는 데 필요한 개략적인 단계를 간략하게 설명 합니다. 이러한 바인딩을 실제로 준비할 때는 여러 세부적인 단계가 수반되며 네이티브 도구 및 언어의 변경 사항을 적용하는 등 추가 세부 정보를 고려해야 합니다. 이를 통해 이 개념과 이 프로세스와 관련된 개략적인 단계를 보다 깊이 있게 이해할 수 있습니다. 자세한 단계별 가이드는 [Xamarin Swift Binding 연습](walkthrough.md) 설명서를 참조 하세요.

## <a name="related-links"></a>관련 링크

- [Xcode](https://apps.apple.com/us/app/xcode/id497799835)
- [Mac용 Visual Studio](https://visualstudio.microsoft.com/downloads)
- [Objective Sharpie](../../../cross-platform/macios/binding/objective-sharpie/index.md)
- [Sharpie 메타 데이터 확인](../../../cross-platform/macios/binding/objective-sharpie/platform/verify.md)
- [바인딩 목표-C 프레임 워크](../binding-objective-c/walkthrough.md)
- [Gigya iOS SDK (Swift framework)](https://developers.gigya.com/display/GD/Swift+SDK)
- [Swift 5.1 ABI 안정성](https://swift.org/blog/swift-5-1-released/)
- [SwiftRuntimeSupport NuGet](https://www.nuget.org/packages/Xamarin.iOS.SwiftRuntimeSupport/)
- [Xamarin UITest automation](/appcenter/test-cloud/uitest/)
- [Xamarin.ios UITest 구성](/appcenter/test-cloud/preparing-for-upload/xamarin-ios-uitest)
- [AppCenter Test Cloud](/appcenter/test-cloud/preparing-for-upload/xamarin-ios-uitest)
- [샘플 프로젝트 리포지토리](https://github.com/xamcat/xamarin-binding-swift-framework)
---
title: Xamarin에서 watchOS 레이아웃 작업
description: 이 문서에서는 Xamarin을 사용 하 여 watchOS 레이아웃을 만드는 방법을 설명 합니다. 인터페이스 컨트롤러, 그룹, 구분 기호 및 콘텐츠 컨트롤에 대해 설명 합니다.
ms.prod: xamarin
ms.assetid: BEDB62A1-2249-4459-986F-413A41E63DF0
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/17/2017
ms.openlocfilehash: 1fdb7a10bd767085ba8758fa2e026cc36c93639a
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91436926"
---
# <a name="working-with-watchos-layout-in-xamarin"></a>Xamarin에서 watchOS 레이아웃 작업

Apple Watch [화면 크기](~/ios/watchos/app-fundamentals/screen-sizes.md) 의 레이아웃을 디자인 하는 데는 고유한 과제가 있습니다.

## <a name="design-tips"></a>디자인 팁

핵심 요소는 작은 조사식 화면에서 사용자 인터페이스를 읽을 수 있고 사용 가능 하도록 설정 하는 것입니다. **IOS 시뮬레이터** (매우 큰 것으로 나타남) 및 **마우스 포인터** (가장 작은 터치 대상에서 작동 함)에 대 한 디자인의 트랩에 속하지 않습니다.

- 검은색 배경을 사용 합니다 .이는 시청의 검정 베젤을 사용 하 여 큰 화면 효과를 만듭니다.

- 화면 레이아웃 주위에 채움 안 함-베젤은 자연 시각적 안쪽 여백을 형성 합니다.

- 가독성에 집중 합니다. 텍스트를 읽을 수 있도록 글꼴 크기와 색을 신중 하 게 사용 합니다. 자동 동적 형식 지원을 받으려면 기본 제공 텍스트 스타일을 사용 합니다.

![동적 형식 지원의 예](layout-images/type.png)

- 터치 대상 크기에 집중 합니다. 텍스트 레이블이 있는 Buttons/tappable 테이블 행은 전체 화면에 걸쳐 있어야 합니다. Apple은 "세 개 이상의 항목을 나란히 표시 하지 않음"을 의미 하 고, 텍스트 레이블이 아닌 아이콘을 사용 하는 경우를 말합니다.

- 이 [ `Menu` 컨트롤](~/ios/watchos/user-interface/menu.md) 을 사용 하 여 자주 사용 하지 않는 기능을 노출 하 여 응용 프로그램 디자인을 명확 하 고 간결 하 게 유지 합니다.

## <a name="implementation"></a>구현

Watch 키트에는 멋진 조사식 앱 레이아웃을 작성 하는 데 도움이 되는 다음 컨트롤이 포함 되어 있습니다.

### <a name="interface-controller"></a>인터페이스 컨트롤러

는 `WKInterfaceController` 모든 장면의 기본 클래스입니다.

인터페이스 컨트롤러의 디자인 화면은 세로 **그룹**처럼 동작 합니다. 다른 컨트롤은 인터페이스 컨트롤러로 끌 수 있으며, 다른 컨트롤은 다른 컨트롤 위에 자동으로 배치 됩니다.

![컨트롤은 자동으로 한 컨트롤 위에 자동으로 배치 됩니다.](layout-images/controller-scene.png)

각 컨트롤의 **위치** 및 **크기** 속성을 설정 하 여 모양을 제어할 수 있습니다.

![각 컨트롤의 위치 및 크기 속성 설정](layout-images/positionsize-attributes.png)

크기를 **컨테이너에 상대적** 으로 설정 하면 비례 값과 오프셋 조정을 제공할 수 있습니다. 이 스크린샷은 조사식 화면 너비 (**0.8**)의 80%를 사용 하도록 설정 된 단추를 보여 줍니다.

![비례 값 및 오프셋 조정 제공](layout-images/button-attributes.png)

### <a name="group"></a>그룹

`WKInterfaceGroup` 는 컨트롤을 가로 또는 세로로 쌓기 위해 구성할 수 있는 간단한 레이아웃 컨테이너입니다. 기본적으로 각 컨트롤 간의 간격을 포함 하지만 **특성** 검사자에서 간격 (및 인세트)을 수정할 수 있습니다.

![특성 검사자에서 간격 및 인세트 수정](layout-images/group-attributes.png)

그룹 자체의 크기를 조정 하 고 주위에 컨트롤을 기준으로 위치를 지정 하 고 그룹을 중첩 하 여 복잡 한 레이아웃을 만들 수 있습니다.

![그룹을 중첩 하 여 복잡 한 레이아웃을 만들 수 있습니다.](layout-images/group-scene.png)

### <a name="separator"></a>구분 기호

구분 기호 컨트롤은 레이아웃에 시각적 지침을 제공 하기 위한 것입니다. 구분 기호 (또는 배경색 또는 이미지)를 사용 하 여 사용자가 화면에 관련 된 콘텐츠를 이해할 수 있습니다.

![구분 기호 사용 예](layout-images/separator-scene.png)

참고 화면의 전체 너비를 사용 하지 않는 파랑 및 녹색 구분 기호는 **고정** 또는 **컨테이너 크기를 기준** 으로 구성 됩니다.

### <a name="content-controls"></a>콘텐츠 컨트롤

`Label`, `Image` ,,,, `Button` `Switch` `Slider` `Map` 및 [기타 컨트롤이](~/ios/watchos/user-interface/index.md)없으면 레이아웃이 완료 되지 않습니다.
각 컨트롤의 위치 및 크기 설정 또는 **그룹** 을 사용 하 여 레이아웃에 배치할 수 있습니다.

## <a name="related-links"></a>관련 링크

- [WatchKitCatalog (샘플)](/samples/xamarin/ios-samples/watchos-watchkitcatalog)
- [Apple의 레이아웃 참조](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/WatchHumanInterfaceGuidelines/Layout.html)
- [Apple 색 & 입력 체계 참조](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/WatchHumanInterfaceGuidelines/ColorandTypography.html)
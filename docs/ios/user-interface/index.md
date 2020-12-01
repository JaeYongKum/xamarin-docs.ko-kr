---
title: Xamarin.ios를 사용 하 여 사용자 인터페이스 빌드
description: 이 문서에서는 Xamarin.ios 앱에서 사용자 인터페이스를 작성 하는 방법을 설명 합니다. IOS designer, storyboard, 일반 iOS 인터페이스 개념 및 iOS 사용자 인터페이스 컨트롤에 대 한 가이드의 링크를 제공 합니다.
ms.prod: xamarin
ms.assetid: 2B3E45FA-C30F-D708-0E8F-3EE02BD1A867
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 06/21/2017
ms.openlocfilehash: 4d98e061ae935605613eb0d2a9c10b3866b610c9
ms.sourcegitcommit: d1f0e0a9100548cfe0960ed2225b979cc1d7c28f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439418"
---
# <a name="building-user-interfaces-with-xamarinios"></a>Xamarin.ios를 사용 하 여 사용자 인터페이스 빌드

## <a name="storyboards"></a>[스토리보드](~/ios/user-interface/storyboards/index.md)

스토리 보드는 응용 프로그램의 모양과 흐름을 시각적으로 표현한 것입니다. Mac용 Visual Studio를 사용 하면 Xcode Interface Builder와 상호 작용 하 여 시각적으로 응용 프로그램 화면을 디자인 하 고, c #을 사용 하 여 뷰, 컨트롤러 및 segue에 액세스 하 여 더 많은 제어를 할 수 있습니다. 

## <a name="ios-designer"></a>[iOS Designer](~/ios/user-interface/designer/index.md)

> [!WARNING]
> IOS Designer는 Visual Studio 2019 버전 16.8 및 Mac 용 Visual Studio 2019 버전 8.8에서 단계적으로 시작 됩니다.
> IOS 사용자 인터페이스를 작성 하는 데 권장 되는 방법은 Xcode를 실행 하는 Mac에서 직접입니다. 자세한 내용은 [Xcode를 사용 하 여 사용자 인터페이스 디자인](~/ios/user-interface/storyboards/index.md)을 참조 하세요. 

Mac용 Visual Studio에 완전히 통합 된 iOS storyboard 형식에 대 한 디자이너를 빌드 했습니다. IOS 디자이너는 Xcode 또는 Mac용 Visual Studio에서 파일을 편집할 수 있도록 스토리 보드 형식과의 완전 한 호환성을 유지 합니다. 또한 편집기는 디자인 타임에 편집기에서 렌더링 하는 사용자 지정 컨트롤과 같은 고급 기능을 지원 합니다.

## <a name="user-interface-in-ios"></a>[iOS의 사용자 인터페이스](~/ios/user-interface/ios-ui/index.md)

햅 앱에서 사용자 인터페이스를 사용 하 여 작업을 수행 하 고, 사용자 인터페이스 개체를 만들고, 레이아웃 옵션을 제공 하 고, 사용자 의견을 제공 하 고, UI 스레드를 사용 하는 작업을 다룹니다.

## <a name="user-interface-controls"></a>[사용자 인터페이스 컨트롤](~/ios/user-interface/controls/index.md)

Xamarin.ios는 Apple에서 제공 하는 모든 네이티브 사용자 인터페이스 개체를 노출 합니다. IOS Designer, Xcode의 Interface Builder를 사용 하거나 프로그래밍 방식으로 Xamarin.ios 응용 프로그램에 쉽게 추가할 수 있습니다. 선택 하는 방법에 관계 없이 Xamarin.ios는 c #의 모든 사용자 인터페이스 개체 속성 및 메서드를 노출 합니다.

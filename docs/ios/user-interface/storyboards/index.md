---
title: Xcode를 사용 하 여 사용자 인터페이스 디자인
description: Mac에서 Xcode를 사용 하 여 직접 iOS 사용자 인터페이스를 빌드하는 권장 방법에 대해 알아봅니다.
ms.prod: xamarin
ms.assetid: af9f95db-5cd6-475d-867d-f73e1574e8fc
ms.technology: xamarin-ios
author: joshspicer
ms.author: jospicer
ms.date: 10/27/2020
ms.openlocfilehash: b25245250bd9ea17034ea8f6b11388a12fc13241
ms.sourcegitcommit: d1f0e0a9100548cfe0960ed2225b979cc1d7c28f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439576"
---
# <a name="designing-user-interfaces-with-xcode"></a>Xcode를 사용 하 여 사용자 인터페이스 디자인

Visual Studio 2019 버전 16.8 및 Mac용 Visual Studio 버전 8.8부터 storyboard 및 nib 파일을 편집 하는 권장 방법은 Mac의 Xcode Interface Builder에서 편집 하는 것입니다.

> [!NOTE]
> Visual Studio 2019 버전 16.9부터 Windows에서 iOS storyboard를 편집 하는 데 지원 되는 방법은 없습니다. Mac용 Visual Studio 및 Xcode Interface Builder를 사용 하 여 Xamarin.ios 사용자 인터페이스 빌드를 계속 합니다.

이 문서에서는 Xcode Interface Builder를 사용 하 여 사용자 인터페이스를 구축 하는 일반적인 솔루션을 설명 합니다.  이 문서는 이전에 Xamarin.ios 디자이너를 사용 하 여 Ui를 편집한 경우에 특히 유용할 수 있습니다. 

스토리 보드에 대 한 자세한 연습은 [xamarin.ios의 스토리 보드](./indepth-storyboard.md)를 참조 하세요.

## <a name="how-to-open-a-storyboard"></a>스토리 보드를 여는 방법 

스토리 보드 파일을 마우스 오른쪽 단추로 클릭 하 고 **Xcode Interface Builder** 를 선택 하 여 Mac용 Visual Studio에서 iOS 사용자 인터페이스 파일을 엽니다.

[![Interface Builder 선택](images/select-interface-builder.png)](images/select-interface-builder.png#lightbox)

그러면 Xcode 창이 열립니다. 여기에 저장 된 모든 편집 내용은 Visual Studio 프로젝트에 반영 됩니다.

[![Xcode 창](images/xcode.png)](images/xcode.png#lightbox)

Xcode Interface Builder에 대 한 자세한 내용은 [기본 제공 Interface Builder](https://developer.apple.com/xcode/interface-builder/)을 참조 하세요.

## <a name="creating-a-new-control"></a>새 컨트롤 만들기

Xcode Interface Builder를 사용 하 여 새 컨트롤을 만들려면 먼저 편집할 storyboard를 선택 합니다. 그런 다음 Xcode library 대화 상자 (**View**  >  **Show library**)를 열고 컨트롤을 storyboard로 끌어 놓습니다.

[![라이브러리 선택기](images/library-picker.png)](images/library-picker.png#lightbox)

그런 다음 해당 뷰 컨트롤러 헤더 파일을 엽니다.  빈 "단일 뷰" Xamarin.ios 앱의 경우 기본 storyboard를 기본 storyboard 라고 합니다 **.** Xcode에서 볼 때 해당 **viewcontroller .h** 헤더 파일을 사용 하 여 Visual Studio에서 해당 뷰 컨트롤러 파일을 **ViewController.cs** 이라고 합니다.

Xcode Interface Builder에서 storyboard와 해당 뷰 컨트롤러 헤더 파일을 엽니다.  **컨트롤** 키 ()를 유지 하 고 **^** Xcode 대화 상자를 표시 하 라는 메시지가 표시 될 때까지 storyboard에서 뷰 컨트롤러 파일로 컨트롤을 끕니다.

[![데모 링크 컨트롤](images/demo-link-control.gif)](images/demo-link-control.gif#lightbox)

위에서 설명한 것 처럼 해당 c # 코드는 뷰 컨트롤러의 코드 숨김이 파일에 자동으로 생성 됩니다.  이제 Xamarin.ios 프로젝트 내에서이 컨트롤에 액세스할 수 있습니다.

## <a name="editing-an-existing-controls-name"></a>기존 컨트롤의 이름 편집

Xcode Interface Builder에서 기존 컨트롤의 이름을 편집 하 고 해당 변경 내용을 c # 프로젝트에 다시 반영 하려면 적절 한 뷰 컨트롤러 헤더 파일인 고로 이동 하 고 **리팩터링** 을 선택 합니다.   

[![리팩터링 컨트롤](images/refactor-control.png)](images/refactor-control.png#lightbox)

코드 숨겨진 파일은 새 이름으로 다시 생성 되므로 Mac용 Visual Studio 코드를 통해 컨트롤에 액세스할 수 있습니다.

## <a name="known-problems"></a>알려진 문제

이 섹션에서는 알려진 문제에 대해 설명 합니다.

### <a name="visual-studio-could-not-communicate-with-xcode"></a>"Visual Studio에서 Xcode와 통신할 수 없습니다."

MacOS Catalina.properties 이상에서 아래 오류가 발생할 수 있습니다.

[![오류를 전달할 없음](images/could-not-communicate.png)](images/could-not-communicate.png#lightbox)

먼저, Mac의 시스템 기본 설정의 **보안 & 개인 정보 > 자동화** 에서 Visual Studio가 나열 되 고 **Xcode** 이 선택 되어 있는지 확인 합니다.

[![macOS 보안](images/macos-security.png)](images/macos-security.png#lightbox)

**Xcode** 를 선택 하 고 오류 메시지가 계속 표시 되는 경우 Mac용 Visual Studio 개인 정보 사용 권한을 다시 설정 해야 할 수 있습니다.

터미널 창을 시작 하 고 다음 명령을 실행 하 여이 작업을 수행할 수 있습니다.

```bash
sudo tccutil reset All "com.microsoft.visual-studio"
```

위의 변경 내용이 적용 되도록 하려면 Mac의 PRAM을 다시 설정 합니다. 지침은 [Mac에서 NVRAM 또는 PRAM 다시 설정](https://support.apple.com/HT204063)을 참조 하세요.

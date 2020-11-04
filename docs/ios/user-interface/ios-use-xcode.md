---
title: Xcode를 사용 하 여 Ui 디자인
description: 이제 Mac에서 Xcode를 사용 하 여 iOS 사용자 인터페이스를 작성 하는 것이 좋습니다.
ms.prod: xamarin
ms.assetid: af9f95db-5cd6-475d-867d-f73e1574e8fc
ms.technology: xamarin-ios
author: joshspicer
ms.author: jospicer
ms.date: 10/27/2020
ms.openlocfilehash: b6fc5c89e9221bc84b364290a275fbd6d35c12c4
ms.sourcegitcommit: d2aa3a8bf9a60b6708db55b10b0c6893c06d3256
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93343321"
---
# <a name="using-xcode-to-design-user-interfaces"></a>Xcode를 사용 하 여 사용자 인터페이스 디자인

_스토리 보드 및 nib 파일을 편집 하는 권장 방법은 Mac의 Xcode Interface Builder에서 편집 하는 것입니다._

## <a name="how-to-open-a-storyboard"></a>스토리 보드를 여는 방법 

스토리 보드 파일을 마우스 오른쪽 단추로 클릭 하 고 **Xcode Interface Builder** 를 선택 하 여 Mac용 Visual Studio에서 iOS 사용자 인터페이스 파일을 엽니다.

[![Interface Builder 선택](images/select-interface-builder.png)](images/select-interface-builder.png#lightbox)

그러면 Xcode 창 시작이 표시 됩니다. 여기에 저장 된 모든 편집 내용은 Visual Studio 프로젝트에 반영 됩니다.

[![Xcode 창](images/xcode.png)](images/xcode.png#lightbox)

Xcode Interface Builder에 대 한 자세한 내용은 [여기](https://developer.apple.com/xcode/interface-builder/)에서 찾을 수 있습니다.

## <a name="known-problems"></a>알려진 문제

알려진 문제는이 섹션에 설명 되어 있습니다.

### <a name="visual-studio-could-not-communicate-with-xcode"></a>"Visual Studio에서 Xcode와 통신할 수 없습니다."

MacOS Catalina.properties 이상에서 아래 오류가 발생할 수 있습니다.

[![오류를 전달할 없음](images/could-not-communicate.png)](images/could-not-communicate.png#lightbox)

먼저, **보안 & 개인 정보 > 보호** 의 Mac 시스템 기본 설정에서 Visual Studio가 나열 되 고 **Xcode** 가 선택 되어 있는지 확인 합니다.

[![macOS 보안](images/macos-security.png)](images/macos-security.png#lightbox)

**Xcode** 를 선택 하 고 오류 메시지가 계속 표시 되는 경우 Mac용 Visual Studio 개인 정보 사용 권한을 다시 설정 해야 할 수 있습니다.

터미널 창을 시작 하 고 명령을 실행 하 여이 작업을 수행할 수 있습니다.

```bash
sudo tccutil reset All "com.microsoft.visual-studio"
```

위의 변경 내용이 적용 되도록 하려면 Mac의 PRAM을 다시 설정 합니다. 이 작업을 수행 하는 방법에 대 한 지침은 [여기](https://support.apple.com/HT204063)에서 찾을 수 있습니다.

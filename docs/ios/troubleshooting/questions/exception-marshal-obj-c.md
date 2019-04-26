---
title: '다음 메시지가 표시되며 내 iOS 9 앱이 실패한 이유는 무엇인가요? System.Exception: Objective-C 개체를 마샬링하지 못했습니다.'
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 8805ABEC-48D4-4CCB-A226-3A5B2ECE4BF0
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 04/03/2018
ms.openlocfilehash: dfe1918d271946eb96d1f57d32c533a075f6d0bd
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61421959"
---
# <a name="why-does-my-ios-9-app-fail-with-systemexception-failed-to-marshal-the-objective-c-object"></a>다음 메시지가 표시되며 내 iOS 9 앱이 실패한 이유는 무엇인가요? System.Exception: Objective-C 개체를 마샬링하지 못했습니다.

이 폼의 오류가 표시 될 수 있습니다.

> System.Exception: Objective-c 개체를 마샬링할 하지 못했습니다. 이 개체에 대 한 기존 관리 되는 인스턴스를 찾을 수 없습니다...

IOS 9에서에서 API 변경 필요 이제 기본 API로 관리 되지 않는 코드를 호출 하는 경우 콜백 생성자를 사용는 필요 합니다. 콜백 생성자 클래스를 추가 하려면 다음 줄을 사용 합니다. 

`public foo (IntPtr handle) : base (handle) ` 

### <a name="next-steps"></a>다음 단계

추가 지원이 필요한 경우, 우리에 게 문의 하 여 위의 정보를 활용 하 여 한 후에이 문제가 여전히 발생 하는 경우를 참조 하세요 [Xamarin에 대해 사용할 수 있는 지원 옵션?](~/cross-platform/troubleshooting/support-options.md) 연락처 옵션을 제안에 대 한 정보에 대 한 방법 뿐만 아니라 필요한 경우 새 버그를 파일입니다. 

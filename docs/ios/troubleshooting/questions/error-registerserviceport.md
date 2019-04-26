---
title: RegisterServicePort에 발생하는 iOS 디자이너 오류
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 929A0080-B126-4744-BF88-A4A1EFBB6CC2
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 04/03/2018
ms.openlocfilehash: fc4c143d6b5f7c211d24e6e3ed2ed3bb8d264410
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61421972"
---
# <a name="ios-designer-error-with-registerserviceport"></a>RegisterServicePort에 발생하는 iOS 디자이너 오류

## <a name="sample-error"></a>샘플 오류
> System.AggregateException: System.SystemException---> 하나 이상의 오류가 발생 합니다. RegisterServicePort(com.xamarin.MTHosting.2a0b1, com.apple.PowerManagement.control): 반환 되는 커널:-308 (-308): (ipc/마이그레이션) 서버 종료

## <a name="explanation"></a>설명
사용 하 여 오류 `RegisterServicePort` 위에 같은 유사한 오류 메시지는 일반적으로 스파이웨어/컴퓨터의 맬웨어 문제가 및 합니다. 것을 고려 하세요 합니다 [이 버그 보고서에 주석](https://bugzilla.xamarin.com/show_bug.cgi?id=21907#c4) 에 대 한 링크와 함께 자세한 합니다 [Apple 포럼 토론](https://discussions.apple.com/thread/5596008) 가능한 감염을 제거 하는 방법에 합니다. 

문제를 진단 하는 데 도움이 되, macOS 응용 프로그램을 엽니다 **콘솔** 내에서 모든 파일을 삭제 합니다 **진단 보고서가 사용자** 섹션 [ http://screencast.com/t/y9i3NKcuMy ](http://screencast.com/t/y9i3NKcuMy). 그런 다음 Mac 용 Visual Studio를 시작 하 고 디자이너를 사용 하려고 합니다. 디자이너 초기화에 실패 한 후 새 로그 파일 모두이 섹션에 표시를 분석 하기 위해 저장 하십시오.  

확인 하려면 가장 중요 한 점은이 파일 note 하십시오. 
> /usr/lib/libimckit.dylib

위의 결과 관계 없이 해당 파일이 있으면 앞에서 언급 한 스파이웨어/맬웨어 문제는 컴퓨터에 설치.  

다음 링크에는이 스파이웨어/맬웨어를 제거 하는 단계에 있습니다. [http://www.thesafemac.com/arg-genieo/](http://www.thesafemac.com/arg-genieo/)  


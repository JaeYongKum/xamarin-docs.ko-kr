---
ms.openlocfilehash: d46968f9c53314abe561e7f4871cfbf6e07b7002
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61047856"
---
## <a name="firewall-configuration"></a>방화벽 구성

Xamarin Test Cloud에 제출 해야 하는 테스트에 대 한 순서로 테스트를 제출 하는 컴퓨터 Test Cloud 서버와 통신할 수 있어야 합니다. 에 있는 서버에서 네트워크 트래픽을 허용 하도록 방화벽을 구성 해야 합니다 **testcloud.xamarin.com** 포트 80 및 443입니다. 이 끝점은 DNS에서 관리 하 고 IP 주소가 변경 될 수 있습니다. 

상황에 따라 테스트 (또는 테스트를 실행 하는 장치)는 방화벽으로 보호 하는 웹 서버와 통신 해야 합니다. 이 시나리오에서는 다음 IP 주소에서 트래픽을 허용 하도록 방화벽을 구성 합니다.

* **195.249.159.238**
* **195.249.159.239**

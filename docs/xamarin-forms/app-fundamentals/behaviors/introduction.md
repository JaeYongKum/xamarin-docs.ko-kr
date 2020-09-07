---
title: 동작 소개
description: 동작을 사용하면 서브클래스 없이도 사용자 인터페이스 컨트롤에 기능을 추가할 수 있습니다. 대신 기능은 동작 클래스에서 구현되고 컨트롤 자체의 일부였던 것처럼 컨트롤에 연결됩니다. 이 문서에서는 동작을 소개합니다.
ms.prod: xamarin
ms.assetid: 0DF1EF8C-A212-4142-A3C6-DF760A82A757
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/06/2016
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 37c76a5f325c363a92c2a2c1e597dab28f064cd9
ms.sourcegitcommit: a003b036f6fb83818e2ecc9c72a641e3aeb373bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88964612"
---
# <a name="introduction-to-behaviors"></a>동작 소개

_동작을 사용하면 서브클래스 없이도 사용자 인터페이스 컨트롤에 기능을 추가할 수 있습니다. 대신 기능은 동작 클래스에서 구현되고 컨트롤 자체의 일부였던 것처럼 컨트롤에 연결됩니다. 이 문서에서는 동작을 소개합니다._

동작을 사용하면 코드가 컨트롤에 간결하게 첨부되고 둘 이상의 애플리케이션에서 재사용하도록 패키지될 수 있도록 컨트롤의 API와 직접 상호 작용하기 때문에, 대개 코드 숨김으로 작성해야 하는 코드를 구현할 수 있습니다. 다음과 같은 컨트롤에 광범위한 기능을 제공하는 데 사용할 수 있습니다.

- 이메일 유효성 검사기를 [`Entry`](xref:Xamarin.Forms.Entry)에 추가합니다.
- 탭 제스처 인식기를 사용하여 등급 컨트롤을 만듭니다.
- 애니메이션을 제어합니다.
- 컨트롤에 효과를 추가합니다.

또한 동작은 더 고급 시나리오를 사용하도록 설정합니다. *명령* 컨텍스트에서 동작은 명령에 컨트롤을 연결하는 데 유용한 접근 방식입니다. 또한 동작은 명령과 상호 작용하도록 설계되지 않은 컨트롤과 명령을 연결하는 데 사용할 수 있습니다. 예를 들어, 발생하는 이벤트에 대한 응답에서 명령을 호출하는 데 사용할 수 있습니다.

Xamarin.Forms는 두 가지 동작 스타일을 지원합니다.

- **Xamarin.Forms 동작** – [`Behavior`](xref:Xamarin.Forms.Behavior) 또는 [`Behavior<T>`](xref:Xamarin.Forms.Behavior`1) 클래스에서 파생된 클래스입니다. 여기서 `T`는 동작이 적용되어야 하는 컨트롤의 형식입니다. Xamarin.Forms 동작에 관한 자세한 내용은 [Xamarin.Forms 동작](~/xamarin-forms/app-fundamentals/behaviors/creating.md)을 참조하세요.
- **연결된 동작** – 첨부된 속성이 하나 이상 있는 `static` 클래스입니다. 연결된 동작에 대한 자세한 내용은 [연결된 동작](~/xamarin-forms/app-fundamentals/behaviors/attached.md)을 참조하세요.

이 가이드에서는 선호되는 동작 생성 방식인 Xamarin.Forms 동작을 집중적으로 다룹니다.

## <a name="related-links"></a>관련 링크

- [동작](xref:Xamarin.Forms.Behavior)
- [동작&lt;T&gt;](xref:Xamarin.Forms.Behavior`1)

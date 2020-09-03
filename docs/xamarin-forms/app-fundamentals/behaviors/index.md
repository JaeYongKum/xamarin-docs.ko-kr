---
title: Xamarin.Forms 동작
description: 동작을 사용하면 서브클래스 없이도 사용자 인터페이스 컨트롤에 기능을 추가할 수 있습니다. 동작은 코드로 작성되고 XAML 또는 코드의 컨트롤에 추가됩니다.
ms.prod: xamarin
ms.assetid: 42E32AD7-8E3B-48B3-B402-E75B758DA913
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/06/2016
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: d917d7d6421cfae7fc877c81023a835573fa99b1
ms.sourcegitcommit: a003b036f6fb83818e2ecc9c72a641e3aeb373bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88964625"
---
# <a name="no-locxamarinforms-behaviors"></a>Xamarin.Forms 동작

_동작을 사용하면 서브클래스 없이도 사용자 인터페이스 컨트롤에 기능을 추가할 수 있습니다. 동작은 코드로 작성되고 XAML 또는 코드의 컨트롤에 추가됩니다._

## <a name="introduction-to-behaviors"></a>[동작 소개](introduction.md)

동작을 사용하면 코드가 컨트롤에 간결하게 첨부될 수 있도록 컨트롤의 API와 직접 상호 작용하기 때문에, 대개 코드 숨김으로 작성해야 하는 코드를 구현할 수 있습니다. 이 문서에서는 동작을 소개합니다.

## <a name="attached-behaviors"></a>[연결된 동작](attached.md)

연결된 동작은 연결된 속성이 하나 이상 있는 `static` 클래스입니다. 이 문서에서는 연결된 동작을 만들고 사용하는 방법을 설명합니다.

## <a name="no-locxamarinforms-behaviors"></a>[Xamarin.Forms 동작](creating.md)

Xamarin.Forms 동작은 [`Behavior`](xref:Xamarin.Forms.Behavior) 또는 [`Behavior<T>`](xref:Xamarin.Forms.Behavior`1) 클래스에서 파생되어 만들어집니다. 이 문서에서는 Xamarin.Forms 동작을 만들고 사용하는 방법을 보여 줍니다.

## <a name="reusable-effectbehavior"></a>[재사용 가능한 EffectBehavior](effect-behavior.md)

동작은 컨트롤에 효과를 추가하고 코드 숨김 파일에서 표준 효과 처리 코드를 제거하는 데 유용한 방법입니다. 이 문서에서는 Xamarin.Forms 동작을 만들고 사용하여 컨트롤에 효과를 추가하는 방법을 보여 줍니다.

---
title: Xamarin.Forms 제스처
description: 이 가이드에서는 Xamarin.Forms 제스처 인식기를 사용하여 Xamarin.Forms 애플리케이션에서 사용자의 보기 상호 작용을 감지할 수 있습니다.
ms.prod: xamarin
ms.assetid: 0E197A51-2304-4C09-A710-C7FF24A89F15
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/04/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 7528afd0971cf06eb69df4ed7c08c3fd6dcc9e22
ms.sourcegitcommit: 08290d004d1a7e7ac579bf1f96abf8437921dc70
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87917831"
---
# <a name="no-locxamarinforms-gestures"></a>Xamarin.Forms 제스처

제스처 인식기를 사용하여 Xamarin.Forms 애플리케이션에서 사용자의 보기 상호 작용을 감지할 수 있습니다.

Xamarin.Forms [`GestureRecognizer`](xref:Xamarin.Forms.GestureRecognizer) 클래스는 [`View`](xref:Xamarin.Forms.View) 인스턴스에서 탭, 축소, 이동, 살짝 밀기 및 끌어서 놓기 제스처를 지원합니다.

## <a name="add-a-tap-gesture-recognizer"></a>[탭 제스처 인식기 추가](tap.md)

탭 제스처는 탭을 감지하는 데 사용되며 [`TapGestureRecognizer`](xref:Xamarin.Forms.TapGestureRecognizer) 클래스로 인식됩니다.

## <a name="add-a-pinch-gesture-recognizer"></a>[축소 제스처 인식기 추가](pinch.md)

손가락 모으기 제스처는 대화형 확대/축소 작업을 수행하는 데 사용되며 [`PinchGestureRecognizer`](xref:Xamarin.Forms.PinchGestureRecognizer) 클래스로 인식됩니다.

## <a name="add-a-pan-gesture-recognizer"></a>[이동 제스처 인식기 추가](pan.md)

이동 제스처는 화면에서 손가락의 움직임을 감지하고 이 움직임을 콘텐츠에 적용하는 데 사용되며 [`PanGestureRecognizer`](xref:Xamarin.Forms.PanGestureRecognizer) 클래스로 인식됩니다.

## <a name="add-a-swipe-gesture-recognizer"></a>[살짝 밀기 제스처 인식기 추가](swipe.md)

살짝 밀기 제스처는 화면에서 손가락이 가로나 세로 방향으로 이동하는 경우 발생하며 콘텐츠에 대한 탐색을 시작하는 데 종종 사용됩니다. 살짝 밀기 제스처는 [`SwipeGestureRecognizer`](xref:Xamarin.Forms.SwipeGestureRecognizer) 클래스로 인식됩니다.

## <a name="add-a-drag-and-drop-gesture-recognizer"></a>[끌어서 놓기 제스처 인식기 추가](drag-and-drop.md)

끌어서 놓기 제스처를 사용하면 한 번의 연속 제스처를 사용하여 항목 및 연결된 데이터 패키지를 화면의 한 위치에서 다른 위치로 끌어올 수 있습니다. 끌기 제스처는 `DragGestureRecognizer` 클래스를 사용하여 인식되고, 놓기 제스처는 `DropGestureRecognizer` 클래스를 사용하여 인식됩니다.

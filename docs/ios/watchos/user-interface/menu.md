---
title: Xamarin의 watchOS Menu 컨트롤 (Force Touch)
description: 이 문서에서는 Xamarin에서 watchOS force touch 제스처를 사용 하는 방법을 설명 합니다. 이 예에서는 force touch에 응답 하는 방법, 메뉴를 추가 하는 방법 및 메뉴 항목을 변경 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 5A7F83FB-9BC4-4812-92C5-CEC8DAE8211E
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/17/2017
ms.openlocfilehash: 5ad45e1cc17a58875037f20996463f55f2b68685
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91431555"
---
# <a name="watchos-menu-control-force-touch-in-xamarin"></a>Xamarin의 watchOS Menu 컨트롤 (Force Touch)

Watch 키트는 감시 앱 화면에서 구현 될 때 메뉴를 트리거하는 Force Touch 제스처를 제공 합니다.

![메뉴를 표시 하 Apple Watch](menu-images/menu.png)
<!-- watch image courtesy of http://infinitapps.com/bezel/ -->

## <a name="responding-to-force-touch"></a>Force Touch에 응답

가 `Menu` 인터페이스 컨트롤러에 대해 구현 된 경우 사용자가 Force Touch을 수행 하면 메뉴가 표시 됩니다. 메뉴를 구현 하지 않은 경우 화면에 잠시 애니메이션 효과가 적용 됩니다.

Force 접촉은 화면의 특정 요소와 연결 되지 않습니다. 인터페이스 컨트롤러에는 하나의 메뉴만 연결 될 수 있으며 화면에서 Force Touch 키가 발생 하는 위치에 관계 없이 표시 됩니다.

1 ~ 4 개의 메뉴 옵션이 표시 될 수 있습니다.

## <a name="adding-a-menu"></a>메뉴 추가

`Menu` `InterfaceController` 디자인 타임에 스토리 보드의에를 추가 해야 합니다. 메뉴 컨트롤을 인터페이스 컨트롤러에 끌어 놓으면 storyboard 미리 보기에 시각적 표시가 없지만 **문서 개요** 패드에 **메뉴가** 나타납니다.

![디자인 타임에 메뉴 편집](menu-images/menu-action.png)

메뉴 항목을 메뉴 컨트롤에 최대 4 개까지 추가할 수 있습니다. 이러한 **속성은 속성** 패드에서 구성할 수 있습니다. 다음 특성을 설정할 수 있습니다.

- 제목 및
- 사용자 지정 이미지 또는
- 시스템 이미지: 수락, 추가, 차단, 거부, 정보, 없음, 추가, 음소거, 일시 중지, 재생, 반복, 다시 시작, 공유, 순서 섞기, 발표자, 휴지통.

`Action` **속성** 패드의 **이벤트** 섹션을 선택 하 고 동작 메서드의 이름을 입력 하 여를 만듭니다. 다음과 같이 인터페이스 컨트롤러 클래스에서 구현할 수 있는 코드에서 부분 메서드가 생성 됩니다.

```csharp
partial void MenuItemTapped ()
{
    Console.WriteLine ("A menu item was tapped.");
}
```

### <a name="custom-images"></a>사용자 지정 이미지

IOS의 탭 이미지와 마찬가지로 메뉴 항목 이미지에는 배경을 통해 표시할 수 있는 알파 채널의 불투명 패턴이 필요 합니다.

최상의 성능을 위해 메뉴에 사용 되는 이미지를 watch 앱 확장 프로젝트가 아닌 watch 앱 프로젝트에 추가 해야 합니다.

## <a name="changing-the-menu-items"></a>메뉴 항목 변경

<!--
### Design Time Items

Menu items added the storyboard can be shown and hidden programmatically.
-->

### <a name="adding-at-runtime"></a>런타임에 추가

를 `Menu` `MenuItem` 프로그래밍 방식으로 변경할 *수* 있지만 런타임에를 인터페이스 컨트롤러에 추가할 수는 없습니다.
다음과 같이 메서드를 사용 합니다 `AddMenuItem` .

```csharp
AddMenuItem (WKMenuItemIcon.Accept, "Yes", new ObjCRuntime.Selector ("tapped"));
```

Xamarin.ios Watch 키트 API는 현재 `selector` 메서드에 대 한가 필요 하며 `AdMenuItem` ,이는 다음과 같이 선언 해야 합니다.

```csharp
[Export("tapped")]
void MenuItemTapped ()
{
    Console.WriteLine ("The dynamically added 'Yes' menu item was tapped.");
}
```

### <a name="removing-at-runtime"></a>런타임에 제거

`ClearAllMenuItems`메서드를 호출 하 여 *프로그래밍 방식으로 추가* 된 모든 메뉴 항목을 제거할 수 있습니다.

스토리 보드에서 구성 된 메뉴 항목은 지울 수 없습니다.

## <a name="related-links"></a>관련 링크

- [WatchKitCatalog (샘플)](/samples/xamarin/ios-samples/watchos-watchkitcatalog)
- [Apple의 메뉴 문서](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/Menus.html)
---
title: Xamarin.ios의 macOS 사용자 인터페이스 컨트롤
description: 이 문서는 Xamarin.ios 개발자에 게 제공 되는 다양 한 사용자 인터페이스 컨트롤을 설명 하는 가이드로 연결 됩니다. 연결 된 콘텐츠는 창, 대화 상자, 경고, 메뉴, 도구 모음, 테이블 보기, 개요 보기 등을 살펴봅니다.
ms.prod: xamarin
ms.assetid: 876B6EC2-E158-43F2-B9C9-03F54F3D2A49
ms.technology: xamarin-mac
author: davidortinau
ms.author: daortin
ms.date: 03/27/2018
ms.openlocfilehash: 7ae33883b83a4080903b524ea78e0da009ad0a3a
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91431530"
---
# <a name="macos-user-interface-controls-in-xamarinmac"></a>Xamarin.ios의 macOS 사용자 인터페이스 컨트롤

_이 문서는 다양 한 macOS UI 컨트롤을 설명 하는 가이드로 연결 됩니다._

Xamarin.ios 응용 프로그램에서 c # 및 .NET으로 작업 하는 경우 *목표-C* 및 *Xcode* 에서 작업 하는 개발자가 동일한 사용자 인터페이스 컨트롤에 액세스할 수 있습니다. Xamarin.ios는 Xcode와 직접 통합 되므로 Xcode의 _Interface Builder_ 를 사용 하 여 사용자 인터페이스를 만들고 유지 관리할 수 있습니다 (또는 필요에 따라 c # 코드에서 직접 만들 수 있음).

아래에 나열 된 가이드는 Xamarin.ios 응용 프로그램에서 macOS UI 요소를 사용 하는 방법에 대 한 자세한 정보를 제공 합니다. [Hello, Mac](~/mac/get-started/hello-mac.md) 문서를 먼저 사용 하는 것이 좋습니다. 특히 [Xcode 및 Interface Builder](~/mac/get-started/hello-mac.md#introduction-to-xcode-and-interface-builder) 및 [콘센트 및 작업](~/mac/get-started/hello-mac.md#outlets-and-actions) 섹션을 소개 하 고, 모든 문서에서 사용할 주요 개념 및 기술을 설명 하 고 있습니다.

C # 클래스를 대상으로 하는 c # 클래스 [/메서드](~/mac/internals/how-it-works.md#exposing-c-classes--methods-to-objective-c) 를 목표- [Xamarin.Mac Internals](~/mac/internals/how-it-works.md) `Register` `Export` c 개체 및 UI 요소에 연결 하는 데 사용 되는 및 특성에 대해 설명 하 고 있습니다.

## <a name="windows"></a>[Windows](~/mac/user-interface/window.md)

이 문서에서는 Xamarin.ios 응용 프로그램에서 창과 패널을 사용 하는 방법을 설명 합니다. Xcode 및 Interface Builder에서 창과 패널을 만들고 유지 관리 하 고, windows를 사용 하 고, c # 코드에서 windows에 응답 하 여 xib 파일에서 창과 패널을 로드 하는 방법을 다룹니다.

## <a name="dialogs"></a>[다이얼로그](~/mac/user-interface/dialog.md)

이 문서에서는 Xamarin.ios 응용 프로그램에서 대화 상자 및 모달 창을 사용 하는 방법을 설명 합니다. Xcode 및 Interface Builder에서 모달 창을 만들고 유지 관리 하 고, 표준 대화 상자를 사용 하 고, c # 코드에서 windows를 표시 하 고 응답 하는 방법을 다룹니다.

## <a name="alerts"></a>[경고](~/mac/user-interface/alert.md)

이 문서에서는 Xamarin.ios 응용 프로그램에서 경고를 사용 하는 방법을 설명 합니다. C # 코드에서 경고를 생성 및 표시 하 고 경고에 응답 하는 과정을 다룹니다.

## <a name="menus"></a>[메뉴](~/mac/user-interface/menu.md)

메뉴는 Mac 응용 프로그램의 사용자 인터페이스에서 다양 한 부분에 사용 됩니다. 화면 맨 위에 있는 응용 프로그램의 주 메뉴에서 창에 표시 될 수 있는 팝업 메뉴 및 상황에 맞는 메뉴를 표시 합니다. 메뉴는 Mac 애플리케이션의 사용자 환경에서 필수 요소입니다. 이 문서에서는 Xamarin.ios 응용 프로그램에서 Cocoa 메뉴를 사용 하는 방법을 설명 합니다.

## <a name="standard-controls"></a>[표준 컨트롤](~/mac/user-interface/standard-controls.md)

Xamarin.ios 응용 프로그램에서 단추, 레이블, 텍스트 필드, 확인란 및 분할 된 컨트롤과 같은 표준 AppKit 컨트롤을 사용 합니다. 이 가이드에서는 Xcode의 Interface Builder에서 사용자 인터페이스 디자인에 추가 하 고, 콘센트 및 작업을 통해 코드에 노출 하 고, c # 코드에서 AppKit 컨트롤을 사용 하는 방법을 설명 합니다.

## <a name="toolbars"></a>[도구 모음](~/mac/user-interface/toolbar.md)

이 문서에서는 Xamarin.ios 응용 프로그램의 도구 모음 작업을 설명 합니다. Xcode 및 Interface Builder에서 도구 모음을 만들고 유지 관리 하는 방법, 콘센트 및 작업을 사용 하 여 코드에 도구 모음 항목을 표시 하 고, 도구 모음 항목을 활성화 및 비활성화 하 고, 마지막으로 c # 코드에서 도구 모음 항목에 응답

## <a name="table-views"></a>[테이블 보기](~/mac/user-interface/table-view.md)

이 문서에서는 Xamarin.ios 응용 프로그램의 테이블 뷰 작업을 설명 합니다. Xcode 및 Interface Builder에서 테이블 뷰를 만들고 유지 관리 하는 방법, 콘센트 및 동작을 사용 하 여 코드에 테이블 뷰 항목을 노출 하는 방법, 테이블 뷰 채우기, c # 코드의 테이블 뷰 항목에 대 한 응답 등을 다룹니다.

## <a name="outline-views"></a>[개요 보기](~/mac/user-interface/outline-view.md)

이 문서에서는 Xamarin.ios 응용 프로그램에서 개요 보기를 사용 하는 방법을 설명 합니다. Xcode 및 Interface Builder에서 개요 보기를 만들고 유지 관리 하는 방법, 콘센트 및 작업을 사용 하 여 코드에 개요 보기 항목을 노출 하는 방법, 개요 뷰 채우기 및 c # 코드의 개요 보기 항목에 응답 하는 방법을 다룹니다.

## <a name="source-lists"></a>[소스 목록](~/mac/user-interface/source-list.md)

이 문서에서는 Xamarin.ios 응용 프로그램의 원본 목록 작업에 대해 설명 합니다. Xcode 및 Interface Builder에서 소스 목록을 만들고 유지 관리 하는 방법, 콘센트 및 작업을 사용 하 여 소스 목록 항목을 코드에 노출 하 고, 소스 목록을 채우고, c # 코드에서 소스 목록 항목에 응답 하는 방법에 대해 설명 합니다.

## <a name="collection-views"></a>[컬렉션 뷰](~/mac/user-interface/collection-view.md)

이 문서에서는 Xamarin.ios 응용 프로그램에서 컬렉션 보기를 사용 하는 방법을 설명 합니다. Xcode 및 Interface Builder에서 컬렉션 뷰를 만들고 유지 관리 하는 방법, 콘센트 및 작업을 사용 하 여 코드에 컬렉션 뷰 항목을 노출 하는 방법, 컬렉션 뷰 채우기, c # 코드의 컬렉션 뷰에 응답 하는 방법에 대해 설명 합니다.

## <a name="creating-custom-controls"></a>[사용자 지정 컨트롤 만들기](~/mac/user-interface/custom-controls.md)

이 문서에서는에서 상속 하 여 사용자 지정 사용자 인터페이스 컨트롤을 만들고 `NSControl` , 컨트롤에 대 한 사용자 지정 인터페이스를 그리거나, Xcode의 Interface Builder와 함께 사용할 수 있는 사용자 지정 작업을 만드는 방법을 설명 합니다.

## <a name="mac-samples-gallery"></a>Mac 샘플 갤러리

[Mac 샘플 갤러리](/samples/browse/?products=xamarin&term=Xamarin.Mac)를 살펴보는 것도 좋습니다. 여기에는 Xamarin.ios 프로젝트를 신속 하 게 시작 하는 데 도움이 되는 다양 한 바로 사용할 수 있는 코드가 포함 되어 있습니다.

## <a name="related-links"></a>관련 링크

- [macOS 휴먼 인터페이스 지침](https://developer.apple.com/macos/human-interface-guidelines/overview/themes/)
---
title: Xamarin에서 tvOS 단추 사용
description: 이 문서에서는 Xamarin에 내장 된 tvOS 앱에서 단추를 사용 하는 방법을 설명 합니다. 스토리 보드 및 코드에서 단추를 사용 하는 방법에 설명 하 고 단추 스타일을 지정 하는 방법을 검사 합니다.
ms.prod: xamarin
ms.assetid: DA6EF400-A4E3-4245-A0D4-F2398CAE2C9B
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/07/2017
ms.openlocfilehash: 6d8fc1daaced24dccead78c4f9d0e5d0959b3755
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61199072"
---
# <a name="working-with-tvos-buttons-in-xamarin"></a>Xamarin에서 tvOS 단추 사용

인스턴스를 사용 합니다 `UIButton` tvOS 창의 포커스를 선택할 수 있는 단추를 만들려면 클래스입니다. 대상 개체에 동작 메시지를 보내는 사용자가 단추를 선택 하면 사용자에 게 응답 하 여 Xamarin.tvOS 앱의 입력을 허용 합니다.

[![](buttons-images/buttons01.png "예제에서는 단추")](buttons-images/buttons01.png#lightbox)

Siri 원격을 사용 하 여 탐색 및 포커스 작업에 대 한 자세한 내용은 참조 하십시오 우리의 [탐색 및 포커스 작업](~/ios/tvos/app-fundamentals/navigation-focus.md) 하 고 [Siri 원격 및 Bluetooth 컨트롤러](~/ios/tvos/platform/remote-bluetooth.md) 설명서.

<a name="About-Buttons" />

## <a name="about-buttons"></a>단추 정보

TvOS 단추 앱 별 작업에 사용 됩니다 하 고 제목, 아이콘 또는 둘 다 포함 될 수 있습니다. 사용자 앱의 사용자 인터페이스를 사용 하 여 탐색 하면서를 [Siri 원격](~/ios/tvos/platform/remote-bluetooth.md#The-Siri-Remote), 텍스트 및 배경색을 변경할 수 있도록 지정된 된 단추 포커스가 이동 합니다. 그림자 효과 추가 하면 3D 사용자 인터페이스의 나머지 부분을 극복 하기 표시 되 게 단추에도 적용 됩니다.

[![](buttons-images/buttons01.png "예제에서는 단추")](buttons-images/buttons01.png#lightbox)

Apple에 단추를 사용 하 여 작업 하기 위한 다음 제안에 있습니다.

- **에 제목을 또는 아이콘을 사용 하 여** -는 두 아이콘 단추에 제목을 포함 될 수 있습니다를 좌석이 제한 되어 있으므로 해 둘 다를 결합 합니다.
- **명확 하 게 표시 파괴적 단추** -단추 수행 안전 하지 않은 경우 (예: 파일 삭제) 작업에 따라서 텍스트 및/또는 아이콘을 사용 하 여 항목을 명확 하 게 표시 합니다. 삭제 작업은 항상을 [경고](~/ios/tvos/user-interface/alerts.md) 사용자에 게 작업을 제한 하 합니다.
- **뒤로 단추 사용 안 함** -Siri 원격 The 메뉴 단추를 사용 하 여 이전 화면으로 반환 하 합니다. 이 규칙의 한 가지 예외는 앱 내 구매 또는 삭제 작업에 대 한 위치를 **취소** 단추를 표시 해야 합니다.

포커스 및 탐색 작업에 대 한 자세한 내용은 참조 하십시오 우리의 [탐색 및 포커스 작업](~/ios/tvos/app-fundamentals/navigation-focus.md) 설명서.

<a name="Button-Icons" />

### <a name="button-icons"></a>단추 아이콘

Apple에 단추 아이콘에 대 한 간단 하 고 항상 인식할 수 있는 이미지를 사용 하는 것을 제안 합니다. 지나치게 복잡 한 아이콘을 couch에서 대화방에서 TV 화면에서 인식, 따라서 가장 간단한 표현 아이디어를 얻을 수를 사용 하려고 하기 어려운 합니다. 가능 하면 표준을 사용 하 여, 잘 알려진 아이콘 (예: 검색 돋보기)에 대 한 이미지입니다.

<a name="Button-Titles" />

### <a name="button-titles"></a>단추 제목

Apple 단추에 대 한 제목을 만들 때 다음 제안에 있습니다.

- **아이콘 단추 아래 설명 텍스트를 표시** -가능한 한 명확 하 고 설명이 포함 된 텍스트를 아래 아이콘 위치 에서만 단추 추가 get에서 단추의 용도 하는 경우.
- **제목에 동사 또는 동사 구 사용할** -사용자 단추를 클릭할 때 명확 하는 데 필요한 작업을 배치 합니다.
- **제목 스타일 대/소문자를 사용 하 여** -문서, 결합 또는 전치사를 제외 하 고 (네 글자 이하의), 단추의 제목의 모든 단어는 대문자로 시작 해야 합니다.
- **짧은, 지점에 제목을 사용 하 여** -단추의 동작을 설명 하는 가장 짧은 가능한 스크립트를 사용 합니다.

<a name="Buttons-and-Storyboards" />

## <a name="buttons-and-storyboards"></a>단추 및 스토리 보드

Xamarin.tvOS 앱에서 단추를 사용 하는 가장 쉬운 방법은 Xamarin 디자이너를 사용 하 여 iOS 용 앱의 UI에 추가할 경우

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)


1. 에 **솔루션 탐색기**를 두 번 클릭 합니다 `Main.storyboard` 파일을 편집용으로 엽니다.
1. 끌어서를 **단추** 에서 **라이브러리** 보기에 놓습니다. 

    [![](buttons-images/storyboard01.png "단추")](buttons-images/storyboard01.png#lightbox)
1. 에 **속성 탐색기**와 같은 여러 단추의 속성을 조정할 수 있습니다 해당 **제목** 하 고 **텍스트 색**: 

    [![](buttons-images/storyboard02.png "단추 속성")](buttons-images/storyboard02.png#lightbox)
1. 다음으로 전환 하는 **이벤트 탭** 및 연결을 **이벤트** 에서 **단추** 호출 `ButtonPressed`: 

    [![](buttons-images/storyboard03.png "이벤트 탭")](buttons-images/storyboard03.png#lightbox)
1. 하면 자동으로 전환 됩니다는 `ViewController.cs` 뷰를 사용 하 여 코드에서 새 작업을 배치할 수 있습니다 합니다 **위로** 및 **아래로** 화살표 키: 

    [![](buttons-images/storyboard04.png "새 작업을 코드에 배치")](buttons-images/storyboard04.png#lightbox)
1. 키를 눌러 합니다 **Enter** 위치를 선택 하려면: 

    [![](buttons-images/storyboard05.png "코드 편집기")](buttons-images/storyboard05.png#lightbox)
1. 모든 파일에 변경 내용을 저장 합니다.


# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

1. 에 **솔루션 탐색기**를 두 번 클릭 합니다 `Main.storyboard` 파일을 편집용으로 엽니다.
1. 끌어서를 **단추** 에서 **라이브러리** 보기에 놓습니다. 

    [![](buttons-images/storyboard01vs.png "단추")](buttons-images/storyboard01vs.png#lightbox)
1. 에 **속성 탐색기**와 같은 여러 단추의 속성을 조정할 수 있습니다 해당 **제목** 하 고 **텍스트 색**: 

    [![](buttons-images/storyboard02vs.png "속성 탐색기")](buttons-images/storyboard02vs.png#lightbox)
1. 다음으로 전환 하는 **이벤트 탭** 및 연결을 **이벤트** 에서 **단추** 호출 `ButtonPressed`: 

    [![](buttons-images/storyboard03vs.png "이벤트 탭")](buttons-images/storyboard03vs.png#lightbox)
1. 모든 파일에 변경 내용을 저장 합니다.



편집 보기 컨트롤러 (예제 `ViewController.cs`) 파일을 선택 된 단추를 처리 하는 다음 코드를 추가 합니다.


```

using System;
using UIKit;

namespace tvRemote
{
    public partial class ViewController : UIViewController
    {
        ...

        partial void ButtonPressed (UIButton sender) {
            // Handle click here
            ...
        }
    }
}

```

-----

단추의 오랫동안 `Enabled` 속성은 `true` 다른 컨트롤이 나 보기에서 다루지 않은, 포커스 내 항목 Siri 원격을 사용 하 여 만들 수 있습니다. 사용자가 단추를 선택 하 고 터치 화면을 클릭 하는 경우는 `ButtonPressed` 위에 정의 된 작업이 실행 됩니다.

> [!IMPORTANT]
> 와 같은 작업을 할당할 수 있지만 `TouchUpInside` 에 `UIButton` iOS 디자이너를 만들 때에 **이벤트 처리기**, Apple TV 화면 또는 터치 이벤트를 지 원하는 터치 없기 때문에 되지 호출 됩니다. 항상 기본값을 사용 해야 **동작 유형** 만들면 **동작** tvOS 사용자 인터페이스 요소에 대 한 합니다.




스토리 보드를 사용 하 여 작업에 대 한 자세한 내용은 참조 하십시오 우리의 [Tvos 빠른 시작 가이드](~/ios/tvos/get-started/hello-tvos.md)합니다.

<a name="Buttons-and-Code" />

## <a name="buttons-and-code"></a>단추 및 코드

필요에 따라 한 `UIButton` 에서 만들 수 있습니다 C# 코드 및 tvOS 앱의 보기에 추가 합니다. 예를 들어:

```csharp
var button = new UIButton(UIButtonType.System);
button.Frame = new CGRect (25, 25, 300, 150);
button.SetTitle ("Hello", UIControlState.Normal);
button.AllEvents += (sender, e) => {
    // Do something when the button is clicked
    ...
};
View.AddSubview (button);
```

새로 만들 때 `UIButton` 지정할 코드에서 해당 `UIButtonType` 으로 다음 중 하나:

- **시스템** -tvOS에서 제공 되는 단추의 표준 종류 이며 가장 자주 사용 하는 형식입니다.
- **DetailDisclosure** -숨기 거 나 자세한 정보를 표시 하는 데 사용 되는 단추의 형식을 "해제"를 표시 합니다.
- **InfoDark** -진한 원 "i" 단추를 표시 하는 정보를 자세히 설명 합니다.
- **InfoLight** -광원 원 "i" 단추를 표시 하는 정보를 자세히 설명 합니다.
- **AddContact** -단추는 연락처 추가 단추를 표시 합니다.
- **사용자 지정** -단추의 여러 특성을 사용자 지정할 수 있습니다.

그런 다음, 화면 크기 정의 및 단추의 위치 합니다. 예제:

```csharp
button.Frame = new CGRect (25, 25, 300, 150);
```

그런 다음 단추에 대 한 제목을 설정 합니다. `UIButtons` 대부분 다릅니다 `UIKit` 제목의 변경할 수 있으므로 간단히 수 없는 상태를 포함 된 컨트롤에 대 한 변경 해야 할는 주어진 `UIControlState`합니다. 예를 들어:

```csharp
button.SetTitle ("Hello", UIControlState.Normal);
```

다음을 사용 하 여는 `AllEvents` 이벤트를 사용자가 단추를 클릭 하는 경우를 참조 하세요. 예제:

```csharp
button.AllEvents += (sender, e) => {
    // Do something when the button is clicked
    ...
};
```

뷰를 표시 하려면 단추를 추가 하는 마지막으로,

```csharp
View.AddSubview (button);
```

> [!IMPORTANT]
> 와 같은 작업을 할당할 수 있지만 `TouchUpInside` 에 `UIButton`, Apple TV 화면 또는 터치 이벤트를 지 원하는 터치 없기 때문에 되지 호출 됩니다. 항상 사용 해야 이벤트와 같은 **AllEvents** 하거나 **PrimaryActionTriggered**합니다.




<a name="Styling-a-Button" />

## <a name="styling-a-button"></a>단추 스타일 지정

tvOS의 여러 속성을 제공 된 `UIButton` 제목을 제공 배경색 및 이미지 등을 사용 하 여 스타일을 사용할 수 있는 합니다.

<a name="Button-Titles" />

### <a name="button-titles"></a>단추 제목

위에서 살펴본 것 처럼 `UIButtons` 대부분 다릅니다 `UIKit` 제목의 변경할 수 있으므로 간단히 수 없는 상태를 포함 된 컨트롤에 대 한 변경 해야 할는 지정 된 `UIControlState`합니다. 예를 들어:

```csharp
button.SetTitle ("Hello", UIControlState.Normal);
```

사용 하 여 단추에 대 한 제목 색을 설정할 수는 `SetTitleColor` 메서드. 예를 들어:

```csharp
button.SetTitleColor (UIColor.White, UIControlState.Normal);
```

타이틀의 조정할 수 있습니다 사용 하 여 그림자를 `SetTitleShadowColor`입니다. 예를 들어:

```csharp
button.SetTitleShadowColor(UIColor.Black, UIControlState.Normal);
```

제목 그림자를 변경 하려면 설정할 수 있습니다 *Engraved* 하 *볼록* 단추는 다음 코드를 사용 하 여 강조 표시 하는 경우:

```csharp
button.ReverseTitleShadowWhenHighlighted = true;
```

또한 단추의 제목으로 특성이 지정 된 텍스트를 사용할 수 있습니다. 예를 들어:

```csharp
var normalAttributedTitle = new NSAttributedString (buttonTitle, foregroundColor: UIColor.Blue, strikethroughStyle: NSUnderlineStyle.Single);
myButton.SetAttributedTitle (normalAttributedTitle, UIControlState.Normal);

var highlightedAttributedTitle = new NSAttributedString (buttonTitle, foregroundColor: UIColor.Green, strikethroughStyle: NSUnderlineStyle.Thick);
myButton.SetAttributedTitle (highlightedAttributedTitle, UIControlState.Highlighted);
```

### <a name="button-images"></a>단추 이미지

`UIButton` 연결 된 이미지를 가질 수 있으며 해당 배경으로 이미지를 사용할 수 있습니다.

단추에 배경 이미지를 설정 하는 지정 된 `UIControlState`, 다음 코드를 사용 하 여:

```csharp
button.SetBackgroundImage(UIImage.FromFile("my image.png"), UIControlState.Normal);
```

설정 된 `AdjustsImageWhenHiglighted` 속성을 `true` 이미지를 그릴 밝은 단추를 강조 표시 되 면 (기본값임). 설정 된 `AdjustsImageWhenDisabled` 속성을 `true` 이미지를 그릴 음영이 짙을 수록 단추가 비활성화 되는 경우 (다시이 기본값임).

단추에 표시할 이미지를 설정 하려면 다음 코드를 사용 합니다.

```csharp
button.SetImage(UIImage.FromFile("my image.png"), UIControlState.Normal);
```

사용 된 `TintColor` 제목과 단추의 이미지 모두에 적용 되는 색 농도 설정 하는 속성입니다. 단추에 대 한 합니다 `Custom` 형식,이 속성에 영향을 주지 않습니다, 구현 해야 합니다는 `TintColor` 동작 직접.

<a name="Summary" />

## <a name="summary"></a>요약

이 문서에서는 디자인 및 Xamarin.tvOS 앱 내에서 단추를 사용 하 여 작업 검사가 수행 합니다. IOS 디자이너에서에서 단추를 사용 하는 방법 및 단추를 만드는 방법에 알아보았습니다 C# 코드입니다. 마지막으로 단추의 제목을 수정 하 고 해당 모양과 스타일을 변경 하는 방법에 알아보았습니다.



## <a name="related-links"></a>관련 링크

- [tvOS 샘플](https://developer.xamarin.com/samples/tvos/all/)
- [tvOS](https://developer.apple.com/tvos/)
- [tvOS 휴먼 인터페이스 지침](https://developer.apple.com/tvos/human-interface-guidelines/)
- [TvOS 앱 프로그래밍 가이드](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/)

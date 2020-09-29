---
title: Xamarin.ios의 고급 메시지 앱 확장
description: 이 문서에서는 메시지 앱과 통합 되 고 사용자에 게 새로운 기능을 제공 하는 Xamarin.ios 솔루션에서 메시지 앱 확장을 사용 하는 고급 기술을 보여 줍니다.
ms.prod: xamarin
ms.assetid: 394A1FDA-AF70-4493-9B2C-4CFE4BE791B6
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/16/2017
ms.openlocfilehash: 8a1f386209ccc1f2cb33348930f29bf5ac65ce4f
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91435616"
---
# <a name="advanced-message-app-extensions-in-xamarinios"></a>Xamarin.ios의 고급 메시지 앱 확장

_이 문서에서는 메시지 앱과 통합 되 고 사용자에 게 새로운 기능을 제공 하는 Xamarin.ios 솔루션에서 메시지 앱 확장을 사용 하는 고급 기술을 보여 줍니다._

IOS 10의 새로운 기능으로, 메시지 앱 확장은 **메시지** 앱과 통합 되며 사용자에 게 새로운 기능을 제공 합니다. 확장은 텍스트, 스티커, 미디어 파일 및 대화형 메시지를 보낼 수 있습니다.

## <a name="about-message-app-extensions"></a>메시지 앱 확장 정보

위에서 설명한 것 처럼 메시지 앱 확장은 **메시지** 앱과 통합 되며 사용자에 게 새로운 기능을 제공 합니다. 확장은 텍스트, 스티커, 미디어 파일 및 대화형 메시지를 보낼 수 있습니다. 다음과 같은 두 가지 유형의 메시지 앱 확장을 사용할 수 있습니다.

- **스티커 팩** -사용자가 메시지에 추가할 수 있는 스티커의 컬렉션을 포함 합니다. 스티커 팩은 코드를 작성 하지 않고도 만들 수 있습니다.
- **IMessage apps** -스티커를 선택 하 고, 미디어 파일 (선택적 형식 변환 포함)을 포함 하 여 텍스트를 입력 하 고, 상호 작용 메시지를 만들고 편집 하 고 보내는 메시지 앱 내에 사용자 지정 사용자 인터페이스를 제공할 수 있습니다.

메시지 앱 확장은 세 가지 주요 내용 유형을 제공 합니다.

- **대화형 메시지** -앱이 생성 하는 사용자 지정 메시지 콘텐츠의 형식으로, 사용자가 메시지를 탭 하면 응용 프로그램이 포그라운드에서 시작 됩니다.
- **스티커** -사용자 간에 전송 된 메시지에 포함할 수 있는 앱에 의해 생성 된 이미지입니다. 스티커 팩 앱을 구현 하는 예제는 [Ice (Ice) 빌더](/samples/xamarin/ios-samples/ios10-icecreambuilder) 샘플 앱을 참조 하세요.
- **기타 지원 되는 콘텐츠** -앱은 메시지 앱에서 항상 지원 되는 형식의 사진, 비디오, 텍스트 또는 링크와 같은 콘텐츠를 제공할 수 있습니다.

IOS 10의 새로운 기능으로, 이제 메시지 앱은 자체의 전용 기본 제공 앱 스토어를 포함 합니다. 메시지 앱 확장을 포함 하는 모든 앱이이 저장소에 표시 되 고 승격 됩니다. 새 메시지 앱 서랍에는 사용자에 게 신속 하 게 액세스할 수 있도록 메시지 앱 스토어에서 다운로드 한 앱이 표시 됩니다.

IOS 10 에서도 새로 추가 된 Apple에는 사용자가 앱을 쉽게 검색할 수 있도록 하는 인라인 앱 특성이 추가 되었습니다. 예를 들어 한 사용자가 두 번째 사용자가 설치 하지 않은 앱에서 다른 사용자에 게 콘텐츠를 전송 하는 경우 (예: 스티커) 보내는 앱의 이름이 메시지 기록의 내용에 나열 됩니다. 사용자가 앱의 이름을 탭 하면 메시지 앱 스토어가 열리고 앱이 스토어에서 선택 됩니다.

메시지 앱 확장은 개발자가 작성 하는 데 익숙한 기존 iOS 앱과 비슷하며 표준 iOS 앱의 모든 표준 프레임 워크 및 기능에 액세스할 수 있습니다. 다음은 그 예입니다.

- 앱 내 구매에 액세스할 수 있습니다.
- Apple Pay에 대 한 액세스 권한이 있습니다.
- 카메라와 같은 장치 하드웨어에 액세스할 수 있습니다.

메시지 앱 확장은 iOS 10 에서만 지원 됩니다. 그러나 이러한 확장에서 전송 하는 콘텐츠는 watchOS 및 macOS 장치에서 볼 수 있습니다. WatchOS 3에 추가 된 새 _최근 페이지_ 에는 메시지 앱 확장의 항목을 비롯 하 여 휴대폰에서 전송 된 최근 스티커가 표시 되 고 사용자가이 스티커를 시청에서 보낼 수 있습니다.

## <a name="about-interactive-messages"></a>대화형 메시지 정보

대화형 메시지는 사용자 지정 메시지 거품형을 제공 하며 메시지 앱 확장에서 제공 됩니다. 사용자가 대화형 메시지 콘텐츠를 만들고 메시지 입력 필드에 삽입 한 후 보낼 수 있습니다.

[![대화형 메시지 콘텐츠 만들기](advanced-message-app-extensions-images/interactive01.png)](advanced-message-app-extensions-images/interactive01.png#lightbox)

받는 사용자는 메시지 기록에서 메시지 거품형을 탭 하 여 대화형 메시지에 회신할 수 있습니다. 메시지 앱 확장을 로드 합니다. 확장은 전체 화면으로 시작 되며 사용자가 회신을 작성 하 여 원래 사용자에 게 다시 보낼 수 있습니다.

[![전체 화면으로 시작 된 확장](advanced-message-app-extensions-images/interactive02.png)](advanced-message-app-extensions-images/interactive02.png#lightbox)

다음 항목에 대해서는 아래에서 자세히 설명 합니다.

- 메시지 API 개요
- 확장 수명 주기
- 메시지 작성
- 메시지 보내기

## <a name="messages-api-overview"></a>메시지 API 개요

사용자가 호출 하면 메시지 앱 확장이 압축 보기 모드의 메시지 기록 아래쪽에 표시 됩니다.

[![메시지 API 개요](advanced-message-app-extensions-images/interactive03.png)](advanced-message-app-extensions-images/interactive03.png#lightbox)

1. `MSMessageAppViewController`메시지 앱 확장의 개체는 확장의 뷰가 사용자에 게 표시 될 때 호출 되는 주 클래스입니다.
2. 대화는 사용자에 게 개체 인스턴스로 제공 됩니다 `MSConversation` .
3. `MSMessage`클래스는 대화의 지정 된 메시지 거품형을 나타냅니다.
4. `MSSession` 메시지를 보내는 방법을 제어 합니다.
5. `MSMessageTemplateLayout` 메시지가 표시 되는 방식을 제어 합니다.

## <a name="the-extension-lifecycle"></a>확장 수명 주기

활성화 되는 메시지 앱 확장 프로세스를 살펴보겠습니다.

[![메시지 앱 확장을 활성화 하는 프로세스입니다.](advanced-message-app-extensions-images/interactive04.png)](advanced-message-app-extensions-images/interactive04.png#lightbox)

1. 앱 서랍에서와 같이 확장이 시작 되 면 메시지 앱이 프로세스를 시작 합니다.
2. `DidBecomeActive`메서드를 호출 하 고 `MSConversation` 메시지 앱 확장이 실행 되는 대화를 나타내는를 전달 합니다.
3. 확장은 둘 다를 기반으로 하기 때문에를 `UIViewController` `ViewWillAppear` `ViewDidAppear` 호출 합니다.

다음으로 비활성화 되는 메시지 앱 확장 프로세스를 살펴보겠습니다.

[![메시지 앱 확장을 비활성화 하는 프로세스입니다.](advanced-message-app-extensions-images/interactive05.png)](advanced-message-app-extensions-images/interactive05.png#lightbox)

1. 메시지 앱 확장을 비활성화 하는 경우 `ViewWillDisappear` 메서드가 먼저 호출 됩니다.
2. 그런 다음 `ViewDidDisappear` 메서드가 호출 됩니다.
3. `WillResignActive`메서드를 호출 하 고 `MSConversation` 메시지 앱 확장이 실행 되는 대화를 나타내는를 전달 합니다. 이 시점에서 메시지 앱과 확장의 연결을 해제 하려고 합니다.
4. 나중에 메시지 앱이 프로세스를 종료 합니다.

확장은 수명이 짧은 프로세스 이므로 시스템에서 처리 및 배터리 전원을 절약 하기 위해 적극적으로 종료 됩니다. 개발자는 메시지 앱 확장을 디자인 하 고 구현할 때이 점을 염두에 두어야 합니다.

## <a name="composing-a-message"></a>메시지 작성

메시지 앱 확장이 프로세스에서 실행 중이 고 해당 사용자 인터페이스를 표시 한 후에는 다음 코드를 사용 하 여 새 메시지를 작성할 수 있습니다.

```csharp
MSMessage ComposeMessage (IceCream iceCream, string caption, MSSession session = null)
{
    var components = new NSUrlComponents {
        QueryItems = iceCream.QueryItems
    };

    var layout = new MSMessageTemplateLayout {
        Image = iceCream.RenderSticker (true),
        Caption = caption
    };

    var message = new MSMessage (session ?? new MSSession()) {
        Url = components.Url,
        Layout = layout
    };

    return message;
}
```

이 코드는 새를 만들고 `MSMessage` 여러 속성을 설정 합니다 (예: `Url` ). IOS 에서만 메시지를 만들 수 있지만 표시 되려면 iOS와 macOS 모두에 메시지를 보낼 수 있습니다.

사용자가 macOS에서 대화의 메시지 버블을 클릭 하면 Mac이 웹 브라우저에서 URL에 지정 된 주소를 열려고 시도 합니다. 따라서 개발자의 웹 사이트는 macOS 기반 컴퓨터의 웹 브라우저에서 메시지의 일부 표시를 표시할 수 있어야 합니다.

`AccessibilityLabel`속성은 화면 판독기에서 사용자에 대 한 대화의 기록을 읽는 데 사용 됩니다. `Layout`속성은 메시지가 표시 되는 방법을 지정 합니다. 현재만 `MSMessageTemplateLayout` 지원 되며 다음과 같습니다.

[![MSMessageTemplateLayout 템플릿](advanced-message-app-extensions-images/interactive06.png)](advanced-message-app-extensions-images/interactive06.png#lightbox)

`Image`의 속성은 `MSMessageTemplateLayout` 화면에 messagebubble의 본문에 대 한 콘텐츠를 제공 합니다. `MediaFileUrl`또한 속성은 메시지 거품형의 본문에 대 한 콘텐츠를 제공 하지만에서 지원 하지 않는 콘텐츠 `UIImage` (예: 백그라운드에서 반복 되는 비디오 파일)를 허용 합니다. `Image`및 `MediaFileUrl` 속성이 모두 제공 되는 경우 `Image` 속성이 우선적으로 적용 됩니다. 는 `MediaFileUrl` PNG, JPEG, GIF 및 비디오 (Media Player 프레임 워크에서 재생할 수 있는 모든 형식) 미디어 형식을 지원 합니다.

3 배 해상도의 권장 미디어 크기는 300 x 300 픽셀입니다. 약간 더 크고 작은 자산도 수락 되며 Apple에서 최상의 결과를 얻기 위해 몇 가지 크기의 테스트를 제안 합니다. 메시지 앱은 필요에 따라이 미디어를 다운 샘플링 하 고 크기를 조정 합니다.

자산이 받는 사람에 게 전송 되 면 연결 된 모든 미디어는 네트워크를 통해 전송 되는 것을 최적화 하기 위해 메시지 앱에 의해 자동으로 트랜스 코딩 됩니다. 이로 인해, 미디어는 전송을 위해 축소 되 고 압축 되기 때문에 메시지에 첨부 되는 미디어에는 텍스트를 포함 하는 것이 좋습니다. 따라서 illegible 텍스트를 렌더링 하는 경우도 있습니다.

`ImageTitle`및 `ImageSubtitle` 속성은 메시지 거품형에 표시 되는 미디어에 대 한 설명을 제공 합니다. 이러한 속성은 이미지의 왼쪽 아래 모서리에 crisply 렌더링 되는 수신 장치에 텍스트로 전송 됩니다.

`Caption`, `SubCaption` `TrailingCaption` 및 속성은 `TrailingSubcaption` 이미지에 대해 자세히 설명 하 고 이미지 아래의 섹션에서 렌더링 됩니다. 이러한 속성을 모두로 설정 `null` 하면 캡션 영역 없이 메시지 거품형이 생성 됩니다.

[![캡션 영역이 없는 메시지 거품형](advanced-message-app-extensions-images/interactive07.png)](advanced-message-app-extensions-images/interactive07.png#lightbox)

마지막으로 메시지 앱은 메시지 거품형의 왼쪽 위 모퉁이에 메시지 앱 확장 아이콘을 그립니다.

## <a name="sending-a-message"></a>메시지 보내기

를 구성한 후에는 `MSMessage` 다음 코드를 사용 하 여 메시지를 보낼 수 있습니다.

```csharp
public void SendMessage (MSMessage message)
{
    // Insert the message into the conversation
    ActiveConversation.InsertMessage (message, (error) => {
        // Did the message send successfully?
        if (error == null) {
            // Handle successful send
        } else {
            // Report Error
            Console.WriteLine ("Error: {0}", error);
        }
    };

}
```

`ActiveConversation`의 속성에는 `MSMessagesAppViewController` 메시지 앱 확장이 시작 된 현재 대화가 포함 됩니다.

의를 호출 `InsertMessage` `MSConversation` 하 여 대화에 메시지를 포함 하 고 발생할 수 있는 오류를 처리 합니다. 메시지가 성공적으로 포함 되 면 메시지 버블이 입력 필드에 표시 됩니다.

또한 확장은 다음과 같은 다양 한 유형의 데이터를 대화에 보낼 수 있습니다.

- **본문** - `ActiveConversation.InsertText ("Message", (error) => {...});`
- **첨부할** - `ActiveConversation.InsertAttachment (new NSUrl ("path"), "filename", (error) => {...});`
- **Stickers**  -  스티커 `ActiveConversation.InsertSticker (sticker, (obj) => {...});` 여기서 `sticker` 는입니다 `MSSticker` .

새 콘텐츠가 입력 필드에 있으면 사용자는 일반적인 메시지와 마찬가지로 파란색 **보내기** 단추를 눌러 메시지를 보낼 수 있습니다. 메시지 앱 확장에서 자동으로 콘텐츠를 보낼 수 있는 방법은 없습니다 .이 프로세스는 전적으로 사용자의 제어를 받고 있습니다.

## <a name="handling-the-compact-and-expanded-modes"></a>압축 및 확장 모드 처리

메시지 앱 확장은 다음 두 가지 보기 모드 중 하나로 표시 될 수 있습니다.

[![메시지 앱 확장은 다음 두 가지 보기 모드로 표시 됩니다. Compact & 확장 됨](advanced-message-app-extensions-images/interactive08.png)](advanced-message-app-extensions-images/interactive08.png#lightbox)

- **Compact** -메시지 앱 확장이 메시지 보기의 하위 25%를 차지 하는 기본 모드입니다. 압축 모드에서는 앱에 키보드, 가로 스크롤 또는 살짝 밀기 제스처 인식기에 대 한 액세스 권한이 없습니다. 앱은 입력 필드에 대 한 액세스 권한을 가지 며에 대 한 호출은 `InsertMessage` 사용자에 게 즉시 표시 됩니다.
- **확장** 됨-메시지 앱 확장은 전체 메시지 뷰를 채웁니다. 입력 필드에 대 한 액세스 권한은 없지만 키보드, 가로 스크롤 및 살짝 밀기 제스처 인식기에 대 한 액세스 권한이 있습니다.

메시지 앱 확장은 언제 든 지 사용자가 프로그래밍 방식으로 또는 수동으로 사용자가 수동으로 전환할 수 있으며, 보기 모드의 모든 변경 내용에 즉시 반응 해야 합니다.

두 가지 서로 다른 보기 모드 간의 전환을 처리 하는 다음 예를 살펴보겠습니다. 각 상태에는 두 개의 서로 다른 뷰 컨트롤러가 필요 합니다. 는 `StickerBrowserViewController` **Compact** 뷰를 처리 하 고는 `AddStickerViewController` **확장** 된 뷰를 처리 합니다.

```csharp
using System;

using Messages;
using Foundation;
using UIKit;

namespace MessagesExtension {
    public partial class MessagesViewController : MSMessagesAppViewController, IIceCreamsViewControllerDelegate, IBuildIceCreamViewControllerDelegate {
        public MessagesViewController (IntPtr handle) : base (handle)
        {
        }

        public override void WillBecomeActive (MSConversation conversation)
        {
            base.WillBecomeActive (conversation);

            // Present the view controller appropriate for the conversation and presentation style.
            PresentViewController (conversation, PresentationStyle);
        }

        public override void WillTransition (MSMessagesAppPresentationStyle presentationStyle)
        {
            var conversation = ActiveConversation;
            if (conversation == null)
                throw new Exception ("Expected an active converstation");

            // Present the view controller appropriate for the conversation and presentation style.
            PresentViewController (conversation, presentationStyle);
        }

        void PresentViewController (MSConversation conversation, MSMessagesAppPresentationStyle presentationStyle)
        {
            // Determine the controller to present.
            UIViewController controller;

            if (presentationStyle == MSMessagesAppPresentationStyle.Compact) {
                // Show a list of previously created ice creams.
                controller = InstantiateIceCreamsController ();
            } else {
                var iceCream = new IceCream (conversation.SelectedMessage);
                controller = iceCream.IsComplete ? InstantiateCompletedIceCreamController (iceCream) : InstantiateBuildIceCreamController (iceCream);
            }

            foreach (var child in ChildViewControllers) {
                child.WillMoveToParentViewController (null);
                child.View.RemoveFromSuperview ();
                child.RemoveFromParentViewController ();
            }

            AddChildViewController (controller);
            controller.View.Frame = View.Bounds;
            controller.View.TranslatesAutoresizingMaskIntoConstraints = false;
            View.AddSubview (controller.View);

            controller.View.LeftAnchor.ConstraintEqualTo (View.LeftAnchor).Active = true;
            controller.View.RightAnchor.ConstraintEqualTo (View.RightAnchor).Active = true;
            controller.View.TopAnchor.ConstraintEqualTo (View.TopAnchor).Active = true;
            controller.View.BottomAnchor.ConstraintEqualTo (View.BottomAnchor).Active = true;

            controller.DidMoveToParentViewController (this);
        }

        UIViewController InstantiateIceCreamsController ()
        {
            // Instantiate a `IceCreamsViewController` and present it.
            var controller = Storyboard.InstantiateViewController (IceCreamsViewController.StoryboardIdentifier) as IceCreamsViewController;
            if (controller == null)
                throw new Exception ("Unable to instantiate an IceCreamsViewController from the storyboard");

            controller.Builder = this;
            return controller;
        }

        UIViewController InstantiateBuildIceCreamController (IceCream iceCream)
        {
            // Instantiate a `BuildIceCreamViewController` and present it.
            var controller = Storyboard.InstantiateViewController (BuildIceCreamViewController.StoryboardIdentifier) as BuildIceCreamViewController;
            if (controller == null)
                throw new Exception ("Unable to instantiate an BuildIceCreamViewController from the storyboard");

            controller.IceCream = iceCream;
            controller.Builder = this;

            return controller;
        }

        public UIViewController InstantiateCompletedIceCreamController (IceCream iceCream)
        {
            // Instantiate a `BuildIceCreamViewController` and present it.
            var controller = Storyboard.InstantiateViewController (CompletedIceCreamViewController.StoryboardIdentifier) as CompletedIceCreamViewController;
            if (controller == null)
                throw new Exception ("Unable to instantiate an CompletedIceCreamViewController from the storyboard");

            controller.IceCream = iceCream;
            return controller;
        }

        public void DidSelectAdd (IceCreamsViewController controller)
        {
            Request (MSMessagesAppPresentationStyle.Expanded);
        }

        public void Build (BuildIceCreamViewController controller, IceCreamPart iceCreamPart)
        {
            var conversation = ActiveConversation;
            if (conversation == null)
                throw new Exception ("Expected a conversation");

            var iceCream = controller.IceCream;
            if (iceCream == null)
                throw new Exception ("Expected the controller to be displaying an ice cream");

            string messageCaption = string.Empty;
            var b = iceCreamPart as Base;
            var s = iceCreamPart as Scoops;
            var t = iceCreamPart as Topping;

            if (b != null) {
                iceCream.Base = b;
                messageCaption = "Let's build an ice cream";
            } else if (s != null) {
                iceCream.Scoops = s;
                messageCaption = "I added some scoops";
            } else if (t != null) {
                iceCream.Topping = t;
                messageCaption = "Our finished ice cream";
            } else {
                throw new Exception ("Unexpected type of ice cream part selected.");
            }

            // Create a new message with the same session as any currently selected message.
            var message = ComposeMessage (iceCream, messageCaption, conversation.SelectedMessage?.Session);

            // Add the message to the conversation.
            conversation.InsertMessage (message, null);

            // If the ice cream is complete, save it in the history.
            if (iceCream.IsComplete) {
                var history = IceCreamHistory.Load ();
                history.Append (iceCream);
                history.Save ();
            }

            Dismiss ();
        }

        MSMessage ComposeMessage (IceCream iceCream, string caption, MSSession session = null)
        {
            var components = new NSUrlComponents {
                QueryItems = iceCream.QueryItems
            };

            var layout = new MSMessageTemplateLayout {
                Image = iceCream.RenderSticker (true),
                Caption = caption
            };

            var message = new MSMessage (session ?? new MSSession()) {
                Url = components.Url,
                Layout = layout
            };

            return message;
        }
    }
}
```

`DidTransition`메서드는 두 가지 모드 간의 전환을 처리 하도록 재정의 됩니다.

```csharp
public override void DidTransition (MSMessagesAppPresentationStyle presentationStyle)
{
    base.DidTransition (presentationStyle);

    // Take action based on style
    switch (presentationStyle) {
    case MSMessagesAppPresentationStyle.Compact:
        PresentStickerBrowser ();
        break;
    case MSMessagesAppPresentationStyle.Expanded:
        PresentAddSticker ();
        break;
    }
}
```

필요에 따라 앱은 `WillTransition` 사용자에 게 표시 되기 전에 메서드를 사용 하 여 보기 모드 변경을 처리할 수 있습니다 (위의 Icecream 빌더 예제에서 수행 된 것과 같이). 자세한 내용은 [추가 스티커 사용자 지정](~/ios/platform/message-app-integration/intro-to-message-app-extensions.md) 설명서를 참조 하세요.

## <a name="replying-to-a-message"></a>메시지에 회신

메시지에 회신할 때 메시지 앱 확장이 처리 해야 하는 두 가지 경우는 다음과 같습니다.

[![비활성 모드 및 활성 모드의 메시지 앱 확장](advanced-message-app-extensions-images/interactive09.png)](advanced-message-app-extensions-images/interactive09.png#lightbox)

- **확장이 비활성 상태임** -사용자가 확장을 활성화 하 고 대화형 대화를 계속 하기 위해 탭 할 수 있는 메시지 기록에 메시지 앱 확장의 메시지 풍선 메시지가 있습니다.
- **확장이 활성 상태입니다** . 사용자는 메시지 내용에서 메시지 앱 확장의 메시지 거품형을 탭 하 여 확장 된 보기 모드로 전환 하 고 대화형 프로세스를 계속할 수 있습니다.

### <a name="the-extension-is-inactive"></a>확장이 비활성 상태임

메시지 기록의 사용자가 메시지 버블을 탭 하 고 메시지 앱 확장이 비활성화 된 경우 다음 프로세스가 수행 됩니다.

[![비활성 메시지 거품형 처리](advanced-message-app-extensions-images/interactive10.png)](advanced-message-app-extensions-images/interactive10.png#lightbox)

1. 사용자가 확장의 메시지 거품형을 탭 합니다.
2. 확장이 시작 되 면 메시지 앱이 프로세스를 시작 합니다.
3. `DidBecomeActive`메서드를 호출 하 고 `MSConversation` 메시지 앱 확장이 실행 되는 대화를 나타내는를 전달 합니다.
4. 확장은 둘 다를 기반으로 하기 때문에를 `UIViewController` `ViewWillAppear` `ViewDidAppear` 호출 합니다.

프로세스가 완료 되 면 확장 된 보기 모드로 메시지 앱 확장이 표시 됩니다.

### <a name="the-extension-is-active"></a>확장이 활성 상태입니다.

메시지 기록의 사용자가 메시지 버블을 탭 하 고 메시지 앱 확장이 활성화 된 경우 다음 프로세스가 수행 됩니다.

[![활성 메시지 거품형 처리](advanced-message-app-extensions-images/interactive11.png)](advanced-message-app-extensions-images/interactive11.png#lightbox)

1. 사용자가 확장의 메시지 거품형을 탭 합니다.
2. 메시지 앱 확장이 이미 활성화 되어 있으므로 `WillTransition` 의 메서드를 `MSMessagesAppViewController` 호출 하 여 압축에서 확장 된 보기 모드로 전환 하는 것을 처리 합니다.
3. `DidSelectMessage`의 메서드를 `MSMessagesAppViewController` 호출 하 고 `MSMessage` `MSConversation` 메시지 거품이 속한 및를 전달 합니다.
4. `DidTransition`의 메서드는 `MSMessagesAppViewController` 압축 된 보기 모드로 전환 하는 것을 처리 하기 위해 호출 됩니다.

그리고 프로세스가 완료 되 면 메시지 앱 확장이 확장 된 보기 모드로 표시 됩니다.

### <a name="accessing-the-selected-message"></a>선택한 메시지에 액세스

두 경우 모두 사용자가 메시지 앱 확장에 속하는 메시지 거품형을 탭 할 때 `MSMessage` 의 속성을 사용 하 여 탭 한에 대 한 액세스 권한을 얻어야 합니다 `SelectedMessage` `MSConversation` .

다음은 그 예입니다.

```csharp
using System;
using Foundation;
using Messages;
using UIKit;

namespace MessageExtension
{
    public partial class MessagesViewController : MSMessagesAppViewController
    {
        ...

        #region Override Methods
        public override void DidSelectMessage (MSMessage message, MSConversation conversation)
        {
            base.DidSelectMessage (message, conversation);

            // Get selected message
            var selected = conversation.SelectedMessage;

            // Present the user interface to continue editing
            // the conversation
            ...
        }
        #endregion
    }
}
```

선택한 메시지가 메시지 앱 확장의 UI에 표시 되 고 사용자가 응답을 구성할 수 있어야 합니다.

## <a name="removing-partially-completed-messages"></a>부분적으로 완료 된 메시지 제거

대화의 두 사용자 간에 대화형 대화의 서로 다른 단계를 전송 하는 과정에서 부분적으로 완료 된 메시지 방울은 메시지 기록을 간단 하 게 시작할 수 있습니다.

[![부분적으로 완료 된 메시지 거품은 메시지 기록을 복잡 하 게 만들 수 있습니다.](advanced-message-app-extensions-images/interactive12.png)](advanced-message-app-extensions-images/interactive12.png#lightbox)

대신 메시지 앱 확장은 이전 메시지 거품을 메시지 기록의 간결한 주석으로 축소 해야 합니다.

[![메시지 기록을 통해 이전 메시지 거품 축소](advanced-message-app-extensions-images/interactive13.png)](advanced-message-app-extensions-images/interactive13.png#lightbox)

이는를 사용 하 여 `MSSession` 모든 기존 단계를 축소 하기 위해 처리 됩니다. 따라서 `DidSelectMessage` 클래스의 메서드를 `MSMessagesAppViewController` 다음과 같이 수정할 수 있습니다.

```csharp
public override void DidSelectMessage (MSMessage message, MSConversation conversation)
{
    base.DidSelectMessage (message, conversation);

    MSSession session;
    var summary = "";

    // Get selected message
    var selected = conversation.SelectedMessage;

    // Does the selected message already have a session?
    if (selected.Session == null) {
        // No, create a new session
        session = new MSSession ();
        summary = "Let's build an ice cream";
    } else {
        // Yes, use the existing session
        session = selected.Session;
        summary = "I added some scoops";
    }

    // Create an instance of the message being composed
    var existingMessage = new MSMessage (session);
    message.SummaryText = summary;
    ...

    // Present the user interface to continue editing
    // the conversation
    ...
}
```

선택한 메시지가 이미 종료 된 경우에 `MSSession` 는 새 `MSSession` 가 만들어집니다. `SummaryText`의 속성은 `MSMessage` 축소 된 이전 단계에 캡션을 추가 하는 데 사용 됩니다. `SummaryText`속성이로 설정 되 면 대화 `null` 의 이전 단계가 대화 성적에서 완전히 제거 됩니다.

## <a name="advanced-message-api-features"></a>고급 메시지 API 기능

위에서 자세히 설명 된 새 메시지 API의 기본 기능을 사용 하 여 Apple에서 프레임 워크에 기본 제공 하는 고급 기능 중 일부를 살펴보겠습니다.

먼저 `MSMessagesAppViewController` 클래스에 대화에 대 한 보다 심층적인 액세스를 제공 하는 몇 가지 다른 재정의 메서드가 있습니다.

- `DidStartSendingMessage` -사용자가 보내기 단추를 누를 때 호출 됩니다. 이는 메시지가 실제로 받는 사람에 게 배달 되었다는 것을 의미 하는 것이 아니라 송신 프로세스가 시작 된 것입니다.
- `DidCancelSendingMessage` -사용자가 대화 내용에서 메시지 거품형의 오른쪽 위 모퉁이에 있는 *X* 단추를 누르면 발생 합니다.
- `DidReceiveMessage` -이 메서드는 메시지 앱 확장이 활성화 된 상태에서 대화의 참가자 중 하나 로부터 새 메시지를 받은 경우 호출 됩니다.

### <a name="group-conversations"></a>그룹 대화

사용자가 그룹 대화 (3 명 이상)에 참여 하는 동안 메시지 앱 확장을 사용할 수 있으며, 메시지 앱 확장을 디자인 하 고 구현할 때이를 고려해 야 합니다.

세 명의 사용자를 사용 하 여 그룹 대화에서 다음과 같은 상호 작용을 살펴보겠습니다.

[![3 명의 사용자를 사용 하는 그룹 대화의 상호 작용](advanced-message-app-extensions-images/interactive14.png)](advanced-message-app-extensions-images/interactive14.png#lightbox)

1. 사용자 1은 먹으며 즐길 topping을 선택 하기 위해 사용자 2와 사용자 3에 게 요청 하는 그룹 대화형 메시지를 보냅니다.
2. 사용자 2가 tomatoes를 선택 합니다.
3. 사용자 3은 pickles를 선택 합니다.
4. 사용자 2와 사용자 3의 선택 항목은 거의 동시에 사용자 1에 게 도착 합니다. 결과적으로 사용자 2의 선택은 요약 줄로 축소 되 고 사용할 수 없습니다. 사용자 2의 선택이 표시 되 고 사용자 3이 축소 되는 경우에도이 사례가 대칭 이동 되었을 수 있습니다.

두 경우 모두 사용자 1이 사용자 2와 사용자 3의 선택 항목에 모두 액세스할 수 있으므로이 동작은 바람직하지 않습니다. 이러한 상황을 처리 하기 위해 Apple에서는 메시지 앱 확장이 클라우드에 메시지 상태를 저장 하 고, (사용자 간에 전송 됨)의 URL 속성을 사용 하 여 `MSMessage` 이 상태에 액세스 하는 것을 제안 합니다.

사용자가 메시지를 보내면 세션 토큰이 생성 되어 현재 메시지 상태를 사용 하 여 클라우드에 푸시됩니다. 사용자가 대화 내용에서 메시지 거품형을 누르면 세션 토큰이 클라우드에서 현재 세션 상태를 검색 하는 데 사용 됩니다.

### <a name="sender-identifiers"></a>보낸 사람 식별자

메시지 보낸 사람의 식별자에 대 한 액세스를 논의 하려면 위에 지정 된 그룹 대화의 예를 사용 합니다.

[![그룹 대화 전송 식별자](advanced-message-app-extensions-images/interactive15.png)](advanced-message-app-extensions-images/interactive15.png#lightbox)

1. 다시, 사용자 1은 먹으며 즐길 topping을 선택 하는 사용자 2와 사용자 3을 요청 하는 그룹 대화형 메시지를 보냅니다.
2. 사용자 3은 pickles를 선택 합니다.
3. 사용자 3의 선택 항목이 사용자 1에 게 도착 하 고 사용자 2가 아직 회신 하지 않았습니다.
4. Apple은 사용자 개인 정보 보호와 매우 관련이 있으므로, 메시지 앱 확장은 `NSUUID` 대화의 각 참가자에 게 할당 되는 고유 식별자 ()만 알고 있습니다. 로컬 장치에서는 현재 사용자의 식별자만 알려집니다.
5. 에는 `MSMessage` `SenderIdentifier` 확장에 알려진 참가자 목록의 사용자 중 하 나와 일치 하는 속성이 있습니다.
6. 각 사용자 장치에는 로컬 사용자의 식별자만 알려진 참가자 목록의 자체 복사본이 있습니다.
7. 메시지를 보낼 때 해당 `SenderIdentifier` 속성은 로컬 사용자의 속성으로도 알려져 있습니다.

보낸 사람 식별자는 다음과 같은 방법으로 사용할 수 있습니다.

- 참가자 목록을 보면 확장이 대화의 사용자 수를 가져올 수 있습니다.
- 확장은 사용자 로부터 메시지를 받으면 보낸 사람 식별자를 추적할 수 있습니다. 동일한 보낸 사람 식별자를 가진 다른 메시지를 수신 하는 경우 확장은 동일한 사용자의 것임을 인식 합니다.
- 대화의 특정 사용자를 식별 하는 데 사용할 수 있습니다.

보낸 사람 식별자는의 텍스트 필드에 `MSMessageTemplateLayout` 달러 기호 ()를 접두사로 사용 하 여 사용할 수 있습니다 `$` . 다음은 그 예입니다.

```csharp
// Pass along the sender identifier
var layout = new MSMessageTemplateLayout()
layout.Caption = string.format("${0} wants pickles.",Conversation.LocalParticipantIdentifier.UuidString);
```

메시지 앱이 이러한 형식의 형식으로 메시지 거품형을 표시 하는 경우 메시지를 `$uuid...` 보낸 대화에서 참가자의 연락처 이름으로를 바꿉니다.

보낸 사람 식별자는 각 장치에서 고유 하므로 위의 다이어그램에서 다시 살펴보면 사용자 1의 장치 및 사용자 3의 장치에는 대화의 각 참가자에 대 한 고유한 보낸 사람 Id가 서로 다릅니다.

보낸 사람 식별자의 범위는 메시지 앱 확장의 설치로 지정 됩니다. 따라서 사용자가 메시지 앱 확장을 제거 하 고 다시 설치 하는 경우 새 설치를 위해 새 발신자 식별자가 생성 됩니다.

보낸 사람 식별자에 액세스 하려면 확장에서 다음 코드를 사용할 수 있습니다.

```csharp
public override void DidStartSendingMessage (MSMessage message, MSConversation conversation)
{
    base.DidStartSendingMessage (message, conversation);

    // Get the sender's participant ID
    var senderID = message.SenderParticipantIdentifier;

    // Get the local participant ID
    var localID = conversation.LocalParticipantIdentifier;

    // Get the remote participant IDs
    var remoteIDs = conversation.RemoteParticipantIdentifiers;
}
```

## <a name="supported-platforms"></a>지원되는 플랫폼

메시지 앱 확장에 의해 생성 된 대화형 메시지는 다음과 같은 Apple 플랫폼에서 배달 됩니다.

- watchOS 3
- macOS Sierra
- iOS 10

세 플랫폼 중에서 iOS 10만 사용자가 대화형 메시지를 생성할 수 있습니다. MacOS Sierra에서 사용자가 대화형 메시지 거품형을 클릭 하면에 연결 된 URL `MSMessage` 이 Safari에서 열리고 메시지 표시가 표시 됩니다.

WatchOS에서 메시지 앱은 사용자가 회신을 작성할 수 있는 첨부 된 iOS 장치로 대화형 메시지를 전달할 수 있습니다.

새 메시지 API는 이전 Apple 플랫폼에서 대화형 메시지를 수신 하는 경우 대체 (fallback)를 지원 합니다.

- watchOS 2 +
- OS X 10.11 +
- iOS 9 이상

두 개의 개별 메시지로 대체 형식으로 전달 됩니다.

- 하나는 템플릿 레이아웃에서 제공 되는 이미지입니다.
- 다른은에서 제공 되는 URL `MSMessage` 입니다.

## <a name="summary"></a>요약

이 문서에는 **메시지** 앱과 통합 되 고 사용자에 게 새로운 기능을 제공 하는 xamarin.ios 솔루션에서 메시지 앱 확장을 사용 하기 위한 고급 기술이 제시 되어 있습니다.

## <a name="related-links"></a>관련 링크

- [아이스크림 빌더 (샘플)](/samples/xamarin/ios-samples/ios10-icecreambuilder)
- [메시지 참조](https://developer.apple.com/reference/messages)
- [앱 확장 프로그래밍 가이드](https://developer.apple.com/library/prerelease/content/documentation/General/Conceptual/ExtensibilityPG/index.html#//apple_ref/doc/uid/TP40014214)
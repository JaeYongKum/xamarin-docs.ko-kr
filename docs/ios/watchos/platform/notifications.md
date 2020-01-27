---
title: watchOS 中 Xamarin 的通知
description: 本文档介绍如何使用 Xamarin 中的 watchOS 通知。 它讨论了创建通知控制器，生成通知，并将测试通知。
ms.prod: xamarin
ms.assetid: 0BC1306E-0713-4592-996E-7530CCF281E7
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/17/2017
ms.openlocfilehash: 85a55967446da5cf89e8ce19dadf88d0de16d80a
ms.sourcegitcommit: db422e33438f1b5c55852e6942c3d1d75dc025c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76725071"
---
# <a name="watchos-notifications-in-xamarin"></a>watchOS 中 Xamarin 的通知

如果包含 iOS 应用程序支持它们，watch 应用可以接收通知。 没有内置通知处理，以便不这样做*需要*添加其他通知支持下述，但是如果你想要自定义通知行为和外观请继续阅读。

请参阅[iOS 通知](~/ios/platform/user-notifications/deprecated/index.md)将通知支持添加到你的解决方案中的 iOS 应用程序的详细信息的文档。

## <a name="creating-notification-controllers"></a>创建通知控制器

情节提要上通知控制器有一种特殊类型的 segue 触发它们。 当您将一个新**通知界面控制器**到情节提要上，它会自动将具有附加 segue:

![](notifications-images/notification-storyboard1.png "A new Notification Interface Controller with a segue attached")

选择通知的 segue 时您可以编辑其属性：

![](notifications-images/notification-storyboard2.png "The notification segue selected")

自定义控制器后，它可能看起来如以下示例从 WatchKitCatalog:

![](notifications-images/notifications-segue.png "The Notification Properties")

有两种类型的通知：

- 시스템에서 정의한 스크롤할 때 스크롤할 때 정적 뷰가 아닙니다.

- **长时间看**-滚动的由你定义的可自定义视图 ！ 可以指定一个更简单的、 静态版本和更复杂的动态版本。

### <a name="short-look-notification-controller"></a>短查看通知控制器

简短介绍 UI 包含只是应用程序图标、 应用程序名称和通知标题字符串。

如果用户不会忽略该通知，系统将自动切换到提供的详细信息的长时间查看通知。

### <a name="long-look-notification-controller"></a>长时间查看通知控制器

操作系统决定是否显示基于许多因素的静态或动态视图。 必须提供静态接口，并可以选择性地还包括了动态接口以通知。

#### <a name="static"></a>Static

静态视图应该既简单又快速显示。

![](notifications-images/notification-static.png "The static view")

#### <a name="dynamic"></a>Dynamic

动态视图可以显示更多数据，并提供更多交互性。

![](notifications-images/notification-dynamic.png "The dynamic view")

## <a name="generating-notifications"></a>生成通知

알림은 원격 서버에서 제공 될 수도 있고 iOS 앱에서 로컬로 생성 될 수도 있습니다.

로컬 알림을 생성 하는 방법에 대 한 예제는 [IOS 알림 연습](~/ios/platform/user-notifications/deprecated/local-notifications-in-ios-walkthrough.md) 을 참조 하세요.

必须具有本地通知`AlertTitle`设置为显示在 Apple Watch-`AlertTitle`短外观界面中显示字符串。 同时`AlertTitle`并`AlertBody`显示在通知列表; 和`AlertBody`长时间看界面中显示。

이 스크린샷에서는 알림 목록에 표시 되는 `AlertTitle` 및 긴 모양 인터페이스에 표시 되는 `AlertBody`를 보여 줍니다.

![](notifications-images/watch-notificationslist-sml.png "이 스크린샷은 알림 목록에 표시 되는 AlertTitle을 보여 줍니다.") ![](notifications-images/watch-notificationcontroller-sml.png "긴 모양 인터페이스에 표시 되는 AlertBody")

## <a name="testing-notifications"></a>测试通知

通知 （本地和远程） 可以仅正确测试在设备上，但可以使用模拟它们 **.json** iOS 模拟器中的文件。

### <a name="testing-on-apple-watch"></a>在 Apple Watch 上进行测试

在测试时在 Apple Watch 上的通知，请记住[Apple 的文档](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/BasicSupport.html)指出：

> 当用户的 iPhone 上的一个应用程序的本地或远程通知到达时，iOS 将决定是否在 iPhone 上或在 Apple Watch 上显示该通知。

这这一事实 alluding 该 iOS 决定是否在 iPhone 或 Watch 上将出现一条通知。 如果配对的 iPhone 激活时收到通知，通知是有可能显示在 iPhone 上并*不*路由到手表。

若要确保 watch 上会显示通知，请关闭 iPhone 屏幕 （一次按电源按钮） 或让其进入睡眠状态。 如果配对的监视处于范围内，已通电并且佩戴手腕上，通知会存在路由和监视文件 （伴随细微） 上显示。

### <a name="testing-on-the-ios-simulator"></a>在 iOS 模拟器上测试

您*必须*在 iOS 模拟器中测试通知模式时提供测试 JSON 有效负载。 在中设置路径**自定义执行参数**窗口在 Visual Studio for mac。

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

监视扩展设置为时，visual Studio for Mac 将显示其他选项**启动项目**。
右键单击监视扩展项目并选择**运行与 > 自定义参数...** :

[![](notifications-images/runwith-customparams-sml.png "Running with Custom Properties")](notifications-images/runwith-customparams.png#lightbox)

그러면 **WatchKit** 탭이 포함 된 **실행 인수** 창이 열립니다. **알림** 을 선택 하 고 JSON 페이로드를 제공한 다음 **실행** 을 눌러 시뮬레이터에서 조사식 앱을 시작 합니다.

[![](notifications-images/runwith-execargs-sml.png "Select Notification Payload Default")](notifications-images/runwith-execargs.png#lightbox)

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

若要编辑的监视扩展中右键单击 Visual Studio 设置测试通知有效负载**项目属性**。 转到**调试**部分，并从列表中 （它会自动列出项目中包含的所有 JSON 文件） 选择通知 JSON 文件。

[![](notifications-images/runwith-execargs-sml-vs.png "Select a notifications JSON file")](notifications-images/runwith-execargs-vs.png#lightbox)

监视扩展时**启动项目**，Visual Studio 将显示其他选项，如下所示。 选择其中一个**通知**选项以在启动监视应用程序**通知**模式 （使用属性窗口中选择的 JSON 文件）：

![](notifications-images/runwith-vs.png "The Device menu")

-----

在模拟器上测试使用默认有效负载的 JSON 文件时，默认通知控制器如下所示：

![](notifications-images/notification-debug-sml.png "An example notification")

它也是可以使用[命令行](~/ios/watchos/troubleshooting.md#command_line)启动 iOS 模拟器。

### <a name="example-notification-payload"></a>示例通知有效负载

在中[监视工具包目录](https://docs.microsoft.com/samples/xamarin/ios-samples/watchos-watchkitcatalog)示例有是 JSON 文件的示例有效负载**NotificationPayload.json** （列举如下）。

```json
{
    "aps": {
        "alert": "Test message content",
        "title": "Optional title",
        "category": "myCategory"
        },

        "WatchKit Simulator Actions": [
        {
            "title": "First Button",
            "identifier": "firstButtonAction"
        }
        ],

        "customKey": "Use this file to define a testing payload for your notifications. The aps dictionary specifies the category, alert text and title. The WatchKit Simulator Actions array can provide info for one or more action buttons in addition to the standard Dismiss button. Any other top level keys are custom payload. If you have multiple such JSON files in your project, you'll be able to choose between them in when selecting to debug the notification interface of your Watch App."
    }
```

## <a name="related-links"></a>관련 링크

- [WatchKitCatalog （示例）](https://docs.microsoft.com/samples/xamarin/ios-samples/watchos-watchkitcatalog)
- [Apple Watch 工具包通知文档](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/BasicSupport.html)

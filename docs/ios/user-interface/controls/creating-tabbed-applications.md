---
title: Xamarin.ios의 탭 모음 및 탭 모음 컨트롤러
description: 이 문서에서는 iOS 탭 모음 컨트롤러 및 Xamarin.ios와 함께 사용 하는 방법을 설명 합니다. Uitab 컨트롤러를 설정 하 고, 이미지 작업을 수행 하 고, 배지 값을 설정 하 고, 이벤트에 대 한 작업을 수행 하는 방법을 보여 줍니다.
ms.prod: xamarin
ms.assetid: 7C772899-2900-F139-D642-F3C4F3F14DDC
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/21/2017
ms.openlocfilehash: 2e8dde87456c6e33eda6846967ceea13eb412b93
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86934305"
---
# <a name="tab-bars-and-tab-bar-controllers-in-xamarinios"></a>Xamarin.ios의 탭 모음 및 탭 모음 컨트롤러

탭 응용 프로그램은 iOS에서 여러 화면에 특정 순서로 액세스할 수 있는 사용자 인터페이스를 지 원하는 데 사용 됩니다. `UITabBarController`응용 프로그램은 클래스를 통해 이러한 다중 화면 시나리오에 대 한 지원을 쉽게 포함할 수 있습니다. `UITabBarController`응용 프로그램 개발자가 각 화면에 대 한 세부 정보에 집중할 수 있도록 하는 다중 화면 관리를 처리 합니다.

일반적으로 탭 응용 프로그램은 `UITabBarController` 주 창의로 빌드됩니다 `RootViewController` . 그러나 약간의 추가 코드를 사용 하면 응용 프로그램에서 먼저 로그인 화면을 표시 한 다음 탭 인터페이스를 사용 하는 시나리오와 같은 다른 초기 화면에도 탭 응용 프로그램을 연속 해 서 사용할 수 있습니다.

이 페이지에서는 두 가지 시나리오를 모두 설명 합니다. 탭이 응용 프로그램 뷰 계층의 루트에 있고 비 시나리오에도 해당 합니다. `RootViewController`

## <a name="introducing-uitabbarcontroller"></a>UITabBarController 소개

는 `UITabBarController` 다음과 같은 방법으로 탭 응용 프로그램 개발을 지원 합니다.

- 여러 컨트롤러를 추가할 수 있습니다.
- `UITabBar`클래스를 통해 사용자가 컨트롤러와 뷰 간을 전환할 수 있도록 하는 탭 사용자 인터페이스 제공

컨트롤러는 `UITabBarController` 해당 `ViewControllers` 속성 (배열)을 통해에 추가 됩니다 `UIViewController` . `UITabBarController`자체는 적절 한 컨트롤러 로드를 처리 하 고 선택 된 탭을 기준으로 뷰를 표시 합니다.

탭은 `UITabBarItem` 인스턴스에 포함 된 클래스의 인스턴스입니다 `UITabBar` . 각 `UITabBar` 인스턴스는 `TabBarItem` 각 탭에 있는 컨트롤러의 속성을 통해 액세스할 수 있습니다.

를 사용 하는 방법을 이해 하려면 `UITabBarController` 하나를 사용 하는 간단한 응용 프로그램을 빌드하는 과정을 살펴보겠습니다.

## <a name="tabbed-application-walkthrough"></a>탭 응용 프로그램 연습

이 연습에서는 다음 응용 프로그램을 만듭니다.

[![샘플 탭 앱](creating-tabbed-applications-images/00-app.png)](creating-tabbed-applications-images/00-app.png#lightbox)

Mac용 Visual Studio에서 사용할 수 있는 탭 응용 프로그램 템플릿이 이미 있지만이 예에서는 빈 프로젝트에서 이러한 지침을 사용 하 여 응용 프로그램의 구성 방식을 보다 잘 이해할 수 있습니다.

### <a name="creating-the-application"></a>응용 프로그램 만들기

새 응용 프로그램을 만들어 시작 합니다.

Mac용 Visual Studio에서 **파일 > 새 > 솔루션** 메뉴 항목을 선택 하 고, 아래와 같이 **iOS > 앱 > 빈 프로젝트** 템플릿을 선택 하 고 프로젝트 이름을로 선택 합니다 `TabbedApplication` .

[![빈 프로젝트 템플릿을 선택 합니다.](creating-tabbed-applications-images/newsolution1.png)](creating-tabbed-applications-images/newsolution1.png#lightbox)

[![프로젝트 이름 TabbedApplication](creating-tabbed-applications-images/newsolution2.png)](creating-tabbed-applications-images/newsolution2.png#lightbox)

### <a name="adding-the-uitabbarcontroller"></a>UITabBarController 추가

그런 다음 **파일 > 새 파일** 을 선택 하 고 **일반: 빈 클래스** 템플릿을 선택 하 여 빈 클래스를 추가 합니다. `TabController`아래와 같이 파일의 이름을로 표시 합니다.

[![TabController 클래스를 추가 합니다.](creating-tabbed-applications-images/02-newclass.png)](creating-tabbed-applications-images/02-newclass.png#lightbox)

클래스에는 `TabController` 배열을 관리할의 구현이 포함 됩니다 `UITabBarController` `UIViewControllers` . 사용자가 탭을 선택 하면는 `UITabBarController` 적절 한 뷰 컨트롤러에 대 한 보기를 제공 합니다.

을 구현 하려면 `UITabBarController` 다음을 수행 해야 합니다.

1. 의 기본 클래스 `TabController` 를로 설정 `UITabBarController` 합니다.
1. 에 `UIViewController` 추가할 인스턴스를 만듭니다 `TabController` .
1. 인스턴스를 `UIViewController` 의 속성에 할당 된 배열에 추가 `ViewControllers` `TabController` 합니다.

클래스에 다음 코드를 추가 `TabController` 하 여 이러한 단계를 수행 합니다.

```csharp
using System;
using UIKit;

namespace TabbedApplication {
    public class TabController : UITabBarController {

        UIViewController tab1, tab2, tab3;

        public TabController ()
        {
            tab1 = new UIViewController();
            tab1.Title = "Green";
            tab1.View.BackgroundColor = UIColor.Green;

            tab2 = new UIViewController();
            tab2.Title = "Orange";
            tab2.View.BackgroundColor = UIColor.Orange;

            tab3 = new UIViewController();
            tab3.Title = "Red";
            tab3.View.BackgroundColor = UIColor.Red;

            var tabs = new UIViewController[] {
                tab1, tab2, tab3
            };

            ViewControllers = tabs;
        }
    }
}
```

각 `UIViewController` 인스턴스에 대해의 속성을 설정 합니다 `Title` `UIViewController` . 컨트롤러를에 추가 하면 `UITabBarController` 에서 `UITabBarController` `Title` 각 컨트롤러에 대 한를 읽고 아래와 같이 관련 된 탭의 레이블에 표시 합니다.

[![샘플 앱 실행](creating-tabbed-applications-images/00-app.png)](creating-tabbed-applications-images/00-app.png#lightbox)

#### <a name="setting-the-tabcontroller-as-the-rootviewcontroller"></a>TabController를 RootViewController로 설정

컨트롤러가 탭에 배치 되는 순서는 배열에 추가 되는 순서에 해당 합니다 `ViewControllers` .

을 `UITabController` 첫 번째 화면으로 로드 하려면에 `RootViewController` 대 한 다음 코드에 표시 된 것 처럼을 창의로 설정 해야 합니다 `AppDelegate` .

```csharp
[Register ("AppDelegate")]
public partial class AppDelegate : UIApplicationDelegate
{
    UIWindow window;
    TabController tabController;

    public override bool FinishedLaunching (UIApplication app, NSDictionary options)
    {
        window = new UIWindow (UIScreen.MainScreen.Bounds);

        tabController = new TabController ();
        window.RootViewController = tabController;

        window.MakeKeyAndVisible ();

        return true;
    }
}
```

이제 응용 프로그램을 실행 하는 경우가 `UITabBarController` 기본적으로 선택 된 첫 번째 탭과 함께 로드 됩니다. 다른 탭 중 하나를 선택 하면 `UITabBarController,` 아래와 같이 최종 사용자가 두 번째 탭을 선택한 위치에 연결 된 컨트롤러의 뷰가 표시 됩니다.

![표시 되는 두 번째 탭](creating-tabbed-applications-images/03-secondtab-sml.png)

### <a name="modifying-tabbaritems"></a>Tab바 항목 수정

이제 실행 중인 탭 응용 프로그램이 있으므로를 수정 `TabBarItem` 하 여 표시 되는 이미지와 텍스트를 변경 하 고 탭 중 하나에 배지를 추가 해 보겠습니다.

#### <a name="setting-a-system-item"></a>시스템 항목 설정

먼저 시스템 항목을 사용 하도록 첫 번째 탭을 설정 해 보겠습니다. 의 생성자에서 `TabController` 인스턴스의 컨트롤러를 설정 하는 줄을 제거 하 `Title` `tab1` 고 다음 코드로 바꾸어 컨트롤러의 속성을 설정 합니다 `TabBarItem` .

```csharp
tab1.TabBarItem = new UITabBarItem (UITabBarSystemItem.Favorites, 0);
```

`UITabBarItem`을 사용 하 여를 만들 때 `UITabBarSystemItem` 제목 및 이미지는 다음 스크린샷에 표시 된 것 처럼 iOS에서 자동으로 제공 됩니다. **Favorites**

 ![별표 아이콘을 사용 하는 첫 번째 탭](creating-tabbed-applications-images/04a-tabimage-sml.png)

#### <a name="setting-the-image"></a>이미지 설정

시스템 항목을 사용 하는 것 외에도의 제목과 이미지를 `UITabBarItem` 사용자 지정 값으로 설정할 수 있습니다. 예를 들어 `TabBarItem` 라는 컨트롤러의 속성을 설정 하는 코드를 다음과 같이 변경 합니다 `tab2` .

```csharp
tab2 = new UIViewController ();
tab2.TabBarItem = new UITabBarItem ();
tab2.TabBarItem.Image = UIImage.FromFile ("second.png");
tab2.TabBarItem.Title = "Second";
tab2.View.BackgroundColor = UIColor.Orange;
```

위의 코드에서는 라는 이미지가 `second.png` 프로젝트의 루트 또는 **리소스** 디렉터리에 추가 된 것으로 가정 합니다. 모든 화면 밀도를 지원 하려면 아래와 같이 세 개의 이미지가 필요 합니다.

![프로젝트에 추가 된 이미지](creating-tabbed-applications-images/tabbedimages7new.png)

올바른 차원에 대 한 지침은 [Apple 사용자 지정 아이콘 페이지](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/custom-icons/) 의 **탭 모음 아이콘 크기** 섹션을 참조 하세요. 권장 되는 크기는 이미지의 스타일 (원형, 사각형, 와이드 또는 높이)에 따라 달라 집니다.

`Image`속성은 **second.png** 파일 이름 으로만 설정 해야 하며, 필요할 때 iOS에서 더 높은 해상도 파일을 자동으로 로드 합니다. [이미지 작업](~/ios/app-fundamentals/images-icons/index.md) 가이드에서이에 대해 자세히 알아볼 수 있습니다. 기본적으로 탭 모음 항목은 회색 이며 선택 시 파란색 색조가 표시 됩니다.

#### <a name="overriding-the-title"></a>제목 재정의

`Title`에서 직접 속성을 설정 하면 `TabBarItem` 컨트롤러 자체에서에 대해 설정 된 모든 값이 재정의 됩니다 `Title` .

이 스크린샷에서 두 번째 (가운데) 탭에는 사용자 지정 제목 및 이미지가 표시 됩니다.

![사각형 아이콘이 있는 두 번째 탭](creating-tabbed-applications-images/05-customtab-sml.png)

#### <a name="setting-the-badge-value"></a>배지 값 설정

탭에 배지를 표시할 수도 있습니다. 예를 들어 세 번째 탭에 배지를 설정 하는 다음 코드 줄을 추가 합니다.

```csharp
tab3.TabBarItem.BadgeValue = "Hi";
```

이를 실행 하면 아래와 같이 탭의 왼쪽 위 모퉁이에 문자열 "Hi"가 표시 된 빨간색 레이블이 표시 됩니다.

![Hi 배지를 포함 하는 두 번째 탭](creating-tabbed-applications-images/06-badge-sml.png)

배지는 읽지 않은 항목, 새 항목을 표시 하는 데 종종 사용 됩니다. 배지를 제거 하려면 `BadgeValue` 아래와 같이을 null로 설정 합니다.

```csharp
tab3.TabBarItem.BadgeValue = null;
```

## <a name="tabs-in-non-rootviewcontroller-scenarios"></a>비 RootViewController 시나리오의 탭

위의 예제에서는 창의 인 경우를 사용 하 여 작업 하는 방법을 살펴보았습니다 `UITabBarController` `RootViewController` . 이 예제에서는가 아닐 때를 사용 하는 방법과 `UITabBarController` `RootViewController` 이를 만드는 방법을 보여 줍니다. storyboard를 사용 합니다.

### <a name="initial-screen-example"></a>초기 화면 예제

이 시나리오의 경우 초기 화면은이 아닌 컨트롤러에서 로드 됩니다 `UITabBarController` . 사용자가 단추를 탭 하 여 화면을 조작할 때 동일한 뷰 컨트롤러가에 로드 된 `UITabBarController` 다음 사용자에 게 표시 됩니다. 다음 스크린샷에서는 애플리케이션 흐름을 보여줍니다.

[![이 스크린샷은 응용 프로그램 흐름을 보여 줍니다.](creating-tabbed-applications-images/inital-screen-application.png)](creating-tabbed-applications-images/inital-screen-application.png#lightbox)

이 예에서는 새 응용 프로그램을 시작 해 보겠습니다. 다시, **iPhone > 앱 > 빈 프로젝트 (c #)** 템플릿을 사용 합니다. 이번에는 프로젝트 이름을 지정 `InitialScreenDemo` 합니다.

이 예에서는 storyboard를 사용 하 여 뷰 컨트롤러를 레이아웃 합니다. 스토리 보드를 추가 하려면:

- 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 **추가 > 새 파일**을 선택 합니다.

- 새 파일 대화 상자가 나타나면 **iOS > 빈 IPhone Storyboard**로 이동 합니다.

아래 그림과 같이 새 Storyboard **mainstoryboard.storyboard** 를 호출 해 보겠습니다.

[![프로젝트에 Mainstoryboard.storyboard 파일 추가](creating-tabbed-applications-images/new-file-dialog.png)](creating-tabbed-applications-images/new-file-dialog.png#lightbox)

스토리 보드 [소개](~/ios/user-interface/storyboards/index.md) 가이드에 설명 되어 있는 이전 비 storyboard 파일에 스토리 보드를 추가할 때 유의 해야 하는 몇 가지 중요 한 단계가 있습니다. 이러한 항목은 다음과 같습니다.

1. 스토리 보드 이름을의 **주 인터페이스** 섹션에 추가 합니다 `Info.plist` .

    [![주 인터페이스를 Mainstoryboard.storyboard로 설정 합니다.](creating-tabbed-applications-images/project-options.png)](creating-tabbed-applications-images/project-options.png#lightbox)
1. 에서 `App Delegate` 다음 코드를 사용 하 여 Window 메서드를 재정의 합니다.

    ```csharp
    public override UIWindow Window {
        get;
        set;
    }
    ```

이 예에서는 3 개의 보기 컨트롤러가 필요 합니다. 이라는 하나는 `ViewController1` 초기 뷰 컨트롤러로 사용 되 고 첫 번째 탭에서는 사용 됩니다. 두 `ViewController2` `ViewController3` 번째 및 세 번째 탭에서 각각 사용 되는 및 라는 다른 두 개의입니다.

Mainstoryboard.storyboard 파일을 두 번 클릭 하 여 디자이너를 열고 세 개의 뷰 컨트롤러를 디자인 화면으로 끌어 옵니다. 이러한 각 뷰 컨트롤러에는 위의 이름에 해당 하는 고유한 클래스가 있어야 합니다. 따라서 **id > 클래스**아래 스크린샷에 나와 있는 것 처럼 이름을 입력 합니다.

[![클래스를 ViewController1로 설정 합니다.](creating-tabbed-applications-images/class-name.png)](creating-tabbed-applications-images/class-name.png#lightbox)

필요한 클래스 및 디자이너 파일을 자동으로 생성 Mac용 Visual Studio 아래 그림과 같이 Solution Pad에서 볼 수 있습니다.

[![프로젝트에서 자동 생성 된 파일](creating-tabbed-applications-images/solution-pad2.png)](creating-tabbed-applications-images/solution-pad2.png#lightbox)

#### <a name="creating-the-ui"></a>UI 만들기

다음으로, Xamarin iOS Designer를 사용 하 여 각 ViewController의 보기에 대 한 간단한 사용자 인터페이스를 만듭니다.

`Label` `Button` 오른쪽의 **도구 상자** 에서를 ViewController1로 끌어 놓습니다. 다음으로 Properties Pad를 사용 하 여 컨트롤의 이름과 텍스트를 다음과 같이 편집 합니다.

- **레이블** : `Text`  =  **One**
- **단추** : `Title`  =  **사용자가 초기 작업을 수행** 합니다.

이벤트에서 단추의 표시 여부를 제어 하 `TouchUpInside` 고, 코드 숨김으로이를 참조 해야 합니다. 다음 스크린샷에 표시 된 대로 Properties Pad **이름을** 사용 하 여 식별 해 보겠습니다 `aButton` .

[![Properties Pad의 이름을 aButton으로 설정 합니다.](creating-tabbed-applications-images/abutton-properties.png)](creating-tabbed-applications-images/abutton-properties.png#lightbox)

이제 Design Surface는 아래 스크린샷에서와 같이 표시 됩니다.

[![이제 Design Surface이 스크린샷 처럼 표시 됩니다.](creating-tabbed-applications-images/design-surface1.png)](creating-tabbed-applications-images/design-surface1.png#lightbox)

각각 `ViewController2` `ViewController3` 에 레이블을 추가 하 고 텍스트를 각각 ' 2 ' 및 ' 3 '으로 변경 하 여 및에 대 한 세부 정보를 추가 해 보겠습니다. 이는 사용자가 원하는 탭/보기를 표시 합니다.

#### <a name="wiring-up-the-button"></a>단추를 연결 합니다.

`ViewController1`응용 프로그램이 처음 시작 될 때 로드 됩니다. 사용자가 단추를 탭 하면 단추를 숨기고 `UITabBarController` `ViewController1` 첫 번째 탭에서 인스턴스와 함께을 로드 합니다.

사용자가를 놓으면 `aButton` TouchUpInside 이벤트가 트리거됩니다. 단추를 선택 하 고, 속성 패드의 **이벤트 탭** 에서 이벤트 처리기를 선언 합니다 `InitialActionCompleted` . 그러면 코드에서 참조 될 수 있습니다. 이는 아래 스크린샷에 설명 되어 있습니다.

[![사용자가 aButton을 해제 하면 TouchUpInside 이벤트를 트리거합니다.](creating-tabbed-applications-images/event-handler.png)](creating-tabbed-applications-images/event-handler.png#lightbox)

이제 이벤트가 발생 하는 경우 보기 컨트롤러에 단추를 숨기도록 지시 해야 `InitialActionCompleted` 합니다. 에서 `ViewController1` 다음 부분 메서드를 추가 합니다.

```csharp
partial void InitialActionCompleted (UIButton sender)
{
    aButton.Hidden = true;  
}
```

파일을 저장 하 고 응용 프로그램을 실행 합니다. 화면이 표시 되 고 터치 시 단추가 사라집니다.

#### <a name="adding-the-tab-bar-controller"></a>탭 표시줄 컨트롤러 추가

이제 초기 보기가 정상적으로 작동 합니다. 다음으로, `UITabBarController` 보기 2 및 3과 함께에 추가 하려고 합니다. 디자이너에서 Storyboard를 열어 보겠습니다.

**도구 상자**의 컨트롤러 & 개체에서 **탭 모음 컨트롤러** 를 검색 하 고이를 Design Surface으로 끌어 옵니다. 아래 스크린샷에서 볼 수 있듯이 탭 모음 컨트롤러는 UI를 포함 하지 않으므로 기본적으로 두 개의 뷰 컨트롤러를 제공 합니다.

[![레이아웃에 탭 표시줄 컨트롤러 추가](creating-tabbed-applications-images/tabbarcontroller.png)](creating-tabbed-applications-images/tabbarcontroller.png#lightbox)

아래쪽에 있는 검은색 표시줄을 선택 하 고 delete 키를 눌러 새 뷰 컨트롤러를 삭제 합니다.

이 스토리 보드에서 Segue를 사용 하 여 Tab바 컨트롤러와 뷰 컨트롤러 간의 전환을 처리할 수 있습니다. 초기 보기와 상호 작용 한 후 사용자에 게 제공 되는 TabBarController로 로드 하려고 합니다. 디자이너에서 설정 해 보겠습니다.

**Ctrl 키를 누른 채** 단추를 TabBarController로 **끕니다** . 마우스를 가져가면 상황에 맞는 메뉴가 표시 됩니다. 모달 segue를 사용 하려고 합니다.

각 탭을 설정 하려면 아래 그림과 같이 각 보기 컨트롤러에 대 한 Tab 컨트롤러에서 각 보기 컨트롤러에 대 한 **Ctrl + 클릭** 을 차례로 클릭 하 고 상황에 맞는 메뉴에서 관계 **탭** 을 선택 합니다.

[![탭 관계 선택](creating-tabbed-applications-images/context-menu.png)](creating-tabbed-applications-images/context-menu.png#lightbox)

스토리 보드는 아래 스크린샷에서와 비슷해야 합니다.

[![스토리 보드는이 스크린샷과 비슷합니다.](creating-tabbed-applications-images/segue-layout.png)](creating-tabbed-applications-images/segue-layout.png#lightbox)

탭 모음 항목 중 하나를 클릭 하 고 속성 패널을 탐색 하는 경우 아래 그림과 같이 다양 한 옵션을 볼 수 있습니다.

[![속성 탐색기에서 탭 옵션 설정](creating-tabbed-applications-images/properties-panel.png)](creating-tabbed-applications-images/properties-panel.png#lightbox)

이를 사용 하 여 배지, 제목 및 iOS 식별자와 같은 특정 특성을 편집할 수 있습니다.

지금 응용 프로그램을 저장 하 고 실행 하면 ViewController1 인스턴스가 TabBarController로 로드 될 때 단추가 다시 나타납니다. 현재 뷰에 부모 뷰 컨트롤러가 있는지 확인 하 여이 문제를 해결 해 보겠습니다. 이 경우에는 Tab 컨트롤러 내에 있다는 것을 알 수 있으므로 단추를 숨겨야 합니다. ViewController1 클래스에 아래 코드를 추가 해 보겠습니다.

```csharp
public override void ViewDidLoad ()
{
    if (ParentViewController != null){
        aButton.Hidden = true;
    }
}
```

응용 프로그램이 실행 되 고 사용자가 첫 번째 화면에서 단추를 누르면 아래와 같이 첫 번째 탭에 있는 첫 번째 화면의 뷰가 포함 된 Uitab바 컨트롤러가 로드 됩니다.

[![샘플 앱 출력](creating-tabbed-applications-images/first-view-sml.png)](creating-tabbed-applications-images/first-view.png#lightbox)

## <a name="summary"></a>요약

이 문서에서는 응용 프로그램에서를 사용 하는 방법을 살펴보았습니다 `UITabBarController` . 각 탭에 컨트롤러를 로드 하는 방법 뿐만 아니라 제목, 이미지, 배지 등의 탭에 대 한 속성을 설정 하는 방법을 살펴보았습니다. 그런 다음 storyboard를 사용 하 여 창의가 아닐 때 런타임에를 로드 하는 방법을 검사 합니다 `UITabBarController` `RootViewController` .

## <a name="related-links"></a>관련 링크

- [탭 응용 프로그램 만들기 (샘플)](https://docs.microsoft.com/samples/xamarin/ios-samples/creatingtabbedapplications)
- [Images.zip](https://github.com/xamarin/ios-samples/blob/master/CreatingTabbedApplications/Resources/images.zip?raw=true)
- [UITabBarController 클래스 참조](https://developer.apple.com/library/ios/#documentation/uikit/reference/UITabBarController_Class/Reference/Reference.html)

---
title: Xamarin.ios의 스토리 보드
description: 이 문서에서는 Xamarin.ios의 스토리 보드를 소개 합니다. 스토리 보드를 사용 하 여 사용자 인터페이스를 정의 하는 방법, segue 및 iOS Designer를 사용 하 여 스토리 보드 파일을 편집 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/22/2017
ms.openlocfilehash: e6bbc9d7d404136984e3d1ec93186dc85691c751
ms.sourcegitcommit: d1f0e0a9100548cfe0960ed2225b979cc1d7c28f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439744"
---
# <a name="storyboards-in-xamarinios"></a>Xamarin.ios의 스토리 보드

이 가이드에서는 Storyboard가 무엇 인지 설명 하 고 Segue와 같은 몇 가지 주요 구성 요소를 검토 합니다. 스토리 보드를 만들고 사용 하는 방법과 개발자에 게 제공 되는 이점에 대해 살펴보겠습니다.

Apple에서 iOS 응용 프로그램 UI의 시각적 표현으로 Storyboard 파일 형식을 도입 하기 전에 개발자는 각 뷰 컨트롤러에 대 한 XIB 파일을 만들고 각 뷰 간의 탐색을 수동으로 프로그래밍 했습니다.  스토리 보드를 사용 하면 개발자가 두 뷰 컨트롤러를 모두 정의 하 고 디자인 화면에서 뷰 컨트롤러 간을 탐색할 수 있으며 응용 프로그램의 사용자 인터페이스에 대 한 WYSIWYG 편집 기능을 제공 합니다.

Mac용 Visual Studio를 사용 하 여 스토리 보드를 만들고 열 수 있습니다. 이 가이드에서는 Xcode Interface Builder를 사용 하 여 c #을 사용 하 여 탐색을 프로그래밍 하는 동안 스토리 보드를 만드는 방법에 대해서도 살펴봅니다.

## <a name="requirements"></a>요구 사항

스토리 보드는 Xcode와 함께 사용 하 고 Mac용 Visual Studio의 Xamarin.ios 프로젝트 내에서 시작할 수 있습니다.

## <a name="what-is-a-storyboard"></a>스토리 보드 란?

스토리 보드는 응용 프로그램의 모든 화면에 대 한 시각적 표현입니다. 각 장면에는 *뷰 컨트롤러* 및 *뷰* 를 나타내는 일련의 장면이 포함 되어 있습니다. 이러한 보기에는 사용자가 응용 프로그램과 상호 작용할 수 있도록 하는 개체 및 [컨트롤이](~/ios/user-interface/controls/index.md) 포함 될 수 있습니다. 이 뷰 및 컨트롤 컬렉션 (또는 *하위 뷰*)을 *콘텐츠 뷰 계층 구조* 라고 합니다. 장면은 뷰 컨트롤러 간의 전환을 나타내는 segue 개체로 연결 됩니다. 이는 일반적으로 초기 뷰와 연결 보기의 개체 사이에 segue를 만들어 수행 합니다. 디자인 화면의 관계는 다음 그림에 나와 있습니다.

 [![디자인 화면의 관계는이 이미지에 나와 있습니다.](images/storyboardsview.png)](images/storyboardsview.png#lightbox)

표시 된 것 처럼 storyboard는 이미 렌더링 된 콘텐츠를 사용 하 여 각 장면을 배치 하 고 두 항목 간의 연결을 보여 줍니다. IPhone에서 장면에 대해 이야기 하는 경우 스토리 보드의 한 *장면이* 장치에 있는 한 콘텐츠의 *화면과* 같다고 가정 하는 것이 안전 합니다. 그러나 iPad를 사용 하면 팝 오버 view controller를 사용 하는 경우와 같이 한 번에 여러 장면이 표시 될 수 있습니다.

특히 Xamarin을 사용 하는 경우 storyboard를 사용 하 여 응용 프로그램의 UI를 만들 때 많은 이점이 있습니다. 먼저 [사용자 지정 컨트롤](../designer/ios-designable-controls-overview.md) 을 포함 하 여 모든 개체가 디자인 타임에 렌더링 됨에 따라 UI의 시각적 표현입니다.
즉, 응용 프로그램을 빌드하거나 배포 하기 전에 모양과 흐름을 시각화할 수 있습니다. 예를 들어 이전 이미지를 사용 합니다. 디자인 화면에 얼마나 많은 장면이 있는지, 각 뷰의 레이아웃 및 모든 항목의 관계를 빠르게 확인할 수 있습니다. 이를 통해 Storyboard를 강력 하 게 만들 수 있습니다.

Storyboard를 사용 하 여 이벤트를 관리할 수도 있습니다.  대부분의 UI 컨트롤에는 Properties Pad에서 가능한 이벤트 목록이 있습니다. 이벤트 처리기는 여기에 추가 하 고, 뷰 컨트롤러 클래스의 부분 메서드에서 완료할 수 있습니다.

스토리 보드의 내용은 XML 파일로 저장 됩니다. 빌드 시 모든 `.storyboard` 파일은 nibs 라는 이진 파일로 컴파일됩니다. 런타임에는 이러한 nibs를 초기화 하 고 인스턴스화하여 새 뷰를 만듭니다.

## <a name="segues"></a>Segue

*Segue* 또는 *Segue 개체* 는 iOS 개발에서 장면 간 전환을 나타내는 데 사용 됩니다. Segue를 만들려면 **Ctrl** 키를 누른 채 한 장면에서 다른 장면으로를 클릭 합니다. 마우스를 끌면 segue이 이어질 위치를 나타내는 파란색 연결선이 나타납니다. 이는 다음 그림에 나와 있습니다.

 [![Segue가이 이미지에 표시 된 것 처럼 이어질 위치를 나타내는 파란색 커넥터가 표시 됩니다.](images/createsegue.png)](images/createsegue.png#lightbox)

마우스 위로 마우스를 가져가면 segue 작업을 선택할 수 있는 메뉴가 나타납니다. 다음 이미지와 유사할 수 있습니다.

**IOS 전 8 및 크기 클래스**:

[![Size 클래스가 없는 Action Segue dropdown](images/segue1.png)](images/segue1.png#lightbox)

**Size 클래스 및 적응 segue를 사용 하는 경우**:

[![Size 클래스를 사용 하는 Action Segue dropdown](images/16new.png)](images/16new.png#lightbox)

> [!IMPORTANT]
> Windows 가상 머신에 대해 VMWare를 사용 하는 경우 Ctrl + 클릭은 기본적으로 마우스 _오른쪽 단추 클릭_ 으로 매핑됩니다. Segue을 만들려면 **기본 설정**  >  **키보드 & 마우스**  >  **마우스 바로 가기** 를 통해 키보드 기본 설정을 편집 하 고 아래 그림과 같이 **보조 단추** 를 다시 매핑합니다.
>
> [![키보드 및 마우스 기본 설정](images/image22.png)](images/image22.png#lightbox)
>
> 이제 뷰 컨트롤러 간에 segue를 정상적으로 추가할 수 있습니다.

전환 유형에는 여러 가지가 있으며, 각각은 새 뷰 컨트롤러를 사용자에 게 표시 하는 방법과 Storyboard의 다른 뷰 컨트롤러와 상호 작용 하는 방식을 제어 합니다. 이러한 사항은 아래에 설명 되어 있습니다. Segue 개체를 하위 클래스로 지정 하 여 사용자 지정 전환을 구현할 수도 있습니다.

- **Show/push** – push segue는 뷰 컨트롤러를 탐색 스택에 추가 합니다. 이 클래스는 뷰가 스택에 추가 될 뷰 컨트롤러와 동일한 탐색 컨트롤러의 일부인 것으로 가정 합니다. 이는와 동일한 작업  `pushViewController` 을 수행 하며, 일반적으로 화면에 있는 데이터 간의 관계가 있는 경우에 사용 됩니다. Push segue를 사용 하면 뷰 계층 구조를 통해 드릴 다운 탐색을 허용 하는 뒤로 단추와 제목 (스택의 각 뷰에 추가 됨)이 포함 된 탐색 모음이 있는 luxury 제공 됩니다.
- **Modal** – 모달 segue는 애니메이션 전환을 표시 하는 옵션을 사용 하 여 프로젝트의 두 뷰 컨트롤러 간에 관계를 만듭니다. 자식 뷰 컨트롤러는 표시 될 때 부모 뷰 컨트롤러를 완전히 숨깁니다. 후면 단추를 추가 하는 push segue와 달리, `DismissViewController` 이전 뷰 컨트롤러로 돌아가려면 모달 segue를 사용할 때를 사용 해야 합니다.
- **사용자 지정** -사용자 지정 segue을의 하위 클래스로 만들 수 있습니다 `UIStoryboardSegue` .
- **해제** – 해제 segue를 사용 하 여 push 또는 modal segue를 통해 다시 탐색할 수 있습니다. 예를 들어, 모달로 제공 된 뷰 컨트롤러를 해제할 수 있습니다. 이 외에도 한 번만 사용 하 고 일련의 푸시 및 모달 segue을 해제 하 고 단일 해제 작업으로 탐색 계층 구조에서 여러 단계를 되돌릴 수 있습니다. IOS에서 해제 segue를 사용 하는 방법을 이해 하려면  [해제 Segue 만들기](https://github.com/xamarin/recipes/tree/master/Recipes/ios/general/storyboard/unwind_segue) 조리법을 읽어 보세요.
- **원본 없는** – A 원본 없는 segue는 초기 뷰 컨트롤러를 포함 하는 장면을 나타내며 사용자에 게 먼저 표시 되는 보기입니다. 다음 segue 표시 됩니다.

    [![원본 없는 segue](images/sourcelesssegue.png)](images/sourcelesssegue.png#lightbox)

### <a name="adaptive-segue-types"></a>적응 Segue 형식

 ios 8에는 iOS storyboard 파일이 사용 가능한 모든 화면 크기에서 작동할 수 있도록 하는 [크기 클래스가](../storyboards/unified-storyboards.md#size-classes) 도입 되어 개발자가 모든 ios 장치에 대해 하나의 UI를 만들 수 있습니다. 기본적으로 모든 새 Xamarin.ios 응용 프로그램은 size 클래스를 사용 합니다. 이전 프로젝트의 크기 클래스를 사용 하려면 [통합 된 스토리 보드 소개](~/ios/user-interface/storyboards/unified-storyboards.md) 가이드를 참조 하세요.

Size 클래스를 사용 하는 모든 응용 프로그램은 새로운 [*적응 segue*](unified-storyboards.md)사용 합니다. Size 클래스를 사용 하는 경우 iPhone 또는 iPad를 사용 하 고 있는지 여부를 직접 지정 하지 않는다는 점에 주의 해야 합니다. 즉, 작업 해야 하는 부동산의 양에 관계 없이 항상 동일 하 게 표시 되는 하나의 UI를 만듭니다. 적응 Segue는 환경을 심사 하 고 콘텐츠를 표시 하는 데 가장 적합 한 방법을 결정 합니다. 적응 Segue 다음과 같이 표시 됩니다.

[![적응 Segue 드롭다운](images/adaptivesegue.png)](images/adaptivesegue.png#lightbox)

|Segue|설명|
|--- |--- |
|표시|이는 푸시 segue 매우 유사 하지만 화면의 내용을 고려 합니다.|
|세부 정보 표시|앱이 마스터 및 세부 정보 보기를 표시 하는 경우 (예: iPad의 분할 보기 컨트롤러에서) 콘텐츠가 자세히 보기를 대체 합니다. 앱에 마스터 또는 세부 정보만 표시 되는 경우 콘텐츠는 뷰 컨트롤러 스택의 맨 위를 대체 합니다.|
|프레젠테이션|이는 모달 segue 유사 하며, 프레젠테이션 및 전환 스타일을 선택할 수 있습니다.|
|팝 오버 프레젠테이션|그러면 콘텐츠가 팝 오버로 표시 됩니다.|

### <a name="transferring-data-with-segues"></a>Segue를 사용 하 여 데이터 전송

Segue의 이점은 전환으로 끝나지 않습니다. 또한 뷰 컨트롤러 간의 데이터 전송을 관리 하는 데 사용할 수 있습니다. 이는 `PrepareForSegue` 초기 뷰 컨트롤러에서 메서드를 재정의 하 고 직접 데이터를 처리 하 여 수행 됩니다. 예를 들어 단추 누르기를 사용 하 여 segue를 트리거할 때 응용 프로그램은이 메서드를 호출 하 여 탐색이 발생 *하기 전에* 새 뷰 컨트롤러를 준비할 수 있는 기회를 제공 합니다. [Phoneword](/samples/xamarin/ios-samples/hello-ios) 샘플의 다음 코드는이를 보여 줍니다.

```csharp
public override void PrepareForSegue (UIStoryboardSegue segue,
NSObject sender)
{
    base.PrepareForSegue (segue, sender);

    var callHistoryController = segue.DestinationViewController
                                  as CallHistoryController;

    if (callHistoryController != null) {
        callHistoryController.PhoneNumbers = PhoneNumbers;
    }
}
```

이 예제에서는 사용자가 `PrepareForSegue` segue를 트리거할 때 메서드가 호출 됩니다. 먼저 ' 수신 ' 뷰 컨트롤러의 인스턴스를 만들고이를 segue의 대상 뷰 컨트롤러로 설정 해야 합니다. 다음 코드 줄에서이 작업을 수행 합니다.

```csharp
var callHistoryController = segue.DestinationViewController as CallHistoryController;
```

이제 메서드에서 속성을 설정할 수 `DestinationViewController` 있습니다. 이 예제에서는 라는 목록을에 전달 하 `PhoneNumbers` `CallHistoryController` 고 같은 이름의 개체에 할당 하 여 해당 기능을 활용 합니다.

```csharp
if (callHistoryController != null) {
        callHistoryController.PhoneNumbers = PhoneNumbers;
    }
```

전환이 완료 되 면 사용자에 게 채워진 목록이 포함 된이 표시 됩니다 `CallHistoryController` .

## <a name="adding-a-storyboard-to-a-non-storyboard-project"></a>Storyboard가 아닌 프로젝트에 스토리 보드 추가

경우에 따라 이전 비 storyboard 파일에 Storyboard를 추가 해야 할 수도 있습니다. 다음 단계를 수행 하 여 Mac용 Visual Studio에서 프로세스를 간소화할 수 있습니다.

# <a name="visual-studio-for-mac"></a>[Mac용 Visual Studio](#tab/macos)

1. **파일 > 새 파일 > iOS > storyboard** 로 이동 하 여 새 스토리 보드 파일을 만듭니다.

    [![새 파일 대화 상자](images/new-storyboard-xs.png)](images/new-storyboard-xs.png#lightbox)

2. **Info.plist** 의 **주 인터페이스** 섹션에 스토리 보드 이름을 추가 합니다.

    [![Info.plist 편집기](images/infoplist.png)](images/infoplist.png#lightbox)

    이는 `FinishedLaunching` 앱 대리자 내 메서드에서 초기 뷰 컨트롤러를 인스턴스화하는 것과 동일 합니다. 이 옵션을 설정 하면 응용 프로그램은 창을 인스턴스화하고 (다음 단계 참조), 주 storyboard를 로드 하 고, 스토리 보드의 초기 뷰 컨트롤러 (원본 없는 Segue 옆에 있는 하나)의 인스턴스를 창의 속성으로 할당 합니다 `RootViewController` . 그런 다음 창이 화면에 표시 되도록 합니다.

3. 에서 `AppDelegate` `Window` windows 속성을 구현 하는 다음 코드를 사용 하 여 기본 메서드를 재정의 합니다.

    ```csharp
    public override UIWindow Window {
        get;
        set;
    }
    ```

# <a name="visual-studio"></a>[Visual Studio](#tab/windows)

1. 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 새 **파일 > 추가 하 고 새 파일 > iOS > 빈 스토리 보드에 추가** 하 여 새 스토리 보드 파일을 만듭니다.

    [![새 항목 대화 상자](images/new-storyboard-vs.png)](images/new-storyboard-vs.png#lightbox)

2. IOS 응용 프로그램의 **주 인터페이스** 섹션에 스토리 보드 이름을 추가 합니다.

    [![Info.plist 편집기](images/ios-app.png)](images/ios-app.png#lightbox)

    이는 `FinishedLaunching` 앱 대리자 내 메서드에서 초기 뷰 컨트롤러를 인스턴스화하는 것과 동일 합니다. 이 옵션을 설정 하면 응용 프로그램은 창을 인스턴스화하고 (다음 단계 참조), 주 storyboard를 로드 하 고, 스토리 보드의 초기 뷰 컨트롤러 (원본 없는 Segue 옆에 있는 하나)의 인스턴스를 창의 속성으로 할당 합니다 `RootViewController` . 그런 다음 창이 화면에 표시 되도록 합니다.

3. 에서 `AppDelegate` `Window` windows 속성을 구현 하는 다음 코드를 사용 하 여 기본 메서드를 재정의 합니다.

    ```csharp
    public override UIWindow Window {
        get;
        set;
    }
    ```

-----

## <a name="creating-a-storyboard-with-xcode"></a>Xcode를 사용 하 여 스토리 보드 만들기

Mac용 Visual Studio를 사용 하 여 개발한 iOS 앱에서 사용 하기 위해 Xcode을 사용 하 여 스토리 보드를 만들고 수정할 수 있습니다.

스토리 보드는 프로젝트에서 개별 XIB 파일을 완전히 대체 하지만 Storyboard의 개별 뷰 컨트롤러는를 사용 하 여 계속 인스턴스화할 수 있습니다 `Storyboard.InstantiateViewController` .

경우에 따라 응용 프로그램에는 디자이너에서 제공 하는 기본 제공 storyboard 전환을 사용 하 여 처리할 수 없는 특별 한 요구 사항이 있습니다. 예를 들어 응용 프로그램의 현재 상태에 따라 동일한 단추에서 다른 화면을 시작 하는 응용 프로그램을 만드는 경우 뷰 컨트롤러를 수동으로 인스턴스화하고 직접 전환을 프로그래밍할 수 있습니다.

다음 스크린샷은 디자인 화면에서 두 개의 뷰 컨트롤러 사이에 segue 없는 두 개의 뷰 컨트롤러를 보여 줍니다. 다음 섹션에서는 코드에서 전환을 설정 하는 방법을 안내 합니다.

1. 기존 프로젝트 프로젝트에 _빈 IPhone Storyboard_ 를 추가 합니다.

    [![스토리 보드 추가](images/add-storyboard2.png)](images/add-storyboard2.png#lightbox)

2. 스토리 보드 파일을 마우스 오른쪽 단추로 클릭 하 고 **> Xcode Interface Builder를 사용 하 여 열기** 를 선택 하 여 Xcode에서 엽니다.

   > 잠깐만 기본적으로 Xcode Interface builder를 사용 하려는 경우 **프로젝트 > iOS** 의 Mac용 Visual Studio 기본 설정에서 선택할 수 있습니다.  Visual Studio 버전 16.9 및 Mac용 Visual Studio 8.9에서는 Xcode Interface Builder만 옵션이 됩니다. *

   ![기본 디자이너 도구를 선택 합니다.](images/set-preferred-designer-tool.png)

3. Xcode에서 라이브러리 ( **View > Show library** 또는 **Shift + Command + L**)를 통해 스토리 보드에 추가할 수 있는 개체의 목록을 표시 합니다. `Navigation Controller`목록에서 스토리 보드로 개체를 끌어서 스토리 보드에를 추가 합니다. 기본적으로는 `Navigation Controller` 두 개의 화면을 제공 합니다. 오른쪽 화면은이 보기를 클릭 하 `TableViewController` 고 Delete 키를 눌러 제거할 수 있는 간단한 뷰로 바꿀입니다.

    [![라이브러리에서 NavigationController 추가](images/add-navigation-controller.png)](images/add-navigation-controller.png#lightbox)

4. 이 뷰 컨트롤러는 자체 사용자 지정 클래스를 포함 하며 고유한 Storyboard ID도 필요 합니다. 이 새로 추가 된 보기 위의 상자를 클릭 하면 세 개의 아이콘이 표시 되 고 가장 왼쪽에는 뷰의 뷰 컨트롤러가 표시 됩니다. 이 아이콘을 선택 하면 오른쪽 창의 id 탭에서 클래스 및 ID 값을 설정할 수 있습니다. 이러한 값을로 설정 하 `MainViewController` 고 확인 해야 `Use Storyboard ID` 합니다.

    [![Id 패널에서 MainViewController 설정](images/identity-panel.png)](images/identity-panel.png#lightbox)

5. 라이브러리를 다시 사용 하 여 뷰 컨트롤러 컨트롤을 화면으로 끌어옵니다. 루트 뷰 컨트롤러로 설정 됩니다. **컨트롤** 키를 누른 상태에서 왼쪽의 탐색 컨트롤러에서 오른쪽에 있는 새로 추가 된 뷰 컨트롤러까지 클릭 하 여 끌고 메뉴에서 **루트 뷰 컨트롤러** 를 선택 합니다.

    [![라이브러리에서 NavigationController를 추가 하 고 루트 뷰 컨트롤러로 MainViewController 설정](images/add-view-controller.png)](images/add-view-controller.png#lightbox)

6. 이 앱은 다른 보기로 이동 하므로 이전과 마찬가지로 Storyboard에 뷰를 하나 더 추가 합니다. 을 호출 하 `PinkViewController` 고와 동일한 방식으로 해당 값을 설정 합니다 `MainViewController` .

    [![추가 뷰 컨트롤러 추가](images/add-additional-view-controller.png)](images/add-additional-view-controller.png#lightbox)

7. 뷰 컨트롤러는 분홍색 배경을 포함 하므로 옆의 드롭다운을 사용 하 여 특성 패널에서 해당 속성을 설정 `Background` 합니다.

    [![추가 뷰 컨트롤러 추가](images/set-pink-background.png)](images/set-pink-background.png#lightbox)

8. 에서로 이동 하려고 하기 때문에 이전에는 `MainViewController` `PinkViewController` 와 상호 작용 하는 단추가 필요 합니다. 라이브러리를 사용 하 여 단추를에 추가 `MainViewController` 합니다.

    [![MainViewController에 단추 추가](images/add-button.png)](images/add-button.png#lightbox)

스토리 보드가 완성 되지만 지금 프로젝트를 배포 하면 빈 화면이 표시 됩니다. IDE에 storyboard를 사용 하도록 지시 하 고 첫 번째 뷰로 사용 하도록 루트 뷰 컨트롤러를 설정 해야 하기 때문입니다. 일반적으로이 작업은 앞에서 설명한 것 처럼 프로젝트 옵션을 통해 수행할 수 있습니다. 그러나이 예제에서는 동일한 결과를 얻기 위해 다음 코드를 **AppDelegate** 에 추가 합니다.

```csharp
public partial class AppDelegate : UIApplicationDelegate
{
    UIWindow window;
    public static UIStoryboard Storyboard = UIStoryboard.FromName ("MainStoryboard", null);
    public static UIViewController initialViewController;

    public override bool FinishedLaunching (UIApplication app, NSDictionary options)
    {
        window = new UIWindow (UIScreen.MainScreen.Bounds);

        initialViewController = Storyboard.InstantiateInitialViewController () as UIViewController;

        window.RootViewController = initialViewController;
        window.AddSubview(initialViewController.View);
        window.MakeKeyAndVisible ();
        return true;
    }
}
```

코드는 많지만 몇 줄만 알지 못합니다. 먼저 storyboard의 이름인 **mainstoryboard.storyboard** 를 전달 하 여 **AppDelegate** 에 스토리 보드를 등록 합니다. 다음에는 스토리 보드에서를 호출 하 여 스토리 보드에서 초기 뷰 컨트롤러를 인스턴스화하기 위해 응용 프로그램에 지시 하 `InstantiateInitialViewController` 고 해당 뷰 컨트롤러를 응용 프로그램의 루트 뷰 컨트롤러로 설정 합니다. 이 메서드는 사용자에 게 표시 되는 첫 번째 화면을 확인 하 고 해당 뷰 컨트롤러의 새 인스턴스를 만듭니다.

솔루션 창에서 `MainViewcontroller.cs` `*.designer.cs` 4 단계에서 Properties Pad에 클래스 이름을 추가할 때 IDE에서 클래스 및 해당 파일을 만들었는지 확인 합니다. 이 클래스는 기본 클래스를 포함 하는 특수 생성자를 만들었습니다.

```csharp
public MainViewController (IntPtr handle) : base (handle)
{
}
```

Xcode를 사용 하 여 스토리 보드를 만들 때 IDE는 클래스 맨 위에 [[Register]](xref:Foundation.RegisterAttribute) 특성을 자동으로 추가 `*.designer.cs` 하 고 이전 단계에서 지정한 Storyboard ID와 동일한 문자열 식별자를 전달 합니다. 그러면 c #이 Storyboard의 관련 장면에 연결 됩니다.

```csharp
[Register ("MainViewController")]
public partial class MainViewController : UIViewController
{
    public MainViewController (IntPtr handle) : base (handle)
    {
    }
    //...
}
```

클래스 및 메서드를 등록 하는 방법에 대 한 자세한 내용은 [형식 등록자](../../internals/registrar.md)를 참조 하세요.

이 클래스의 마지막 단계는 단추를 연결 하 고 분홍색 보기 컨트롤러에 전환 하는 것입니다. `PinkViewController`스토리 보드에서를 인스턴스화하면 다음 예제 코드에 표시 된 대로를 사용 하 여 push segue를 프로그래밍 합니다 `PushViewController` .

```csharp
public partial class MainViewController : UIViewController
{
    UIViewController pinkViewController;

    public MainViewController (IntPtr handle) : base (handle)
    {
    }

    public override void AwakeFromNib ()
    {
        // Called when loaded from xib or storyboard.
        this.Initialize ();
    }

    public void Initialize()
    {
        //Instantiating View Controller with Storyboard ID 'PinkViewController'
        pinkViewController = Storyboard.InstantiateViewController ("PinkViewController") as PinkViewController;
    }

    public override void ViewDidLoad ()
    {
        base.ViewDidLoad ();

        //When we push the button, we will push the pinkViewController onto our current Navigation Stack
        PinkButton.TouchUpInside += (o, e) =&gt;
        {
            this.NavigationController.PushViewController (pinkViewController, true);
        };
    }
}
```

응용 프로그램을 실행 하면 2 화면 응용 프로그램이 생성 됩니다.

![샘플 앱 실행 화면](images/finishedstoryboard.png)

## <a name="conditional-segues"></a>조건부 Segue

특정 조건에 따라 뷰 컨트롤러 간을 이동 하는 경우가 많습니다. 예를 들어 간단한 로그인 화면을 작성 하는 경우 사용자 이름 및 암호를 확인 한 *경우* 다음 화면 으로만 이동 하려고 합니다.

다음 예제에서는 이전 샘플에 암호 필드를 추가 합니다. 사용자가 올바른 암호를 입력 하는 경우에만 *PinkViewController* 에 액세스할 수 있습니다. 그렇지 않으면 오류가 표시 됩니다.

시작 하기 전에 1 – 8의 이전 단계를 수행 합니다. 이러한 단계에서는 스토리 보드를 만들고, UI 만들기를 시작 하 고, RootViewController로 사용할 뷰 컨트롤러를 앱 대리자에 게 알립니다.

1. 이제 UI를 빌드하고에 나열 된 추가 뷰를 추가 하 여 다음에 나오는 `MainViewController` 스크린샷에서와 같이 보이도록 합니다.

    - UITextField
        - 이름: PasswordTextField
        - 자리 표시자: ' 비밀 암호 입력 '
    - UILabel
        - 텍스트: ' 오류: 암호가 잘못 되었습니다. ! '을 (를) 전달 하지 않아야 합니다.
        - 색: 빨간색
        - 맞춤: 가운데
        - 줄: 2
        - ' 숨김 ' 확인란이 선택 됨    

    [![가운데 선](images/passwordvc.png)](images/passwordvc.png#lightbox)

2. *PinkButton* 에서 *PinkViewController* 로 마우스를 끌어서 Segue에서 분홍색으로 이동 단추와 뷰 컨트롤러 간의 관계를 만든 다음 마우스 위로 **누름** 을 선택 합니다.

3. Segue을 클릭 하 고 *id* 를 지정 합니다 `SegueToPink` .

    [![Segue을 클릭 하 고 SegueToPink를 지정 합니다.](images/namesegue.png)](images/namesegue.png#lightbox)  

4. 마지막으로 클래스에 다음 메서드를 추가 합니다 `ShouldPerformSegue` `MainViewController` .

    ```csharp
    public override bool ShouldPerformSegue (string segueIdentifier, NSObject sender)
    {

        if(segueIdentifier == "SegueToPink"){
            if (PasswordTextField.Text == "password") {
                PasswordTextField.ResignFirstResponder ();
                return true;
            }
            else{
                ErrorLabel.Hidden = false;
                return false;
            }
        }
        return base.ShouldPerformSegue (segueIdentifier, sender);
    }
    ```

이 코드에서는 segueIdentifier와 segue를 비교 하 여 `SegueToPink` 조건을 테스트할 수 있습니다 .이 경우 유효한 암호입니다. 조건에서을 반환 하는 경우 `true` Segue가를 수행 하 고를 표시 합니다 `PinkViewController` . 이면 `false` 새 뷰 컨트롤러가 표시 되지 않습니다.

SegueIdentifier 인수를 ShouldPerformSegue 메서드에 확인 하 여이 뷰 컨트롤러의 모든 Segue에이 방법을 적용할 수 있습니다. 이 경우 하나의 Segue identifier만 `SegueToPink` 있습니다.

작업 예제를 보려면 [수동 storyboard 샘플](/samples/xamarin/ios-samples/manualstoryboard) 에서 Storyboard. 조건부 솔루션을 참조 하십시오.

## <a name="summary"></a>요약

이 문서에서는 Storyboard의 개념과 iOS 응용 프로그램 개발에 도움이 되는 방법에 대해 소개 합니다. 이 예에서는 장면, 뷰 컨트롤러, 보기 및 뷰 계층 구조와 다른 유형의 Segue와의 장면을 연결 하는 방법을 설명 합니다.  또한 storyboard에서 뷰 컨트롤러를 수동으로 인스턴스화하고 조건부 Segue을 만드는 방법을 살펴봅니다.

## <a name="related-links"></a>관련 링크

- [수동 Storyboard (샘플)](/samples/xamarin/ios-samples/manualstoryboard/)
- [IOS Designer 소개](../designer/introduction.md)
- [Storyboard로 변환](https://developer.apple.com/library/ios/#releasenotes/Miscellaneous/RN-AdoptingStoryboards/)
- [UIStoryboard 클래스 참조](https://developer.apple.com/library/ios/#documentation/UIKit/Reference/UIStoryboard_Class/Reference/Reference.html)
---
title: watchOS에서 Xamarin 테이블 컨트롤
description: 이 문서에는 Xamarin에서 watchOS 테이블 컨트롤을 사용 하는 방법을 설명 합니다. 테이블 추가, 행 컨트롤러 추가, 만들기 및 채우기 탭, 및 기타 정보에 응답 하는 행을 설명 합니다.
ms.prod: xamarin
ms.assetid: 7C14126D-9591-4387-A588-3C4521F11C55
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/17/2017
ms.openlocfilehash: cd5e7299874bbfb1b652315a549b9d067d58e9a0
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60881338"
---
# <a name="watchos-table-controls-in-xamarin"></a>watchOS에서 Xamarin 테이블 컨트롤

watchOS `WKInterfaceTable` 컨트롤은 해당 iOS 누구 보다 훨씬 간단 하지만 비슷한 역할을 수행 합니다. 터치 이벤트에 응답 하는 사용자 지정 레이아웃을 가질 수 있는 행의 스크롤 목록을 만듭니다.

![](table-images/table-list-sml.png "조사식 테이블 목록") ![](table-images/table-detail-sml.png)
<!-- watch image courtesy of http://infinitapps.com/bezel/ -->

## <a name="adding-a-table"></a>테이블 추가

끌어서 합니다 **테이블** 는 장면을 제어 합니다. 기본적으로이 (표시 단일 지정 되지 않은 행 레이아웃) 같습니다.

[![](table-images/add-table-sml.png "테이블 추가")](table-images/add-table.png#lightbox)

테이블 이름을 지정 합니다 **속성** 패드의 **이름** 상자, 코드에서를 참조할 수 있도록 합니다.

## <a name="add-a-row-controller"></a>행 컨트롤러 추가

테이블은 자동으로 포함 하는 행 컨트롤러를 나타내는 단일 행을 포함 한 **그룹** 기본적으로 제어 합니다.

설정 하는 **클래스** 행 컨트롤러에 대 한 행을 선택 합니다 **문서 개요** 에 클래스 이름을 입력 하 고는 **속성** 패드:

[![](table-images/add-row-controller-sml.png "Properties pad에서 클래스 이름 입력")](table-images/add-row-controller.png#lightbox)

IDE는 해당 만들어집니다 행의 컨트롤러에 대 한 클래스 설정 되 면 C# 프로젝트의 파일입니다. 행에 컨트롤 (예: 레이블)를 끈 코드에서를 참조할 수 있도록 이름을 지정 합니다.




## <a name="create-and-populate-rows"></a>만들기 및 채우기 행

`SetNumberOfRows` 각 행을 컨트롤러 클래스를 만듭니다 행을 사용 하 여는 `Identifier` 올바른 템플릿을 선택 합니다. 사용자 지정 행 컨트롤러를 지정한 경우 `Identifier`, 변경 **기본** 사용한 식별자로 아래 코드 조각에서입니다. `RowController` *모든 행에 대해* 면 만들어집니다 `SetNumberOfRows` 라고 및 표시 되는 테이블입니다.

```csharp
myTable.SetNumberOfRows ((nint)rows.Count, "default");
        // loads row controller by identifier
```

> [!IMPORTANT]
> 테이블 행은 iOS에서와 같은 가상화 되지 않습니다. (Apple 20 보다 작기 사용 권장) 하는 행 수를 제한 하려고 합니다.

행을 만든 후 각 셀을 채웁니다 해야 합니다 (같은 `GetCell` iOS의 경우). 이 코드 조각은 합니다 [WatchTables 예제](https://developer.xamarin.com/samples/monotouch/watchOS/WatchTables/) 각 행의 레이블을 업데이트

```csharp
for (var i = 0; i < rows.Count; i++) {
    var elementRow = (RowController)myTable.GetRowController (i);
    elementRow.myRowLabel.SetText (rows [i]);
}
```

> [!IMPORTANT]
> 사용 하 여 `SetNumberOfRows` 를 사용 하 여 반복 및 `GetRowController` 시계를 전송할 수 있도록 전체 테이블입니다. 테이블의 후속 뷰 추가 또는 제거 하는 경우 특정 행 사용 하 여 `InsertRowsAt` 고 `RemoveRowsAt` 성능 향상을 위해.


## <a name="respond-to-taps"></a>탭에 응답

두 가지 방법으로 행 선택에 응답할 수 있습니다.

- 구현 된 `DidSelectRow` 인터페이스 컨트롤러에서 메서드 또는
- 스토리 보드 segue를 만들고 구현 `GetContextForSegue` 다른 장면 열려는 행 선택 하려는 경우.

### <a name="didselectrow"></a>DidSelectRow

행 선택 영역을 프로그래밍 방식으로 처리 하려면 구현 합니다 `DidSelectRow` 메서드. 사용 하 여 새 장면을 열려면 `PushController` 장면의 식별자 및를 사용 하 여 데이터 컨텍스트를 전달 합니다.

```csharp
public override void DidSelectRow (WKInterfaceTable table, nint rowIndex)
{
    var rowData = rows [(int)rowIndex];
    Console.WriteLine ("Row selected:" + rowData);
    // if selection should open a new scene
    PushController ("secondInterface", rows[(int)rowIndex]);
}
```

### <a name="getcontextforsegue"></a>GetContextForSegue

다른 장면에 해당 테이블 행에서 스토리 보드 segue를 끌어 (누른 합니다 **제어** 드래그 하는 동안 키).
Segue를 선택 하 고 식별자를 제공 해야 합니다 **속성** 패드 (같은 `secondLevel` 아래 예제에서).

인터페이스 컨트롤러에서 구현 된 `GetContextForSegue` 메서드와 segue를 제시 하는 장면에 제공 해야 하는 데이터 컨텍스트를 반환 합니다.

```csharp
public override NSObject GetContextForSegue (string segueIdentifier, WKInterfaceTable table, nint rowIndex)
{
    if (segueIdentifier == "secondLevel") {
        return new NSString (rows[(int)rowIndex]);
    }
    return null;
}
```

이 데이터의 대상 스토리 보드 장면에 전달 되는 `Awake` 메서드.

## <a name="multiple-row-types"></a>여러 행 형식

기본적으로 테이블 컨트롤에는 디자인할 수 있는 단일 행 형식이 있습니다. 더 많은 행 '템플릿을' 사용을 추가 하는 **행** 상자에 **속성** 패드 자세한 행 컨트롤러를 만들려면:

![](table-images/prototype-rows1.png "프로토타입 행의 수를 설정합니다.")

설정 된 **행** 속성을 **3** 에 컨트롤을 끌어다 놓을 수에 대 한 자리 표시자 추가 행이 만들어집니다. 각 행에 대해 설정 합니다 **클래스** 이름을 합니다 **속성** 행 컨트롤러 클래스를 만들 수 있도록 채움 합니다.

![](table-images/prototype-rows2.png "디자이너에서 프로토타입 행")

다른 행 형식 사용 하 여 테이블을 채우는 데는 `SetRowTypes` 표의 각 행에 사용 되는 행 컨트롤러 형식을 지정 하는 방법입니다. 각 행에 대해 행 컨트롤러를 사용할지를 지정 하는 행의 식별자를 사용 합니다.

이 배열에 있는 요소의 수는 예상 되는 테이블의 행 수가 일치 해야 합니다.

```csharp
myTable.SetRowTypes (new [] {"type1", "default", "default", "type2", "default"});
```

여러 행 컨트롤러를 사용 하 여 테이블을 채울 때 UI를 채울 때 예상한 유형을 추적 하는 것이 해야 합니다.

```csharp
for (var i = 0; i < rows.Count; i++) {
    if (i == 0) {
        var elementRow = (Type1RowController)myTable.GetRowController (i);
        // populate UI controls
    } else if (i == 3) {
        var elementRow = (Type2RowController)myTable.GetRowController (i);
        // populate UI controls
    } else {
        var elementRow = (DefaultRowController)myTable.GetRowController (i);
        // populate UI controls
    }
}
```


## <a name="vertical-detail-paging"></a>세로 세부 페이징

watchOS 3에는 테이블에 대 한 새 기능이 도입 되었습니다: 테이블에 다시 이동 하 고 다른 행을 선택 하지 않고도 각 행에 관련 된 세부 정보 페이지를 스크롤할 수 있습니다. 위아래로 살짝 하거나 디지털 Crown를 사용 하 여 세부 정보 화면을 스크롤할 수 있습니다.

![](table-images/table-scroll-sml.png "세로 세부 페이징 예제") ![](table-images/table-detail-sml.png)

> [!IMPORTANT]
> 이 기능은 현재만 사용할 수 있는 Xcode Interface Builder 스토리 보드를 편집 하 여 합니다.

이 기능을 사용 하려면 선택 합니다 `WKInterfaceTable` 디자인 화면 및 눈금에는 **세로 세부 페이징** 옵션:

![](table-images/vertical-detail-paging-sml.png "세로 세부 페이징 옵션을 선택 하면")

로 [Apple에서 설명한](https://developer.apple.com/reference/watchkit/wkinterfacetable#1682023) 테이블 탐색을 사용 해야 합니다 segue 페이징 기능이 제대로 작동 하도록 합니다. 다시 사용 하는 기존 코드를 작성 `PushController` 데 segue 대신 합니다.

<a name="add_row_controller" />

## <a name="appendix-row-controller-code-example"></a>부록: 행 컨트롤러 코드 예제

IDE 자동으로 만들어집니다 두 개의 코드 파일이 디자이너에서 행 컨트롤러를 만들 때. 생성 된 파일의 코드는 참조에 대 한 아래 표시 됩니다.

첫 번째 클래스의 경우에 예를 들어 라는 **RowController.cs**를 다음과 같이 합니다.

```csharp
using System;
using Foundation;

namespace WatchTablesExtension
{
    public partial class RowController : NSObject
    {
        public RowController ()
        {
        }
    }
}
```

다른 **. designer.cs** 출 선 및 하나를 사용 하 여이 예제와 같은 디자이너 화면에서 생성 된 작업을 포함 하는 partial 클래스 정의 파일이 `WKInterfaceLabel` 제어 합니다.

```csharp
using Foundation;
using System;
using System.CodeDom.Compiler;
using UIKit;

namespace WatchTables.OnWatchExtension
{
    [Register ("RowController")]
    partial class RowController
    {
        [Outlet]
        [GeneratedCode ("iOS Designer", "1.0")]
        public WatchKit.WKInterfaceLabel MyLabel { get; set; }

        void ReleaseDesignerOutlets ()
        {
            if (MyLabel != null) {
                MyLabel.Dispose ();
                MyLabel = null;
            }
        }
    }
}
```

출 선 및 여기에 선언 된 작업을 참조할 수 있습니다-코드에 있지만 **. designer.cs** 파일은 직접 편집할 수 없습니다.



## <a name="related-links"></a>관련 링크

- [WatchTables (샘플)](https://developer.xamarin.com/samples/monotouch/watchOS/WatchTables/)
- [WatchKitCatalog (샘플)](https://developer.xamarin.com/samples/monotouch/watchOS/WatchKitCatalog/)
- [Apple의 테이블 문서](https://developer.apple.com/reference/watchkit/wkinterfacetable)

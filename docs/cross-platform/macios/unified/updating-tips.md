---
title: 코드를 Unified API로 업데이트하는 팁
description: 이 문서에서는 Xamarin의 통합 API를 사용 하도록 응용 프로그램을 업데이트 하는 경우 일반적인 오류 및 유용한 다양 한 팁을 설명 합니다.
ms.prod: xamarin
ms.assetid: 8DD34D21-342C-48E9-97AA-1B649DD8B61F
ms.date: 03/29/2017
author: asb3993
ms.author: amburns
ms.openlocfilehash: a5083e1d31377caece1b8fb4faf33b6e3ff88202
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61211822"
---
# <a name="tips-for-updating-code-to-the-unified-api"></a>코드를 Unified API로 업데이트하는 팁

이전 Xamarin 솔루션을 통합 API로 업데이트할 때 다음 오류가 발생할 수 있습니다.

## <a name="nsinvalidargumentexception-could-not-find-storyboard-error"></a>오류 NSInvalidArgumentException 찾지 스토리 보드

[버그](https://bugzilla.xamarin.com/show_bug.cgi?id=25569) Unified Api로 프로젝트를 변환 하려면 자동화 된 마이그레이션 도구를 사용한 후 발생할 수 있는 Mac 용 Visual Studio의 현재 버전에서입니다. 양식에서 오류 메시지를 받게 되 면 업데이트 후:

```console
Objective-C exception thrown. Name: NSInvalidArgumentException Reason: Could not find a storyboard named 'xxx' in bundle NSBundle...
```

이 문제를 해결 하려면 다음 빌드 대상 파일을 찾아 다음을 수행할 수 있습니다.

```console
/Library/Frameworks/Xamarin.iOS.framework/Versions/Current/lib/mono/2.1/Xamarin.iOS.Common.targets
```

이 파일에 다음 선언을 찾아 대상 해야 합니다.

```xml
<Target Name="_CopyContentToBundle"
        Inputs = "@(_BundleResourceWithLogicalName)"
        Outputs = "@(_BundleResourceWithLogicalName -> '$(_AppBundlePath)%(LogicalName)')" >
```

추가 된 `DependsOnTargets="_CollectBundleResources"` 특성을 합니다. 다음과 같습니다.

```xml
<Target Name="_CopyContentToBundle"
        DependsOnTargets="_CollectBundleResources"
        Inputs = "@(_BundleResourceWithLogicalName)"
        Outputs = "@(_BundleResourceWithLogicalName -> '$(_AppBundlePath)%(LogicalName)')" >
```

파일을 저장, Mac 용 Visual Studio를 다시 부팅 및 정리를 수행 및 프로젝트가 다시 작성 합니다. 이 문제에 대 한 수정 xamarin 곧 출시 될 해야 합니다.

## <a name="useful-tips"></a>유용한 팁

마이그레이션 도구를 사용한 후 수동 개입이 필요한 일부 컴파일러 오류가 여전히 발생할 수 있습니다.
수동으로 수정 해야 할 수 있는 몇 가지 사항은 다음과 같습니다.

* 비교 `enum`가 필요할 수 있습니다는 `(int)` 캐스트 합니다.

* `NSDictionary.IntValue` 이제 반환를 `nint`, 있는지는 `Int32Value` 대신 사용할 수 있습니다.

* `nfloat` 및 `nint` 형식으로 표시할 수 없습니다 `const`;   `static readonly nint` 는 적절 한 대안입니다.

* 직접 사용 하는 것은 `MonoTouch.` 네임 스페이스는 이제 일반적으로는 `ObjCRuntime.` 네임 스페이스 (예:: `MonoTouch.Constants.Version` 이제 `ObjCRuntime.Constants.Version`).

* 개체를 serialize 하는 코드는 serialize 하려고 할 때 중단 될 수 있습니다 `nint` 고 `nfloat` 형식입니다. Serialization 코드에는 마이그레이션 후 예상 대로 작동 하는지 확인 해야 합니다.

* 자동화 된 도구 내에서 코드를 누락 하는 경우에 따라 `#if #else` 조건부 컴파일러 지시문입니다. 수정 프로그램을 수동으로 수행 해야 하는 예제의 (아래 일반적인 오류 참조).

* 수동으로 내보낸된 메서드를 사용 하 여 `[Export]` 반환 형식이 수동으로 업데이트 해야 하는이 코드 snippert의 예를 들어 마이그레이션 도구에서 자동으로 해결 하지 않을 수 있습니다 `nfloat`:

    ```csharp
    [Export("tableView:heightForRowAtIndexPath:")]
    public nfloat HeightForRow(UITableView tableView, NSIndexPath indexPath)
    ```

 * 무손실 변환 하지 않기 때문에 통합 API NSDate 및.NET DateTime 간에 암시적 변환이 발생을 제공 하지 않습니다. 와 관련 된 오류를 방지 하기 위해 `DateTimeKind.Unspecified` .NET 변환 `DateTime` 으로 로컬 또는 UTC로 캐스팅 하기 전에 `NSDate`입니다.

 * Objective C 범주 메서드는 이제 통합 API의 확장 메서드로 생성 됩니다. 예를 들어 코드에 사용 했던 `UIView.DrawString` 이제 참조 `NSString.DrawString` Unified API에서 합니다.

 * AVFoundation 클래스를 사용 하는 코드 `VideoSettings` 사용으로 변경 해야 합니다 `WeakVideoSettings` 속성입니다. 이 위해서는 `Dictionary`를 사용할 수 있는 설정 클래스에서 속성으로 예를 들어:

    ```csharp
    vidrec.WeakVideoSettings = new AVVideoSettings() { ... }.Dictionary;
    ```

 * NSObject `.ctor(IntPtr)` 생성자에서 변경 된 public 보호 ([부적절 한 사용을 방지 하기 위해](~/cross-platform/macios/unified/overview.md#NSObject_ctor)).

 * `NSAction` 되었습니다 [대체](~/cross-platform/macios/unified/overview.md#NSAction) starndard.NET을 사용 하 여 `Action`입니다. 또한 몇 가지 간단한 단일 매개 변수인 대리자로 대체 되었습니다 `Action<T>`합니다.

마지막으로, 참조를 [클래식 v Unified API 차이점](https://developer.xamarin.com/releases/ios/api_changes/classic-vs-unified-8.6.0/) Api 코드에서 변경 내용을 조회 하 합니다. 검색 [이 페이지](https://developer.xamarin.com/releases/ios/api_changes/classic-vs-unified-8.6.0/) 클래식 Api에 대 한 새로운 했습니다 된 업데이트를 찾을 수 있도록 도와줍니다.

**참고:** 는 `MonoTouch.Dialog` 네임 스페이스 마이그레이션 후 동일 하 게 유지 합니다. 코드를 사용 하는 경우 **MonoTouch.Dialog** 네임 스페이스를 사용 하 여 수행 해야 할 *되지* 변경 `MonoTouch.Dialog` 에 `Dialog`!

## <a name="common-compiler-errors"></a>일반적인 컴파일러 오류

일반적인 오류에 대 한 다른 예제는 솔루션과 함께 아래에:

**Error CS0012: 'MonoTouch.UIKit.UIView' 형식이 참조 되지 않은 어셈블리에 정의 됩니다.**

해결 방법: 이 구성 요소 또는 통합 API를 사용 하 여 빌드되지 않았습니다 하는 NuGet 패키지를 프로젝트 참조 의미 합니다. 삭제 하 고 다시 모든 구성 요소와 NuGet 추가 패키지 있습니다. 이 오류가 해결 되지 않으면, 외부 라이브러리는 통합 API를 아직 지원 하지 않습니다.

**오류 MT0034: -동일한 Xamarin.iOS 프로젝트에서 'monotouch.dll' 및 'Xamarin.iOS.dll' 둘 다 포함할 수 없습니다 'Xamarin.iOS.dll'는 'monotouch.dll'에서 참조 하는 동안 명시적으로 참조 됩니다 ' Xamarin.Mobile, 버전 0.6.3.0, Culture = neutral, PublicKeyToken = null'.**

해결 방법: 이 오류를 발생 시키는 구성 요소를 삭제 하 고 프로젝트를 다시 추가 합니다.

**Error CS0234: 'Foundation' 'MonoTouch' 네임 스페이스에 존재 하지 않는 형식 또는 네임 스페이스 이름입니다. 어셈블리 참조가 없습니다?**

해결 방법: Mac 용 Visual Studio에서 자동화 된 마이그레이션 도구 *해야* 모든 업데이트 `MonoTouch.Foundation` 에 대 한 참조 `Foundation`이지만 경우에 따라서는 이러한 해야 수동으로 업데이트 해야 합니다. 에 포함 된 이전에 다른 네임 스페이스에 대 한 유사한 오류가 나타날 수 있습니다 `MonoTouch`와 같은 `UIKit`합니다.

**오류 CS0266: 'System.float'를 ' double '를 암시적으로 변환할 수 없습니다.**

해결 방법: 유형을 변경 하며 캐스팅할 `nfloat`합니다. 64 비트 드라이버가 사용 하 여 다른 형식에 대 한도이 오류가 발생할 수 있습니다 (같은 `nint`,)

```csharp
nfloat scale = (nfloat)Math.Min(rect.Width, rect.Height);
```

**오류 CS0266: 형식 'CoreGraphics.CGRect' 'System.Drawing.RectangleF'를 암시적으로 변환할 수 있습니다. 명시적 변환이 있습니다 (누락 된 캐스트?)**

해결 방법: 인스턴스를 변경 `RectangleF` 하 `CGRect`, `SizeF` 에 `CGSize`, 및 `PointF` 에 `CGPoint`입니다. 네임 스페이스 `using System.Drawing;` 바꿔야 `using CoreGraphics;` (이미 존재 하지) 경우입니다.

**오류 CS1502: 가장에 대 한 일치 하는 메서드에 오버 로드 된 ' CoreGraphics.CGContext.SetLineDash (System.nfloat, System.nfloat[])'에 잘못 된 인수가 있습니다.**

해결 방법: 배열 형식을 변경 `nfloat[]` 명시적으로 캐스팅 하 고 `Math.PI`입니다.

```csharp
grphc.SetLineDash (0, new nfloat[] { 0, 3 * (nfloat)Math.PI });
```

**오류 CS0115: 'WordsTableSource.RowsInSection (UIKit.UITableView, int)'를 재정의 하지만 재정의할를 찾을 수는 적절 한 방법을 표시 됩니다.**

해결 방법: 반환 값 및 매개 변수 유형을 변경 하 여 `nint`입니다. 일반적으로 이런 것과 같은 메서드 재정의에서 온 `UITableViewSource`등 `RowsInSection`, `NumberOfSections`, `GetHeightForRow`를 `TitleForHeader`, `GetViewForHeader`등입니다.

```csharp
public override nint RowsInSection (UITableView tableview, nint section) {
```

**오류 CS0508: `WordsTableSource.NumberOfSections(UIKit.UITableView)': return type must be 'System.nint' to match overridden member `UIKit.UITableViewSource.NumberOfSections(UIKit.UITableView)'**

해결 방법: 반환 형식이 변경 되 면 `nint`를 반환 값을 캐스팅 `nint`합니다.

```csharp
public override nint NumberOfSections (UITableView tableView)
{
    return (nint)navItems.Count;
}
```

**오류 CS1061: 형식 'CoreGraphics.CGPath' 'AddElipseInRect'에 대 한 정의가 포함 되지 않습니다.**

해결 방법: 에 대 한 맞춤법 수정 `AddEllipseInRect`합니다. 다른 이름 변경 내용은 다음과 같습니다.

* 'Color.Black' 변경 `NSColor.Black`합니다.
* MapKit 'AddAnnotation' 변경 `AddAnnotations`합니다.
* 'DataUsingEncoding' AVFoundation 변경 `Encode`합니다.
* 'AVMetadataObject.TypeQRCode' AVFoundation 변경 `AVMetadataObjectType.QRCode`합니다.
* 'VideoSettings' AVFoundation 변경 `WeakVideoSettings`합니다.
* 변경 하려면 PopViewControllerAnimated `PopViewController`합니다.
* 'CGBitmapContext.SetRGBFillColor' CoreGraphics 변경 `SetFillColor`합니다.

**'MapKit.MKAnnotation.Coordinate'에 재정의 가능한 set 접근자 (CS0546) 없기 때문에 오류 CS0546: 재정의할 수 없습니다.**

MKAnnotation 서브클래싱 사용자 지정 주석을 만드는 경우 좌표 필드에는 setter, getter만

[해결](https://forums.xamarin.com/discussion/comment/109505/#Comment_109505):

* 에 대 한 좌표를 추적 하기 위해 필드 추가
* 좌표 속성의 getter에서이 필드를 반환 합니다.
* SetCoordinate 메서드를 재정의 하 고 필드를 설정 합니다.
* 전달 된 좌표 매개 변수를 사용 하 여 프로그램 ctor SetCoordinate 호출

결과는 다음과 비슷합니다.

```csharp
class BasicPinAnnotation : MKAnnotation
{
    private CLLocationCoordinate2D _coordinate;

    public override CLLocationCoordinate2D Coordinate
    {
        get
        {
            return _coordinate;
        }
    }

    public override void SetCoordinate(CLLocationCoordinate2D value)
    {
        _coordinate = value;
    }

    public BasicPinAnnotation (CLLocationCoordinate2D coordinate)
    {
        SetCoordinate(coordinate);
    }
}
```

## <a name="related-links"></a>관련 링크

- [앱 업데이트](~/cross-platform/macios/unified/updating-apps.md)
- [IOS 앱 업데이트](~/cross-platform/macios/unified/updating-ios-apps.md)
- [Mac 앱 업데이트](~/cross-platform/macios/unified/updating-mac-apps.md)
- [Xamarin.Forms 앱 업데이트](~/cross-platform/macios/unified/updating-xamarin-forms-apps.md)
- [바인딩 업데이트](~/cross-platform/macios/unified/update-binding.md)
- [플랫폼 간 앱에서의 네이티브 형식 작업](~/cross-platform/macios/native-types-cross-platform.md)
- [클래식 vs 통합 API 차이점](https://developer.xamarin.com/releases/ios/api_changes/classic-vs-unified-8.6.0/)

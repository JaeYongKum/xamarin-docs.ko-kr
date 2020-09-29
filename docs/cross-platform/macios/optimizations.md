---
title: 빌드 최적화
description: 이 문서에서는 Xamarin.ios 및 Xamarin.ios 앱에 대 한 빌드 시 적용 되는 다양 한 최적화에 대해 설명 합니다.
ms.prod: xamarin
ms.assetid: 84B67E31-B217-443D-89E5-CFE1923CB14E
author: davidortinau
ms.author: daortin
ms.date: 04/16/2018
ms.openlocfilehash: d3076e35d6e9b7e44ec2f9537f250295eaff7e2e
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91453560"
---
# <a name="build-optimizations"></a>빌드 최적화

이 문서에서는 Xamarin.ios 및 Xamarin.ios 앱에 대 한 빌드 시 적용 되는 다양 한 최적화에 대해 설명 합니다.

## <a name="remove-uiapplicationensureuithread--nsapplicationensureuithread"></a>UIApplication/NSApplication. EnsureUIThread를 제거 합니다.

[EnsureUIThread][1] (xamarin.ios의 경우) 또는 (xamarin.ios의 경우)에 대 한 호출을 제거 `NSApplication.EnsureUIThread` 합니다.

이 최적화는 다음 코드 유형을 변경 합니다.

```csharp
public virtual void AddChildViewController (UIViewController childController)
{
    global::UIKit.UIApplication.EnsureUIThread ();
    // ...
}
```

다음과 같이 합니다.

```csharp
public virtual void AddChildViewController (UIViewController childController)
{
    // ...
}
```

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

기본적으로 릴리스 빌드에 대해 사용 하도록 설정 됩니다.

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]remove-uithread-checks` .

[1]: /dotnet/api/UIKit.UIApplication.EnsureUIThread

## <a name="inline-intptrsize"></a>인라인 IntPtr 크기

대상 플랫폼에 따라의 상수 값을 Inlines `IntPtr.Size` 합니다.

이 최적화는 다음 코드 유형을 변경 합니다.

```csharp
if (IntPtr.Size == 8) {
    Console.WriteLine ("64-bit platform");
} else {
    Console.WriteLine ("32-bit platform");
}
```

다음으로 (64 비트 플랫폼용으로 빌드하는 경우):

```csharp
if (8 == 8) {
    Console.WriteLine ("64-bit platform");
} else {
    Console.WriteLine ("32-bit platform");
}
```

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

기본적으로 단일 아키텍처를 대상으로 하는 경우 또는 플랫폼 어셈블리 (**Xamarin.iOS.dll**, **Xamarin.TVOS.dll**, **Xamarin.WatchOS.dll** 또는 **Xamarin.Mac.dll**)에 대해 사용 하도록 설정 됩니다.

여러 아키텍처를 대상으로 하는 경우이 최적화는 32 비트 버전 및 64 비트 버전의 앱에 대해 서로 다른 어셈블리를 만들며, 두 버전은 앱에 포함 되어야 하므로 최종 앱 크기를 줄이는 대신 효과적으로 확장 합니다.

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]inline-intptr-size` .

## <a name="inline-nsobjectisdirectbinding"></a>인라인 NSObject. IsDirectBinding

`NSObject.IsDirectBinding` 특정 인스턴스가 래퍼 형식 인지 여부를 확인 하는 인스턴스 속성입니다. 래퍼 형식은 네이티브 형식에 매핑되는 관리 되는 형식입니다. 예를 들어 관리 되는 `UIKit.UIView` 형식은 네이티브 형식에 매핑됩니다 .이 경우에는 사용자 형식이 반대로 사용 됩니다 `UIView` `class MyUIView : UIKit.UIView` .

`IsDirectBinding`값에 따라 사용할 버전이 결정 되기 때문에 목표-C를 호출할 때의 값을 알고 있어야 합니다 `objc_msgSend` .

다음 코드만 제공 됩니다.

```csharp
class UIView : NSObject {
    public virtual string SomeProperty {
        get {
            if (IsDirectBinding) {
                return "true";
            } else {
                return "false"
            }
        }
    }
}

class NSUrl : NSObject {
    public virtual string SomeOtherProperty {
        get {
            if (IsDirectBinding) {
                return "true";
            } else {
                return "false"
            }
        }
    }
}

class MyUIView : UIView {
}
```

`UIView.SomeProperty`의 값 `IsDirectBinding` 이 상수가 아니고 인라인 될 수 없음을 확인할 수 있습니다.

```csharp
void uiView = new UIView ();
Console.WriteLine (uiView.SomeProperty); /* prints 'true' */
void myView = new MyUIView ();
Console.WriteLine (myView.SomeProperty); // prints 'false'
```

그러나 앱의 모든 형식을 확인 하 고에서 상속 되는 형식이 없는지 확인할 수 `NSUrl` 있으며, 따라서이 값을 상수로 인라인 하는 것이 안전 합니다 `IsDirectBinding` `true` .

```csharp
void myURL = new NSUrl ();
Console.WriteLine (myURL.SomeOtherProperty); // prints 'true'
// There's no way to make SomeOtherProperty print anything but 'true', since there are no NSUrl subclasses.
```

특히이 최적화는 다음 코드 형식을 변경 합니다 (에 대 한 바인딩 코드 `NSUrl.AbsoluteUrl` ).

```csharp
if (IsDirectBinding) {
    return Runtime.GetNSObject<NSUrl> (global::ObjCRuntime.Messaging.IntPtr_objc_msgSend (this.Handle, Selector.GetHandle ("absoluteURL")));
} else {
    return Runtime.GetNSObject<NSUrl> (global::ObjCRuntime.Messaging.IntPtr_objc_msgSendSuper (this.SuperHandle, Selector.GetHandle ("absoluteURL")));
}
```

응용 프로그램에의 서브 클래스가 없다는 것을 확인할 수 있는 경우 다음과 `NSUrl` 같이 합니다.

```csharp
if (true) {
    return Runtime.GetNSObject<NSUrl> (global::ObjCRuntime.Messaging.IntPtr_objc_msgSend (this.Handle, Selector.GetHandle ("absoluteURL")));
} else {
    return Runtime.GetNSObject<NSUrl> (global::ObjCRuntime.Messaging.IntPtr_objc_msgSendSuper (this.SuperHandle, Selector.GetHandle ("absoluteURL")));
}
```

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

항상 Xamarin.ios에 대해 기본적으로 사용 하도록 설정 되며, xamarin.ios의 경우 항상 기본적으로 사용 하지 않도록 설정 되어 있습니다. Xamarin.ios에서 어셈블리를 동적으로 로드할 수 있기 때문에 특정 클래스가 서브클래싱 되지 않는 것을 확인할 수 없습니다.

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]inline-isdirectbinding` .

## <a name="inline-runtimearch"></a>인라인 런타임.

이 최적화는 다음 코드 유형을 변경 합니다.

```csharp
if (Runtime.Arch == Arch.DEVICE) {
    Console.WriteLine ("Running on device");
} else {
    Console.WriteLine ("Running in the simulator");
}
```

다음으로 (장치를 빌드하는 경우):

```csharp
if (Arch.DEVICE == Arch.DEVICE) {
    Console.WriteLine ("Running on device");
} else {
    Console.WriteLine ("Running in the simulator");
}
```

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

Xamarin.ios의 경우 항상 기본적으로 사용 하도록 설정 되어 있습니다 (Xamarin.ios에는 사용할 수 없음).

Mtouch에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]inline-runtime-arch` .

## <a name="dead-code-elimination"></a>데드 코드 제거

이 최적화는 다음 코드 유형을 변경 합니다.

```csharp
if (true) {
    Console.WriteLine ("Doing this");
} else {
    Console.WriteLine ("Not doing this");
}
```

범주로

```csharp
Console.WriteLine ("Doing this");
```

또한 다음과 같이 상수 비교를 평가 합니다.

```csharp
if (8 == 8) {
    Console.WriteLine ("Doing this");
} else {
    Console.WriteLine ("Not doing this");
}
```

그리고 식이 항상 true 인지 확인 하 `8 == 8` 고 다음과 같이 줄입니다.

```csharp
Console.WriteLine ("Doing this");
```

이는 다음 코드 형식을 변환할 수 있기 때문에 인라인 최적화와 함께 사용 하는 경우의 강력한 최적화입니다 (의 바인딩 코드 `NFCIso15693ReadMultipleBlocksConfiguration.Range` ).

```csharp
NSRange ret;
if (IsDirectBinding) {
    if (Runtime.Arch == Arch.DEVICE) {
        if (IntPtr.Size == 8) {
            ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSend (this.Handle, Selector.GetHandle ("range"));
        } else {
            global::ObjCRuntime.Messaging.NSRange_objc_msgSend_stret (out ret, this.Handle, Selector.GetHandle ("range"));
        }
    } else if (IntPtr.Size == 8) {
        ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSend (this.Handle, Selector.GetHandle ("range"));
    } else {
        ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSend (this.Handle, Selector.GetHandle ("range"));
    }
} else {
    if (Runtime.Arch == Arch.DEVICE) {
        if (IntPtr.Size == 8) {
            ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSendSuper (this.SuperHandle, Selector.GetHandle ("range"));
        } else {
            global::ObjCRuntime.Messaging.NSRange_objc_msgSendSuper_stret (out ret, this.SuperHandle, Selector.GetHandle ("range"));
        }
    } else if (IntPtr.Size == 8) {
        ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSendSuper (this.SuperHandle, Selector.GetHandle ("range"));
    } else {
        ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSendSuper (this.SuperHandle, Selector.GetHandle ("range"));
    }
}
return ret;
```

(64 비트 장치에 대해 빌드할 때 및 앱에 하위 클래스가 없도록 할 수 있는 경우 `NFCIso15693ReadMultipleBlocksConfiguration` ).

```csharp
NSRange ret;
ret = global::ObjCRuntime.Messaging.NSRange_objc_msgSend (this.Handle, Selector.GetHandle ("range"));
return ret;
```

AOT 컴파일러는 이와 같이 데드 코드를 제거할 수 있지만이 최적화는 링커 내에서 수행 됩니다. 즉, 링커가 더 이상 사용 되지 않아 제거 될 수 있는 여러 메서드가 있는지 확인할 수 있습니다 (다른 곳에서 사용 하지 않는 경우).

* `global::ObjCRuntime.Messaging.NSRange_objc_msgSend_stret`
* `global::ObjCRuntime.Messaging.NSRange_objc_msgSendSuper`
* `global::ObjCRuntime.Messaging.NSRange_objc_msgSendSuper_stret`

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

링커에서는 항상 기본적으로 사용 하도록 설정 되어 있습니다 (링커를 사용 하는 경우).

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]dead-code-elimination` .

## <a name="optimize-calls-to-blockliteralsetupblock"></a>BlockLiteral에 대 한 호출 최적화. SetupBlock

Xamarin.ios/Mac 런타임은 관리 되는 대리자에 대 한 목표-C 블록을 만들 때 블록 시그니처를 알고 있어야 합니다. 이 작업은 비용이 많이 드는 작업 일 수 있습니다. 이 최적화는 빌드 시 블록 시그니처를 계산 하 고, `SetupBlock` 대신 인수로 시그니처를 사용 하는 메서드를 호출 하도록 IL을 수정 합니다. 이렇게 하면 런타임에 서명을 계산 하지 않아도 됩니다.

벤치 마크는 10 ~ 15 계수 블록을 호출 하는 속도를 향상 시키는 것을 보여 줍니다.

다음 [코드](https://github.com/xamarin/xamarin-macios/blob/018f7153441d9d7e0f58e2046f39eeb46f1ff480/src/UIKit/UIAccessibility.cs#L198-L211)를 변환 합니다.

```csharp
public static void RequestGuidedAccessSession (bool enable, Action<bool> completionHandler)
{
    // ...
    block_handler.SetupBlock (callback, completionHandler);
    // ...
}
```

범주로

```csharp
public static void RequestGuidedAccessSession (bool enable, Action<bool> completionHandler)
{
    // ...
    block_handler.SetupBlockImpl (callback, completionHandler, true, "v@?B");
    // ...
}
```

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

정적 등록자를 사용 하는 경우 기본적으로 사용 하도록 설정 됩니다. (Xamarin.ios에서 정적 등록자는 장치 빌드에 대해 기본적으로 사용 하도록 설정 되 고, Xamarin.ios에서 정적 등록자는 릴리스 빌드에 대해 기본적으로 사용 하도록 설정 됩니다.)

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]blockliteral-setupblock` .

## <a name="optimize-support-for-protocols"></a>프로토콜에 대 한 지원 최적화

Xamarin.ios/Mac 런타임에는 관리 되는 형식이 목표-C 프로토콜을 구현 하는 방법에 대 한 정보가 필요 합니다. 이 정보는 인터페이스 (및 이러한 인터페이스의 특성)에 저장 되며,이는 매우 효율적인 형식이 아니며 링커에 친숙 하지 않습니다.

한 가지 예는 이러한 인터페이스가 특성의 모든 프로토콜 멤버에 대 한 정보를 저장 하는 것입니다. 여기에는 `[ProtocolMember]` 해당 멤버의 매개 변수 형식에 대 한 참조가 포함 됩니다. 즉, 이러한 인터페이스를 구현 하기만 하면 앱이 호출 하거나 구현 하지 않는 선택적 멤버에 대해서도 링커에서 해당 인터페이스에서 사용 되는 모든 형식을 유지 하 게 됩니다.

이러한 최적화를 통해 정적 등록자는 런타임에 쉽고 빠르게 찾을 수 있는 적은 양의 메모리를 사용 하는 효율적인 형식으로 필요한 정보를 저장할 수 있습니다.

또한 이러한 인터페이스 및 관련 특성을 유지 해야 하는 것은 아니지만 링커에 대해 학습 합니다.

이러한 최적화를 위해서는 링커와 정적 등록자를 모두 사용 하도록 설정 해야 합니다.

Xamarin.ios에서이 최적화는 링커 및 정적 등록자를 모두 사용 하도록 설정한 경우 기본적으로 사용 하도록 설정 됩니다.

Xamarin.ios에서이 최적화는 기본적으로 사용 되지 않습니다. Xamarin.ios에서 어셈블리를 동적으로 로드 하는 것을 지원 하기 때문에 이러한 어셈블리는 빌드 시간에 알려지지 않아 최적화 되지 않을 수 있기 때문입니다.

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=-register-protocols` .

## <a name="remove-the-dynamic-registrar"></a>동적 등록자 제거

Xamarin.ios 및 Xamarin.ios 런타임에는 목표-C 런타임에 [관리 되는 형식을 등록](~/ios/internals/registrar.md) 하는 기능이 포함 되어 있습니다. 빌드 시간이 나 런타임에 (또는 빌드 시간에 부분적으로 또는 빌드 시간에 부분적으로) 수행 될 수 있지만 빌드 시간에 완전히 수행 되는 경우 런타임에이를 수행 하는 지원 코드를 제거할 수 있습니다. 이로 인해 특히 확장 또는 watchOS apps와 같은 작은 앱에 대 한 앱 크기가 상당히 줄어듭니다.

이렇게 최적화 하려면 정적 등록자와 링커를 모두 사용 하도록 설정 해야 합니다.

링커는 동적 등록자를 제거 하는 것이 안전한 지 여부를 확인 하 고, 그럴 경우 제거 하려고 시도 합니다.

Xamarin.ios는 런타임에 어셈블리를 동적으로 로드 하는 것을 지원 하기 때문에 (빌드 시간에 알려지지 않음) 빌드 시 안전 최적화 인지 여부를 확인할 수 없습니다. 즉, Xamarin.ios 앱에 대해서는이 최적화가 기본적으로 사용 되지 않습니다.

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]remove-dynamic-registrar` .

동적 등록자를 제거 하도록 기본값을 재정의 하는 경우 링커에서는 안전 하지 않은 것을 감지 하면 경고를 내보냅니다. 그러나 동적 등록자는 여전히 제거 됩니다.

## <a name="inline-runtimedynamicregistrationsupported"></a>인라인 런타임. DynamicRegistrationSupported

`Runtime.DynamicRegistrationSupported`빌드 시간에 결정 된 대로의 값을 Inlines 합니다.

동적 등록자를 제거 하는 경우 ( [동적 등록자 최적화 제거](#remove-the-dynamic-registrar) 참조) 상수 값이 고, `false` 그렇지 않으면 상수 `true` 값입니다.

이 최적화는 다음 코드 유형을 변경 합니다.

```csharp
if (Runtime.DynamicRegistrationSupported) {
    Console.WriteLine ("do something");
} else {
    throw new Exception ("dynamic registration is not supported");
}
```

동적 등록자를 제거 하는 경우 다음과 같이 됩니다.

```csharp
throw new Exception ("dynamic registration is not supported");
```

동적 등록자를 제거 하지 않은 경우에는 다음을 수행 합니다.

```csharp
Console.WriteLine ("do something");
```

이러한 최적화를 위해서는 링커를 사용 하도록 설정 해야 하며 특성을 가진 메서드에만 적용 됩니다 `[BindingImpl (BindingImplOptions.Optimizable)]` .

링커에서는 항상 기본적으로 사용 하도록 설정 되어 있습니다 (링커를 사용 하는 경우).

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]inline-dynamic-registration-supported` .

## <a name="precompute-methods-to-create-managed-delegates-for-objective-c-blocks"></a>목적-C 블록에 대 한 관리 되는 대리자를 만드는 메서드를 미리 계산 합니다.

목표-C가 블록을 매개 변수로 사용 하는 선택기를 호출 하 고 관리 코드에서 해당 메서드를 재정의 한 경우 Xamarin.ios/Xamarin.ios 런타임에서는 해당 블록에 대 한 대리자를 만들어야 합니다.

바인딩 생성기에 의해 생성 되는 바인딩 코드에는 `[BlockProxy]` `Create` 이 작업을 수행할 수 있는 메서드를 사용 하 여 형식을 지정 하는 특성이 포함 됩니다.

다음과 같은 목표-C 코드를 지정 합니다.

```objc
@interface ObjCBlockTester : NSObject {
}
-(void) classCallback: (void (^)())completionHandler;
-(void) callClassCallback;
@end

@implementation ObjCBlockTester
-(void) classCallback: (void (^)())completionHandler
{
}

-(void) callClassCallback
{
    [self classCallback: ^()
    {
        NSLog (@"called!");
    }];
}
@end
```

다음 바인딩 코드는 다음과 같습니다.

```csharp
[BaseType (typeof (NSObject))]
interface ObjCBlockTester
{
    [Export ("classCallback:")]
    void ClassCallback (Action completionHandler);
}
```

생성기는 다음을 생성 합니다.

```csharp
[Register("ObjCBlockTester", true)]
public unsafe partial class ObjCBlockTester : NSObject {
    // unrelated code...

    [Export ("callClassCallback")]
    [BindingImpl (BindingImplOptions.GeneratedCode | BindingImplOptions.Optimizable)]
    public virtual void CallClassCallback ()
    {
        if (IsDirectBinding) {
            ApiDefinition.Messaging.void_objc_msgSend (this.Handle, Selector.GetHandle ("callClassCallback"));
        } else {
            ApiDefinition.Messaging.void_objc_msgSendSuper (this.SuperHandle, Selector.GetHandle ("callClassCallback"));
        }
    }

    [Export ("classCallback:")]
    [BindingImpl (BindingImplOptions.GeneratedCode | BindingImplOptions.Optimizable)]
    public unsafe virtual void ClassCallback ([BlockProxy (typeof (Trampolines.NIDActionArity1V0))] System.Action completionHandler)
    {
        // ...

    }
}

static class Trampolines
{
    [UnmanagedFunctionPointerAttribute (CallingConvention.Cdecl)]
    [UserDelegateType (typeof (System.Action))]
    internal delegate void DActionArity1V0 (IntPtr block);

    static internal class SDActionArity1V0 {
        static internal readonly DActionArity1V0 Handler = Invoke;

        [MonoPInvokeCallback (typeof (DActionArity1V0))]
        static unsafe void Invoke (IntPtr block) {
            var descriptor = (BlockLiteral *) block;
            var del = (System.Action) (descriptor->Target);
            if (del != null)
                del (obj);
        }
    }

    internal class NIDActionArity1V0 {
        IntPtr blockPtr;
        DActionArity1V0 invoker;

        [Preserve (Conditional=true)]
        [BindingImpl (BindingImplOptions.GeneratedCode | BindingImplOptions.Optimizable)]
        public unsafe NIDActionArity1V0 (BlockLiteral *block)
        {
            blockPtr = _Block_copy ((IntPtr) block);
            invoker = block->GetDelegateForBlock<DActionArity1V0> ();
        }

        [Preserve (Conditional=true)]
        [BindingImpl (BindingImplOptions.GeneratedCode | BindingImplOptions.Optimizable)]
        ~NIDActionArity1V0 ()
        {
            _Block_release (blockPtr);
        }

        [Preserve (Conditional=true)]
        [BindingImpl (BindingImplOptions.GeneratedCode | BindingImplOptions.Optimizable)]
        public unsafe static System.Action Create (IntPtr block)
        {
            if (block == IntPtr.Zero)
                return null;
            if (BlockLiteral.IsManagedBlock (block)) {
                var existing_delegate = ((BlockLiteral *) block)->Target as System.Action;
                if (existing_delegate != null)
                    return existing_delegate;
            }
            return new NIDActionArity1V0 ((BlockLiteral *) block).Invoke;
        }

        [Preserve (Conditional=true)]
        [BindingImpl (BindingImplOptions.GeneratedCode | BindingImplOptions.Optimizable)]
        unsafe void Invoke ()
        {
            invoker (blockPtr);
        }
    }
}
```

객관적인 C를 호출 하면 `[ObjCBlockTester callClassCallback]` xamarin.ios/xamarin.ios 런타임이 `[BlockProxy (typeof (Trampolines.NIDActionArity1V0))]` 매개 변수의 특성을 확인 합니다. 그런 다음 해당 `Create` 형식에서 메서드를 조회 하 고 해당 메서드를 호출 하 여 대리자를 만듭니다.

이 최적화는 `Create` 빌드 시 메서드를 찾을 수 있으며, 정적 등록자는 특성 및 리플렉션을 사용 하 여 런타임에 메타 데이터 토큰을 사용 하 여 런타임에 메서드를 조회 하는 코드를 생성 합니다 .이는 훨씬 더 빠르며 링커가 해당 런타임 코드를 제거 하 여 앱을 더 작게 만들 수도 있습니다.

Mmp/mtouch가 메서드를 찾을 수 없는 경우 `Create` MT4174/MM4174 경고가 표시 되 고 대신 조회가 런타임에 수행 됩니다.
가장 가능성이 높은 원인은 필요한 특성이 없는 바인딩 코드를 수동으로 작성 하는 것입니다 `[BlockProxy]` .

이 최적화를 위해서는 정적 등록자를 사용 하도록 설정 해야 합니다.

정적 등록자를 사용 하도록 설정한 경우 항상 기본적으로 사용 하도록 설정 됩니다.

Mtouch/mmp에 전달 하 여 기본 동작을 재정의할 수 있습니다 `--optimize=[+|-]static-delegate-to-block-lookup` .
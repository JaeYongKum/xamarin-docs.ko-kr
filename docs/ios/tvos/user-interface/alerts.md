---
title: Xamarin에서 tvOS 경고 사용
description: 이 문서에서는 Xamarin의 tvOS 경고를 사용 하는 방법을 설명 합니다. 설명 텍스트 필드 및 도우미 클래스 추가 경고를 표시 합니다.
ms.prod: xamarin
ms.assetid: F969BB28-FF2C-4A7D-88CA-F8076AD48538
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/16/2017
ms.openlocfilehash: 13c5ae3fac76ec1ec1a0ade135d5919403066226
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61409836"
---
# <a name="working-with-tvos-alerts-in-xamarin"></a>Xamarin에서 tvOS 경고 사용

_이 문서에서는 UIAlertController Xamarin.tvOS에서 사용자에 게 경고 메시지를 표시 하려면를 사용 하 여 작업을 설명 합니다._

TvOS 사용자의 관심을 가져오거나 삭제 작업 (예: 파일 삭제)를 수행할 수 있는 권한을 요청 해야 할 경우 사용 하 여 경고 메시지를 제공할 수 있습니다는 `UIAlertViewController`:

[![](alerts-images/alert01.png "UIAlertViewController 예제")](alerts-images/alert01.png#lightbox)

경우 메시지를 표시 합니다. 또한 추가할 수 단추 및 텍스트 필드 사용자 동작에 응답 하 고 피드백을 제공할 수 있도록 경고 합니다.

<a name="About-Alerts" />

## <a name="about-alerts"></a>경고에 대 한

위에서 설명한 대로 사용자의 주의 가져오고 앱 또는 요청 피드백의 상태를 알리는 경고 사용 됩니다. 경고 제목이 있어야 합니다., 메시지 및 하나 이상의 단추 또는 텍스트 필드를 가질 필요에 따라 수 있습니다.

[![](alerts-images/alert04.png "경고 예제")](alerts-images/alert04.png#lightbox)

Apple 알림 작업에 대 한 다음 제안에 있습니다.

- **경고 제한적으로 사용 하 여** -경고 사용자 환경을 중단 및 이와 같이 사용 해야 삭제 작업 오류 알림, 앱 내 구매 등 중요 한 상황에 대 한 앱을 사용 하 여 사용자의 흐름을 방해 합니다. 
- **유용한 옵션이 제공** -경고 옵션을 사용자에 게 제공 하는 경우에 각 옵션에서는 중요 한 정보를 제공 하 고 되려면 사용자에 대 한 유용한 작업을 제공 해야 합니다.

<a name="Alert-Titles-and-Messages" />

### <a name="alert-titles-and-messages"></a>경고 제목 및 메시지

Apple에는 경고의 제목 및 선택적 메시지를 제공 하기 위한 다음 제안에 있습니다.

- **Multiword 제목을 사용** -경고의 제목 지점을 명확 하 게 유지 하면서 여전히 간단한 상황에서 가져와야 합니다. 한 단어 제목을 거의 충분 한 정보를 제공합니다.
- **메시지는 필요 하지 않은 설명이 포함 된 제목을 사용** 가능할-경고의 제목 설명 된 선택적 메시지 텍스트를 충분히 필수를 만드는 것이 좋습니다. 
- **확인 메시지를 줄여서 완전 한 문장** -선택적 메시지에서 경고의 요점을 최대한 단순하게 유지 하 고 적절 한 대/소문자 및 문장 부호를 사용 하 여 완전 한 문장 있도록 데 필요한 경우.

<a name="Alert-Buttons" />

### <a name="alert-buttons"></a>경고 단추

Apple에는 경고에 단추를 추가 하기 위한 다음 제안에 있습니다.

- **두 개의 단추에 제한이** 가능할-경고를 최대 두 개의 단추를 제한 합니다. 단일 단추 경고 정보 제공 작업이 없습니다. 두 개의 단추 경고 제공 간단한 작업의 예/아니요 선택 합니다.
- **Succinct, 논리 단추 제목을 사용 하 여** -명확 하 게 단추의 동작을 설명 하는 1 ~ 2 word 단추 제목을 가장 잘 작동 하는 단순 합니다. 자세한 내용은 참조 하세요. 당사의 [단추를 사용 하 여 작업](~/ios/tvos/user-interface/buttons.md) 설명서.
- **명확 하 게 표시 파괴적 단추** -(예: 파일을 삭제 해도) 안전 하지 않은 작업을 수행 하는 단추에 사용 하 여 항목을 명확 하 게 표시 합니다 `UIAlertActionStyle.Destructive` 스타일입니다.

<a name="Displaying-an-Alert" />

## <a name="displaying-an-alert"></a>경고 표시

인스턴스를 만든 경고를 표시 하려면를 `UIAlertViewController` 및 작업 (단추)를 추가 하 고 경고의 스타일을 선택 하 여 구성 합니다. 예를 들어, 다음 코드를 확인/취소 경고를 표시 합니다.

```csharp
const string title = "A Short Title is Best";
const string message = "A message should be a short, complete sentence.";
const string acceptButtonTitle = "OK";
const string cancelButtonTitle = "Cancel";
const string deleteButtonTitle = "Delete";
...
        
var alertController = UIAlertController.Create (title, message, UIAlertControllerStyle.Alert);

// Create the action.
var acceptAction = UIAlertAction.Create (acceptButtonTitle, UIAlertActionStyle.Default, _ => 
    Console.WriteLine ("The \"OK/Cancel\" alert's other action occurred.")
);

var cancelAction = UIAlertAction.Create (cancelButtonTitle, UIAlertActionStyle.Cancel, _ => 
    Console.WriteLine ("The \"OK/Cancel\" alert's other action occurred.")
);

// Add the actions.
alertController.AddAction (acceptAction);
alertController.AddAction (cancelAction);
PresentViewController (alertController, true, null);
```

이 코드를 자세히 살펴보겠습니다. 먼저 지정 된 제목 및 메시지를 사용 하 여 새 경고를 만듭니다.

```csharp
UIAlertController.Create (title, message, UIAlertControllerStyle.Alert)
```

그런 다음 경고에 표시 하려는 각 단추에 대 한 제목 단추, 스타일 및 단추를 누를 경우 수행 하려는 작업을 정의 하는 작업을 만듭니다.

```csharp
UIAlertAction.Create ("Button Title", UIAlertActionStyle.Default, _ => 
    // Do something when the button is pressed
    ...
);
```

`UIAlertActionStyle` 열거형을 사용 하면 다음 중 하나로 단추의 스타일을 설정할 수 있도록 합니다.

- **기본** -단추가 기본 단추로 경고를 표시할 때 선택 됩니다.
- **취소** -단추를 경고에 대 한 취소 단추입니다.
- **안전 하지 않은** -파일 삭제와 같은 안전 하지 않은 작업을으로 단추를 강조 표시 합니다. 현재, tvOS 빨간색 배경의 삭제 단추를 렌더링합니다.

`AddAction` 에 지정된 된 작업을 추가 하는 메서드를 `UIAlertViewController` 마지막으로 `PresentViewController (alertController, true, null)` 메서드는 사용자에 게 지정 된 경고를 표시 합니다.

<a name="Adding-Text-Fields" />

## <a name="adding-text-fields"></a>텍스트 필드를 추가합니다.

작업 (단추)에 경고를 추가 하는 것 외에도 사용자가 사용자 Id 및 암호와 같은 정보를 입력 하도록 허용 하는 경고를 텍스트 필드를 추가할 수 있습니다.

[![](alerts-images/alert02.png "경고의 텍스트 필드")](alerts-images/alert02.png#lightbox)

사용자가 텍스트 필드를 선택 하면 필드에 대 한 값을 입력할 수 있도록 표준 tvOS 키보드 표시 됩니다.

[![](alerts-images/alert03.png "텍스트를 입력합니다.")](alerts-images/alert03.png#lightbox)

다음 코드 값을 입력 하는 것에 대 한 단일 텍스트 필드를 사용 하 여를 확인/취소 경고를 표시 합니다.

```csharp
UIAlertController alert = UIAlertController.Create(title, description, UIAlertControllerStyle.Alert);
UITextField field = null;

// Add and configure text field
alert.AddTextField ((textField) => {
    // Save the field
    field = textField;

    // Initialize field
    field.Placeholder = placeholder;
    field.Text = text;
    field.AutocorrectionType = UITextAutocorrectionType.No;
    field.KeyboardType = UIKeyboardType.Default;
    field.ReturnKeyType = UIReturnKeyType.Done;
    field.ClearButtonMode = UITextFieldViewMode.WhileEditing;

});

// Add cancel button
alert.AddAction(UIAlertAction.Create("Cancel",UIAlertActionStyle.Cancel,(actionCancel) => {
    // User canceled, do something
    ...
}));

// Add ok button
alert.AddAction(UIAlertAction.Create("OK",UIAlertActionStyle.Default,(actionOK) => {
    // User selected ok, do something
    ...
}));

// Display the alert
controller.PresentViewController(alert,true,null);
```

`AddTextField` 메서드 경고를 구성할 수 있습니다 (필드가 비어 있을 때 표시 되는 텍스트) 텍스트, 텍스트 기본값 및 키보드의 형식 자리 표시자와 같은 속성을 설정 하 여 새 텍스트 필드를 추가 합니다. 예를 들어:

```csharp
// Initialize field
field.Placeholder = placeholder;
field.Text = text;
field.AutocorrectionType = UITextAutocorrectionType.No;
field.KeyboardType = UIKeyboardType.Default;
field.ReturnKeyType = UIReturnKeyType.Done;
field.ClearButtonMode = UITextFieldViewMode.WhileEditing;
```

나중에 텍스트 필드의 값에 참조할 수 있도록 것도 저장 하는 다음 코드를 사용 하 여 복사본:

```csharp
UITextField field = null;
...

// Add and configure text field
alert.AddTextField ((textField) => {
    // Save the field
    field = textField;
    ...
});
```

사용자가 텍스트 필드에 입력 한 값을 한 후 사용할 수 있습니다는 `field` 해당 값에 액세스 하는 변수입니다.

<a name="Alert-View-Controller-Helper-Class" />

## <a name="alert-view-controller-helper-class"></a>경고 보기 컨트롤러 도우미 클래스

간단 하 고 일반적인 유형의 사용 하 여 경고를 표시 하므로 `UIAlertViewController` 많은 양의 중복 된 코드에서 발생할 수 있습니다, 도우미 클래스를 사용 하 여 반복 되는 코드의 양을 줄일 수 있습니다. 예를 들어:

```csharp
using System;
using Foundation;
using UIKit;
using System.CodeDom.Compiler;

namespace UIKit
{
    /// <summary>
    /// Alert view controller is a reusable helper class that makes working with <c>UIAlertViewController</c> alerts
    /// easier in a tvOS app.
    /// </summary>
    public class AlertViewController
    {
        #region Static Methods
        public static UIAlertController PresentOKAlert(string title, string description, UIViewController controller) {
            // No, inform the user that they must create a home first
            UIAlertController alert = UIAlertController.Create(title, description, UIAlertControllerStyle.Alert);

            // Configure the alert
            alert.AddAction(UIAlertAction.Create("OK",UIAlertActionStyle.Default,(action) => {}));

            // Display the alert
            controller.PresentViewController(alert,true,null);

            // Return created controller
            return alert;
        }

        public static UIAlertController PresentOKCancelAlert(string title, string description, UIViewController controller, AlertOKCancelDelegate action) {
            // No, inform the user that they must create a home first
            UIAlertController alert = UIAlertController.Create(title, description, UIAlertControllerStyle.Alert);

            // Add cancel button
            alert.AddAction(UIAlertAction.Create("Cancel",UIAlertActionStyle.Cancel,(actionCancel) => {
                // Any action?
                if (action!=null) {
                    action(false);
                }
            }));

            // Add ok button
            alert.AddAction(UIAlertAction.Create("OK",UIAlertActionStyle.Default,(actionOK) => {
                // Any action?
                if (action!=null) {
                    action(true);
                }
            }));

            // Display the alert
            controller.PresentViewController(alert,true,null);

            // Return created controller
            return alert;
        }

        public static UIAlertController PresentDestructiveAlert(string title, string description, string destructiveAction, UIViewController controller, AlertOKCancelDelegate action) {
            // No, inform the user that they must create a home first
            UIAlertController alert = UIAlertController.Create(title, description, UIAlertControllerStyle.Alert);

            // Add cancel button
            alert.AddAction(UIAlertAction.Create("Cancel",UIAlertActionStyle.Cancel,(actionCancel) => {
                // Any action?
                if (action!=null) {
                    action(false);
                }
            }));

            // Add ok button
            alert.AddAction(UIAlertAction.Create(destructiveAction,UIAlertActionStyle.Destructive,(actionOK) => {
                // Any action?
                if (action!=null) {
                    action(true);
                }
            }));

            // Display the alert
            controller.PresentViewController(alert,true,null);

            // Return created controller
            return alert;
        }

        public static UIAlertController PresentTextInputAlert(string title, string description, string placeholder, string text, UIViewController controller, AlertTextInputDelegate action) {
            // No, inform the user that they must create a home first
            UIAlertController alert = UIAlertController.Create(title, description, UIAlertControllerStyle.Alert);
            UITextField field = null;

            // Add and configure text field
            alert.AddTextField ((textField) => {
                // Save the field
                field = textField;

                // Initialize field
                field.Placeholder = placeholder;
                field.Text = text;
                field.AutocorrectionType = UITextAutocorrectionType.No;
                field.KeyboardType = UIKeyboardType.Default;
                field.ReturnKeyType = UIReturnKeyType.Done;
                field.ClearButtonMode = UITextFieldViewMode.WhileEditing;

            });

            // Add cancel button
            alert.AddAction(UIAlertAction.Create("Cancel",UIAlertActionStyle.Cancel,(actionCancel) => {
                // Any action?
                if (action!=null) {
                    action(false,"");
                }
            }));

            // Add ok button
            alert.AddAction(UIAlertAction.Create("OK",UIAlertActionStyle.Default,(actionOK) => {
                // Any action?
                if (action!=null && field !=null) {
                    action(true, field.Text);
                }
            }));

            // Display the alert
            controller.PresentViewController(alert,true,null);

            // Return created controller
            return alert;
        }
        #endregion

        #region Delegates
        public delegate void AlertOKCancelDelegate(bool OK);
        public delegate void AlertTextInputDelegate(bool OK, string text);
        #endregion
    }
}
```

이 클래스를 사용 하 여 표시 하 고 간단한 경고는 다음과 같이 수행할 수 있습니다.

```csharp
#region Custom Actions
partial void DisplayDestructiveAlert (Foundation.NSObject sender) {
    // User helper class to present alert
    AlertViewController.PresentDestructiveAlert("A Short Title is Best","The message should be a short, complete sentence.","Delete",this, (ok) => {
        Console.WriteLine("Destructive Alert: The user selected {0}",ok);
    });
}

partial void DisplayOkCancelAlert (Foundation.NSObject sender) {
    // User helper class to present alert
    AlertViewController.PresentOKCancelAlert("A Short Title is Best","The message should be a short, complete sentence.",this, (ok) => {
        Console.WriteLine("OK/Cancel Alert: The user selected {0}",ok);
    });
}

partial void DisplaySimpleAlert (Foundation.NSObject sender) {
    // User helper class to present alert
    AlertViewController.PresentOKAlert("A Short Title is Best","The message should be a short, complete sentence.",this);
}

partial void DisplayTextInputAlert (Foundation.NSObject sender) {
    // User helper class to present alert
    AlertViewController.PresentTextInputAlert("A Short Title is Best","The message should be a short, complete sentence.","placeholder", "", this, (ok, text) => {
        Console.WriteLine("Text Input Alert: The user selected {0} and entered `{1}`",ok,text);
    });
}
#endregion
```


<a name="Summary" />

## <a name="summary"></a>요약

이 문서에서는 작업에 설명 했습니다 `UIAlertController` Xamarin.tvOS에서 사용자에 게 경고 메시지를 표시 합니다. 먼저 간단한 경고를 표시 하 고 단추를 추가 하는 방법을 보여 주었습니다. 그런 다음 경고에 텍스트 필드를 추가 하는 방법을 보여 주었습니다. 마지막으로 경고를 표시 하는 데 필요한 반복 코드의 양을 줄이기 위해 도우미 클래스를 사용 하는 방법에 알아보았습니다.



## <a name="related-links"></a>관련 링크

- [tvOS 샘플](https://developer.xamarin.com/samples/tvos/all/)
- [tvOS](https://developer.apple.com/tvos/)
- [tvOS 휴먼 인터페이스 지침](https://developer.apple.com/tvos/human-interface-guidelines/)
- [TvOS 앱 프로그래밍 가이드](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/)

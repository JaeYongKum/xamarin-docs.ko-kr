---
title: 'Xamarin.Essentials: 앱 작업'
description: Xamarin.Essentials의 가속도계 클래스를 사용하면 앱 아이콘에서 앱 바로 가기를 만들고 응답할 수 있습니다.
ms.assetid: 5edf9bc5-b721-448c-a8a2-0a9d4d0c792c
author: jamesmontemagno
ms.author: jamont
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: add9143ff1a9546d3d2c8cfb851f621083bf356d
ms.sourcegitcommit: 744f977b0595f489c592e29c8a3ba548fde02b6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414687"
---
# <a name="no-locxamarinessentials-app-actions"></a>Xamarin.Essentials: 앱 작업

**AppActions** 클래스를 사용하면 앱 아이콘에서 앱 바로 가기를 만들고 응답할 수 있습니다.

![시험판 API](~/media/shared/preview.png)

## <a name="get-started"></a>시작하기

[!include[](~/essentials/includes/get-started.md)]

**AppActions** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

`MainActivity`에서 동작 처리를 위해 다음 논리를 추가합니다.

```csharp
protected override void OnResume()
{
    base.OnResume();

    Xamarin.Essentials.Platform.OnResume(this);
}

protected override void OnNewIntent(Intent intent)
{
    base.OnNewIntent(intent);

    Xamarin.Essentials.Platform.OnNewIntent(intent);
}
```

# <a name="ios"></a>[iOS](#tab/ios)

`AppDelegate.cs`에서 동작 처리를 위해 다음 논리를 추가합니다.

```csharp
public override void PerformActionForShortcutItem(UIApplication application, UIApplicationShortcutItem shortcutItem, UIOperationHandler completionHandler)
    => Xamarin.Essentials.Platform.PerformActionForShortcutItem(application, shortcutItem, completionHandler);
```

# <a name="uwp"></a>[UWP](#tab/uwp)

`OnLaunched` 메서드의 `App.xaml.cs` 파일에서 메서드의 맨 아래에 다음 논리를 추가합니다.

```csharp
Xamarin.Essentials.Platform.OnLaunched(e);
```

-----

## <a name="create-actions"></a>작업 만들기

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```
앱 작업은 언제든 만들 수 있지만 애플리케이션이 시작할 때 생성되는 경우가 많습니다. `SetAsync` 메서드를 호출하여 앱에 대한 작업 목록을 만듭니다.


```csharp
try
{
    await AppActions.SetAsync(
        new AppAction("app_info", "App Info", icon: "app_info_action_icon"),
        new AppAction("battery_info", "Battery Info"));
}
catch (FeatureNotSupportedException ex)
{
    Debug.WriteLine("App Actions not supported");
}
```

특정 운영 체제 버전에서 앱 작업이 지원되지 않는 경우 `FeatureNotSupportedException`이 throw됩니다. 

`AppAction`에서 다음 속성을 지정할 수 있습니다.

* Id: 작업 탭에 응답하는 데 사용되는 고유 식별자입니다.
* 제목: 표시되어 보이는 제목입니다.
* 부제목: 지원되는 경우 제목 아래에 부제목이 표시됩니다.
* 아이콘: 각 플랫폼의 해당 리소스 디렉터리에 있는 아이콘과 일치해야 합니다.

![홈 화면의 앱 작업](images/appactions.png)

## <a name="responding-to-actions"></a>작업에 응답

애플리케이션이 `OnAppAction` 이벤트에 대한 등록을 시작할 때 앱 작업을 선택한 경우 선택한 작업에 따라 정보와 함께 이벤트를 보냅니다.

```csharp
public App()
{
    //...
    AppActions.OnAppAction += AppActions_OnAppAction;
}

void AppActions_OnAppAction(object sender, AppActionEventArgs e)
{
    // Don't handle events fired for old application instances
    // and cleanup the old instance's event handler
    if (Application.Current != this && Application.Current is App app)
    {
        AppActions.OnAppAction -= app.AppActions_OnAppAction;
        return;
    }
    Device.BeginInvokeOnMainThread(async () =>
    {
        var page = e.AppAction.Id switch
        {
            "battery_info" => new BatteryPage(),
            "app_info" => new AppInfoPage(),
            _ => default(Page)
        };
        if (page != null)
        {
            await Application.Current.MainPage.Navigation.PopToRootAsync();
            await Application.Current.MainPage.Navigation.PushAsync(page);
        }
    });
}
```

## <a name="getactions"></a>GetActions
`AppActions.GetAsync()`를 호출하여 현재 앱 작업 목록을 가져올 수 있습니다.

## <a name="api"></a>API

- [AppActions 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/AppActions)
- [AppActions API 설명서](xref:Xamarin.Essentials.AppActions)

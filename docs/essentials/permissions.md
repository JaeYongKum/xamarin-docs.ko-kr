---
title: 'Xamarin.Essentials: 사용 권한'
description: 이 문서에서는 런타임 권한을 확인하고 요청하는 기능을 제공하는 Xamarin.Essentials의 Permissions 클래스에 대해 설명합니다.
ms.assetid: 34062D84-3E55-4AF7-A688-8551068B1E57
author: jamesmontemagno
ms.author: jamont
ms.custom: video
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 01902942c750a3cd278d648fa82499af4c5d3ab6
ms.sourcegitcommit: dac04cec56290fb19034f3e135708f6966a8f035
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92169971"
---
# <a name="no-locxamarinessentials-permissions"></a>Xamarin.Essentials: 사용 권한

**Permissions** 클래스는 런타임 권한을 확인하고 요청하는 기능을 제공합니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

[!include[](~/essentials/includes/android-permissions.md)]

## <a name="using-permissions"></a>권한 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

## <a name="checking-permissions"></a>권한 확인

권한의 현재 상태를 확인하려면 상태를 가져올 특정 권한과 함께 `CheckStatusAsync` 메서드를 사용합니다.

```csharp
var status = await Permissions.CheckStatusAsync<Permissions.LocationWhenInUse>();
```

필요한 권한이 선언되지 않은 경우에는 `PermissionException`이 throw됩니다.

권한을 요청하기 전에 권한 상태를 확인하는 것이 좋습니다. 사용자에게 메시지가 표시되지 않는 경우 각 운영 체제는 다른 기본 상태를 반환합니다. iOS는 `Unknown`을 반환하고, 다른 운영 체제는 `Denied`를 반환합니다. 상태가 `Granted`인 경우 다른 호출을 하지 않아도 됩니다. iOS에서 상태가 `Denied`인 경우 사용자에게 설정에서 권한을 변경하라는 메시지를 표시해야 하며, Android에서는 `ShouldShowRationale`을 호출하여 과거에 사용자가 권한 요청을 거부한 적이 있는지 감지할 수 있습니다.

## <a name="requesting-permissions"></a>권한 요청

사용자에게 권한을 요청하려면 요청할 특정 권한과 함께 `RequestAsync` 메서드를 사용합니다. 사용자가 이전에 권한을 부여하고 취소하지 않은 경우 이 메서드는 즉시 `Granted`를 반환하고 대화 상자를 표시하지 않습니다.

```csharp
var status = await Permissions.RequestAsync<Permissions.LocationWhenInUse>();
```

필요한 권한이 선언되지 않은 경우에는 `PermissionException`이 throw됩니다.

일부 플랫폼에서 권한 요청은 한 번만 활성화될 수 있습니다. 권한이 `Denied` 상태인지 확인하고 사용자에게 수동으로 설정하도록 요청하려면 개발자가 추가 프롬프트를 처리해야 합니다. 

## <a name="permission-status"></a>권한 상태

`CheckStatusAsync` 또는 `RequestAsync`를 사용하는 경우 다음 단계를 결정하는 데 사용할 수 있는 `PermissionStatus`가 반환됩니다.

* 알 수 없음 - 권한이 알 수 없는 상태입니다.
* 거부됨 - 사용자가 권한 요청을 거부했습니다.
* 사용 안 함 - 디바이스에서 이 기능을 사용할 수 없습니다.
* 부여됨 - 사용자가 권한을 부여했거나 권한이 자동으로 부여됩니다.
* 제한됨 - 제한된 상태입니다.


## <a name="explain-why-permission-is-needed"></a>권한이 필요한 이유 설명

![시험판 API](~/media/shared/preview.png)

애플리케이션에 특정 권한이 필요한 이유를 설명하는 것이 모범 사례입니다. iOS에서는 사용자에게 표시하는 문자열을 지정해야 합니다. Android에는 이 기능이 없으며 기본 권한 상태도 사용 안 함으로 설정되어 있습니다. 이 때문에 사용자가 권한을 거부했는지 또는 사용자에게 메시지를 처음으로 표시하는지 여부를 파악하지 못합니다. `ShouldShowRationale` 메서드를 사용하여 교육용 UI를 표시할지 여부를 결정할 수 있습니다. 메서드가 `true`를 반환한다면 사용자가 이전에 권한을 거부하거나 사용하지 않도록 설정한 것입니다. 다른 플랫폼은 이 메서드를 호출할 때 항상 `false`를 반환합니다.

## <a name="available-permissions"></a>사용 가능한 권한

Xamarin.Essentials는 최대한 많은 권한을 추상화하려고 시도합니다. 그러나 각 운영 체제에는 서로 다른 런타임 권한 집합이 있습니다. 또한 일부 권한에 대해 단일 API를 제공한다는 차이점이 있습니다. 다음은 현재 사용할 수 있는 권한에 대한 가이드입니다.

아이콘 지침:

* ![전체 지원](~/media/shared/yes.png "전체 지원") - 지원됨
* ![지원 안 함](~/media/shared/no.png "지원되지 않음 또는 필요 없음") - 지원되지 않음/필요하지 않음

| 사용 권한 | Android | iOS | UWP | watchOS | tvOS | Tizen |
| --- | :---: | :---: | :---: | :---: | :---: | :---: | :---:
| CalendarRead   | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원](~/media/shared/yes.png "watchOS 지원") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| CalendarWrite | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원](~/media/shared/yes.png "watchOS 지원") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| 카메라 | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원](~/media/shared/yes.png "Tizen 지원") |
| ContactsRead | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원](~/media/shared/yes.png "UWP 지원") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| ContactsWrite | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원](~/media/shared/yes.png "UWP 지원") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| 손전등 | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원 안 함](~/media/shared/no.png "iOS 지원 안 함") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원](~/media/shared/yes.png "Tizen 지원") |
| LocationWhenInUse | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원](~/media/shared/yes.png "UWP 지원") | ![watchOS 지원](~/media/shared/yes.png "watchOS 지원") | ![tvOS 지원](~/media/shared/yes.png "tvOS 지원")  | ![Tizen 지원](~/media/shared/yes.png "Tizen 지원") |
| LocationAlways | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원](~/media/shared/yes.png "UWP 지원") | ![watchOS 지원](~/media/shared/yes.png "watchOS 지원") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원](~/media/shared/yes.png "Tizen 지원") |
| 미디어 | ![Android 지원 안 함](~/media/shared/no.png "Android 지원 안 함") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| 마이크 | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원](~/media/shared/yes.png "UWP 지원") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원](~/media/shared/yes.png "Tizen 지원") |
| 전화 | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| 사진 | ![Android 지원 안 함](~/media/shared/no.png "Android 지원 안 함") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원](~/media/shared/yes.png "tvOS 지원") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| 미리 알림 | ![Android 지원 안 함](~/media/shared/no.png "Android 지원 안 함") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원](~/media/shared/yes.png "watchOS 지원") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| 센서 | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원](~/media/shared/yes.png "UWP 지원") | ![watchOS 지원](~/media/shared/yes.png "watchOS 지원") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| Sms | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| Speech | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원](~/media/shared/yes.png "iOS 지원") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| StorageRead | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원 안 함](~/media/shared/no.png "iOS 지원 안 함") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |
| StorageWrite | ![Android 지원](~/media/shared/yes.png "Android 지원") | ![iOS 지원 안 함](~/media/shared/no.png "iOS 지원 안 함") | ![UWP 지원 안 함](~/media/shared/no.png "UWP 지원 안 함") | ![watchOS 지원 안 함](~/media/shared/no.png "watchOS 지원 안 함") | ![tvOS 지원 안 함](~/media/shared/no.png "tvOS 지원 안 함") | ![Tizen 지원 안 함](~/media/shared/no.png "Tizen 지원 안 함") |

권한이 ![지원되지 않음](~/media/shared/no.png "지원되지 않음")으로 표시되는 경우 확인 또는 요청 시 항상 `Granted`를 반환합니다.

## <a name="general-usage"></a>일반적인 사용법
권한을 처리하기 위한 일반적인 사용 패턴은 다음과 같습니다.

```csharp
public async Task<PermissionStatus> CheckAndRequestLocationPermission()
{
    var status = await Permissions.CheckStatusAsync<Permissions.LocationWhenInUse>();
    
    if (status == PermissionStatus.Granted)
        return status;
        
    
    if (status == PermissionStatus.Denied && DeviceInfo.Platform == DevicePlatform.iOS)
    {
        // Prompt the user to turn on in settings
        // On iOS once a permission has been denied it may not be requested again from the application
        return status;
    }
    
    if (Permissions.ShouldShowRationale<Permissions.LocationWhenInUse>())
    {
        // Prompt the user with additional information as to why the permission is needed
    }   

    status = await Permissions.RequestAsync<Permissions.LocationWhenInUse>();

    return status;
}
```

각 권한 형식에는 메서드를 직접 호출할 수 있도록 생성된 인스턴스가 있을 수 있습니다.

```csharp
public async Task GetLocationAsync()
{
    var status = await CheckAndRequestPermissionAsync(new Permissions.LocationWhenInUse());
    if (status != PermissionStatus.Granted)
    {
        // Notify user permission was denied
        return;
    }

    var location = await Geolocation.GetLocationAsync();
}

public async Task<PermissionStatus> CheckAndRequestPermissionAsync<T>(T permission)
            where T : BasePermission
{
    var status = await permission.CheckStatusAsync();
    if (status != PermissionStatus.Granted)
    {
        status = await permission.RequestAsync();
    }

    return status;
}
```

## <a name="extending-permissions"></a>권한 확장

권한 API는 Xamarin.Essentials에 포함되지 않은 추가 유효성 검사 또는 권한이 필요한 애플리케이션을 위해 유연하고 확장 가능하도록 만들어졌습니다. `BasePermission`에서 상속되는 새 클래스를 만들고 필요한 추상 메서드를 구현합니다.

```csharp
public class MyPermission : BasePermission
{
    // This method checks if current status of the permission
    public override Task<PermissionStatus> CheckStatusAsync()
    {
        throw new System.NotImplementedException();
    }

    // This method is optional and a PermissionException is often thrown if a permission is not declared
    public override void EnsureDeclared()
    {
        throw new System.NotImplementedException();
    }

    // Requests the user to accept or deny a permission
    public override Task<PermissionStatus> RequestAsync()
    {
        throw new System.NotImplementedException();
    }
}
```

특정 플랫폼에서 권한을 구현하는 경우 `BasePlatformPermission` 클래스를 상속할 수 있습니다. 그러면 자동으로 선언을 확인하는 추가 플랫폼 도우미 메서드가 제공됩니다. 이는 그룹화를 수행하는 사용자 지정 권한을 만들 때 유용할 수 있습니다. 예를 들어 다음 사용자 지정 권한을 사용하여 Android에서 스토리지에 대한 읽기 및 쓰기 권한을 요청할 수 있습니다.

```csharp
public class ReadWriteStoragePermission : Xamarin.Essentials.Permissions.BasePlatformPermission
{
    public override (string androidPermission, bool isRuntime)[] RequiredPermissions => new List<(string androidPermission, bool isRuntime)>
    {
        (Android.Manifest.Permission.ReadExternalStorage, true),
        (Android.Manifest.Permission.WriteExternalStorage, true)
    }.ToArray();
}
```

그런 다음 Android 프로젝트에서 새 권한을 호출할 수 있습니다.

```csharp
await Permissions.RequestAsync<ReadWriteStoragePermission>();
```

공유 코드에서 이 API를 호출하려는 경우 인터페이스를 만들고 [종속성 서비스](../xamarin-forms/app-fundamentals/dependency-service/index.md)를 사용하여 구현을 등록하고 가져올 수 있습니다.

```csharp
public interface IReadWritePermission
{        
    Task<PermissionStatus> CheckStatusAsync();
    Task<PermissionStatus> RequestAsync();
}
```

그런 다음 플랫폼 프로젝트에 인터페이스를 구현합니다.

```csharp
public class ReadWriteStoragePermission : Xamarin.Essentials.Permissions.BasePlatformPermission, IReadWritePermission
{
    public override (string androidPermission, bool isRuntime)[] RequiredPermissions => new List<(string androidPermission, bool isRuntime)>
    {
        (Android.Manifest.Permission.ReadExternalStorage, true),
        (Android.Manifest.Permission.WriteExternalStorage, true)
    }.ToArray();
}
```

그런 다음 특정 구현을 등록할 수 있습니다.

```csharp
DependencyService.Register<IReadWritePermission, ReadWriteStoragePermission>();
```
그리고 공유 프로젝트에서 구현을 해결하고 사용할 수 있습니다.

```csharp
var readWritePermission = DependencyService.Get<IReadWritePermission>();
var status = await readWritePermission.CheckStatusAsync();
if (status != PermissionStatus.Granted)
{
    status = await readWritePermission.RequestAsync();
}
```

## <a name="platform-implementation-specifics"></a>플랫폼 구현 관련 정보

# <a name="android"></a>[Android](#tab/android)

권한은 Android 매니페스트 파일에 일치하는 특성이 설정되어 있어야 합니다. 권한 상태의 기본값이 거부됨입니다.

자세한 내용은 [Xamarin Android 권한](../android/app-fundamentals/permissions.md) 설명서를 참조하세요.

# <a name="ios"></a>[iOS](#tab/ios)

권한은 `Info.plist` 파일에 일치하는 문자열이 있어야 합니다. 권한 요청 후 요청이 거부되면 해당 권한을 두 번째 요청해도 팝업이 더 이상 표시되지 않습니다. iOS의 애플리케이션 설정 화면에서 수동으로 설정을 조정하도록 사용자에게 메시지를 표시해야 합니다. 권한 상태의 기본값이 알 수 없음입니다.

[iOS 보안 및 개인 정보 보호 기능](../ios/app-fundamentals/security-privacy.md) 설명서를 참조하세요.

# <a name="uwp"></a>[UWP](#tab/uwp)

권한은 패키지 매니페스트에 일치하는 기능이 선언되어 있어야 합니다. 대부분의 경우 권한 상태의 기본값은 알 수 없음입니다.

자세한 내용은 [앱 기능 선언](/windows/uwp/packaging/app-capability-declarations) 설명서를 참조하세요.

--------------

## <a name="api"></a>API

- [권한 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Permissions)
- [권한 API 설명서](xref:Xamarin.Essentials.Permissions)


## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Permissions-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

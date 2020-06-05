---
title: “Xamarin.Essentials: 지리적 위치” description: “이 문서에서는 디바이스의 현재 지리적 위치 좌표를 검색하기 위한 API를 제공하는 Xamarin.Essentials의 Geolocation 클래스를 설명합니다.”
ms.assetid: 8F66092C-13F0-4FEE-8AA5-901D5F79B357 author: jamesmontemagno ms.custom: video ms.author: jamont ms.date: 03/13/2019 no-loc: [Xamarin.Forms, Xamarin.Essentials]
---

# <a name="xamarinessentials-geolocation"></a>Xamarin.Essentials: 지리적 위치

**Geolocation** 클래스는 디바이스의 현재 지리적 위치 좌표를 검색하기 위한 API를 제공합니다.

## <a name="get-started"></a>시작

[!include[](~/essentials/includes/get-started.md)]

**지리적 위치** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

Coarse 및 Fine Location 권한이 필요하며 Android 프로젝트에서 구성해야 합니다. 또한 앱이 Android 5.0(API 레벨 21) 이상을 대상으로 하는 경우 해당 앱에서 매니페스트 파일의 하드웨어 기능을 사용하도록 선언해야 합니다. 이 권한은 다음과 같은 방법으로 추가할 수 있습니다.

**속성** 폴더 아래의 **AssemblyInfo.cs** 파일을 열고 다음을 추가합니다.

```csharp
[assembly: UsesPermission(Android.Manifest.Permission.AccessCoarseLocation)]
[assembly: UsesPermission(Android.Manifest.Permission.AccessFineLocation)]
[assembly: UsesFeature("android.hardware.location", Required = false)]
[assembly: UsesFeature("android.hardware.location.gps", Required = false)]
[assembly: UsesFeature("android.hardware.location.network", Required = false)]
```

또는 Android 매니페스트를 업데이트합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-feature android:name="android.hardware.location" android:required="false" />
<uses-feature android:name="android.hardware.location.gps" android:required="false" />
<uses-feature android:name="android.hardware.location.network" android:required="false" />
```

또는 Android 프로젝트를 마우스 오른쪽 단추로 클릭하고 프로젝트의 속성을 엽니다. **Android 매니페스트** 아래에서 **필요한 권한:** 영역을 찾아서 **ACCESS_COARSE_LOCATION** 및 **ACCESS_FINE_LOCATION** 권한을 확인합니다. 그러면 **AndroidManifest.xml** 파일이 자동으로 업데이트됩니다.

[!include[](~/essentials/includes/android-permissions.md)]

# <a name="ios"></a>[iOS](#tab/ios)

디바이스 위치에 액세스하려면 앱의 **Info.plist**에 `NSLocationWhenInUseUsageDescription` 키가 포함되어야 합니다.

plist 편집기를 연 다음, **개인 정보 - 위치 사용 시 사용 설명** 속성을 추가하고 사용자에게 표시할 값을 입력합니다.

또는 수동으로 파일을 편집하여 다음을 추가하고 이유를 업데이트합니다.

```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>Fill in a reason why your app needs access to location.</string>
```

# <a name="uwp"></a>[UWP](#tab/uwp)

애플리케이션에 대한 `Location` 권한을 설정해야 합니다. 이 작업을 수행하려면 **Package.appxmanifest**를 열고, **기능** 탭을 선택하고, **Location**을 선택합니다.

-----

## <a name="using-geolocation"></a>지리적 위치 사용

클래스에서 Xamarin.Essentials에 대한 참조를 추가합니다.

```csharp
using Xamarin.Essentials;
```

또한 지리적 위치 API는 필요한 경우 권한을 요청하는 메시지를 사용자에게 표시합니다.

`GetLastKnownLocationAsync` 메서드를 호출하여 디바이스의 마지막으로 알려진 [위치](xref:Xamarin.Essentials.Location)를 가져올 수 있습니다. 이는 일반적으로 전체 쿼리를 수행하는 것보다 더 빠르지만 캐시된 위치가 없는 경우 `null`을 반환할 수 있습니다.

```csharp
try
{
    var location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Console.WriteLine($"Latitude: {location.Latitude}, Longitude: {location.Longitude}, Altitude: {location.Altitude}");
    }
}
catch (FeatureNotSupportedException fnsEx)
{
    // Handle not supported on device exception
}
catch (FeatureNotEnabledException fneEx)
{
    // Handle not enabled on device exception
}
catch (PermissionException pEx)
{
    // Handle permission exception
}
catch (Exception ex)
{
    // Unable to get location
}
```

고도를 항상 사용할 수는 없습니다. 사용할 수 없는 경우 `Altitude` 속성은 `null`이거나 값이 0일 수 있습니다. 고도를 사용할 수 있는 경우 값은 해발 미터 단위입니다.

현재 디바이스의 [위치](xref:Xamarin.Essentials.Location) 좌표를 쿼리하는 데는 `GetLocationAsync`를 사용할 수 있습니다. 디바이스 위치를 가져오는 데 약간 시간이 걸릴 수 있으므로 전체 `GeolocationRequest` 및 `CancellationToken`으로 전달하는 것이 가장 좋습니다.

```csharp
try
{
    var request = new GeolocationRequest(GeolocationAccuracy.Medium);
    var location = await Geolocation.GetLocationAsync(request);

    if (location != null)
    {
        Console.WriteLine($"Latitude: {location.Latitude}, Longitude: {location.Longitude}, Altitude: {location.Altitude}");
    }
}
catch (FeatureNotSupportedException fnsEx)
{
    // Handle not supported on device exception
}
catch (FeatureNotEnabledException fneEx)
{
    // Handle not enabled on device exception
}
catch (PermissionException pEx)
{
    // Handle permission exception
}
catch (Exception ex)
{
    // Unable to get location
}
```

## <a name="geolocation-accuracy"></a>지리적 위치 정확도

다음 표에서는 플랫폼별 정확도를 개략적으로 설명합니다.

### <a name="lowest"></a>가장 낮음

| 플랫폼 | 거리(미터) |
| --- | --- |
| Android | 500 |
| iOS | 3000 |
| UWP | 1000 - 5000 |

### <a name="low"></a>낮음

| 플랫폼 | 거리(미터) |
| --- | --- |
| Android | 500 |
| iOS | 1000 |
| UWP | 300 - 3000 |

### <a name="medium-default"></a>중간(기본값)

| 플랫폼 | 거리(미터) |
| --- | --- |
| Android | 100 - 500 |
| iOS | 100 |
| UWP | 30-500 |

### <a name="high"></a>높음

| 플랫폼 | 거리(미터) |
| --- | --- |
| Android | 0 - 100 |
| iOS | 10 |
| UWP | <= 10 |

### <a name="best"></a>가장 좋음

| 플랫폼 | 거리(미터) |
| --- | --- |
| Android | 0 - 100 |
| iOS | ~0 |
| UWP | <= 10 |

<a name="calculate-distance" />

## <a name="detecting-mock-locations"></a>Mock 위치 검색
일부 디바이스는 공급자에서 또는 모의 위치를 제공하는 애플리케이션에 의해 모의 위치를 반환할 수 있습니다. [`Location`](xref:Xamarin.Essentials.Location)에서 `IsFromMockProvider`를 사용하여 이를 탐지할 수 있습니다.

```csharp
var request = new GeolocationRequest(GeolocationAccuracy.Medium);
var location = await Geolocation.GetLocationAsync(request);

if (location != null)
{
    if(location.IsFromMockProvider)
    {
        // location is from a mock provider
    }
}
```

## <a name="distance-between-two-locations"></a>두 위치 간 거리

[`Location`](xref:Xamarin.Essentials.Location) 및 [`LocationExtensions`](xref:Xamarin.Essentials.LocationExtensions) 클래스는 두 지리적 위치 간 거리를 계산할 수 있는 `CalculateDistance` 메서드를 정의합니다. 이 계산된 거리는 도로 또는 다른 경로를 고려하지 않으며, ‘대권 거리(great-circle distance)’라고도 하는 지표면에 따라 두 지점 간의 가장 짧은 거리 또는 구어로 “일직선” 거리일 뿐입니다.

예를 들면 다음과 같습니다.

```csharp
Location boston = new Location(42.358056, -71.063611);
Location sanFrancisco = new Location(37.783333, -122.416667);
double miles = Location.CalculateDistance(boston, sanFrancisco, DistanceUnits.Miles);
```

`Location` 생성자에는 해당 순서로 위도 및 경도 인수가 포함됩니다. 양수 위도 값은 적도의 북쪽이고 양수 경도 값은 본초 자오선의 동쪽입니다. `CalculateDistance`에 대한 마지막 인수를 사용하여 마일 또는 킬로미터를 지정합니다. 또한 `UnitConverters` 클래스는 두 단위 간에 변환하기 위한 `KilometersToMiles` 및 `MilesToKilometers` 메서드를 정의합니다.

## <a name="platform-differences"></a>플랫폼의 차이점

고도는 플랫폼마다 다르게 계산됩니다.

# <a name="android"></a>[Android](#tab/android)

Android에서 사용 가능한 경우 [고도](https://developer.android.com/reference/android/location/Location#getAltitude())는 WGS 84 참조 타원면 위에 미터 단위로 반환됩니다. 이 위치에 고도가 없는 경우에는 0.0이 반환됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

iOS에서 [고도](https://developer.apple.com/documentation/corelocation/cllocation/1423820-altitude)는 미터 단위로 측정됩니다. 양수 값은 해발 고도를 나타내고, 음수 값은 해수면 아래를 나타냅니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

UWP에서 고도는 미터 단위로 반환됩니다. 자세한 내용은 [AltitudeReferenceSystem](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geopoint.altitudereferencesystem#Windows_Devices_Geolocation_Geopoint_AltitudeReferenceSystem) 문서를 참조하세요.

-----

## <a name="api"></a>API

- [지리적 위치 소스 코드](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Geolocation)
- [지리적 위치 API 문서](xref:Xamarin.Essentials.Geolocation)

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Shows/XamarinShow/Geolocation-XamarinEssentials-API-of-the-Week/player]

[!include[](~/essentials/includes/xamarin-show-essentials.md)]

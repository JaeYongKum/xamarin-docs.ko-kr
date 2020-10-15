---
title: 'Xamarin.Essentials: 미디어 선택기'
description: Xamarin.Essentials의 MediaPicker 클래스를 통해 사용자는 디바이스에서 사진 또는 비디오를 선택하거나 촬영할 수 있습니다.
ms.assetid: 23460875-6cf9-4440-a97b-46c55b0bca69
author: jamesmontemagno
ms.author: jamont
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 7c4299abf9c461a16f67ccf3d8caf03d5e568f13
ms.sourcegitcommit: 827daa78c090bf79a1b55da45bb8012a1723b720
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91997504"
---
# <a name="no-locxamarinessentials-media-picker"></a>Xamarin.Essentials: 미디어 선택기

**MediaPicker** 클래스를 통해 사용자는 디바이스에서 사진 또는 비디오를 선택하거나 촬영할 수 있습니다.

![시험판 API](~/media/shared/preview.png)

## <a name="get-started"></a>시작하기

[!include[](~/essentials/includes/get-started.md)]

**MediaPicker** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

다음 권한이 필요하며 Android 프로젝트에서 구성해야 합니다. 이 권한은 다음과 같은 방법으로 추가할 수 있습니다.

**속성** 폴더 아래의 **AssemblyInfo.cs** 파일을 열고 다음을 추가합니다.

```csharp
// Needed for Picking photo/video
[assembly: UsesPermission(Android.Manifest.Permission.ReadExternalStorage)]

// Needed for Taking photo/video
[assembly: UsesPermission(Android.Manifest.Permission.WriteExternalStorage)]
[assembly: UsesPermission(Android.Manifest.Permission.Camera)]

// Add these properties if you would like to filter out cameras that do not have cameras or set to false to make them optional
[assembly: UsesFeature("android.hardware.camera", Required = true)]
[assembly: UsesFeature("android.hardware.camera.autofocus", Required = true)]
```

또는 Android 매니페스트를 업데이트합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.CAMERA" />
```

또는 Android 프로젝트를 마우스 오른쪽 단추로 클릭하고 프로젝트의 속성을 엽니다. **Android 매니페스트** 아래에서 **필요한 권한:** 영역을 찾아 다음 권한을 선택합니다. 그러면 **AndroidManifest.xml** 파일이 자동으로 업데이트됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

`Info.plist`에 다음 키를 추가합니다.

```xml
<key>NSCameraUsageDescription</key>
<string>This app needs access to the camera to take photos.</string>
<key>NSMicrophoneUsageDescription</key>
<string>This app needs access to microphone for taking videos.</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>This app needs access to the photo gallery for picking photos and videos.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>This app needs access to photos gallery for picking photos and videos.</string>
```

사용자에게 표시되는 앱에 특정한 설명으로 각각의 `<string>`을 업데이트해야 합니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

`Package.appxmanifest`의 **기능**에서 `Microphone` 및 `Webcam` 기능을 선택합니다.

-----

## <a name="using-media-picker"></a>미디어 선택기 사용

`MediaPicker` 클래스에는 파일 위치를 가져오거나 `Stream`으로 읽는 데 사용할 수 있는 `FileResult`를 모두 반환하는 다음과 같은 메서드가 있습니다.

* `PickPhotoAsync`: 미디어 브라우저를 열어 사진을 선택합니다.
* `CapturePhotoAsync`: 카메라를 열어 사진을 촬영합니다.
* `PickVideoAsync`: 미디어 브라우저를 열어 비디오를 선택합니다.
* `CaptureVideoAsync`: 카메라를 열어 비디오를 촬영합니다.

각 메서드는 사용자에게 표시되는 일부 운영 체제에서 `Title`이 설정될 수 있게 하는 `MediaPickerOptions` 매개 변수를 선택적으로 사용합니다.

## <a name="general-usage"></a>일반적인 사용법

```csharp
async Task TakePhotoAsync()
{
    try
    {
        var photo = await MediaPicker.CapturePhotoAsync();
        await LoadPhotoAsync(photo);
        Console.WriteLine($"CapturePhotoAsync COMPLETED: {PhotoPath}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"CapturePhotoAsync THREW: {ex.Message}");
    }
}

async Task LoadPhotoAsync(FileResult photo)
{
    // canceled
    if (photo == null)
    {
        PhotoPath = null;
        return;
    }
    // save the file into local storage
    var newFile = Path.Combine(FileSystem.CacheDirectory, photo.FileName);
    using (var stream = await photo.OpenReadAsync())
    using (var newStream = File.OpenWrite(newFile))
        await stream.CopyToAsync(newStream);

    PhotoPath = newFile;
}
```


## <a name="api"></a>API

- [MediaPicker 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/MediaPicker)
- [MediaPicker API 설명서](xref:Xamarin.Essentials.MediaPicker)

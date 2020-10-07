---
title: 'Xamarin.Essentials: 파일 선택기'
description: Xamarin.Essentials의 FilePicker 클래스를 사용하면 사용자가 디바이스에서 단일 또는 여러 파일을 선택할 수 있습니다.
ms.assetid: 00bdbd57-56b1-47ca-8abe-cebe1b01f61a
author: jamesmontemagno
ms.author: jamont
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: b3ee20de5534329f9e4686c908fe923ba94f3fff
ms.sourcegitcommit: 744f977b0595f489c592e29c8a3ba548fde02b6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414691"
---
# <a name="no-locxamarinessentials-file-picker"></a>Xamarin.Essentials: 파일 선택기

**FilePicker** 클래스를 사용하면 사용자가 디바이스에서 단일 또는 여러 파일을 선택할 수 있습니다.

![시험판 API](~/media/shared/preview.png)

## <a name="get-started"></a>시작하기

[!include[](~/essentials/includes/get-started.md)]

**FilePicker** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

`ReadExternalStorage` 권한이 필요하며 Android 프로젝트에서 구성해야 합니다. 이 권한은 다음과 같은 방법으로 추가할 수 있습니다.

**속성** 폴더 아래의 **AssemblyInfo.cs** 파일을 열고 다음을 추가합니다.

```csharp
[assembly: UsesPermission(Android.Manifest.Permission.ReadExternalStorage)]
```

또는 Android 매니페스트를 업데이트합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

또는 Android 프로젝트를 마우스 오른쪽 단추로 클릭하고 프로젝트의 속성을 엽니다. **Android 매니페스트** 아래에서 **필요한 권한:** 영역을 찾아 이 권한을 선택합니다. 그러면 **AndroidManifest.xml** 파일이 자동으로 업데이트됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

추가 설정이 필요하지 않습니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

추가 설정이 필요하지 않습니다.

-----

## <a name="pick-file"></a>파일 선택

`FilePicker.PickAsync()` 메서드를 사용하면 사용자가 디바이스에서 파일을 선택할 수 있습니다. 표시할 제목과, 사용자가 선택할 수 있는 파일 형식을 지정할 수 있는 메서드를 호출할 때 다른 `PickOptions`를 특정할 수 있습니다. 기본적으로 

```csharp
async Task<FileResult> PickAndShow(PickOptions options)
{
    try
    {
        var result = await FilePicker.PickAsync();
        if (result != null)
        {
            Text = $"File Name: {result.FileName}";
            if (result.FileName.EndsWith("jpg", StringComparison.OrdinalIgnoreCase) ||
                result.FileName.EndsWith("png", StringComparison.OrdinalIgnoreCase))
            {
                var stream = await result.OpenReadAsync();
                Image = ImageSource.FromStream(() => stream);
            }
        }
    }
    catch (Exception ex)
    {
        // The user canceled or something went wrong
    }
}
```

기본 파일 형식은 `FilePickerFileType.Images`, `FilePickerFileType.Png` 및 `FilePickerFilerType.Videos`로 제공됩니다. `PickOptions`를 만들 때 사용자 지정 파일 형식을 지정하고 플랫폼에 따라 사용자 지정할 수 있습니다. 예를 들어 특정 만화 파일 형식을 지정하는 방법은 다음과 같습니다.

```csharp
var customFileType =
    new FilePickerFileType(new Dictionary<DevicePlatform, IEnumerable<string>>
    {
        { DevicePlatform.iOS, new[] { "public.my.comic.extension" } }, // or general UTType values
        { DevicePlatform.Android, new[] { "application/comics" } },
        { DevicePlatform.UWP, new[] { ".cbr", ".cbz" } },
        { DevicePlatform.Tizen, new[] { "*/*" } },
        { DevicePlatform.macOS, new[] { "cbr", "cbz" } }, // or general UTType values
    });
var options = new PickOptions
{
    PickerTitle = "Please select a comic file",
    FileTypes = customFileType,
};
```

## <a name="pick-multiple-files"></a>여러 파일 선택

사용자가 여러 파일을 선택하게 하려면 `FilePicker.PickMultipleAsync()` 메서드를 호출할 수 있습니다. 또한 추가 정보를 지정하는 매개 변수로 `PickOptions`를 사용합니다. 결과는 `PickAsync`와 동일하지만 `FileResult` 대신, 반복될 수 있는 `IEnumerable<FileResult>`가 반환됩니다.

## <a name="api"></a>API

- [FilePicker 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/FilePicker)
- [FilePicker API 설명서](xref:Xamarin.Essentials.FilePicker)

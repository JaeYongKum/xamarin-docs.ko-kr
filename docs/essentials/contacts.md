---
title: 'Xamarin.Essentials: 연락처'
description: 사용자는 Xamarin.Essentials의 연락처 클래스를 사용하여 연락처를 선택하고 관련 정보를 검색할 수 있습니다.
ms.assetid: 02280c42-720a-44c3-979e-4818a20c9821
author: jamesmontemagno
ms.author: jamont
ms.date: 09/22/2020
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 19c9929706b7cf285b22562b094d2de2a25ff77d
ms.sourcegitcommit: 0a41c4aa6db72cd2d0cecbe0dc893024cecac71d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96749893"
---
# <a name="no-locxamarinessentials-contacts"></a>Xamarin.Essentials: 연락처

사용자는 **연락처** 클래스를 사용하여 연락처를 선택하고 관련 정보를 검색할 수 있습니다.

![시험판 API](~/media/shared/preview.png)

## <a name="get-started"></a>시작하기

[!include[](~/essentials/includes/get-started.md)]

**연락처** 기능에 액세스하려면 다음 플랫폼 관련 설정이 필요합니다.

# <a name="android"></a>[Android](#tab/android)

`ReadContacts` 권한이 필요하며 Android 프로젝트에서 구성해야 합니다. 이 권한은 다음과 같은 방법으로 추가할 수 있습니다.

**속성** 폴더 아래의 **AssemblyInfo.cs** 파일을 열고 다음을 추가합니다.

```csharp
[assembly: UsesPermission(Android.Manifest.Permission.ReadContacts)]
```

또는 Android 매니페스트를 업데이트합니다.

**속성** 폴더 아래의 **AndroidManifest.xml** 파일을 열고 **매니페스트** 노드 내부에 다음을 추가합니다.

```xml
<uses-permission android:name="android.permission.READ_CONTACTS" /> />
```

또는 Android 프로젝트를 마우스 오른쪽 단추로 클릭하고 프로젝트의 속성을 엽니다. **Android 매니페스트** 아래에서 **필요한 권한:** 영역을 찾아 이 권한을 선택합니다. 그러면 **AndroidManifest.xml** 파일이 자동으로 업데이트됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

`Info.plist`에 다음 키를 추가합니다.

```xml
<key>NSContactsUsageDescription</key>
<string>This app needs access to contacts to pick a contact and get info.</string>
```

사용자에게 표시되는 앱에 대한 설명에서 특정하게 `<string>`을 업데이트해야 합니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

`Package.appxmanifest`의 **기능** 에서 `Contact` 기능을 선택합니다.

-----

## <a name="pick-a-contact"></a>연락처 선택

`Contacts.PickContactAsync()`를 호출하여 연락처 대화 상자를 표시하고 사용자가 사용자에 대한 정보를 받을 수 있습니다.


```csharp
try
{
    var contact = await Contacts.PickContactAsync();

    if(contact == null)
        return;

    var id = contact.Id;
    var namePrefix = contact.NamePrefix;
    var givenName = contact.GivenName;
    var middleName = contact.MiddleName;
    var familyName = contact.FamilyName;
    var nameSuffix = contact.NameSuffix;
    var displayName = contact.DisplayName;
    var phones = contact.Phones; // List of phone numbers
    var emails = contact.Emails; // List of email addresses
}
catch (Exception ex)
{
    // Handle exception here.
}
```

## <a name="get-all-contacts"></a>모든 연락처 가져오기

```csharp
ObservableCollection<Contact> contactsCollect = new ObservableCollection<Contact>();

try
{
    // cancellationToken parameter is optional
    var cancellationToken = default(CancellationToken);
    var contacts = await Contacts.GetAllAsync(cancellationToken);

    if (contacts == null)
        return;

    foreach (var contact in contacts)
        contactsCollect.Add(contact);
}
catch (Exception ex)
{
    // Handle exception here.
}
```

## <a name="platform-differences"></a>플랫폼 간 차이점

# <a name="android"></a>[Android](#tab/android)

- `GetAllAsync` 메서드의 `cancellationToken` 매개 변수는 UWP에서만 사용됩니다.

# <a name="ios"></a>[iOS](#tab/ios)

- `GetAllAsync` 메서드의 `cancellationToken` 매개 변수는 UWP에서만 사용됩니다.
- iOS 플랫폼은 기본적으로 `DisplayName` 속성을 지원하지 않으므로 `DisplayName` 값은 "GivenName FamilyName"으로 생성됩니다.

# <a name="uwp"></a>[UWP](#tab/uwp)

플랫폼의 차이점이 없습니다.

-----


## <a name="api"></a>API

- [연락처 소스 코드](https://github.com/xamarin/Essentials/tree/main/Xamarin.Essentials/Contacts)
- [연락처 API 설명서](xref:Xamarin.Essentials.Contacts)

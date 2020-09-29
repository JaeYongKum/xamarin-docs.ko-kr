---
title: 두 번째 도구 모음 추가
ms.prod: xamarin
ms.assetid: FCE0AD27-8B6B-47C6-AD19-2B1C12E1BBBF
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 02/15/2018
ms.openlocfilehash: e6104a58c35b4daf8e204b3937022103d774615c
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91457804"
---
# <a name="adding-a-second-toolbar"></a>두 번째 도구 모음 추가

## <a name="overview"></a>개요 

는 `Toolbar` 활동 내에서 여러 번 사용할 수 있는 작업 모음을 대체 하는 것 보다 더 많은 작업을 수행할 수 있으며 &ndash; , 화면에서 배치 하도록 사용자 지정 하 고, 화면의 일부 너비로만 구성 될 수 있습니다. 아래 예제에서는 두 번째를 만들어 `Toolbar` 화면 아래쪽에 넣는 방법을 보여 줍니다. `Toolbar` **복사**, **잘라내기**및 **붙여넣기** 메뉴 항목을 구현 합니다. 

## <a name="define-the-second-toolbar"></a>두 번째 도구 모음 정의 

레이아웃 파일 **Main. axml** 을 편집 하 고 내용을 다음 XML로 바꿉니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <include
        android:id="@+id/toolbar"
        layout="@layout/toolbar" />
    <LinearLayout
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:id="@+id/main_content"
        android:layout_below="@id/toolbar">
      <ImageView
          android:layout_width="fill_parent"
          android:layout_height="0dp"
          android:layout_weight="1" />
      <Toolbar
          android:id="@+id/edit_toolbar"
          android:minHeight="?android:attr/actionBarSize"
          android:background="?android:attr/colorAccent"
          android:theme="@android:style/ThemeOverlay.Material.Dark.ActionBar"
          android:layout_width="match_parent"
          android:layout_height="wrap_content" />
    </LinearLayout>
</RelativeLayout>
```

이 XML은 화면의 `Toolbar` 가운데에 빈가 있는 화면 아래쪽에 두 번째를 추가 합니다 `ImageView` . 이의 높이는 `Toolbar` 작업 모음의 높이로 설정 됩니다. 

```xml
android:minHeight="?android:attr/actionBarSize"
```

이의 배경색은 `Toolbar` 다음에 정의 되는 악센트 색으로 설정 됩니다.

```xml
android:background="?android:attr/colorAccent
```

이는 `Toolbar` **ThemeOverlay.Material.Dark.ActionBar** `Toolbar` [Replacing the Action Bar](~/android/user-interface/controls/tool-bar/replacing-the-action-bar.md) &ndash; 활동의 창 décor 또는 첫 번째에서 사용 된 테마에 바인딩되지 않은 작업 모음를 대체 하 여 만든에서 사용 하는 것과 다른 테마 (ThemeOverlay ActionBar)를 기반으로 `Toolbar` 합니다.

**리소스/값/styles.xml** 를 편집 하 고 스타일 정의에 다음 강조 색을 추가 합니다. 

```xml
<item name="android:colorAccent">#C7A935</item>
```

그러면 아래쪽 도구 모음에 짙은 주황색 색이 제공 됩니다. 앱을 빌드하고 실행 하면 화면 아래쪽에 빈 두 번째 도구 모음이 표시 됩니다. 

[![화면 아래쪽에 노란색 두 번째 도구 모음이 있는 앱의 스크린샷](adding-a-second-toolbar-images/01-second-toolbar-sml.png)](adding-a-second-toolbar-images/01-second-toolbar.png#lightbox)

## <a name="add-edit-menu-items"></a>편집 메뉴 항목 추가 

이 섹션에서는 아래쪽에 편집 메뉴 항목을 추가 하는 방법에 대해 설명 합니다 `Toolbar` . 

보조 항목에 메뉴 항목을 추가 하려면 `Toolbar` 다음을 수행 합니다. 

1. `mipmap-`응용 프로그램 프로젝트의 폴더 (필요한 경우)에 메뉴 아이콘을 추가 합니다.

2. **리소스/메뉴**에 추가 메뉴 리소스 파일을 추가 하 여 메뉴 항목의 내용을 정의 합니다. 

3. 활동의 메서드에서를 `OnCreate` `Toolbar` 호출 하 여를 찾고 `FindViewById` `Toolbar` 의 메뉴를 확장 합니다.

4. 에서 `OnCreate` 새 메뉴 항목에 대 한 클릭 처리기를 구현 합니다. 

다음 섹션에서는이 프로세스에 대해 자세히 설명 합니다. **잘라내기**, **복사**및 **붙여넣기** 메뉴 항목이 아래쪽에 추가 됩니다 `Toolbar` . 

### <a name="define-the-edit-menu-resource"></a>편집 메뉴 리소스 정의

**리소스/메뉴** 하위 디렉터리에서 **edit_menus.xml** 라는 새 xml 파일을 만들고 내용을 다음 xml로 바꿉니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
  <item
       android:id="@+id/menu_cut"
       android:icon="@mipmap/ic_menu_cut_holo_dark"
       android:showAsAction="ifRoom"
       android:title="Cut" />
  <item
       android:id="@+id/menu_copy"
       android:icon="@mipmap/ic_menu_copy_holo_dark"
       android:showAsAction="ifRoom"
       android:title="Copy" />
  <item
       android:id="@+id/menu_paste"
       android:icon="@mipmap/ic_menu_paste_holo_dark"
       android:showAsAction="ifRoom"
       android:title="Paste" />
</menu>
```

이 XML은 **잘라내기**, **복사**및 **붙여넣기** 메뉴 항목을 만듭니다 .이 메뉴 항목은 폴더에 추가 된 아이콘을 사용 하 여 `mipmap-` [작업 모음 바꿉니다](~/android/user-interface/controls/tool-bar/replacing-the-action-bar.md).

### <a name="inflate-the-menus"></a>메뉴를 확장 합니다.

`OnCreate` **MainActivity.cs**의 메서드 끝에 다음 코드 줄을 추가 합니다. 

```csharp
var editToolbar = FindViewById<Toolbar>(Resource.Id.edit_toolbar);
editToolbar.Title = "Editing";
editToolbar.InflateMenu (Resource.Menu.edit_menus);
editToolbar.MenuItemClick += (sender, e) => {
    Toast.MakeText(this, "Bottom toolbar tapped: " + e.Item.TitleFormatted, ToastLength.Short).Show();
};
```

이 코드는 `edit_toolbar` 늘어납니다에 정의 된 뷰 **를 찾고**, 해당 제목을 **편집**으로 설정 하 고, **edit_menus.xml**에 정의 된 메뉴 항목을 표시 합니다. 누른 편집 아이콘을 표시 하는 알림 메시지를 표시 하는 메뉴 클릭 처리기를 정의 합니다. 

앱을 빌드하여 실행합니다. 앱이 실행 되 면 위에 추가 된 텍스트와 아이콘이 다음과 같이 표시 됩니다. 

[![잘라내기, 복사 및 붙여넣기 아이콘이 있는 아래쪽 도구 모음의 다이어그램](adding-a-second-toolbar-images/02-bottom-toolbar-sml.png)](adding-a-second-toolbar-images/02-bottom-toolbar.png#lightbox)

**잘라내기** 메뉴 아이콘을 탭 하면 다음과 같은 알림이 표시 됩니다. 

[![잘라내기 메뉴 아이콘을 탭 했음을 나타내는 알림 스크린샷](adding-a-second-toolbar-images/03-bottom-tapped-sml.png)](adding-a-second-toolbar-images/03-bottom-tapped.png#lightbox)

두 도구 모음에서 메뉴 항목을 누르면 결과 알림을 표시 됩니다. 

[![탭 하는 저장, 복사 및 붙여넣기 메뉴 항목에 대 한 알림을 스크린샷](adding-a-second-toolbar-images/04-menu-action-sml.png)](adding-a-second-toolbar-images/04-menu-action.png#lightbox)

## <a name="the-up-button"></a>위쪽 단추 

대부분의 Android 앱은 앱 탐색에 대해 **뒤로** 단추를 사용 합니다. **뒤로** 단추를 누르면 사용자가 이전 화면으로 이동 합니다.
그러나 사용자가 앱의 주 화면으로 "위로" 이동할 수 있도록 하 **는 단추를 제공 하는 것** 도 좋습니다. 사용자가 **위로** 단추를 선택 하면 사용자가 앱 계층 구조에서 상위 수준으로 이동 합니다. 즉 &ndash; , 앱이 이전에 방문한 작업을 다시 팝 하지 않고 뒤로 스택에 있는 여러 작업을 다시 팝 합니다. 

작업 모음으로를 사용 하는 두 번째 활동에서 **위로** 단추를 사용 하도록 설정 하려면 `Toolbar` `SetDisplayHomeAsUpEnabled` `SetHomeButtonEnabled` 두 번째 활동의 메서드에서 및 메서드를 호출 합니다 `OnCreate` .

```csharp
SetActionBar (toolbar);
...
ActionBar.SetDisplayHomeAsUpEnabled (true);
ActionBar.SetHomeButtonEnabled (true);
```

[Support V7 Toolbar](/samples/xamarin/monodroid-samples/supportv7-appcompat-toolbar) 코드 샘플은 **Up** 단추를 실행 하는 방법을 보여 줍니다. 이 샘플 (다음에 설명 된 AppCompat 라이브러리 사용)은 이전 작업에 대 한 계층적 탐색을 위한 도구 모음 **위쪽** 단추를 사용 하는 두 번째 활동을 구현 합니다. 이 예제에서 `DetailActivity` 홈 단추는 다음 메서드를 호출 하 여 **Up** 단추를 활성화 합니다 `SupportActionBar` . 

```csharp
SetSupportActionBar (toolbar);
...
SupportActionBar.SetDisplayHomeAsUpEnabled (true);
SupportActionBar.SetHomeButtonEnabled (true);
```

사용자가에서로 이동 `MainActivity` 하면 `DetailActivity` 는 `DetailActivity` 스크린샷에 표시 된 것 처럼 **위쪽** 단추 (왼쪽 화살표)를 표시 합니다.

[![도구 모음에 있는 위로 단추 왼쪽 화살표의 스크린샷 예](adding-a-second-toolbar-images/05-up-button-sml.png)](adding-a-second-toolbar-images/05-up-button.png#lightbox)

이 **위로** 단추를 누르면 앱이로 돌아옵니다 `MainActivity` . 계층의 여러 수준을 포함 하는 더 복잡 한 앱에서이 단추를 누르면 사용자가 이전 화면이 아닌 앱에서 가장 높은 수준으로 돌아갑니다. 

## <a name="related-links"></a>관련 링크

- [롤리팝 도구 모음 (샘플)](/samples/xamarin/monodroid-samples/android50-toolbar)
- [AppCompat 도구 모음 (샘플)](/samples/xamarin/monodroid-samples/supportv7-appcompat-toolbar)
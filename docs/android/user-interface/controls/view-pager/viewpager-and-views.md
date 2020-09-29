---
title: 보기가 있는 ViewPager
description: ViewPager는 gestural 탐색을 구현할 수 있도록 하는 레이아웃 관리자입니다. Gestural 탐색을 사용 하면 사용자가 왼쪽 및 오른쪽으로 이동 하 여 데이터 페이지를 단계별로 이동할 수 있습니다. 이 가이드에서는 뷰를 데이터 페이지로 사용 하 여 ViewPager 및 PagerTabStrip를 사용 하 여 swipeable UI를 구현 하는 방법에 대해 설명 합니다. 이후 가이드에서는 페이지에 대 한 조각을 사용 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 42E5379F-B0F4-4B87-A314-BF3DE405B0C8
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 03/01/2018
ms.openlocfilehash: e4f4243c06d98eac6f3501c41b48508f260d4633
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91456992"
---
# <a name="viewpager-with-views"></a>보기가 있는 ViewPager

_ViewPager는 gestural 탐색을 구현할 수 있도록 하는 레이아웃 관리자입니다. Gestural 탐색을 사용 하면 사용자가 왼쪽 및 오른쪽으로 이동 하 여 데이터 페이지를 단계별로 이동할 수 있습니다. 이 가이드에서는 뷰를 데이터 페이지로 사용 하 여 ViewPager 및 PagerTabStrip를 사용 하 여 swipeable UI를 구현 하는 방법에 대해 설명 합니다. 이후 가이드에서는 페이지에 대 한 조각을 사용 하는 방법을 설명 합니다._

## <a name="overview"></a>개요

이 가이드는를 사용 하 여 `ViewPager` 낙 엽 및가 중 트리의 이미지 갤러리를 구현 하는 방법에 대 한 단계별 데모를 제공 하는 연습입니다. 이 앱에서 사용자는 "트리 카탈로그"를 swipes 하 여 트리 이미지를 볼 수 있습니다. 카탈로그의 각 페이지 맨 위에 있는 트리의 이름이에 나열 되 `PagerTabStrip` 고 트리의 이미지가에 표시 됩니다 `ImageView` . 어댑터는를 `ViewPager` 내부 데이터 모델에 인터페이스 하는 데 사용 됩니다. 이 앱은에서 파생 된 어댑터를 구현 `PagerAdapter` 합니다. 

`ViewPager`기반 앱은 종종 s를 사용 하 여 구현 되지만 `Fragment` 의 추가 복잡성 `Fragment` 이 필요 하지 않은 비교적 간단한 사용 사례가 있습니다. 예를 들어이 연습에서 설명 하는 기본 이미지 갤러리 앱에는를 사용할 필요가 없습니다 `Fragment` . 콘텐츠는 정적이 고 사용자는 서로 다른 이미지 사이에서 앞뒤로 swipes 표준 Android 보기 및 레이아웃을 사용 하 여 구현을 보다 간단 하 게 유지할 수 있습니다. 

## <a name="start-an-app-project"></a>앱 프로젝트 시작

**TreePager** 라는 새 android 프로젝트를 만듭니다 (새 android 프로젝트를 만드는 방법에 대 한 자세한 내용은 [Hello, android](~/android/get-started/hello-android/hello-android-quickstart.md) 참조). 그런 다음 NuGet 패키지 관리자를 시작 합니다. NuGet 패키지를 설치 하는 방법에 대 한 자세한 내용은 [연습: 프로젝트에 Nuget 포함](/visualstudio/mac/nuget-walkthrough)을 참조 하세요. **Android 지원 라이브러리 v4**찾기 및 설치: 

[![NuGet 패키지 관리자에서 선택한 v4 NuGet 지원의 스크린샷](viewpager-and-views-images/01-install-support-lib-sml.png)](viewpager-and-views-images/01-install-support-lib.png#lightbox)

그러면 **Android Support Library v4**로 reaquired 추가 패키지도 설치 됩니다.

## <a name="add-an-example-data-source"></a>예제 데이터 소스 추가

이 예제에서 클래스에 의해 표현 되는 트리 카탈로그 데이터 소스는 `TreeCatalog` `ViewPager` 항목 콘텐츠가 있는를 제공 합니다. 
`TreeCatalog` 어댑터에서를 만드는 데 사용할 트리 이미지 및 트리 제목의 미리 만들어진 컬렉션을 포함 `View` 합니다. 생성자에는 `TreeCatalog` 인수가 필요 하지 않습니다.

```csharp
TreeCatalog treeCatalog = new TreeCatalog();
```

에서 이미지 컬렉션은 `TreeCatalog` 각 이미지에 인덱서를 통해 액세스할 수 있도록 구성 되어 있습니다. 예를 들어 다음 코드 줄은 컬렉션의 세 번째 이미지에 대 한 이미지 리소스 ID를 검색 합니다. 

```csharp
int imageId = treeCatalog[2].imageId;
```

의 구현 세부 정보는 `TreeCatalog` 이해와 관련이 없으므로 `ViewPager` `TreeCatalog` 코드는 여기에 나열 되지 않습니다. 소스 코드는 `TreeCatalog` [TreeCatalog.cs](https://github.com/xamarin/monodroid-samples/blob/master/UserInterface/TreePager/TreePager/TreeCatalog.cs)에서 사용할 수 있습니다. 이 소스 파일을 다운로드 하거나 코드를 복사 하 여 새 **TreeCatalog.cs** 파일에 붙여 넣은 다음 프로젝트에 추가 합니다. 또한 [이미지 파일](https://github.com/xamarin/monodroid-samples/blob/master/UserInterface/TreePager/Resources/tree-images.zip?raw=true) 을 다운로드 하 여 **리소스/그릴** 수 있는 폴더에 압축을 풀고 프로젝트에 포함 합니다. 

## <a name="create-a-viewpager-layout"></a>ViewPager 레이아웃 만들기

**Resources/layout/Main. axml** 을 열고 내용을 다음 xml로 바꿉니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.view.ViewPager
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/viewpager"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

</android.support.v4.view.ViewPager>
```

이 XML은 `ViewPager` 전체 화면을 차지 하는를 정의 합니다. **android.support.v4.view.ViewPager** `ViewPager` 이 지원 라이브러리에 패키지 되어 있기 때문에 정규화 된 이름 android. v a v. `ViewPager`[Android 지원 라이브러리 v4](https://www.nuget.org/packages/Xamarin.Android.Support.v4/)에서만 사용할 수 있습니다. Android SDK에서 사용할 수 없습니다. 

## <a name="set-up-viewpager"></a>ViewPager 설정

**MainActivity.cs** 를 편집 하 고 다음 `using` 문을 추가 합니다.

```csharp
using Android.Support.V4.View;
```

`OnCreate` 메서드를 다음 코드로 바꿉니다.

```csharp
protected override void OnCreate(Bundle bundle)
{
    base.OnCreate(bundle);
    SetContentView(Resource.Layout.Main);
    ViewPager viewPager = FindViewById<ViewPager>(Resource.Id.viewpager);
    TreeCatalog treeCatalog = new TreeCatalog();
}
```

이 코드는 다음을 수행합니다.

1. **주. axml** 레이아웃 리소스에서 뷰를 설정 합니다.

2. 레이아웃에서에 대 한 참조를 검색 `ViewPager` 합니다.

3. 새를 `TreeCatalog` 데이터 소스로 인스턴스화합니다.

이 코드를 작성 하 고 실행 하면 다음 스크린샷에 표시 됩니다. 

[![빈 ViewPager를 표시 하는 앱의 스크린샷](viewpager-and-views-images/02-initial-screen-sml.png)](viewpager-and-views-images/02-initial-screen.png#lightbox)

이 시점에서는 `ViewPager` **TreeCatalog**의 콘텐츠에 액세스 하기 위한 어댑터가 부족 하기 때문에 비어 있습니다. 다음 섹션에서는를 **PagerAdapter** `ViewPager` **TreeCatalog**에 연결 하기 위해 PagerAdapter를 만듭니다. 

## <a name="create-the-adapter"></a>어댑터 만들기

`ViewPager` 는와 데이터 원본 사이에 있는 어댑터 컨트롤러 개체를 사용 `ViewPager` 합니다 ( [어댑터](~/android/user-interface/controls/view-pager/index.md#adapter)의 그림 참조). 이 데이터에 액세스 하려면 `ViewPager` 에서 파생 된 사용자 지정 어댑터를 제공 해야 `PagerAdapter` 합니다. 이 어댑터는 각 `ViewPager` 페이지를 데이터 원본의 콘텐츠로 채웁니다. 이 데이터 소스는 앱 마다 다르므로 사용자 지정 어댑터는 데이터에 액세스 하는 방법을 이해 하는 코드입니다. 사용자가의 페이지 `ViewPager` 를 swipes 어댑터는 데이터 원본에서 정보를 추출 하 여 표시할에 대 한 페이지로 로드 합니다 `ViewPager` . 

을 구현 하는 경우 `PagerAdapter` 다음을 재정의 해야 합니다.

- **InstantiateItem** &ndash; `View`지정 된 위치에 대 한 페이지 ()를 만들어 `ViewPager` 의 뷰 컬렉션에 추가 합니다. 

- **DestroyItem** &ndash; 지정 된 위치에서 페이지를 제거 합니다.

- **개수** &ndash; 사용 가능한 뷰 (페이지) 수를 반환 하는 읽기 전용 속성입니다. 

- **IsViewFromObject** &ndash; 페이지가 특정 키 개체와 연결 되어 있는지 여부를 확인 합니다. 이 개체는 메서드에 의해 생성 됩니다 `InstantiateItem` . 이 예제에서 키 개체는 `TreeCatalog` 데이터 개체입니다.

**TreePagerAdapter.cs** 라는 새 파일을 추가 하 고 해당 내용을 다음 코드로 바꿉니다. 

```csharp
using System;
using Android.App;
using Android.Runtime;
using Android.Content;
using Android.Views;
using Android.Widget;
using Android.Support.V4.View;
using Java.Lang;

namespace TreePager
{
    class TreePagerAdapter : PagerAdapter
    {
        public override int Count
        {
            get { throw new NotImplementedException(); }
        }

        public override bool IsViewFromObject(View view, Java.Lang.Object obj)
        {
            throw new NotImplementedException();
        }

        public override Java.Lang.Object InstantiateItem (View container, int position)
        {
            throw new NotImplementedException();
        }

        public override void DestroyItem(View container, int position, Java.Lang.Object view)
        {
            throw new NotImplementedException();
        }
    }
}
```

이 코드는 필수 구현을 스텁 `PagerAdapter` 합니다. 다음 섹션에서는 이러한 각 메서드가 작업 코드로 대체 되었습니다. 

### <a name="implement-the-constructor"></a>생성자 구현

앱은를 인스턴스화하면 `TreePagerAdapter` 컨텍스트 ( `MainActivity` )와 인스턴스화된를 제공 `TreeCatalog` 합니다. `TreePagerAdapter` **TreePagerAdapter.cs**에서 클래스의 맨 위에 다음 멤버 변수 및 생성자를 추가 합니다. 

```csharp
Context context;
TreeCatalog treeCatalog;

public TreePagerAdapter (Context context, TreeCatalog treeCatalog)
{
    this.context = context;
    this.treeCatalog = treeCatalog;
}
```

이 생성자의 목적은에서 사용할 컨텍스트 및 인스턴스를 저장 하는 것입니다 `TreeCatalog` `TreePagerAdapter` . 

### <a name="implement-count"></a>개수 구현

`Count`구현은 비교적 간단 하며 트리 카탈로그의 트리 수를 반환 합니다. `Count`를 다음 코드로 바꿉니다.

```csharp
public override int Count
{
    get { return treeCatalog.NumTrees; }
}
```

`NumTrees`의 속성은 `TreeCatalog` 데이터 집합의 트리 수 (페이지 수)를 반환 합니다.

### <a name="implement-instantiateitem"></a>InstantiateItem 구현

`InstantiateItem`메서드는 지정 된 위치에 대 한 페이지를 만듭니다. 또한의 뷰 컬렉션에 새로 만든 뷰를 추가 해야 합니다 `ViewPager` . 이를 가능 하 게 하기 위해는 `ViewPager` 자체를 컨테이너 매개 변수로 전달 합니다. 

`InstantiateItem` 메서드를 다음 코드로 바꿉니다.

```csharp
public override Java.Lang.Object InstantiateItem (View container, int position)
{
    var imageView = new ImageView (context);
    imageView.SetImageResource (treeCatalog[position].imageId);
    var viewPager = container.JavaCast<ViewPager>();
    viewPager.AddView (imageView);
    return imageView;
}
```

이 코드는 다음을 수행합니다.

1. 새를 인스턴스화하여 `ImageView` 지정 된 위치에 트리 이미지를 표시 합니다. 앱은 `MainActivity` 생성자에 전달 되는 컨텍스트입니다 `ImageView` .

2. 리소스를 `ImageView` `TreeCatalog` 지정 된 위치에 있는 이미지 리소스 ID로 설정 합니다.

3. 전달 된 컨테이너를 `View` 참조로 캐스팅 합니다 `ViewPager` .
    `JavaCast<ViewPager>()`를 사용 하 여이 캐스트를 올바르게 수행 해야 합니다 .이는 Android에서 런타임 검사 형식 변환을 수행 하는 데 필요 합니다.

4. 인스턴스화된를에 추가 하 `ImageView` `ViewPager` 고를 `ImageView` 호출자에 게 반환 합니다.

에서 `ViewPager` 이미지를 표시 하는 경우 `position` 이를 표시 `ImageView` 합니다. 처음에 `InstantiateItem` 는 처음 두 페이지를 뷰로 채우기 위해가 두 번 호출 됩니다. 사용자가 스크롤하면 현재 표시 된 항목의 바로 뒤에 있는 뷰를 유지 하기 위해 다시 호출 됩니다. 

### <a name="implement-destroyitem"></a>DestroyItem 구현

`DestroyItem`메서드는 지정 된 위치에서 페이지를 제거 합니다. 지정 된 위치의 뷰가 변경 될 수 있는 응용 프로그램에서는 `ViewPager` 새 뷰로 바꾸기 전에 해당 위치에서 오래 된 보기를 제거 하는 방법이 필요 합니다. `TreeCatalog`이 예제에서는 각 위치의 뷰가 변경 되지 않으므로에 의해 제거 된 뷰는 `DestroyItem` `InstantiateItem` 해당 위치에 대해가 호출 될 때만 다시 추가 됩니다. 효율성 향상을 위해 `View` 동일한 위치에 다시 표시 되는를 재활용할 풀을 구현할 수 있습니다. 

`DestroyItem` 메서드를 다음 코드로 바꿉니다. 

```csharp
public override void DestroyItem(View container, int position, Java.Lang.Object view)
{
    var viewPager = container.JavaCast<ViewPager>();
    viewPager.RemoveView(view as View);
}
```

이 코드는 다음을 수행합니다.

1. 전달 된 컨테이너를 `View` 참조로 캐스팅 `ViewPager` 합니다.

2. 전달 된 Java 개체 ( `view` )를 c # ()으로 캐스팅 합니다 `View` `view as View` .

3. 에서 뷰를 제거 합니다 `ViewPager` . 

### <a name="implement-isviewfromobject"></a>IsViewFromObject 구현

사용자가 콘텐츠 페이지에서 왼쪽과 오른쪽으로 이동 하면을 `ViewPager` 호출 `IsViewFromObject` 하 여 지정 된 위치의 자식이 `View` 동일한 위치에 대 한 어댑터의 개체와 연결 되어 있는지 확인 합니다. 따라서 어댑터의 개체를 *개체 키*라고 합니다. 비교적 간단한 앱의 경우 연결은 id 중 하나입니다 &ndash; . 해당 인스턴스에서 어댑터의 개체 키는 이전에를 통해로 반환 된 뷰입니다 `ViewPager` `InstantiateItem` . 그러나 다른 앱의 경우에는 개체 키가 `ViewPager` 해당 위치에 표시 되는 자식 뷰와 연결 되어 있지만 이와는 다른 어댑터별 클래스 인스턴스일 수 있습니다. 어댑터 에서만 전달 된 뷰와 개체 키가 연결 되어 있는지 여부를 알 수 있습니다. 

`IsViewFromObject` 제대로 작동 하려면를 구현 해야 합니다 `PagerAdapter` . 이 `IsViewFromObject` `false` 지정 된 위치에 대해를 반환 하면 `ViewPager` 는 해당 위치에 뷰를 표시 하지 않습니다. 앱에서에 `TreePager` 의해 반환 되는 개체 키는 `InstantiateItem` *is* `View` 트리의 페이지 이므로 코드에서 id를 확인 하기만 하면 됩니다. 즉, 개체 키와 뷰가 동일 합니다. `IsViewFromObject`를 다음 코드로 바꿉니다. 

```csharp
public override bool IsViewFromObject(View view, Java.Lang.Object obj)
{
    return view == obj;
}
```

## <a name="add-the-adapter-to-the-viewpager"></a>ViewPager에 어댑터를 추가 합니다.

가 구현 되었으므로 이제에 추가 해야 합니다 `TreePagerAdapter` `ViewPager` . **MainActivity.cs**에서 메서드의 끝에 다음 코드 줄을 추가 합니다 `OnCreate` .

```csharp
viewPager.Adapter = new TreePagerAdapter(this, treeCatalog);
```

이 코드는를 인스턴스화하고 `TreePagerAdapter` `MainActivity` 컨텍스트 ()로를 전달 합니다 `this` . 인스턴스화된는 `TreeCatalog` 생성자의 두 번째 인수로 전달 됩니다. `ViewPager`의 `Adapter` 속성은 인스턴스화된 개체로 설정 됩니다 `TreePagerAdapter` . 이렇게 하면 `TreePagerAdapter` 가에 연결 됩니다 `ViewPager` . 

이제 코어 구현이 완료 되 &ndash; 고 앱이 실행 됩니다. 다음 스크린샷에 왼쪽에 표시 된 대로 트리 카탈로그의 첫 번째 이미지가 화면에 나타납니다. 왼쪽으로 살짝 밀어 트리 보기를 표시 한 다음 오른쪽으로 살짝 밀어 트리 카탈로그를 통해 다시 이동 합니다. 

[![트리 이미지를 통해 TreePager 앱의 스크린샷 살짝 밀기](viewpager-and-views-images/03-example-views-sml.png)](viewpager-and-views-images/03-example-views.png#lightbox)

## <a name="add-a-pager-indicator"></a>호출기 표시기 추가

이 최소 `ViewPager` 구현에는 트리 카탈로그의 이미지가 표시 되지만 사용자가 카탈로그 내에 있는 위치를 나타내는 것은 표시 되지 않습니다. 다음 단계는을 추가 하는 것입니다 `PagerTabStrip` . 는 `PagerTabStrip` 사용자에 게 표시 되는 페이지를 알리고 이전 및 다음 페이지의 힌트를 표시 하 여 탐색 컨텍스트를 제공 합니다. `PagerTabStrip` 는의 현재 페이지에 대 한 표시기로 사용 하기 위한 것으로 `ViewPager` , 사용자가 각 페이지를 swipes 때 스크롤하고 업데이트 합니다. 

**리소스/레이아웃/기본. axml** 을 열고 레이아웃에를 추가 합니다 `PagerTabStrip` .

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.view.ViewPager
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/viewpager"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <android.support.v4.view.PagerTabStrip
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:layout_gravity="top"
          android:paddingBottom="10dp"
          android:paddingTop="10dp"
          android:textColor="#fff" />

</android.support.v4.view.ViewPager>
```

`ViewPager` 및 `PagerTabStrip` 는 함께 작동 하도록 설계 되었습니다. 레이아웃 내에서를 선언 하면에서 `PagerTabStrip` `ViewPager` `ViewPager` 자동으로를 찾아서 `PagerTabStrip` 어댑터에 연결 합니다. 앱을 빌드하고 실행할 때 `PagerTabStrip` 각 화면 맨 위에 빈가 표시 되어야 합니다. 

[![빈 PagerTabStrip의 확대/확대 스크린 샷](viewpager-and-views-images/04-empty-pagetabstrip-cap-sml.png)](viewpager-and-views-images/04-empty-pagetabstrip-cap.png#lightbox)

### <a name="display-a-title"></a>제목 표시

각 페이지 탭에 제목을 추가 하려면 `GetPageTitleFormatted` 파생 클래스에서 메서드를 구현 합니다 `PagerAdapter` . `ViewPager``GetPageTitleFormatted`(구현 된 경우)를 호출 하 여 지정 된 위치에서 페이지를 설명 하는 제목 문자열을 가져옵니다. `TreePagerAdapter` **TreePagerAdapter.cs**의 클래스에 다음 메서드를 추가 합니다. 

```csharp
public override Java.Lang.ICharSequence GetPageTitleFormatted(int position)
{
    return new Java.Lang.String(treeCatalog[position].caption);
}
```

이 코드는 트리 카탈로그의 지정 된 페이지 (위치)에서 트리 캡션 문자열을 검색 하 고이를 Java로 변환한 `String` 다음로 반환 `ViewPager` 합니다. 이 새 메서드를 사용 하 여 앱을 실행 하면 각 페이지에에 트리 캡션이 표시 됩니다 `PagerTabStrip` . 화면 맨 위에 밑줄 없이 트리 이름이 표시 됩니다. 

[![텍스트 채우기 PagerTabStrip 탭이 있는 페이지의 스크린샷](viewpager-and-views-images/05-final-pagetabstrip-sml.png)](viewpager-and-views-images/05-final-pagetabstrip.png#lightbox)

앞뒤로 살짝 밀어 카탈로그에서 각 캡션 트리 이미지를 볼 수 있습니다. 

### <a name="pagertitlestrip-variation"></a>PagerTitleStrip 변형

`PagerTitleStrip` 는를 제외 하 고는와 매우 유사 `PagerTabStrip` `PagerTabStrip` 합니다. 단, 현재 선택 된 탭에 밑줄을 추가 합니다. `PagerTabStrip` `PagerTitleStrip` 위의 레이아웃에서을로 바꾸고 앱을 다시 실행 하 여 어떻게 표시 되는지 확인할 수 있습니다 `PagerTitleStrip` . 

[![텍스트에서 밑줄이 제거 된 PagerTitleStrip](viewpager-and-views-images/06-pagetitlestrip-example-sml.png)](viewpager-and-views-images/06-pagetitlestrip-example.png#lightbox)

로 변환할 때 밑줄이 제거 됩니다 `PagerTitleStrip` . 

## <a name="summary"></a>요약

이 연습에서는를 사용 하지 않고 기본 기반 앱을 빌드하는 방법에 대 한 단계별 예제를 제공 `ViewPager` `Fragment` 했습니다. 이미지 및 캡션 문자열이 포함 된 예제 데이터 소스, `ViewPager` 이미지를 표시 하는 레이아웃 및를 `PagerAdapter` 데이터 소스에 연결 하는 하위 클래스를 제공 `ViewPager` 합니다. 사용자가 데이터 집합을 탐색 하는 데 도움이 되도록 또는를 추가 하 여 `PagerTabStrip` `PagerTitleStrip` 각 페이지의 맨 위에 이미지 캡션을 표시 하는 방법을 설명 하는 지침이 포함 되어 있습니다. 

## <a name="related-links"></a>관련 링크

- [TreePager (샘플)](/samples/xamarin/monodroid-samples/userinterface-treepager)
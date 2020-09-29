---
title: Xamarin.ios에서 ListView 사용
description: ListView는 Android 응용 프로그램의 중요 한 UI 구성 요소입니다. 메뉴 옵션의 짧은 목록에서 긴 연락처 또는 인터넷 즐겨찾기 목록에 사용 됩니다. 기본 제공 스타일로 서식 지정 하거나 광범위 하 게 사용자 지정할 수 있는 행의 스크롤 목록을 표시 하는 간단한 방법을 제공 합니다.
ms.prod: xamarin
ms.assetid: C2BA2705-9B20-01C2-468D-860BDFEDC157
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 04/25/2018
ms.openlocfilehash: 50784844d35e2f04436b05d9491149a3e0282bdc
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91457192"
---
# <a name="xamarinandroid-listview"></a>Xamarin Android ListView

_ListView는 Android 응용 프로그램의 중요 한 UI 구성 요소입니다. 메뉴 옵션의 짧은 목록에서 긴 연락처 또는 인터넷 즐겨찾기 목록에 사용 됩니다. 기본 제공 스타일로 서식 지정 하거나 광범위 하 게 사용자 지정할 수 있는 행의 스크롤 목록을 표시 하는 간단한 방법을 제공 합니다._

## <a name="overview"></a>개요

목록 뷰와 어댑터는 Android 응용 프로그램의 가장 기본적인 구성 요소에 포함 되어 있습니다. `ListView`클래스는 짧은 메뉴 또는 긴 스크롤 목록 인지 여부에 관계 없이 데이터를 표시 하는 유연한 방법을 제공 합니다. 응용 프로그램에 대 한 모바일 친화적인 사용자 인터페이스를 빌드하는 데 도움이 되는 빠른 스크롤, 인덱스, 단일 또는 다중 선택 등의 유용성 기능을 제공 합니다. `ListView` 인스턴스에는 행 보기에 포함된 데이터를 사용하여 피드하는 *어댑터*가 필요합니다.

이 가이드에서는 `ListView` Xamarin Android에서 및 다양 한 클래스를 구현 하는 방법을 설명 합니다 `Adapter` . 또한의 모양을 사용자 지정 하는 방법을 보여 `ListView` 주고 메모리 사용을 줄이기 위해 행 다시 사용의 중요성에 대해 설명 합니다. 활동 수명 주기가 영향을 주고 사용 하는 방법에 대해서도 설명 `ListView` `Adapter` 합니다. Xamarin.ios를 사용 하 여 플랫폼 간 응용 프로그램에서 작업 하는 경우 컨트롤은 구조적 iOS와 비슷하며, Android는와 `ListView` `UITableView` `Adapter` 유사 `UITableViewSource` 합니다.

먼저 간단한 자습서에서는 `ListView` 기본 코드 예제를 사용 하는를 소개 합니다. 다음으로, `ListView` 실제 응용 프로그램에서 사용 하는 데 도움이 되는 고급 항목에 대 한 링크가 제공 됩니다.

> [!NOTE]
> `RecyclerView`위젯은 보다 고급 및 유연한 버전입니다 `ListView` . `RecyclerView`는 (및)의 후속 작업으로 설계 되었기 때문에 `ListView` `GridView` `RecyclerView` 새 앱 개발 대신를 사용 하는 것이 좋습니다 `ListView` . 자세한 내용은 [RecyclerView](~/android/user-interface/layouts/recycler-view/index.md)를 참조 하세요.

## <a name="listview-tutorial"></a>ListView 자습서

[`ListView`](xref:Android.Widget.ListView) 는입니다. [`ViewGroup`](xref:Android.Views.ViewGroup)
스크롤 가능한 항목 목록을 만드는입니다. 목록 항목은를 사용 하 여 목록에 자동으로 삽입 됩니다 [`IListAdapter`](xref:Android.Widget.IListAdapter) .

이 자습서에서는 문자열 배열에서 읽은 국가 이름으로 스크롤할 수 있는 목록을 만듭니다. 목록 항목을 선택 하면 목록에 있는 항목의 위치가 알림 메시지에 표시 됩니다.

**HelloListView**라는 새 프로젝트를 시작 합니다.

**list_item.xml** 이라는 XML 파일을 만들고 **리소스/레이아웃/** 폴더 내에 저장 합니다. 다음을 삽입 합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:padding="10dp"
    android:textSize="16sp">
</TextView>
```

이 파일은에 배치 될 각 항목의 레이아웃을 정의 [`ListView`](xref:Android.Widget.ListView) 합니다.

를 열고 `MainActivity.cs` 클래스를 수정 하 여 [`ListActivity`](xref:Android.App.ListActivity) (대신)를 확장 합니다 [`Activity`](xref:Android.App.Activity) .

```csharp
public class MainActivity : ListActivity
{
```

메서드에 대 한 다음 코드를 삽입 합니다 [`OnCreate()`](xref:Android.App.Activity.OnCreate*) .

```csharp
protected override void OnCreate (Bundle bundle)
{
    base.OnCreate (bundle);

    ListAdapter = new ArrayAdapter<string> (this, Resource.Layout.list_item, countries);

    ListView.TextFilterEnabled = true;

    ListView.ItemClick += delegate (object sender, AdapterView.ItemClickEventArgs args)
    {
        Toast.MakeText(Application, ((TextView)args.View).Text, ToastLength.Short).Show();
    };
}
```

이는 작업 (일반적으로)에 대 한 레이아웃 파일을 로드 하지 않습니다 [`SetContentView(int)`](xref:Android.App.Activity.SetContentView*) .
대신, 다음을 설정 합니다. [`ListAdapter`](xref:Android.App.ListActivity.ListAdapter)
속성이 자동으로 추가 됩니다. [`ListView`](xref:Android.Widget.ListView)
의 전체 화면을 채웁니다 [`ListActivity`](xref:Android.App.ListActivity) .
이 메서드는에 [`ArrayAdapter<T>`](xref:Android.Widget.ArrayAdapter`1) 배치 될 목록 항목의 배열을 관리 하는를 사용 [`ListView`](xref:Android.Widget.ListView) 합니다.
[`ArrayAdapter<T>`](xref:Android.Widget.ArrayAdapter`1)
생성자는 응용 프로그램 [`Context`](xref:Android.Content.Context) , 각 목록 항목 (이전 단계에서 생성)에 대 한 레이아웃 설명, `T[]` 또는 [`Java.Util.IList<T>`](xref:Java.Util.IList)
에 삽입할 개체의 배열입니다. [`ListView`](xref:Android.Widget.ListView)
(다음에 정의 됨).

[`TextFilterEnabled`](xref:Android.Widget.AbsListView.TextFilterEnabled)
속성은에 대 한 텍스트 필터링을 설정 하 [`ListView`](xref:Android.Widget.ListView) 여 사용자가 입력을 시작 하면 목록이 필터링 됩니다.

[`ItemClick`](xref:Android.Widget.AdapterView.ItemClick)
이벤트를 사용 하 여 클릭에 대 한 처리기를 구독할 수 있습니다. 항목을 [`ListView`](xref:Android.Widget.ListView)
를 클릭 하면 처리기가 호출 되 고, [`Toast`](xref:Android.Widget.Toast)
클릭 한 항목의 텍스트를 사용 하 여 메시지가 표시 됩니다.

에 대 한 고유한 레이아웃 파일을 정의 하는 대신 플랫폼에서 제공 하는 목록 항목 디자인을 사용할 수 있습니다 [`ListAdapter`](xref:Android.App.ListActivity.ListAdapter) .
예를 들어 대신를 사용해 보세요 `Android.Resource.Layout.SimpleListItem1` `Resource.Layout.list_item` .

다음 `using` 문을 추가합니다.

```csharp
using System;
```

다음으로 다음 문자열 배열을의 멤버로 추가 합니다 `MainActivity` .

```csharp
static readonly string[] countries = new String[] {
    "Afghanistan","Albania","Algeria","American Samoa","Andorra",
    "Angola","Anguilla","Antarctica","Antigua and Barbuda","Argentina",
    "Armenia","Aruba","Australia","Austria","Azerbaijan",
    "Bahrain","Bangladesh","Barbados","Belarus","Belgium",
    "Belize","Benin","Bermuda","Bhutan","Bolivia",
    "Bosnia and Herzegovina","Botswana","Bouvet Island","Brazil","British Indian Ocean Territory",
    "British Virgin Islands","Brunei","Bulgaria","Burkina Faso","Burundi",
    "Cote d'Ivoire","Cambodia","Cameroon","Canada","Cape Verde",
    "Cayman Islands","Central African Republic","Chad","Chile","China",
    "Christmas Island","Cocos (Keeling) Islands","Colombia","Comoros","Congo",
    "Cook Islands","Costa Rica","Croatia","Cuba","Cyprus","Czech Republic",
    "Democratic Republic of the Congo","Denmark","Djibouti","Dominica","Dominican Republic",
    "East Timor","Ecuador","Egypt","El Salvador","Equatorial Guinea","Eritrea",
    "Estonia","Ethiopia","Faeroe Islands","Falkland Islands","Fiji","Finland",
    "Former Yugoslav Republic of Macedonia","France","French Guiana","French Polynesia",
    "French Southern Territories","Gabon","Georgia","Germany","Ghana","Gibraltar",
    "Greece","Greenland","Grenada","Guadeloupe","Guam","Guatemala","Guinea","Guinea-Bissau",
    "Guyana","Haiti","Heard Island and McDonald Islands","Honduras","Hong Kong","Hungary",
    "Iceland","India","Indonesia","Iran","Iraq","Ireland","Israel","Italy","Jamaica",
    "Japan","Jordan","Kazakhstan","Kenya","Kiribati","Kuwait","Kyrgyzstan","Laos",
    "Latvia","Lebanon","Lesotho","Liberia","Libya","Liechtenstein","Lithuania","Luxembourg",
    "Macau","Madagascar","Malawi","Malaysia","Maldives","Mali","Malta","Marshall Islands",
    "Martinique","Mauritania","Mauritius","Mayotte","Mexico","Micronesia","Moldova",
    "Monaco","Mongolia","Montserrat","Morocco","Mozambique","Myanmar","Namibia",
    "Nauru","Nepal","Netherlands","Netherlands Antilles","New Caledonia","New Zealand",
    "Nicaragua","Niger","Nigeria","Niue","Norfolk Island","North Korea","Northern Marianas",
    "Norway","Oman","Pakistan","Palau","Panama","Papua New Guinea","Paraguay","Peru",
    "Philippines","Pitcairn Islands","Poland","Portugal","Puerto Rico","Qatar",
    "Reunion","Romania","Russia","Rwanda","Sqo Tome and Principe","Saint Helena",
    "Saint Kitts and Nevis","Saint Lucia","Saint Pierre and Miquelon",
    "Saint Vincent and the Grenadines","Samoa","San Marino","Saudi Arabia","Senegal",
    "Seychelles","Sierra Leone","Singapore","Slovakia","Slovenia","Solomon Islands",
    "Somalia","South Africa","South Georgia and the South Sandwich Islands","South Korea",
    "Spain","Sri Lanka","Sudan","Suriname","Svalbard and Jan Mayen","Swaziland","Sweden",
    "Switzerland","Syria","Taiwan","Tajikistan","Tanzania","Thailand","The Bahamas",
    "The Gambia","Togo","Tokelau","Tonga","Trinidad and Tobago","Tunisia","Turkey",
    "Turkmenistan","Turks and Caicos Islands","Tuvalu","Virgin Islands","Uganda",
    "Ukraine","United Arab Emirates","United Kingdom",
    "United States","United States Minor Outlying Islands","Uruguay","Uzbekistan",
    "Vanuatu","Vatican City","Venezuela","Vietnam","Wallis and Futuna","Western Sahara",
    "Yemen","Yugoslavia","Zambia","Zimbabwe"
  };
```

에 배치 되는 문자열 배열입니다 [`ListView`](xref:Android.Widget.ListView) .

애플리케이션을 실행합니다. 목록을 스크롤하거나를 입력 하 여 필터링 한 다음 항목을 클릭 하 여 메시지를 볼 수 있습니다. 다음과 비슷한 결과가 표시됩니다.

[![Country 이름이 있는 ListView의 예제 스크린샷](images/01-listview-example-sml.png)](images/01-listview-example.png#lightbox)

하드 코드 된 문자열 배열을 사용 하는 것은 최상의 디자인 방법이 아닙니다. 간단한 설명을 위해이 자습서에서 사용 되는 것은 [`ListView`](xref:Android.Widget.ListView)
위젯. `string-array`프로젝트 **리소스/값/Strings.xml** 파일의 리소스와 같이 외부 리소스에 의해 정의 된 문자열 배열을 참조 하는 것이 더 좋습니다. 다음은 그 예입니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
  <string name="app_name">HelloListView</string>
  <string-array name="countries_array">
    <item>Bahrain</item>
    <item>Bangladesh</item>
    <item>Barbados</item>
    <item>Belarus</item>
    <item>Belgium</item>
    <item>Belize</item>
    <item>Benin</item>
  </string-array>
</resources>
```

에 이러한 리소스 문자열을 사용 하려면 [`ArrayAdapter`](xref:Android.Widget.ArrayAdapter`1) 원래 [`ListAdapter`](xref:Android.App.ListActivity.ListAdapter)
다음 줄로 바꿉니다.

```csharp
string[] countries = Resources.GetStringArray (Resource.Array.countries_array);
ListAdapter = new ArrayAdapter<string> (this, Resource.Layout.list_item, countries);
```

애플리케이션을 실행합니다. 다음과 비슷한 결과가 표시됩니다.

[![이름 목록이 작은 ListView의 예제 스크린샷](images/02-smaller-example-sml.png)](images/02-smaller-example.png#lightbox)

## <a name="going-further-with-listview"></a>ListView로 자세히 이동

나머지 토픽 (아래 링크 참조)에서는 `ListView` 클래스와 함께 사용할 수 있는 다양 한 유형의 어댑터 유형을 사용 하는 방법에 대해 포괄적으로 설명 합니다. 구조는 다음과 같습니다.

- **시각적 모양** &ndash; 컨트롤의 부분과 `ListView` 작동 방법

- **클래스** &ndash; 를 표시 하는 데 사용 되는 클래스에 대 한 개요   `ListView` 입니다.

- ListView에서 데이터 **표시** &ndash; 간단한 데이터 목록을 표시 하는 방법 유용성 기능을 구현 하는 방법 `ListView's` , 다른 기본 제공 행 레이아웃을 사용 하는 방법 및 어댑터에서 행 뷰를 다시 사용 하 여 메모리를 절약 하는 방법

- **사용자 지정 모양** &ndash; `ListView` 사용자 지정 레이아웃, 글꼴 및 색을 사용 하 여의 스타일 변경

- **SQLite 사용** &ndash; 를 사용 하 여 SQLite 데이터베이스의 데이터를 표시 하는 방법 `CursorAdapter`

- **활동 수명 주기** &ndash; `ListView` 수명 주기에서 데이터를 채워야 하는 위치 및 리소스를 해제할 시기를 포함 하 여 활동을 구현할 때의 디자인 고려 사항입니다.

토론 (6 개 부분으로 분리 됨)은 클래스 자체의 개요부터 시작 하 여 `ListView` 이를 사용 하는 방법에 대 한 보다 복잡 한 예제를 소개 합니다.

- [ListView 파트 및 기능](~/android/user-interface/layouts/list-view/parts-and-functionality.md)
- [데이터를 사용 하 여 ListView 채우기](~/android/user-interface/layouts/list-view/populating.md)
- [ListView 모양 사용자 지정](~/android/user-interface/layouts/list-view/customizing-appearance.md)
- [CursorAdapters 사용](~/android/user-interface/layouts/list-view/cursor-adapters.md)
- [ContentProvider 사용](~/android/user-interface/layouts/list-view/content-provider.md)
- [ListView 및 작업 수명 주기](~/android/user-interface/layouts/list-view/activity-lifecycle.md)

## <a name="summary"></a>요약

이 항목 집합에서는 `ListView` 의 기본 제공 기능을 사용 하는 방법에 대 한 몇 가지 예제를 소개 하 고 제공 `ListActivity` 했습니다. 또한 `ListView` 다채로운 레이아웃 및 SQLite 데이터베이스 사용이 허용 되는의 사용자 지정 구현에 대해 설명 하 고, 구현에 대 한 작업 수명 주기의 관련성을 간략하게 설명 합니다 `ListView` .

## <a name="related-links"></a>관련 링크

- [AccessoryViews (샘플)](/samples/xamarin/monodroid-samples/accessoryviews)
- [BasicTableAndroid (샘플)](/samples/xamarin/monodroid-samples/basictableandroid)
- [BasicTableAdapter (샘플)](/samples/xamarin/monodroid-samples/basictableadapter)
- [BuiltInViews (샘플)](/samples/xamarin/monodroid-samples/builtinviews)
- [CustomRowView (샘플)](/samples/xamarin/monodroid-samples/customrowview)
- [FastScroll (샘플)](/samples/xamarin/monodroid-samples/fastscroll)
- [섹션 인덱스 (샘플)](/samples/xamarin/monodroid-samples/sectionindex)
- [SimpleCursorTableAdapter (샘플)](/samples/xamarin/monodroid-samples/simplecursortableadapter)
- [CursorTableAdapter (샘플)](/samples/xamarin/monodroid-samples/cursortableadapter)
- [활동 수명 주기 자습서](~/android/app-fundamentals/activity-lifecycle/index.md)
- [테이블 및 셀 작업 (Xamarin.ios)](~/ios/user-interface/controls/tables/index.md)
- [ListView 클래스 참조](xref:Android.Widget.ListView)
- [ListActivity 클래스 참조](xref:Android.App.ListActivity)
- [BaseAdapter 클래스 참조](xref:Android.Widget.BaseAdapter)
- [ArrayAdapter 클래스 참조](xref:Android.Widget.ArrayAdapter)
- [CursorAdapter 클래스 참조](xref:Android.Widget.CursorAdapter)
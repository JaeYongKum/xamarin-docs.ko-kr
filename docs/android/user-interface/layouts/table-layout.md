---
title: Xamarin Android TableLayout
ms.prod: xamarin
ms.assetid: 0C7B9C95-5E5F-A069-BA37-984E49F7DCAD
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 10/08/2020
ms.openlocfilehash: e33dbae13dc9b7af7649777f16bf5d23e11209ad
ms.sourcegitcommit: 124d845f8d2768353e8b7fe1ab1d959a589367f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91872266"
---
# <a name="xamarinandroid-tablelayout"></a>Xamarin Android TableLayout

[`TableLayout`](xref:Android.Widget.TableLayout) 는입니다. [`ViewGroup`](xref:Android.Views.ViewGroup)
자식을 표시 합니다. [`View`](xref:Android.Views.View)
행 및 열의 요소

**HelloTableLayout**라는 새 프로젝트를 시작 합니다.

**리소스/레이아웃/content_main.xml** 파일을 열고 다음을 삽입 합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:stretchColumns="1">

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_column="1"
            android:text="Open..."
            android:padding="3dip"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Ctrl-O"
            android:gravity="right"
            android:padding="3dip"/>
    </TableRow>

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_column="1"
            android:text="Save..."
            android:padding="3dip"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Ctrl-S"
            android:gravity="right"
            android:padding="3dip"/>
    </TableRow>

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_column="1"
            android:text="Save As..."
            android:padding="3dip"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Ctrl-Shift-S"
            android:gravity="right"
            android:padding="3dip"/>
    </TableRow>

    <View
        android:layout_width="wrap_content"
        android:layout_height="2dip"
        android:background="#FF909090"/>

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="X"
            android:padding="3dip"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Import..."
            android:padding="3dip"/>
    </TableRow>

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="X"
            android:padding="3dip"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Export..."
            android:padding="3dip"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Ctrl-E"
            android:gravity="right"
            android:padding="3dip"/>
    </TableRow>

    <View
        android:layout_width="wrap_content"
        android:layout_height="2dip"
        android:background="#FF909090"/>

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_column="1"
            android:text="Quit"
            android:padding="3dip"/>
    </TableRow>
</TableLayout>
```

이것은 HTML 테이블의 구조와 유사 합니다. [`TableLayout`](xref:Android.Widget.TableLayout)
요소가 HTML 요소와 유사 합니다 `<table>` . [`TableRow`](xref:Android.Widget.TableRow)
는 요소와 유사 `<tr>` 하지만 셀의 경우 모든 종류의 요소를 사용할 수 있습니다 [`View`](xref:Android.Views.View) . 이 예제에서는 [`TextView`](xref:Android.Widget.TextView)
각 셀에 사용 됩니다. 일부 행 사이에는 [`View`](xref:Android.Views.View) 가로 선을 그리는 데 사용 되는 기본도 있습니다.

**HelloTableLayout** 활동이 다음에서이 레이아웃을 로드 하는지 확인 합니다.[`OnCreate()`](xref:Android.App.Activity.OnCreate*)
방법이

```csharp
protected override void OnCreate (Bundle savedInstanceState)
{
    base.OnCreate (savedInstanceState);
    SetContentView (Resource.Layout.Main);
}
```

[`SetContentView(int)`](xref:Android.App.Activity.SetContentView*)) 메서드는 리소스 ID로 지정 된에 대 한 레이아웃 파일을 로드 하 고 리소스 [`Activity`](xref:Android.App.Activity) &mdash; `Resource.Layout.Main` **/레이아웃/기본. axml** 레이아웃 파일을 참조 합니다.

애플리케이션을 실행합니다. 다음이 표시되어야 합니다.

[![여러 테이블 행을 표시 하는 TableLayout 앱의 예제 스크린샷](table-layout-images/helloviews3.png)](table-layout-images/helloviews3.png#lightbox)

## <a name="references"></a>참조

- [`TableLayout`](xref:Android.Widget.TableLayout)
- [`TableRow`](xref:Android.Widget.TableRow)
- [`TextView`](xref:Android.Widget.TextView)

_이 페이지의 일부는 Android 오픈 소스 프로젝트에서 만들고 공유 하 고 [Creative Commons 2.5 특성 라이선스](https://creativecommons.org/licenses/by/2.5/)에 설명 된 용어에 따라 사용 되는 작업을 기반으로 수정 됩니다._

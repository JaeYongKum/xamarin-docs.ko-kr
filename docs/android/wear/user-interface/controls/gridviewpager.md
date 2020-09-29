---
title: GridViewPager
ms.prod: xamarin
ms.assetid: A1CDD5F0-049B-4DFA-A268-8A875D26A675
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 02/02/2018
ms.openlocfilehash: 9c80535dfddd2a279fac66ab159c2a600681bb71
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91457005"
---
# <a name="gridviewpager"></a>GridViewPager

[GridViewPager](/samples/xamarin/monodroid-samples/wear-gridviewpager) 샘플에서는 Android 마모를 위한 2d 선택기 탐색 패턴을 구현 하는 방법을 보여 줍니다.

![사각형 표시에 대 한 GridViewPager의 예제 스크린샷](gridviewpager-images/gridviewpager.png)

먼저 [Xamarin Android 마모 지원](https://www.nuget.org/packages/Xamarin.Android.Wear/) NuGet 패키지를 프로젝트에 추가 합니다.

레이아웃 XML은 다음과 같습니다.

```xml
<android.support.wearable.view.GridViewPager xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/pager"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:keepScreenOn="true" />
```

만들기 [`GridPagerAdapter`](https://developer.android.com/reference/android/support/wearable/view/GridPagerAdapter.html)
(또는와 같은 서브 클래스 [`FragmentGridPagerAdapter`](https://developer.android.com/reference/android/support/wearable/view/FragmentGridPagerAdapter.html)
사용자가 탐색할 때 표시할 보기를 제공 합니다.

[샘플 어댑터](https://github.com/xamarin/monodroid-samples/blob/master/wear/GridViewPager/GridViewPager/SimpleGridPagerAdapter.cs) 는 `RowCount` ,, `GetColumnCount` `GetBackground` 및에 대 한 재정의를 비롯 하 여 필요한 메서드를 구현 하는 방법을 보여 줍니다.`GetFragment`

다음과 같이 어댑터를 연결 합니다.

```csharp
pager.Adapter = new SimpleGridPagerAdapter (this, FragmentManager);
```

## <a name="related-links"></a>관련 링크

- [Google의 2D 선택 문서](https://developer.android.com/training/wearables/ui/2d-picker.html)
- [wearable 문서](https://developer.android.com/reference/android/support/wearable/view/package-summary.html)
- [GridViewPager (샘플)](/samples/xamarin/monodroid-samples/wear-gridviewpager)
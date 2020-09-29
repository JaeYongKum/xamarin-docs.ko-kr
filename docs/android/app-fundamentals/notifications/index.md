---
title: Xamarin.Android의 알림
ms.prod: xamarin
ms.assetid: 2E54F1D0-45F4-43A7-B3A3-4F483B7150CB
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 03/01/2018
ms.openlocfilehash: ce19a286a288846a67b73e77d31a5da4c77a2462
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91455588"
---
# <a name="notifications-in-xamarinandroid"></a>Xamarin.Android의 알림

이 섹션에서는 Xamarin.ios에서 알림을 구현 하는 방법을 설명 합니다. Android 알림의 다양 한 UI 요소에 대해 설명 하 고 알림을 만들고 표시 하는 것과 관련 된 API에 대해 설명 합니다.

## <a name="local-notifications-in-android"></a>[Android의 로컬 알림](local-notifications.md)

이 섹션에서는 Xamarin.ios에서 로컬 알림을 구현 하는 방법을 설명 합니다. Android 알림의 다양 한 UI 요소를 설명 하 고 알림을 만들고 표시 하는 데 사용 되는 Api에 대해 설명 합니다.

## <a name="walkthrough---using-local-notifications-in-xamarinandroid"></a>[연습-Xamarin.ios에서 로컬 알림 사용](local-notifications-walkthrough.md)  

이 연습에서는 Xamarin Android 응용 프로그램에서 로컬 알림을 사용 하는 방법을 설명 합니다. 알림을 만들고 게시 하는 기본 사항을 보여 줍니다. 사용자가 알림 서랍에서 알림을 클릭 하면 두 번째 작업을 시작 합니다. 

## <a name="further-reading"></a>추가 정보

[Firebase 클라우드 메시징](~/android/data-cloud/google-messaging/firebase-cloud-messaging.md) &ndash; FCM (Firebase Cloud Messaging)는 모바일 앱과 서버 응용 프로그램 간의 메시징을 용이 하 게 하는 서비스입니다. Firebase 클라우드 메시징은 Xamarin Android 응용 프로그램에서 원격 알림 (푸시 알림)을 구현 하는 데 사용할 수 있습니다.

[알림](https://developer.android.com/guide/topics/ui/notifiers/notifications.html) &ndash; Android 개발자 항목은 Android 알림에 대 한 결정적인 가이드입니다. 이 섹션에는 Android 사용자 인터페이스의 지침을 준수 하도록 알림을 디자인 하는 데 도움이 되는 디자인 고려 사항이 포함 되어 있습니다. 활동을 시작할 때 탐색 유지에 대 한 자세한 배경 정보를 제공 하 고, 알림에 진행률을 표시 하 고 잠금 화면에서 미디어 재생을 제어 하는 방법을 설명 합니다.

[NotificationListenerService](xref:Android.Service.Notification.NotificationListenerService) &ndash; 이 Android 서비스를 사용 하면 앱이 수신 하도록 등록 된 알림 뿐만 아니라 Android 장치에 게시 된 모든 알림을 앱에서 수신 하 고 상호 작용할 수 있습니다.
사용자는 장치에서 알림을 수신할 수 있도록 앱에 대 한 권한을 명시적으로 부여 해야 합니다.

## <a name="related-links"></a>관련 링크

- [로컬 알림 (샘플)](/samples/xamarin/monodroid-samples/localnotifications)
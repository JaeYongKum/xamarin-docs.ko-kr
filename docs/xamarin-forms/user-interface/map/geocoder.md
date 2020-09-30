---
title: Xamarin.Forms 지도 지 오 코딩
description: 이 문서에서는를 사용 하 여 geocode 및 역방향 geocode 맵 데이터를 사용 하는 방법을 설명 합니다 Xamarin.Forms . Maps Geocoder 클래스입니다.
ms.prod: xamarin
ms.assetid: DE7DB31A-8921-4614-8B49-DAEF1E7B03B3
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/22/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: d6a63e952d7466dc4b7f2d3e8cfc39d6c63e4daf
ms.sourcegitcommit: 122b8ba3dcf4bc59368a16c44e71846b11c136c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91559976"
---
# <a name="no-locxamarinforms-map-geocoding"></a>Xamarin.Forms 지도 지 오 코딩

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithmaps)

[`Xamarin.Forms.Maps`](xref:Xamarin.Forms.Maps)네임 스페이스는 [`Geocoder`](xref:Xamarin.Forms.Maps.Geocoder) 개체에 저장 되는 문자열 주소와 위도 및 경도 좌표 간을 변환 하는 클래스를 제공 합니다 [`Position`](xref:Xamarin.Forms.Maps.Position) . 구조체에 대 한 자세한 내용은 [`Position`](xref:Xamarin.Forms.Maps.Position) [지도 위치 및 거리](position-distance.md)를 참조 하세요.

> [!NOTE]
> 대체 지 오 코딩 API는 사용할에 Xamarin.Essentials 있습니다. Xamarin.Essentials `Geocoding` Api는 지 오 코딩 때이 api에서 반환 된 문자열과는 달리 구조화 된 주소 데이터를 제공 합니다. 자세한 내용은 [ Xamarin.Essentials 지 오 코딩](~/essentials/geocoding.md)를 참조 하세요.

## <a name="geocode-an-address"></a>Geocode 주소

주소는 인스턴스를 만들고 [`Geocoder`](xref:Xamarin.Forms.Maps.Geocoder) 인스턴스에서 메서드를 호출 하 여 위도 및 경도 좌표에 대 한 지 오 코딩 될 수 있습니다 [`GetPositionsForAddressAsync`](xref:Xamarin.Forms.Maps.Geocoder.GetPositionsForAddressAsync*) `Geocoder` .

```csharp
using Xamarin.Forms.Maps;
// ...
Geocoder geoCoder = new Geocoder();

IEnumerable<Position> approximateLocations = await geoCoder.GetPositionsForAddressAsync("Pacific Ave, San Francisco, California");
Position position = approximateLocations.FirstOrDefault();
string coordinates = $"{position.Latitude}, {position.Longitude}";
```

[`GetPositionsForAddressAsync`](xref:Xamarin.Forms.Maps.Geocoder.GetPositionsForAddressAsync*)메서드는 주소를 나타내는 인수를 사용 하 `string` 고 주소를 [`Position`](xref:Xamarin.Forms.Maps.Position) 나타낼 수 있는 개체의 컬렉션을 비동기적으로 반환 합니다.

## <a name="reverse-geocode-an-address"></a>역방향 geocode 주소

위도 및 경도 좌표는 인스턴스를 만들고 [`Geocoder`](xref:Xamarin.Forms.Maps.Geocoder) 인스턴스에서 메서드를 호출 하 여 주소에 역방향 지 오 코딩 될 수 있습니다 [`GetAddressesForPositionAsync`](xref:Xamarin.Forms.Maps.Geocoder.GetAddressesForPositionAsync*) `Geocoder` .

```csharp
using Xamarin.Forms.Maps;
// ...
Geocoder geoCoder = new Geocoder();

Position position = new Position(37.8044866, -122.4324132);
IEnumerable<string> possibleAddresses = await geoCoder.GetAddressesForPositionAsync(position);
string address = possibleAddresses.FirstOrDefault();
```

[`GetAddressesForPositionAsync`](xref:Xamarin.Forms.Maps.Geocoder.GetAddressesForPositionAsync*)메서드는 [`Position`](xref:Xamarin.Forms.Maps.Position) 위도 및 경도 좌표로 구성 된 인수를 사용 하 고, 위치 근처의 주소를 나타내는 문자열의 컬렉션을 비동기적으로 반환 합니다.

## <a name="related-links"></a>관련 링크

- [Maps 샘플](/samples/xamarin/xamarin-forms-samples/workingwithmaps)
- [Xamarin.Forms 지도 위치 및 거리](position-distance.md)
- [Geocoder API](xref:Xamarin.Forms.Maps.Geocoder)
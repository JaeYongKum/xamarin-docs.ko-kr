---
title: XAML 미리 보기에서 디자인 타임 데이터 사용
description: 이 문서에서는 디자인 타임 데이터를 사용 하 여 응용 프로그램을 실행 하지 않고 XAML 미리 보기에서 데이터를 많이 사용 하는 레이아웃을 표시 하는 방법을 설명 합니다.
ms.prod: xamarin
ms.assetid: 0F608019-5951-4BE6-80E0-9EEE1733D642
ms.technology: xamarin-forms
author: maddyleger1
ms.author: maleger
ms.date: 03/27/2019
no-loc:
- Xamarin.Forms
- Xamarin.Essentials
ms.openlocfilehash: 4221cd313ca8fbc3f3f9f886e3bd3f774c7472f7
ms.sourcegitcommit: 27f33b0a83b9dc871ad9fb207a1c9960ef197d9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91897949"
---
# <a name="use-design-time-data-with-the-xaml-previewer"></a>XAML 미리 보기에서 디자인 타임 데이터 사용

_일부 레이아웃은 데이터 없이 시각화 하기가 어렵습니다. 이러한 팁을 사용 하 여 XAML 미리 보기에서 데이터를 많이 사용 하는 페이지의 미리 보기를 최대한 활용할 수 있습니다._

> [!NOTE]
> Windows Presentation Foundation (WPF) 또는 UWP를 사용 하는 경우 [데스크톱 응용 프로그램용 XAML 디자이너에서 디자인 타임 데이터 사용](/visualstudio/xaml-tools/xaml-designtime-data) 을 참조 하세요.

## <a name="design-time-data-basics"></a>디자인 타임 데이터 기본 사항

디자인 타임 데이터는 XAML 미리 보기에서 컨트롤을 더 쉽게 시각화할 수 있도록 설정 하는 가짜 데이터입니다. 시작 하려면 XAML 페이지의 헤더에 다음 코드 줄을 추가 합니다.

```xaml
xmlns:d="http://xamarin.com/schemas/2014/forms/design"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

네임 스페이스를 추가한 후에는 `d:` 특성 또는 컨트롤 앞에 배치 하 여 XAML 미리 보기에 표시할 수 있습니다. 가 있는 요소는 `d:` 런타임에 표시 되지 않습니다.

예를 들어 일반적으로 데이터가 바인딩된 레이블에 텍스트를 추가할 수 있습니다.

```xaml
<Label Text="{Binding Name}" d:Text="Name!" />
```

[![레이블에 텍스트를 사용 하 여 시간 데이터 디자인](xaml-previewer-images/designtimedata-label-sm.png "텍스트를 사용 하 여 시간 데이터 디자인")](xaml-previewer-images/designtimedata-label-lg.png#lightbox)

이 예제에서를 사용 하지 않으면 `d:Text` XAML 미리 보기에서 레이블에 아무것도 표시 되지 않습니다. 대신 “Name!”이 표시됩니다. 여기서 레이블에는 런타임에 실제 데이터가 포함 됩니다.

`d:` Xamarin.Forms 색, 글꼴 크기 및 간격과 같은 컨트롤의 특성과 함께를 사용할 수 있습니다. 컨트롤 자체에 추가할 수도 있습니다.

```xaml
<d:Button Text="Design Time Button" />
```

[![단추 컨트롤을 사용 하 여 시간 데이터 디자인](xaml-previewer-images/designtimedata-controls-sm.png "단추 컨트롤을 사용 하 여 시간 데이터 디자인")](xaml-previewer-images/designtimedata-controls-lg.png#lightbox)

이 예제에서 단추는 디자인 타임에만 표시됩니다. 이 메서드를 사용 하 여 [XAML 미리 보기에서 지원 되지 않는 사용자 지정 컨트롤](render-custom-controls.md)에 대 한 자리 표시자를에 삽입할 수 있습니다.

## <a name="preview-images-at-design-time"></a>디자인 타임의 미리 보기 이미지

페이지에 바인딩되거나 동적으로 로드 되는 이미지에 대 한 디자인 타임 소스를 설정할 수 있습니다. Android 프로젝트에서 XAML 미리 보기에 표시 하려는 이미지를 **> 그릴** 수 있는 폴더에 리소스를 추가 합니다. IOS 프로젝트에서 **리소스** 폴더에 이미지를 추가 합니다. 그런 다음 디자인 타임에 XAML 미리 보기에 해당 이미지를 표시할 수 있습니다.

```xaml
<Image Source={Binding ProfilePicture} d:Source="DesignTimePicture.jpg" />
```

[![이미지를 사용 하 여 시간 데이터 디자인](xaml-previewer-images/designtimedata-image-sm.png "Iamges를 사용 하 여 디자인 타임 데이터")](xaml-previewer-images/designtimedata-image-lg.png#lightbox)

## <a name="design-time-data-for-listviews"></a>Listview에 대 한 디자인 타임 데이터

Listview은 모바일 앱에 데이터를 표시 하는 인기 있는 방법입니다. 그러나 실제 데이터 없이 시각화 하기가 어렵습니다. 디자인 타임 데이터를 사용 하려면 System.windows.controls.itemscontrol.itemssource으로 사용할 디자인 타임 배열을 만들어야 합니다. XAML 미리 보기는 디자인 타임에 ListView의 해당 배열에 있는 항목을 표시 합니다.

```xaml
<StackLayout>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type x:String}">
                <x:String>Item One</x:String>
                <x:String>Item Two</x:String>
                <x:String>Item Three</x:String>
            </x:Array>
        </d:ListView.ItemsSource>
        <ListView.ItemTemplate>
            <DataTemplate>
                <TextCell Text="{Binding ItemName}"
                          d:Text="{Binding .}" />
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</StackLayout>
```

[![ListView를 사용 하 여 디자인 타임 데이터](xaml-previewer-images/designtimedata-itemssource-sm.png "ListView를 사용 하 여 디자인 타임 데이터")](xaml-previewer-images/designtimedata-itemssource-lg.png#lightbox)

이 예제에서는 XAML 미리 보기에서 3 개의 TextCells의 ListView를 표시 합니다. `x:String`프로젝트의 기존 데이터 모델로 변경할 수 있습니다.

데이터 개체의 배열을 만들 수도 있습니다. 예를 들어 데이터 개체의 공용 속성을 `Monkey` 디자인 타임 데이터로 생성할 수 있습니다.

```csharp
namespace Monkeys.Models
{
    public class Monkey
    {
        public string Name { get; set; }
        public string Location { get; set; }
    }
}
```

XAML에서 클래스를 사용 하려면 루트 노드의 네임 스페이스를 가져와야 합니다.

```xaml
xmlns:models="clr-namespace:Monkeys.Models"
```

```xaml
<StackLayout>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type models:Monkey}">
                <models:Monkey Name="Baboon" Location="Africa and Asia"/>
                <models:Monkey Name="Capuchin Monkey" Location="Central and South America"/>
                <models:Monkey Name="Blue Monkey" Location="Central and East Africa"/>
            </x:Array>
        </d:ListView.ItemsSource>
        <ListView.ItemTemplate>
            <DataTemplate x:DataType="models:Monkey">
                <TextCell Text="{Binding Name}"
                          Detail="{Binding Location}" />
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</StackLayout>
```

여기서는 사용 하려는 실제 모델에 바인딩할 수 있다는 이점도 있습니다.

## <a name="alternative-hardcode-a-static-viewmodel"></a>대안: 정적 ViewModel 하드 코딩

디자인 타임 데이터를 개별 컨트롤에 추가 하지 않으려는 경우에는 해당 페이지에 바인딩할 모의 데이터 저장소를 설정할 수 있습니다. [디자인 타임 데이터 추가에 대 한](https://montemagno.com/xamarin-forms-design-time-data-tips-best-practices/) James Montemagno의 블로그 게시물을 참조 하 여 XAML에서 정적 ViewModel에 바인딩하는 방법을 확인 하세요.

## <a name="troubleshooting"></a>문제 해결

### <a name="requirements"></a>요구 사항

디자인 타임 데이터에는 최소 3.6 버전이 필요 Xamarin.Forms 합니다.

### <a name="intellisense-shows-squiggly-lines-under-my-design-time-data"></a>IntelliSense가 디자인 타임 데이터 아래에 물결 모양의 선을 표시 합니다.

이것은 알려진 문제 이며 Visual Studio의 향후 버전에서 수정 될 예정입니다. 프로젝트는 여전히 오류 없이 빌드됩니다.

### <a name="the-xaml-previewer-stopped-working"></a>XAML 미리 보기의 작동이 중지 되었습니다.

XAML 파일을 닫았다가 다시 열어 프로젝트를 정리하고 다시 빌드해 보세요.

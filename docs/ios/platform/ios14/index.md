---
title: IOS 14 소개
description: '이 문서에서는 Xamarin이 c # 바인딩을 제공 하는 일부 iOS 14 Api에 대 한 개략적인 설명을 제공 합니다.'
ms.prod: xamarin
ms.assetid: 4953216e-472b-4484-9c1e-7263ac537f21
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 09/17/2020
ms.openlocfilehash: e9793617c76813fb68a57213edd8b48529f19ac7
ms.sourcegitcommit: 0c45e3f810947e3d43223aa01bf3e43a0defca65
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90843614"
---
# <a name="introduction-to-ios-14"></a>IOS 14 소개

다음 [지침](~/ios/platform/ios14/get-started.md) 에 따라 시작 하세요.

## <a name="new-control-uicolorwell"></a>새 컨트롤: UIColorWell

[`UIColorWell`](https://developer.apple.com/documentation/uikit/uicolorwell) 는 선택한 견본에서 색을 선택 하거나, 스 포 이트를 사용 하거나, 수동으로 값을 입력 하는 새로운 UIKit 컨트롤입니다. 컨트롤은 탭 할 때 모달 폼을 시작 하는 원형 색 단추를 표시 합니다.

![UIColorWell](ios14-images/colorwell.png)

```xaml
<ios:UIColorWell
    SelectedColor="{x:Static ios:UIColor.Red}"
    ValueChanged="OnColorChanged" />
```

```csharp
private void OnColorChanged(object sender, EventArgs e)
{
    var colorWell = (UIColorWell)sender; 
    Debug.WriteLine(colorWell.SelectedColor);
}
```

## <a name="modified-controls"></a>수정 된 컨트롤

여러 컨트롤이 업데이트를 수신 했습니다. 특히 다음과 같은 경우가 있습니다.

- 이제 [Ui바 Buttonitem](https://developer.apple.com/documentation/uikit/uibarbuttonitem) 은 팝 오버으로 표시 되는 UIMenu를 추가할 수 있습니다.
- 이제 [UIDatePicker](https://developer.apple.com/documentation/uikit/uidatepicker) 는 자동 (기본값), Compact, 인라인 및 휠의 여러 스타일을 지원 합니다.
- [Uisplitviewcontroller](https://developer.apple.com/documentation/uikit/uisplitviewcontroller) 는 이제 기본, 보조 및 보조 라는 세 개의 열을 지원 합니다.
 
![시험판 API](~/media/shared/preview.png)

## <a name="embedded-widgetkit-support"></a>포함 된 WidgetKit 지원

이 버전의 SDK는 Swift에서 작성 된 WidgetKit 확장을 기본 Xamarin.ios 응용 프로그램에 포함 하기 위한 지원을 추가 합니다. 이를 통해 오늘 Widget 지원으로 앱을 빌드할 수 있습니다.

이 방법을 사용 하 여 "하이브리드" 응용 프로그램을 만들고 SwiftUI를 사용 하 여 위젯 확장을 빌드하고 Xamarin.ios 응용 프로그램에 포함 합니다.

WidgetKit 지원을 활용 하려면 프로젝트 파일을 수동으로 변경 해야 합니다.

프로젝트에 다음과 같은 섹션을 추가 합니다.

```xml
<AdditionalAppExtensions Include="$(MSBuildProjectDirectory)/../../native">
     <Name>NativeTodayExtension</Name>
     <BuildOutput Condition="'$(Platform)' == 'iPhone'">build/Debug-iphoneos</BuildOutput>
     <BuildOutput Condition="'$(Platform)' == 'iPhoneSimulator'">build/Debug-iphonesimulator</BuildOutput>
</AdditionalAppExtensions>
```

Swift UI 확장의 빌드 디렉터리를 가리키도록 첫 번째 링크에 포함 된 경로를 변경 합니다.

Xcode 프로젝트에서 프로젝트의 상대적인 출력 위치 (파일 → 프로젝트 설정)를 사용 하도록 설정 하 여 쉽게 찾을 수 있는 경로를 사용 하는 것이 유용할 수 있습니다.

![Xcode 설정](ios14-images/xcode-settings.png)

이 [샘플 응용 프로그램](https://github.com/chamons/xamarin-ios-swift-extension/blob/master/App/TestApplication/TestApplication.csproj#L143) 에서는 JSON serialization을 사용 하 여 xamarin.ios 앱에서 샘플 위젯을 표시 하기 위해 데이터를 전송 합니다.

[여기에서 사용자 의견](https://github.com/xamarin/xamarin-macios/issues/8933)을 제공 하기 위해 WidgetKit에 관심이 있습니다.

## <a name="related-links"></a>관련 링크

- [Xamarin.ios 14 릴리스 정보](/xamarin/ios/release-notes/14/14.0)
- [UIColorWell 설명서](https://developer.apple.com/documentation/uikit/uicolorwell)

---
title: 1 부입니다. XAML을 사용 하 여 시작
description: Xamarin.Forms 응용 프로그램에서 XAML은 주로 페이지의 시각적 내용 및 코드 숨김 파일과 함께하는 작업을 정의할 때 사용합니다.
ms.prod: xamarin
ms.assetid: 9073FA0E-BD5A-4492-8A93-54C466F6EDB9
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/10/2018
ms.openlocfilehash: 32f809c5b21e56497328ce00bf49a7337ac0270a
ms.sourcegitcommit: 699de58432b7da300ddc2c85842e5d9e129b0dc5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71250036"
---
# <a name="part-1-getting-started-with-xaml"></a>1 부입니다. XAML을 사용 하 여 시작

[![샘플 다운로드](~/media/shared/download.png) 샘플 다운로드](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/xamlsamples)

_Xamarin.Forms 응용 프로그램에서 XAML 페이지의 시각적 콘텐츠를 정의 하는 대부분 및 함께 작동 하는 C# 코드 숨김 파일입니다._

코드 숨김 파일 태그 코드 지원을 제공합니다. 함께이 두 파일 속성 초기화 및 자식 뷰를 포함 하는 새 클래스 정의에 영향을 줍니다. XAML 파일에서 XML 요소 및 특성을 사용 하 여 클래스 및 속성 참조 및 태그와 코드 간 연결이 설정 됩니다.

## <a name="creating-the-solution"></a>솔루션 만들기

첫 번째 XAML 파일 편집을 시작하려면 Visual Studio 또는 Mac용 Visual Studio를 사용하여 새 Xamarin.Forms 솔루션을 만듭니다. (사용자 환경에 해당하는 아래에 있는 탭을 선택합니다.)

<!-- markdownlint-disable MD001 -->

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

Windows에서는 Visual Studio를 사용하여 메뉴에서  **파일 > 새로 만들기 > 프로젝트** 를 선택합니다. **새 프로젝트** 대화 상자에서 왼쪽에 있는 **Visual C# > Cross-Platform** 을 선택한 다음 가운데 있는 목록에서  **모바일 앱(Xamarin.Forms)** 을 선택합니다.

![새 프로젝트 대화 상자](get-started-with-xaml-images/win/newprojectdialog.w157.png)

솔루션에 대 한 위치를 선택의 이름을 지정 **XamlSamples** (또는 원하는) 키를 누릅니다 **확인**합니다.

다음 화면에서 선택 합니다 **비어 있는 앱** 템플릿 및 **.NET 표준** 코드 공유 전략:

![새 응용 프로그램 대화 상자](get-started-with-xaml-images/win/newcrossplatformapp.png)

**확인**을 누릅니다.

솔루션에 다음과 같은 4개의 프로젝트가 생성됩니다. **XamlSamples** .NET Standard 라이브러리 **XamlSamples.Android**, **XamlSamples.iOS**, 및 UWP(Universal Windows Platform) 솔루션  **XamlSamples.UWP**.

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

Mac용 Visual Studio에서 **파일 > 새 솔루션** 을 선택합니다. **새 프로젝트**  대화 상자에서 왼쪽의 **다중 플랫폼 > 앱** 및 템플릿 목록에서 **빈 Forms 앱** (*Forms 앱*이 **아님** ) 을 선택합니다.

![새 프로젝트 대화 상자 1](get-started-with-xaml-images/mac/newprojectdialog1.png)

키를 눌러 **다음**합니다.

다음 대화 상자에서 프로젝트에 이름을입니다 **XamlSamples** (또는 원하는). 있는지 확인 합니다 **사용 하 여.NET Standard** 라디오 단추가 선택:

![새 프로젝트 대화 상자 2](get-started-with-xaml-images/mac/newprojectdialog2.png)

키를 눌러 **다음**합니다.

다음 대화 상자에서 프로젝트의 위치를 선택할 수 있습니다.

![새 프로젝트 대화 상자 3](get-started-with-xaml-images/mac/newprojectdialog3.png)

키를 눌러 **만들기**

다음과 같은 세 개의 프로젝트가 솔루션에 생성됩니다. **XamlSamples** .NET Standard 라이브러리 **XamlSamples.Android**, **XamlSamples.iOS**.

-----

만든 후 합니다 **XamlSamples** 솔루션을 다양 한 플랫폼 프로젝트를 솔루션 시작 프로젝트로 선택 하 여 개발 환경을 테스트 하려는 및 빌드 및 간단한 응용 프로그램을 배포 하 여 생성 phone 에뮬레이터 또는 실제 장치에서 사용 되는 프로젝트 템플릿.

공유 플랫폼 특정 코드를 작성할 필요가 없으면 **XamlSamples** .NET Standard 라이브러리 프로젝트는 여기서을 보내는 거의 모든 시간을 프로그래밍 합니다. 이러한 문서는 해당 프로젝트 외부에서 뛰어들 없습니다.

### <a name="anatomy-of-a-xaml-file"></a>XAML 파일의 분석

내 합니다 **XamlSamples** .NET Standard 라이브러리는 다음과 같은 이름으로 파일 쌍:

- **App.xaml**, XAML 파일 및
- **App.xaml.cs**, C# *코드 숨김* XAML 파일과 연결 된 파일입니다.

다음 화살표를 클릭 해야 **App.xaml** 코드 숨김 파일을 확인 합니다.

**App.xaml** 및 **App.xaml.cs** 모두 `Application`에서 파생된 `App`이라는 클래스와 관련됩니다. XAML 파일과 함께 있는 대부분의 다른 클래스는  `ContentPage`에서 파생된 클래스와 관련됩니다. 해당 파일들은 전체 페이지의 시각적 내용을 정의하기 위해 XAML을 사용합니다. 다음은 **XamlSamples** 프로젝트에 있는 실제적으로 다른 두 파일입니다.

- **MainPage.xaml**, XAML 파일 및
- **MainPage.xaml.cs**, C# 코드 숨김 파일입니다.

합니다 **MainPage.xaml** (하지만 서식을 약간 다를 수 있습니다) 파일은 다음과 같습니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:XamlSamples"
             x:Class="XamlSamples.MainPage">

    <StackLayout>
        <!-- Place new controls here -->
        <Label Text="Welcome to Xamarin Forms!"
               VerticalOptions="Center"
               HorizontalOptions="Center" />
    </StackLayout>

</ContentPage>
```

두 XML 네임 스페이스 (`xmlns`) 선언은 uri를 참조 하 고, 첫 번째는 Xamarin의 웹 사이트에, 두 번째는 Microsoft의에 있습니다. 궁금증에 해당 Uri 지점을 확인 합니다. 아무 것도 없는 합니다. 이는 Xamarin 및 Microsoft 소유의 URI이고 기본적으로 버전 식별자로 작동합니다.

첫 번째 XML 네임 스페이스 선언 의미 태그 접두사가 없는 XAML 파일에 정의 된 xamarin.forms에 클래스를 예를 들어 참조 `ContentPage`합니다. 접두사를 정의 하는 두 번째 네임 스페이스 선언을 `x`합니다. 이 XAML의 다른 구현에서 자체와 여러 요소 및 XAML에 내장 된 특성에 대 한 지원. 그러나 이러한 특성과 해당 요소는 URI에 포함 된 연도 따라 약간 다릅니다. Xamarin.Forms의 전체가 아니라 2009 XAML 사양을 지원합니다.

`local` 네임 스페이스 선언의 사용 하면.NET Standard 라이브러리 프로젝트에서 다른 클래스에 액세스할 수 있습니다.

첫 번째 태그의 끝에는 `x` 이라는 특성에 대 한 접두사는 `Class`합니다. 때문에이 사용 `x` 와 같은 접두사는 XAML 네임 스페이스를 XAML 특성에 대 한 거의 유니버설 `Class` 거의 항상 라고 `x:Class`합니다.

`x:Class` 특성에는 정규화 된.NET 클래스 이름을 지정 합니다: 합니다 `MainPage` 클래스는 `XamlSamples` 네임 스페이스. 즉,이 XAML 파일은 라는 새 클래스를 정의 하 `MainPage` 에 `XamlSamples` 에서 파생 되는 네임 스페이스 `ContentPage`-는 태그를 `x:Class` 특성이 나타납니다.

합니다 `x:Class` 특성이 파생 된 정의를 XAML 파일의 루트 요소에만 나타날 수 있습니다 C# 클래스입니다. XAML 파일에 정의 된 새 클래스입니다. XAML 파일에 표시 되는 모든 항목 대신 단순히 기존 클래스에서 인스턴스화되고 초기화 합니다.

합니다 **MainPage.xaml.cs** 파일은 다음과 같습니다 (사용 되지 않는 외 `using` 지시문):

```csharp
using Xamarin.Forms;

namespace XamlSamples
{
    public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();
        }
    }
}
```

`MainPage` 클래스에서 파생 되며 `ContentPage`, 그러나는 `partial` 클래스 정의 합니다. 이 제안에 대 한 다른 partial 클래스 정의 되도록 `MainPage`에 있지만? 그건 뭐죠 및 `InitializeComponent` 메서드?

Visual Studio는 프로젝트를 빌드할 때 XAML 파일을 C# 코드 파일로 생성하도록 변환합니다. **XamlSamples\XamlSamples\obj\Debug** 디렉터리를 보면 **XamlSamples.MainPage.xaml.g.cs**라는 파일을 찾을 수 있습니다. 'g'는 생성(generated)을 의미합니다. 이것이 `MainPage` 생성자에서 호출되는 `InitializeComponent` 메서드 정의를 포함하는`MainPage` 의 다른 partial 클래스 정의입니다. 이러한 두 개의 partial `MainPage` 클래스 정의는 함께 컴파일될 수 있습니다. XAML이 컴파일 될지 여부에 따라 XAML 파일 또는 XAML 파일의 이진 형식 중 하나가 실행 파일에 포함됩니다.

런타임 시 특정 플랫폼 프로젝트의 코드는 .NET Standard 라이브러리의 `App` 클래스 인스턴스를 전달하는 `LoadApplication`  메서드를 호출합니다. `App` 클래스 생성자는 `MainPage`를 인스턴스화합니다. `MainPage` 클래스의 생성자는 `InitializeComponent`를 호출하고, 그러면 .NET Standard 라이브러리에서 XAML 파일(또는 해당 컴파일된 이진 파일)을 추출하는`LoadFromXaml` 메서드를 호출합니다. `LoadFromXaml`은 XAML 파일에 정의된 모든 개체를 초기화하고, 부모-자식 관계로 개체를 모두 함께 연결하고, 코드에 정의된 이벤트 처리기를 XAML 파일의 이벤트 설정에 연결하고, 개체의 결과 트리를 페이지의 내용으로 설정합니다.

필요는 없지만 일반적으로 생성 된 코드 파일을 사용 하 여 시간을 투자 하, 경우에 따라 런타임 예외 발생 생성된 된 파일의 코드에서 작업할 수 있도록 합니다.

컴파일 및이 프로그램을 실행 하는 경우는 `Label` 요소는 XAML 알 수 있듯이 페이지의 가운데에 표시 합니다.

[![기본 Xamarin 양식 표시](get-started-with-xaml-images/xamlsamples.png)](get-started-with-xaml-images/xamlsamples-large.png#lightbox)

흥미로운 시각적 개체에 대 한 하기만 하면 더 많은 흥미로운 XAML입니다.

## <a name="adding-new-xaml-pages"></a>새 XAML 페이지 추가

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

프로젝트에 다른 XAML 기반 `ContentPage` 를 추가하려면 **XamlSamples** .NET Standard 라이브러리 프로젝트를 선택하고 **프로젝트 > 새 항목 추가** 메뉴 항목을 실행합니다. **새 항목 추가** 대화 상자에서 왼쪽에 있는 **Visual C#**  및 **Xamarin.Forms**를 선택합니다. 목록에서 **콘텐츠 페이지**(코드 전용 페이지를 생성하는  **콘텐츠 페이지 (C#)** 또는 페이지가 아닌**콘텐츠 뷰**가 아님)를 선택합니다. 페이지 이름을 예를 들어 다음과 같이 **HelloXamlPage.xaml**로 입력합니다.

![새 항목 추가 대화 상자](get-started-with-xaml-images/win/addnewitemdialog.w157.png)

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

프로젝트에 다른 XAML 기반 `ContentPage` 를 추가하려면  **XamlSamples**.NET Standard 라이브러리 프로젝트를 선택하고 **파일 > 새 파일** 메뉴 항목을 실행합니다. **새 파일** 대화 상자에서 왼쪽에 있는 **Forms**및 **Forms ContentPage Xaml**(코드 전용 페이지를 생성하는  **Forms ContentPage**또는 페이지가 아닌 **Contents View**가 아님)을 선택합니다. 페이지 이름을 예를 들어 다음과 같이 **HelloXamlPage**로 입력합니다.

![새 파일 대화 상자](get-started-with-xaml-images/mac/newfiledialog.png)

-----

두 파일을 프로젝트에 추가 됩니다 **HelloXamlPage.xaml** 코드 숨김 파일과 **HelloXamlPage.xaml.cs**합니다.

## <a name="setting-page-content"></a>페이지 콘텐츠를 설정합니다.

편집 된 **HelloXamlPage.xaml** 파일에 태그는 대 `ContentPage` 및 `ContentPage.Content`:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="XamlSamples.HelloXamlPage">
    <ContentPage.Content>

    </ContentPage.Content>
</ContentPage>
```

`ContentPage.Content` 태그는 XAML의 고유한 구문의 일부입니다. 처음에 잘못 된 xml에 표시 될 수 있지만 사용할 합니다. 기간은 XML에 특수 문자가 아닙니다.

합니다 `ContentPage.Content` 태그 라고 *property 요소* 태그입니다. `Content` 속성인 `ContentPage`, 단일 뷰나 자식 뷰를 사용 하 여 레이아웃을 일반적으로 설정 됩니다. 일반적으로 속성 수, XAML의 특성 있지만 설정 하기가 것을 `Content` 복잡 한 개체에 특성입니다. 이런 이유로 속성은 클래스 이름과 마침표로 구분 된 속성 이름으로 이루어진 XML 요소로 표현 됩니다. 이제는 `Content` 간에 속성을 설정할 수는 `ContentPage.Content` 다음과 같은 태그:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="XamlSamples.HelloXamlPage"
             Title="Hello XAML Page">
    <ContentPage.Content>

        <Label Text="Hello, XAML!"
               VerticalOptions="Center"
               HorizontalTextAlignment="Center"
               Rotation="-15"
               IsVisible="true"
               FontSize="Large"
               FontAttributes="Bold"
               TextColor="Blue" />

    </ContentPage.Content>
</ContentPage>
```

또한는 `Title` 루트 태그에 특성 설정 되었습니다.

이 때 클래스, 속성 및 XML 간의 관계는 명확 해야 합니다. Xamarin.ios 클래스 (예: `ContentPage` 또는 `Label`)는 XAML 파일에 XML 요소로 표시 됩니다. `ContentPage` 상의 `Title` 및 `Label`의 7가지 속성을 포함하는 해당 클래스의 속성은 일반적으로 XML 특성으로 표시합니다.

대부분의 바로 가기 이러한 속성의 값을 설정할 수 있습니다. 일부 속성은 기본 데이터 형식입니다. `Title` 예를 들어 및 `String` `IsVisible` 속성은`Double`형식이 고, 는형식이`true` 며, 기본적으로이 고 여기서는 그림에만 설정 됨은 형식입니다. `Rotation` `Text` `Boolean`.

합니다 `HorizontalTextAlignment` 형식의 속성이 `TextAlignment`, 열거형입니다. 모든 열거형 형식의 속성을 제공 하면은 멤버 이름입니다.

그러나 더 복잡 한 형식의 속성에 대 한 변환기는 XAML을 구문 분석에 사용 됩니다. 클래스에서 파생 되는 Xamarin.Forms에 이들은 `TypeConverter`합니다. 공용 클래스 대부분은 되지만 일부 없습니다. 이 특정 XAML 파일에 대해 이러한 클래스의 여러 역할을 백그라운드에서:

- `VerticalOptions` 속성에 대한 `LayoutOptionsConverter`
- `FontSize` 속성에 대한 `FontSizeConverter`
- `TextColor` 속성에 대한 `ColorTypeConverter`

이러한 변환기에 허용 되는 구문의 속성 설정 제어합니다.

`ThicknessTypeConverter` 하나, 둘, 또는 쉼표로 구분 된 4 개의 숫자일 처리할 수 있습니다. 1 개의 숫자를 제공 하면 네 면 모두에 적용 됩니다. 두 숫자를 사용 하 여 첫 번째 왼쪽 및 오른쪽에서 안쪽 여백을 이며 두 번째 위쪽 및 아래쪽 합니다. 4 개의 숫자일 순서 왼쪽, 위쪽, 오른쪽 및 아래쪽에 있습니다.

`LayoutOptionsConverter` 의 공용 정적 필드의 이름으로 변환할 수는 `LayoutOptions` 종류의 값에는 구조 `LayoutOptions`.

`FontSizeConverter` 처리할 수는 `NamedSize` 멤버나 숫자 글꼴 크기입니다.

합니다 `ColorTypeConverter` 의 공용 정적 필드의 이름을 허용 합니다 `Color` 구조 또는 알파 채널이 없이 16 진수 RGB 값 앞에 숫자 기호 (#). 알파 채널이 없는 구문은 다음과 같습니다.

 `TextColor="#rrggbb"`

각 적은 문자를 16 진수입니다. 알파 채널은 포함 하는 방법을 다음과 같습니다.

 `TextColor="#aarrggbb">`

알파 채널의 FF는 완전히 불투명 하 00은 완전히 투명 한 염두에서에 둡니다.

다른 두 가지 형식을 사용 하면 각 채널에 대 한 단일 16 진수만를 지정할 수 있습니다.

 `TextColor="#rgb"` `TextColor="#argb"`

이러한 경우에는 숫자 값을 구성 하도록 반복 됩니다. 예를 들어 #CF3 RGB 색 CC-FF-33 사용 됩니다.

## <a name="page-navigation"></a>페이지 탐색

실행 하는 경우는 **XamlSamples** 프로그램은 `MainPage` 표시 됩니다. 새 보려는 `HelloXamlPage` 으로 새 시작 페이지에 설정 하거나 합니다 **App.xaml.cs** 파일 또는에서 새 페이지로 이동 `MainPage`합니다.

탐색을 구현 하려면 코드에서 먼저 변경를 **App.xaml.cs** 생성자 있도록를 `NavigationPage` 개체가 만들어집니다.

```csharp
public App()
{
    InitializeComponent();
    MainPage = new NavigationPage(new MainPage());
}
```

에 **MainPage.xaml.cs** 생성자는 간단한 만들 수 있습니다 `Button` 이벤트 처리기를 사용 하 여 탐색 및 `HelloXamlPage`:

```csharp
public MainPage()
{
    InitializeComponent();

    Button button = new Button
    {
        Text = "Navigate!",
        HorizontalOptions = LayoutOptions.Center,
        VerticalOptions = LayoutOptions.Center
    };

    button.Clicked += async (sender, args) =>
    {
        await Navigation.PushAsync(new HelloXamlPage());
    };

    Content = button;
}
```

설정 합니다 `Content` 속성 페이지의 대체 설정은 `Content` XAML 파일의 속성입니다. 를 컴파일하고이 프로그램의 새 버전을 배포 하는 경우 단추가 화면에 나타납니다. 이 키를 눌러 이동할 `HelloXamlPage`합니다. IPhone, Android 및 UWP 결과 페이지는 다음과 같습니다.

[![회전 된 레이블 텍스트](get-started-with-xaml-images/helloxaml1.png)](get-started-with-xaml-images/helloxaml1-large.png#lightbox)

iOS에서는 **< 뒤로** 버튼을 사용하고, Android에서는 페이지 상단 또는 폰의 맨 아래에 있는 왼쪽 화살표를 사용하며, Windows 10에서는 페이지의 상단에 있는 왼쪽 화살표를 사용하여 `MainPage`로 다시 이동할 수 있습니다.

렌더링 하는 다양 한 방법에 대 한 XAML을 사용해 자유롭게는 `Label`합니다. 텍스트에 유니코드 문자를 포함 하는 경우 표준 XML 구문을 사용할 수 있습니다. 예를 들어, 인사말 둥근 따옴표에 삽입할 다음을 사용 합니다.

 `<Label Text="&#x201C;Hello, XAML!&#x201D;" … />`

해당 모양은 다음과 같습니다.

[![유니코드 문자를 사용 하 여 회전 된 레이블 텍스트](get-started-with-xaml-images/helloxaml2.png)](get-started-with-xaml-images/helloxaml2-large.png#lightbox)

## <a name="xaml-and-code-interactions"></a>XAML 및 코드 상호 작용

**HelloXamlPage** 샘플은 페이지에 단일 `Label`만 포함했지만 아주 일반적인 것은 아닙니다. 대부분의 `ContentPage` 상속은 `StackLayout`과 같은 일종의 레이아웃으로 `Content` 속성을 설정합니다. `StackLayout`의 `Children` 속성은 `IList<View>` 형식이 되도록 정의되지만 그것은 `ElementCollection<View>` 형식의 실제 개체이며, 해당 컬랙션은 여러 뷰 또는 다른 레이아웃으로 채울 수 있습니다. XAML에서 해당 부모-자식 관계는 일반 XML 계층 구조를 사용하여 설정됩니다. **XamlPlusCodePage**라는 이름의 새 페이지에 대한 XAML 파일은 다음과 같습니다.

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="XamlSamples.XamlPlusCodePage"
             Title="XAML + Code Page">
    <StackLayout>
        <Slider VerticalOptions="CenterAndExpand" />

        <Label Text="A simple Label"
               Font="Large"
               HorizontalOptions="Center"
               VerticalOptions="CenterAndExpand" />

        <Button Text="Click Me!"
                HorizontalOptions="Center"
                VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

이 XAML 파일에는 구문상 완료 되며 다음과 같이 표시 됩니다.

[![페이지의 여러 컨트롤](get-started-with-xaml-images/xamlpluscode1.png)](get-started-with-xaml-images/xamlpluscode1-large.png#lightbox)

그러나이 프로그램이 불완전 한 기능적으로 고려해 야 할 가능성이 있습니다. 아마도 `Slider` 발생 할 합니다 `Label` 현재 값을 표시 및 `Button` 프로그램 내에서 작업을 수행 하려는 것입니다.

[4부. 데이터 바인딩 기본 사항 ](~/xamarin-forms/xaml/xaml-basics/data-binding-basics.md)에서 살펴보겠지만, `Label`을 사용하여 `Slider` 값을 표시하는 작업은 데이터 바인딩을 사용하여 XAML에서 완전히 처리할 수 있습니다. 하지만 코드 솔루션을 먼저 보는 것이 유용 합니다. 그렇더라도 `Button`` 클릭을 처리하는 데는 분명히 코드가 있어야 합니다. 즉, `XamlPlusCodePage`에 대한 코드 숨김 파일에는 `Slider`의 `ValueChanged` 이벤트와 `Button`의 `Clicked` 이벤트를 위한 처리기를 포함되어야 합니다. 다음과 같이 추가해 보겠습니다.

```csharp
namespace XamlSamples
{
    public partial class XamlPlusCodePage
    {
        public XamlPlusCodePage()
        {
            InitializeComponent();
        }

        void OnSliderValueChanged(object sender, ValueChangedEventArgs args)
        {

        }

        void OnButtonClicked(object sender, EventArgs args)
        {

        }
    }
}
```

이러한 이벤트 처리기를 공용 필요가 없습니다.

XAML 파일에서 다시를 `Slider` 하 고 `Button` 태그에 대 한 특성을 포함 해야 합니다 `ValueChanged` 및 `Clicked` 이러한 처리기를 참조 하는 이벤트:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="XamlSamples.XamlPlusCodePage"
             Title="XAML + Code Page">
    <StackLayout>
        <Slider VerticalOptions="CenterAndExpand"
                ValueChanged="OnSliderValueChanged" />

        <Label Text="A simple Label"
               Font="Large"
               HorizontalOptions="Center"
               VerticalOptions="CenterAndExpand" />

        <Button Text="Click Me!"
                HorizontalOptions="Center"
                VerticalOptions="CenterAndExpand"
                Clicked="OnButtonClicked" />
    </StackLayout>
</ContentPage>
```

이벤트 처리기를 할당 구문이 동일한 속성에 값을 할당 하는 것을 알 수 있습니다.

경우에 대 한 처리기를 `ValueChanged` 의 이벤트를 `Slider` 사용 하는 `Label` 현재 값을 표시 하려면 처리기 코드에서 해당 개체를 참조 해야 합니다. 합니다 `Label` 지정 하는 이름이 필요 합니다 `x:Name` 특성입니다.

```xaml
<Label x:Name="valueLabel"
       Text="A simple Label"
       Font="Large"
       HorizontalOptions="Center"
       VerticalOptions="CenterAndExpand" />
```

합니다 `x` 접두사를 `x:Name` 특성이이 특성에 XAML 내장 임을 나타냅니다.

이름에 할당 합니다 `x:Name` 특성이 동일한 규칙을 C# 변수 이름. 예를 들어 문자 또는 밑줄로 시작 하 고 공백이 포함된 하면 안을 포함 합니다.

이제는 `ValueChanged` 이벤트 처리기는 `Label` 새 표시할 `Slider` 값입니다. 새 값은 이벤트 인수에서 사용할 수 있습니다.

```csharp
void OnSliderValueChanged(object sender, ValueChangedEventArgs args)
{
    valueLabel.Text = args.NewValue.ToString("F3");
}
```

처리기를 얻을 수 있습니다 또는 `Slider` 에서이 이벤트를 생성 하는 개체를 `sender` 인수 가져오고는 `Value` 는 속성:

```csharp
void OnSliderValueChanged(object sender, ValueChangedEventArgs args)
{
    valueLabel.Text = ((Slider)sender).Value.ToString("F3");
}
```

프로그램을 처음 실행 하면를 `Label` 표시 되지 않습니다는 `Slider` 때문에 값을 `ValueChanged` 이벤트가 아직 실행 되지 않았습니다. 하지만 조작 하는 `Slider` 하면 값이 표시 됩니다.

[![표시 된 슬라이더 값](get-started-with-xaml-images/xamlpluscode2.png)](get-started-with-xaml-images/xamlpluscode2-large.png#lightbox)

이제는 `Button`합니다. 보겠습니다에 대 한 응답을 시뮬레이션을 `Clicked` 사용 하 여 경고를 표시 하 여 이벤트를 `Text` 단추입니다. 이벤트 처리기를 안전 하 게 캐스팅할 수는 `sender` 인수는 `Button` 다음 해당 속성에 액세스:

```csharp
async void OnButtonClicked(object sender, EventArgs args)
{
    Button button = (Button)sender;
    await DisplayAlert("Clicked!",
        "The button labeled '" + button.Text + "' has been clicked",
        "OK");
}
```

메서드가로 정의 된 `async` 때문에 `DisplayAlert` 메서드는 비동기적 이며 앞으로 추가 해야는 `await` 메서드가 완료 될 때 반환 하는 연산자입니다. 이 메서드를 가져옵니다 때문에 `Button` 에서 이벤트를 발생는 `sender` 인수를 여러 단추에 대 한 동일한 처리기를 사용할 수 있습니다.

XAML에 정의 된 개체 코드 숨김 파일에서 처리 되는 이벤트를 발생 시킬 수 및 코드 숨김 파일을 사용 하 여 할당 된 이름을 사용 하 여 XAML에서 정의 된 개체를 액세스할 수 있는지 살펴봤습니다는 `x:Name` 특성입니다. 코드 및 XAML 상호 작용 하는 두 가지 기본 방법은 다음과 같습니다.

새로 생성 된 검사 하 여 XAML works 수 수집 하는 방법에 대 한 몇 가지 추가 정보 **XamlPlusCode.xaml.g.cs 파일**, 이제 하나에 할당 된 모든 이름 포함 `x:Name` 개인 필드로 특성입니다. 해당 파일의 단순화 된 버전은 다음과 같습니다.

```csharp
public partial class XamlPlusCodePage : ContentPage {

    private Label valueLabel;

    private void InitializeComponent() {
        this.LoadFromXaml(typeof(XamlPlusCodePage));
        valueLabel = this.FindByName<Label>("valueLabel");
    }
}
```

이 필드를 선언할 수 변수의 내 어디서 나 자유롭게 사용할 수는 `XamlPlusCodePage` 법적으로 성인이 partial 클래스 파일입니다. 런타임 시 필드를 XAML에 구문 분석 된 후 할당 됩니다. 즉 합니다 `valueLabel` 필드는 `null` 때 합니다 `XamlPlusCodePage` 생성자 시작 후에 유효 하지만 `InitializeComponent` 라고 합니다.

후 `InitializeComponent` 생성자에 다시 반환 컨트롤을 페이지의 시각적 개체 처럼 해당가 인스턴스화되고 초기화 된 코드에서 생성 되었습니다. 더 이상 XAML 파일을 클래스의 모든 역할을 수행합니다. 원하는 예를 들어 뷰를 추가 하 여 어떤 방식으로든 페이지에서 이러한 개체를 조작할 수는 `StackLayout`, 또는 설정은 `Content` 다른 페이지의 속성 완전히 합니다. 있습니다 수 "트리 이동"을 검사 하 여 합니다 `Content` 페이지에 있는 항목의 속성을 `Children` 레이아웃의 컬렉션입니다. 이러한 방식으로 액세스 하는 보기에 속성을 설정할 수도 있고를 이벤트 처리기를 동적으로 할당할 수 있습니다.

자유롭게 있습니다. 페이지에는 것 이며 XAML만 해당 콘텐츠를 빌드 도구입니다.

## <a name="summary"></a>요약

이 소개 글로 XAML 파일과 코드 파일이 클래스 정의에 어떻게 기여하는지, 그리고 XAML 및 코드 파일이 상호 작용하는 방식을 살펴보았습니다. 하지만 XAML에는 매우 유연한 방식으로 사용할 수 있는 자체적인 고유 구문 기능이 있습니다. [2장. 필수 XAML 구문 ](~/xamarin-forms/xaml/xaml-basics/essential-xaml-syntax.md)에서 해당 내용을 살펴볼 수 있습니다.

## <a name="related-links"></a>관련 링크

- [XamlSamples](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/xamlsamples)
- [2부. 필수 XAML 구문](~/xamarin-forms/xaml/xaml-basics/essential-xaml-syntax.md)
- [3부. XAML 태그 확장](~/xamarin-forms/xaml/xaml-basics/xaml-markup-extensions.md)
- [4부. 데이터 바인딩 기본 사항](~/xamarin-forms/xaml/xaml-basics/data-binding-basics.md)
- [5장. MVVM 데이터 바인딩](~/xamarin-forms/xaml/xaml-basics/data-bindings-to-mvvm.md)

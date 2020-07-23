---
title: MonoGame 게임 패드 참조
description: 이 문서에서는 MonoGame의 입력 장치에 액세스 하기 위한 플랫폼 간 클래스인 게임 패드를 설명 합니다. 게임 패드에서 입력을 읽는 방법에 대해 설명 하 고 예제 코드를 제공 합니다.
ms.prod: xamarin
ms.assetid: 1F71F3E8-2397-4C6A-8163-6731ECFB7E03
author: conceptdev
ms.author: crdun
ms.date: 03/28/2017
ms.openlocfilehash: 11b1cfda435e97b09f9d1eded22f11f912d1783d
ms.sourcegitcommit: 008bcbd37b6c96a7be2baf0633d066931d41f61a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86934032"
---
# <a name="monogame-gamepad-reference"></a>MonoGame 게임 패드 참조

_게임 패드는 MonoGame에서 입력 장치에 액세스 하기 위한 표준 플랫폼 간 클래스입니다._

`GamePad`여러 MonoGame 플랫폼의 입력 장치에서 입력을 읽는 데 사용할 수 있습니다. 이 가이드에서는 게임 패드 클래스를 사용 하는 방법을 보여 줍니다. 각 입력 장치는 레이아웃 및 제공 하는 단추 수와 다르므로이 가이드에는 다양 한 장치 매핑을 보여 주는 다이어그램이 포함 되어 있습니다.

## <a name="gamepad-as-a-replacement-for-xbox360gamepad"></a>Xbox360GamePad에 대 한 대체 인 게임 패드

원래 XNA API는 `Xbox360GamePad` Xbox 360 또는 PC의 게임 컨트롤러에서 입력을 읽기 위한 클래스를 제공 했습니다. `GamePad`Xbox 360 컨트롤러는 대부분의 MonoGame 플랫폼 (예: iOS 또는 Xbox one)에서 사용할 수 없기 때문에 MonoGame에서 클래스로 대체 되었습니다. 이름 변경에도 불구 하 고 클래스의 사용은 `GamePad` 클래스와 유사 합니다 `Xbox360GamePad` .

## <a name="reading-input-from-gamepad"></a>게임 패드에서 입력 읽기

`GamePad`클래스는 MonoGame 플랫폼에서 입력을 읽는 표준화 된 방법을 제공 합니다. 다음 두 가지 방법을 통해 정보를 제공 합니다.

- `GetState`– 컨트롤러의 단추, 아날로그 스틱 및 d 패드의 현재 상태를 반환 합니다.
- `GetCapabilities`– 컨트롤러에 특정 단추가 있는지 또는 진동 지원 여부와 같은 하드웨어 기능에 대 한 정보를 반환 합니다.

### <a name="example-moving-a-character"></a>예: 문자 이동

다음 코드에서는 왼쪽 엄지 단추를 사용 하 여 및 속성을 설정 하 여 문자를 이동할 수 있는 방법을 보여 줍니다 `XVelocity` `YVelocity` . 이 코드에서는 `characterInstance` 가 및 속성이 있는 개체의 인스턴스인 것으로 가정 합니다 `XVelocity` `YVelocity` .

```csharp
// In Update, or some code called every frame:
var gamePadState = GamePad.GetState(PlayerIndex.One);
// Use gamePadState to move the character
characterInstance.XVelocity = gamePadState.ThumbSticks.Left.X * characterInstance.MaxSpeed;
characterInstance.YVelocity = gamePadState.ThumbSticks.Left.Y * characterInstance.MaxSpeed;
```

### <a name="example-detecting-pushes"></a>예: 푸시 검색

`GamePadState`특정 단추를 눌렀는지 여부와 같은 컨트롤러의 현재 상태에 대 한 정보를 제공 합니다. 문자 점프를 만드는 등의 특정 작업을 수행 하려면 단추가 푸시 되었는지 (마지막 프레임을 종료 하지는 않지만이 프레임에서 작동 하지 않음) 또는 해제 되어 있는지 확인 해야 합니다 (마지막 프레임은 아니지만이 프레임에는 적용 되지 않음).

이러한 유형의 논리를 수행 하려면 이전 프레임의 및 현재 프레임의를 저장 하는 지역 변수를 `GamePadState` `GamePadState` 만들어야 합니다. 다음 예제에서는 이전 프레임의를 저장 하 고 사용 하 여 점프를 구현 하는 방법을 보여 줍니다 `GamePadState` .

```csharp
// At class scope:
// Store the last frame's and this frame's GamePadStates.
// "new" them so that code doesn't have to perform null checks:
GamePadState lastFrameGamePadState = new GamePadState();
GamePadState currentGamePadState = new GamePadState();
protected override void Update(GameTime gameTime)
{
    // store off the last state before reading the new one:
    lastFrameGamePadState = currentGamePadState;
    currentGamePadState = GamePad.GetState(PlayerIndex.One);
    bool wasAButtonPushed =
currentGamePadState.Buttons.A == ButtonState.Pressed
        && lastFrameGamePadState.Buttons.A == ButtonState.Released;
    if(wasAButtonPushed)
    {
        MakeCharacterJump();
    }
...
}
```

### <a name="example-checking-for-buttons"></a>예: 단추 확인

`GetCapabilities`를 사용 하 여 특정 단추나 아날로그 스틱 등의 특정 하드웨어가 컨트롤러에 있는지 확인할 수 있습니다. 다음 코드에서는 두 단추가 모두 있어야 하는 게임의 컨트롤러에서 B 및 Y 단추를 확인 하는 방법을 보여 줍니다.

```csharp
var capabilities = GamePad.GetCapabilities(PlayerIndex.One);
bool hasBButton = capabilities.HasBButton;
bool hasXButton = capabilities.HasXButton;
if(!hasBButton || !hasXButton)
{
    NotifyUserOfMissingButtons();
}
```

## <a name="ios"></a>iOS

iOS 앱은 무선 게임 컨트롤러 입력을 지원 합니다.

> [!IMPORTANT]
> MonoGame 3.5에 대 한 NuGet 패키지는 무선 게임 컨트롤러에 대 한 지원을 포함 하지 않습니다. IOS에서 게임 패드 클래스를 사용 하려면 소스에서 MonoGame 3.5을 빌드하거나 MonoGame 3.6 NuGet 이진 파일을 사용 해야 합니다.

### <a name="ios-game-controller"></a>iOS 게임 컨트롤러

`GamePad`클래스는 무선 컨트롤러에서 읽은 속성을 반환 합니다. 의 속성은 `GamePad` 다음 다이어그램에 표시 된 것 처럼 표준 iOS 컨트롤러 하드웨어에 대해 적합 한 검사를 제공 합니다.

![이 그림에 표시 된 것 처럼 게임 패드의 속성은 표준 iOS 컨트롤러 하드웨어에 대해 적합 한 검사를 제공 합니다.](input-images/image1.png)

## <a name="apple-tv"></a>Apple TV

Apple TV 게임은 입력에 Siri 원격 또는 무선 게임 컨트롤러를 사용할 수 있습니다.

### <a name="siri-remote"></a>Siri 원격

*Siri Remote* 는 Apple TV에 대 한 네이티브 입력 장치입니다. Siri 원격 [및 Bluetooth 컨트롤러 가이드](~/ios/tvos/platform/remote-bluetooth.md)에 표시 된 것 처럼 Siri 원격의 값은 이벤트를 통해 읽을 수 있지만 `GamePad` 클래스는 siri 원격에서 값을 반환할 수 있습니다.

는 `GamePad` 재생 단추와 터치 표면 에서만 입력을 읽을 수 있습니다.

![게임 패드는 재생 단추와 터치 표면의 입력만 읽을 수 있습니다.](input-images/image2.png)

터치 표면 이동은 속성을 통해 읽기 때문에 `DPad` 이동 값은 클래스를 사용 하 여 보고 됩니다 `ButtonState` . 즉, 값은 `ButtonState.Pressed` `ButtonState.Released` 숫자 값 이나 제스처와는 달리 또는로만 사용할 수 있습니다.

### <a name="apple-tv-game-controller"></a>Apple TV 게임 컨트롤러

Apple TV 용 게임 컨트롤러는 iOS 앱 용 게임 컨트롤러와 동일 하 게 작동 합니다. 자세한 내용은 [IOS 게임 컨트롤러](#ios-game-controller) 섹션을 참조 하세요. 

## <a name="xbox-one"></a>Xbox One

Xbox one 콘솔은 Xbox One 게임 컨트롤러에서 입력 읽기를 지원 합니다.

### <a name="xbox-one-game-controller"></a>Xbox One 게임 컨트롤러

Xbox one 게임 컨트롤러는 Xbox one의 가장 일반적인 입력 장치입니다. `GamePad`클래스는 게임 컨트롤러 하드웨어의 입력 값을 제공 합니다.

![게임 패드 클래스는 게임 컨트롤러 하드웨어의 입력 값을 제공 합니다.](input-images/image3.png)

## <a name="summary"></a>요약

이 가이드에서는 MonoGame의 클래스에 대 한 개요를 제공 하 `GamePad` 고, 입력 읽기 논리를 구현 하는 방법 및 일반적인 구현 다이어그램을 제공 `GamePad` 합니다.

## <a name="related-links"></a>관련 링크

- [MonoGame 게임 패드](http://www.monogame.net/documentation/?page=T_Microsoft_Xna_Framework_Input_GamePad)

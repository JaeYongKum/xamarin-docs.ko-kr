---
title: CocoaPods를 사용 하 여 실제 예제
description: 이 문서의 목적은 Sharpie를 사용 하 여 자동으로 생성 하는 방법에 설명 합니다 C# 바인딩는 CocoaPod에서 정의 합니다.
ms.prod: xamarin
ms.assetid: 233B781D-5841-4250-9F63-0585231D2112
author: asb3993
ms.author: amburns
ms.date: 03/28/2018
ms.openlocfilehash: 266f2bca1f4a96242b17080e60c9f43cb956a5fd
ms.sourcegitcommit: bf18425f97b48661ab6b775195eac76b356eeba0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2019
ms.locfileid: "64977878"
---
# <a name="real-world-example-using-cocoapods"></a>CocoaPods를 사용 하 여 실제 예제

> [!NOTE]
> 이 예제에서는 합니다 [AFNetworking CocoaPod](https://cocoapods.org/pods/AFNetworking)합니다.

새 버전 3.0 이상에서는 목표 Sharpie CocoaPods를 바인딩하는 지원에 다음 명령을 (`sharpie pod`) 다운로드, 구성 및 CocoaPods를 쉽게 작성할 수 있도록 합니다. 수행 해야 합니다 [이해 CocoaPods를 사용 하 여](https://cocoapods.org) 일반적 하기 전에이 기능을 사용 합니다.

## <a name="creating-a-binding-for-a-cocoapod"></a>CocoaPod는에 대 한 바인딩 만들기

`sharpie pod` 명령에 전역 옵션 중 하나 및 두 개의 하위 명령:

```bash
$ sharpie pod -help
usage: sharpie pod [OPTIONS] COMMAND [COMMAND_OPTIONS]

Pod Options:
  -d, -dir DIR     Use DIR as the CocoaPods binding directory,
                   defaulting to the current directory

Available Commands:
  init         Initialize a new Xamarin C# CocoaPods binding project
  bind         Bind an existing Xamarin C# CocoaPods project
```

`init` 하위 명령 역시 몇 가지 유용한 도움말:

```bash
$ sharpie pod init -help
usage: sharpie pod init [INIT_OPTIONS] TARGET_SDK POD_SPEC_NAMES

Init Options:
  -f, -force       Initialize a new Podfile and run actions against
                   it even if one already exists
```

여러 CocoaPod 이름과 subspec에 제공할 수 있습니다 `init`합니다.

```bash
$ sharpie pod init ios AFNetworking
** Setting up CocoaPods master repo ...
   (this may take a while the first time)
** Searching for requested CocoaPods ...
** Working directory:
**   - Writing Podfile ...
**   - Installing CocoaPods ...
**     (running `pod install --no-integrate --no-repo-update`)
Analyzing dependencies
Downloading dependencies
Installing AFNetworking (2.6.0)
Generating Pods project
Sending stats
** 🍻 Success! You can now use other `sharpie podn`  commands.
```

여 CocoaPod 설정한 후에 이제 바인딩을 만들 수 있습니다.

```bash
$ sharpie pod bind
```

이렇게 하면 CocoaPod Xcode 프로젝트 작성 및 다음 평가 되어 목표 Sharpie에서 구문 분석 합니다. 콘솔 출력을 많이 생성 됩니다 있지만 끝에 있는 바인딩 정의 해야 합니다.

```bash
(... lots of build output ...)

Parsing 19 header files...

Binding...
  [write] ApiDefinitions.cs
  [write] StructsAndEnums.cs

Done.
```

## <a name="next-steps"></a>다음 단계

생성 한 후는 **ApiDefinitions.cs** 하 고 **StructsAndEnums.cs** 파일을 사용 하면 앱에서 사용할 어셈블리를 생성 하려면 다음 설명서에 살펴보겠습니다.

- [Objective-c 바인딩 개요](~/cross-platform/macios/binding/overview.md)
- [Objective-c 라이브러리 바인딩](~/cross-platform/macios/binding/objective-c-libraries.md)
- [연습: iOS Objective-c 라이브러리 바인딩](~/ios/platform/binding-objective-c/walkthrough.md)

---
title: 항목 빌드
description: 이 문서에서는 Xamarin.Android 빌드 프로세스에서 지원되는 모든 항목 그룹을 나열합니다.
ms.prod: xamarin
ms.assetid: 5EBEE1A5-3879-45DD-B1DE-5CD4327C2656
ms.technology: xamarin-android
author: jonpryor
ms.author: jopryo
ms.date: 09/23/2020
ms.openlocfilehash: 90efe2533f971180124d044ec39ddcf1591b9d36
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91455042"
---
# <a name="build-items"></a>항목 빌드

빌드 항목은 Xamarin.Android 애플리케이션 또는 라이브러리 프로젝트가 빌드되는 방식을 제어합니다.

## <a name="androidasset"></a>AndroidAsset

Java Android 프로젝트의 `assets` 폴더에 포함되는 파일인 [Android 자산](https://developer.android.com/guide/topics/resources/providing-resources#OriginalFiles)을 지원합니다.

## <a name="androidaarlibrary"></a>AndroidAarLibrary

`.aar` 파일을 직접 참조하려면 `AndroidAarLibrary`의 빌드 작업을 사용해야 합니다. 이 빌드 동작은 Xamarin 구성 요소에서 가장 일반적으로 사용됩니다. 즉, Google Play 및 기타 서비스를 작동하는 데 필요한 `.aar` 파일에 대한 참조를 포함합니다.

이 빌드 동작을 사용하는 파일은 라이브러리 프로젝트에 있는 포함 리소스와 비슷한 방식으로 처리됩니다. `.aar`은 중간 디렉터리로 추출됩니다. 그런 다음, 모든 자산, 자원 및 `.jar` 파일이 적절한 항목 그룹에 포함됩니다.

## <a name="androidaotprofile"></a>AndroidAotProfile

프로필 기반 AOT에서 사용할 AOT 프로필을 제공하는 데 사용됩니다.

## <a name="androidboundlayout"></a>AndroidBoundLayout

`AndroidGenerateLayoutBindings` 속성이 `false`로 설정된 경우 레이아웃 파일에 대해 코드 숨김을 생성해야 함을 나타냅니다. 다른 모든 측면에서는 위에서 설명한 `AndroidResource`와 동일합니다. 이 작업은 레이아웃 파일에서**만** 사용할 수 있습니다.

```xml
<AndroidBoundLayout Include="Resources\layout\Main.axml" />
```

## <a name="androidenvironment"></a>AndroidEnvironment

빌드 동작이 `AndroidEnvironment`인 파일은 [프로세스 시작 시 환경 변수 및 시스템 속성을 초기화](~/android/deploy-test/environment.md)하는 데 사용됩니다.
`AndroidEnvironment` 빌드 동작은 여러 파일에 적용될 수 있으며, 특정 순서로 평가되지 않습니다(따라서 여러 파일에 동일한 환경 변수나 시스템 속성을 지정해서는 안 됨).

## <a name="androidfragmenttype"></a>AndroidFragmentType

레이아웃 바인딩 코드를 생성할 때 모든 `<fragment>` 레이아웃 요소에 사용할 기본 정규화된 형식을 지정합니다. 이 속성의 기본값은 표준 Android `Android.App.Fragment` 형식입니다.

## <a name="androidjavalibrary"></a>AndroidJavaLibrary

빌드 동작이 `AndroidJavaLibrary`인 파일은 최종 Android 패키지에 포함될 Java 아카이브(`.jar` 파일)입니다.

## <a name="androidjavasource"></a>AndroidJavaSource

빌드 동작이 `AndroidJavaSource`인 파일은 최종 Android 패키지에 포함될 Java 소스 코드입니다.

## <a name="androidlintconfig"></a>AndroidLintConfig

빌드 작업 'AndroidLintConfig'는 [`$(AndroidLintEnabled)`](~/android/deploy-test/building-apps/build-properties.md#androidlintenabled) 속성과 함께 사용해야 합니다.
속성의 값에 따라 달라집니다. 이 빌드 작업이 포함된 파일은 함께 병합되어 Android `lint` 도구에 전달됩니다. 테스트를 활성화/비활성화할 정보가 포함된 XML 파일이어야 합니다.

자세한 내용은 [lint 설명서](https://developer.android.com/studio/write/lint)를 참조하세요.

## <a name="androidnativelibrary"></a>AndroidNativeLibrary

[네이티브 라이브러리](~/android/platform/native-libraries.md)는 `AndroidNativeLibrary`에 빌드 동작을 설정하여 빌드에 추가됩니다.

Android는 여러 ABI(애플리케이션 이진 인터페이스)를 지원하므로, 빌드 시스템은 네이티브 라이브러리가 대상으로 하는 ABI를 알아야 합니다. 이는 두 가지 방법으로 수행할 수 있습니다.

1. 경로 "검색".
2. `Abi` 항목 특성 사용.

경로 검색을 사용하면 네이티브 라이브러리의 부모 디렉터리 이름을 사용하여 라이브러리가 대상으로 하는 ABI를 지정할 수 있습니다. 따라서 빌드에 `lib/armeabi-v7a/libfoo.so`를 추가하면 ABI가 `armeabi-v7a`로 "검색"됩니다.

### <a name="item-attribute-name"></a>항목 특성 이름

**Abi** &ndash; 네이티브 라이브러리의 ABI를 지정합니다.

```xml
<ItemGroup>
  <AndroidNativeLibrary Include="path/to/libfoo.so">
    <Abi>armeabi-v7a</Abi>
  </AndroidNativeLibrary>
</ItemGroup>
```

## <a name="androidresource"></a>AndroidResource

빌드 동작이 *AndroidResource*인 모든 파일은 빌드 프로세스 중에 Android 리소스에 컴파일되며, `$(AndroidResgenFile)`을 통해 액세스할 수 있게 됩니다.

```xml
<ItemGroup>
  <AndroidResource Include="Resources\values\strings.xml" />
</ItemGroup>
```

고급 사용자는 동일한 유효 경로를 사용하여 여러 구성에서 여러 리소스를 사용하기를 원할 수 있습니다. 이를 위해서는 여러 리소스 디렉터리가 있고 이러한 여러 디렉터리에 동일한 상대 경로를 가진 파일이 있어야 하며, 여러 구성의 여러 파일을 조건부로 포함하는 MSBuild 조건을 사용해야 합니다. 예를 들어:

```xml
<ItemGroup Condition="'$(Configuration)'!='Debug'">
  <AndroidResource Include="Resources\values\strings.xml" />
</ItemGroup>
<ItemGroup  Condition="'$(Configuration)'=='Debug'">
  <AndroidResource Include="Resources-Debug\values\strings.xml"/>
</ItemGroup>
<PropertyGroup>
  <MonoAndroidResourcePrefix>Resources;Resources-Debug<MonoAndroidResourcePrefix>
</PropertyGroup>
```

**LogicalName** &ndash; 리소스 경로를 명시적으로 지정합니다. 여러 개별 리소스 이름으로 사용할 수 있도록 &ldquo;별칭&rdquo; 파일을 허용합니다.

```xml
<ItemGroup Condition="'$(Configuration)'!='Debug'">
  <AndroidResource Include="Resources/values/strings.xml"/>
</ItemGroup>
<ItemGroup Condition="'$(Configuration)'=='Debug'">
  <AndroidResource Include="Resources-Debug/values/strings.xml">
    <LogicalName>values/strings.xml</LogicalName>
  </AndroidResource>
</ItemGroup>
```

## <a name="androidresourceanalysisconfig"></a>AndroidResourceAnalysisConfig

빌드 작업 `AndroidResourceAnalysisConfig`는 파일을 Xamarin Android Designer 레이아웃 진단 도구에 대한 심각도 수준 구성 파일로 표시합니다. 이는 현재 레이아웃 편집기에서만 사용되며 빌드 메시지에는 사용되지 않습니다.

자세한 내용은 [Android 리소스 분석 설명서](../../user-interface/android-designer/diagnostics.md)를 참조하세요.

Xamarin.Android 10.2에 추가되었습니다.

## <a name="content"></a>Content

일반적인 `Content` 빌드 동작이 지원되지 않습니다(비용이 많이 드는 최초 실행 단계 없이 지원하는 방법을 파악하지 못했기 때문).

Xamarin.Android 5.1부터 `@(Content)` 빌드 작업을 사용하려고 하면 `XA0101` 경고가 표시됩니다.

## <a name="linkdescription"></a>LinkDescription

빌드 동작이 *LinkDescription*인 파일은 [링커 동작을 제어](~/cross-platform/deploy-test/linker.md)하는 데 사용됩니다.

## <a name="proguardconfiguration"></a>ProguardConfiguration

빌드 동작이 *ProguardConfiguration*인 파일에는 `proguard` 동작을 제어하는 데 사용되는 옵션이 포함됩니다. 이 빌드 동작에 대한 자세한 내용은 [ProGuard](~/android/deploy-test/release-prep/proguard.md)를 참조하세요.

이 파일은 [`$(EnableProguard)`](~/android/deploy-test/building-apps/build-properties.md#enableproguard)
MSBuild 속성이 `True`가 아닌 한 무시됩니다.
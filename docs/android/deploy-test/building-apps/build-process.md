---
title: 빌드 프로세스
description: 이 문서에서는 Xamarin.Android 빌드 프로세스에 대한 개요를 제공합니다.
ms.prod: xamarin
ms.assetid: 3BE5EE1E-3FF6-4E95-7C9F-7B443EE3E94C
ms.technology: xamarin-android
author: davidortinau
ms.author: daortin
ms.date: 09/11/2020
ms.openlocfilehash: d89f686be99dc8ae8d1aada12dcbe94d857424d7
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91454964"
---
# <a name="build-process"></a>빌드 프로세스

Xamarin.Android 빌드 프로세스는 [`Resource.designer.cs` 생성](~/android/internals/api-design.md), [`@(AndroidAsset)`](~/android/deploy-test/building-apps/build-items.md#androidasset), [`@(AndroidResource)`](~/android/deploy-test/building-apps/build-items.md#androidresource) 및 기타 [빌드 작업](~/android/deploy-test/building-apps/build-items.md) 지원, [Android 호출 가능 래퍼](~/android/platform/java-integration/android-callable-wrappers.md) 생성 및 Android 디바이스에서의 실행을 위한 `.apk` 생성 등, 모든 것을 결합하는 역할을 합니다.

## <a name="application-packages"></a>애플리케이션 패키지

Xamarin.Android 빌드 시스템이 생성할 수 있는 Android 애플리케이션 패키지(`.apk` 파일)의 종류는 크게 두 가지가 있습니다.

- 완전히 자체 포함되어 있으며 실행할 추가 패키지가 필요 없는 **릴리스** 빌드. 앱 스토어에 제공되는 패키지입니다.

- 이와 반대되는 **디버그** 빌드.

이는 우연치 않게 패키지를 생성하는 MSBuild `Configuration`과 일치합니다.

## <a name="shared-runtime"></a>공유 런타임

*공유 런타임*은 기본 클래스 라이브러리(`mscorlib.dll` 등) 및 Android 바인딩 라이브러리(`Mono.Android.dll` 등)를 제공하는 추가적인 Android 패키지의 쌍입니다. 디버그 빌드는 Android 애플리케이션 패키지 내 기본 클래스 라이브러리 및 바인딩 어셈블리를 포함하는 대신 공유 런타임에 의존하므로 디버그 패키지 크기가 줄어듭니다.

공유 런타임은 [`$(AndroidUseSharedRuntime)`](~/android/deploy-test/building-apps/build-properties.md#androidusesharedruntime) 속성을
`False`로 설정하여 디버그 빌드에서 사용하지 않게 설정할 수 있습니다.

<a name="Fast_Deployment"></a>

## <a name="fast-deployment"></a>빠른 배포

*빠른 배포*는 공유 런타임과 함께 작동하여 Android 애플리케이션의 패키지 크기를 더욱 줄입니다. 이를 위해 패키지 내에 앱의 어셈블리를 묶지 않습니다. 대신 `adb push`를 통해 대상에 복사합니다. 어셈블리가 변경될 *경우에만* 패키지가 다시 설치되지 않으므로 빌드/배포/디버그 주기가 단축됩니다. 대신 업데이트된 어셈블리만 대상 디바이스에 다시 동기화합니다.

빠른 배포는 `adb`가 `/data/data/@PACKAGE_NAME@/files/.__override__` 디렉터리에 동기화되지 않게 차단하는 디바이스에서 실패하는 것으로 알려져 있습니다.

빠른 배포는 기본적으로 활성화되며, 디버그 빌드에서 `$(EmbedAssembliesIntoApk)` 속성을 `True`로 설정하여 비활성화할 수 있습니다.

## <a name="msbuild-projects"></a>MSBuild 프로젝트

Xamarin.Android 빌드 프로세스는 Mac용 Visual Studio 및 Visual Studio에서 사용하는 프로젝트 파일 형식이기도 한 MSBuild에 기반을 두고 있습니다.
일반적으로 사용자는 MSBuild 파일을 직접 편집할 필요가 없습니다. IDE가 완전히 작동하는 프로젝트를 만들고, 여기에 변경 사항을 업데이트하며, 필요에 따라 빌드 대상을 자동으로 호출하기 때문입니다.

고급 사용자가 IDE의 GUI에서 지원하지 않는 작업을 수행할 수도 있으므로, 프로젝트 파일을 직접 편집하여 빌드 프로세스를 사용자 지정할 수 있습니다.
이 페이지에서는 Xamarin.Android 관련 기능과 사용자 지정만 설명하지만 일반적인 MSBuild 항목, 속성 및 대상을 사용하여 여러 가지 작업을 수행할 수 있습니다.

<a name="Build_Targets"></a>

## <a name="binding-projects"></a>바인딩 프로젝트

다음 MSBuild 속성을 [바인딩 프로젝트](~/android/platform/binding-java-library/index.md)와 함께 사용할 수 있습니다.

- [`$(AndroidClassParser)`](~/android/deploy-test/building-apps/build-properties.md#androidclassparser)
- [`$(AndroidCodegenTarget)`](~/android/deploy-test/building-apps/build-properties.md#androidcodegentarget)

## <a name="resourcedesignercs-generation"></a>`Resource.designer.cs` 생성

다음 MSBuild 속성은 `Resource.designer.cs` 파일의 생성을 제어하는 데 사용됩니다.

- [`$(AndroidAapt2CompileExtraArgs)`](~/android/deploy-test/building-apps/build-properties.md#androidaapt2compileextraargs)
- [`$(AndroidAapt2LinkExtraArgs)`](~/android/deploy-test/building-apps/build-properties.md#androidaapt2linkextraargs)
- [`$(AndroidExplicitCrunch)`](~/android/deploy-test/building-apps/build-properties.md#androidexplicitcrunch)
- [`$(AndroidR8IgnoreWarnings)`](~/android/deploy-test/building-apps/build-properties.md#androidr8ignorewarnings)
- [`$(AndroidResgenExtraArgs)`](~/android/deploy-test/building-apps/build-properties.md#androidresgenextraargs)
- [`$(AndroidResgenFile)`](~/android/deploy-test/building-apps/build-properties.md#androidresgenfile)
- [`$(AndroidUseAapt2)`](~/android/deploy-test/building-apps/build-properties.md#androiduseaapt2)
- [`$(MonoAndroidResourcePrefix)`](~/android/deploy-test/building-apps/build-properties.md#monoandroidresourceprefix)

## <a name="signing-properties"></a>서명 속성

서명 속성은 Android 디바이스에 설치할 수 있도록 애플리케이션 패키지에 서명하는 방법을 제어합니다. 더욱 빠른 빌드 반복을 위해 Xamarin.Android 작업은 빌드 프로세스 중에 패키지에 서명되지 않습니다. 서명 속도가 상당히 느리기 때문입니다. 대신, IDE 또는 *설치* 빌드 대상을 통해 설치 전이나 내보내기 중에 서명합니다(필요할 경우). *SignAndroidPackage* 대상을 호출하면 출력 디렉터리에 접미사가 `-Signed.apk`인 패키지가 생성됩니다.

기본적으로 서명 대상은 필요한 경우 새 디버그 서명 키를 생성합니다. 예를 들어 빌드 서버에서 특정 키를 사용하려는 경우 다음 MSBuild 속성을 사용합니다.

- [`$(AndroidDebugKeyAlgorithm)`](~/android/deploy-test/building-apps/build-properties.md#androiddebugkeyalgorithm)
- [`$(AndroidDebugKeyValidity)`](~/android/deploy-test/building-apps/build-properties.md#androiddebugkeyvalidity)
- [`$(AndroidDebugStoreType)`](~/android/deploy-test/building-apps/build-properties.md#androiddebugstoretype)
- [`$(AndroidKeyStore)`](~/android/deploy-test/building-apps/build-properties.md#androidkeystore)
- [`$(AndroidSigningKeyAlias)`](~/android/deploy-test/building-apps/build-properties.md#androidsigningkeyalias)
- [`$(AndroidSigningKeyPass)`](~/android/deploy-test/building-apps/build-properties.md#androidsigningkeypass)
- [`$(AndroidSigningKeyStore)`](~/android/deploy-test/building-apps/build-properties.md#androidsigningkeystore)
- [`$(AndroidSigningStorePass)`](~/android/deploy-test/building-apps/build-properties.md#androidsigningstorepass)
- [`$(JarsignerTimestampAuthorityCertificateAlias)`](~/android/deploy-test/building-apps/build-properties.md#jarsignertimestampauthoritycertificatealias)
- [`$(JarsignerTimestampAuthorityUrl)`](~/android/deploy-test/building-apps/build-properties.md#jarsignertimestampauthorityurl)

### <a name="keytool-option-mapping"></a>`keytool` 옵션 매핑

다음 `keytool` 호출의 경우:

```shell
$ keytool -genkey -v -keystore filename.keystore -alias keystore.alias -keyalg RSA -keysize 2048 -validity 10000
Enter keystore password: keystore.filename password
Re-enter new password: keystore.filename password
...
Is CN=... correct?
  [no]:  yes

Generating 2,048 bit RSA key pair and self-signed certificate (SHA1withRSA) with a validity of 10,000 days
        for: ...
Enter key password for keystore.alias
        (RETURN if same as keystore password): keystore.alias password
[Storing filename.keystore]
```

위에서 생성한 키 저장소를 사용하려면 속성 그룹을 사용합니다.

```xml
<PropertyGroup>
    <AndroidKeyStore>True</AndroidKeyStore>
    <AndroidSigningKeyStore>filename.keystore</AndroidSigningKeyStore>
    <AndroidSigningStorePass>keystore.filename password</AndroidSigningStorePass>
    <AndroidSigningKeyAlias>keystore.alias</AndroidSigningKeyAlias>
    <AndroidSigningKeyPass>keystore.alias password</AndroidSigningKeyPass>
</PropertyGroup>
```

## <a name="build-extension-points"></a>빌드 확장점

Xamarin.Android 빌드 시스템은 빌드 프로세스에 연결하려는 사용자를 위한 몇 가지 공용 확장점을 공개합니다. 이 확장점 중 하나를 사용하려면 사용자 지정 대상을 `PropertyGroup`의 해당하는 MSBuild 속성에 추가해야 합니다. 예를 들어:

```xml
<PropertyGroup>
   <AfterGenerateAndroidManifest>
      $(AfterGenerateAndroidManifest);
      YourTarget;
   </AfterGenerateAndroidManifest>
</PropertyGroup>
```

확장점에는 다음이 포함됩니다.

- [`$(AfterGenerateAndroidManifest)](~/android/deploy-test/building-apps/build-properties.md#aftergenerateandroidmanifest)
- [`$(BeforeGenerateAndroidManifest)](~/android/deploy-test/building-apps/build-properties.md#beforegenerateandroidmanifest)

빌드 프로세스를 확장하는 방법에 대한 주의 사항: 제대로 작성되지 않은 빌드 확장은 특히 모든 빌드에서 실행된다면 빌드 성능에 영향을 줄 수 있습니다. 해당 확장을 구현하기 전에 MSBuild [설명서](/visualstudio/msbuild/msbuild)를 읽는 것이 좋습니다.

## <a name="target-definitions"></a>대상 정의

빌드 프로세스의 Xamarin.Android 관련 부분은 `$(MSBuildExtensionsPath)\Xamarin\Android\Xamarin.Android.CSharp.targets`에 정의되지만 어셈블리를 빌드하기 위해 *Microsoft.CSharp.targets*와 같은 일반적인 언어 관련 대상도 필요합니다.

모든 언어 대상을 가져오기 전에 다음과 같은 빌드 속성을 설정해야 합니다.

```xml
<PropertyGroup>
  <TargetFrameworkIdentifier>MonoDroid</TargetFrameworkIdentifier>
  <MonoDroidVersion>v1.0</MonoDroidVersion>
  <TargetFrameworkVersion>v2.2</TargetFrameworkVersion>
</PropertyGroup>
```

C#에서는 *Xamarin.Android.CSharp.targets*를 가져와서 이러한 대상과 속성을 모두 포함할 수 있습니다.

```xml
<Import Project="$(MSBuildExtensionsPath)\Xamarin\Android\Xamarin.Android.CSharp.targets" />
```

이 파일은 다른 언어에 맞게 쉽게 조정할 수 있습니다.
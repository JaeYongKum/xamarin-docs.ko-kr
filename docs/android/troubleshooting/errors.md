---
title: Xamarin.Android Errors Matrix
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 7EBE4C01-8EFC-4B7E-97BA-D879994F59AB
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/13/2018
ms.openlocfilehash: e9916d8e264c202a914e6fd70e664beea276e93d
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
ms.locfileid: "30774150"
---
# <a name="xamarinandroid-errors-matrix"></a>Xamarin.Android Errors Matrix

## <a name="errors-reference"></a>오류 참조

이 문서 Xamarin에서 다양 한 오류 코드에 대 한 정보를 제공합니다.

|범주|설명|
|--- |--- |
|XA0xxx|mandroid 오류|
|XA1xxx|파일을 복사 / symlink (프로젝트와 관련 된) 오류|
|XA2xxx|링커 오류|
|XA3xxx|AOT 오류|
|XA4xxx|코드 생성 오류|
|XA5xxx|GCC 및 도구 체인 오류|
|XA6xxx|mandroid 내부 도구 오류|
|XA7xxx|예약됨|
|XA8xxx|예약됨|
|XA9xxx|라이선스 오류|


## <a name="error-codes"></a>오류 코드

### <a name="xa0xxx-errors"></a>XA0xxx 오류

|오류 코드|설명|
|--- |--- |
|XA0000|예기치 않은 오류-채우십시오는 [버그 보고서](http://bugzilla.xamarin.com)합니다.|
|XA0001|'-devname 장치별 개입 없이 제공 되었습니다.|
|XA0002|환경 변수 ' {'이 (가) 구문 분석할 수 없습니다.|
|XA0003|응용 프로그램 이름 '{0}.exe' SDK 또는 제품 어셈블리 (.dll) 이름과 충돌 합니다.|
|XA0004|새로운 refcounting 논리 sgen도 사용으로 설정 하려면 필요 합니다.|
|XA0005|출력 디렉터리 ' {'이 (가) 존재 하지 않습니다.|
|XA0006|' {0} 에' 개발자 플랫폼에 없는 경우 사용 하 여-플랫폼 SDK를 지정 하는 구획 =|
|XA0007|루트 어셈블리 ' {'이 (가) 존재 하지 않습니다.|
|XA0008|하나의 루트 어셈블리를 제공 해야 합니다.|
|XA0009|어셈블리를 로드 하는 동안 오류가 발생 했습니다: {0}.|
|XA0010|명령줄 인수 구문 분석 하지 못했습니다: {0}.|
|XA0011|{0}가 MonoTouch 지 원하는 것 보다 더 최신 런타임 ({1 \})에 대해 작성 됩니다.|
|XA0012|' {'이 (0)를 완료 하려면 불완전 한 데이터가 제공 됩니다.|
|XA0013|프로 파일링 지원 sgen도 사용으로 설정 하려면 필요 합니다.|
|XA0014|iOS {0} ARMv6를 대상으로 하는 응용 프로그램 빌드를 지원 하지 않습니다.|
|XA0020|Mandroid 경로 확인할 수 없습니다.|
|XA0100|EmbeddedNativeLibrary ' {'이 (0) Android 응용 프로그램 프로젝트에서 유효 하지 않습니다. AndroidNativeLibrary를 대신 사용 하십시오.|

### <a name="xa1xxx-errors"></a>XA1xxx 오류

|오류 코드|설명|
|--- |--- |
|XA1001|지정된 된 디렉터리에 응용 프로그램을 찾을 수 없습니다.|
|XA1002|Symlink를 만들 수 없습니다, 그리고 파일 복사 합니다.|
|XA1003|' {'이 (0) 응용 프로그램을 종료할 수 없습니다. 응용 프로그램을 수동으로 중지 해야 할 수 있습니다.|
|XA1004|설치 된 응용 프로그램의 목록을 가져올 수 없습니다.|
|XA1005|장치 '{1 \}'에서 ' {'이 (0) 응용 프로그램을 종료 하지 못했습니다: {2 \}입니다. 응용 프로그램을 수동으로 중지 해야 할 수 있습니다.|
|XA1006|장치 '{1 \}'에 ' {'이 (0) 응용 프로그램을 설치 하지 못했습니다: {2 \}입니다.|
|XA1007|장치 '{1 \}'에서 ' {'이 (0)는 응용 프로그램을 시작 하지 못했습니다: {2 \}입니다. 여전히 응용 프로그램을 탭 하 여 수동으로 시작할 수 있습니다.|
|XA1008|시뮬레이터를 시작 하지 못했습니다: {0}.|
|XA1009|어셈블리 ' {'이 (가) '{1 \}'에 복사할 수 없습니다: {2 \}입니다.|
|XA1010|어셈블리 ' {'이 (가)를 로드할 수 없습니다: {1 \}입니다.|
|XA1011|누락 된 리소스 파일을 추가할 수 없습니다: ' {'이 (0).|
|XA1101|응용 프로그램을 시작 하지 못했습니다.|
|XA1102|응용 프로그램에서 (중지)에 연결 하지 못했습니다: {0}.|
|XA1103|분리 하지 못했습니다.|
|XA1104|패킷을 보내지 못했습니다: {0}.|
|XA1105|예기치 않은 응답 유형입니다.|
|XA1106|장치에서 응용 프로그램의 목록을 가져올 수 없습니다: 요청 시간이 초과 되었습니다.|
|XA1107|응용 프로그램 시작 하지 못했습니다.|
|XA1201|시뮬레이터를 로드 하지 못했습니다: {0}.|
|XA1301|현재 빌드 architecture(s) ({2 \})와 일치 하지 않을 네이티브 라이브러리 '{0}' ({1 \})가 무시 되었습니다.|

### <a name="xa2xxx-errors"></a>XA2xxx 오류

|오류 코드|설명|
|--- |--- |
|XA2001|어셈블리를 연결할 수 없습니다.|
|XA2002|참조를 확인할 수 없습니다: {0}.|
|XA2003|링크는 사용 되지 옵션 ' {'이 (가) 무시 됩니다.|
|XA2004|추가 링커 정의 파일 ' {'이 (가) 찾을 수 없습니다.|
|XA2005|' {'이 (0)에서 정의 구문 분석할 수 없습니다.|
|XA2006|'{2 \}'에서 메타 데이터 항목 ' {'이 (가) ('{1 \}'에 정의 됨)에 대 한 참조를 확인할 수 없습니다.|

### <a name="xa3xxx-errors"></a>XA3xxx 오류

이들은 AOT 오류입니다.

|오류 코드|설명|
|--- |--- |
|XA3001|AOT을 어셈블리 ' {'이 (가) 하지 못했습니다.|
|XA3002|AOT 제한: [MonoPInvokeCallback]으로 데코레이팅되 어 있으므로 메서드 ' {'이 (가) 정적 이어야 합니다.|
|XA3003|충돌 하는-디버그 및-원하는 llvm 옵션입니다. 소프트 디버깅 사용할 수 없습니다.|


### <a name="xa4xxx-errors"></a>XA4xxx 오류

이들은 코드 생성 오류입니다.

|오류 코드|설명|
|--- |--- |
|XA4001|기본 서식 파일을 ' {'이 (0) expansed 수 없습니다.|
|XA4101|등록자 형식 ' {'이 (가)에 대 한 서명을 만들 수 없습니다.|
|XA4102|등록자 서명에서 메서드 '{2 \}'에 대 한 잘못 된 형식이 ' {'이 (0)를 찾을 수 있습니다. '{1 \}'을 대신 사용 합니다.|
|XA4103|등록자에서에서 찾을 수는 잘못 된 형식 (를) ' {' 메서드의 시그니처를 '{2 \}': 형식 INativeObject을를 구현 하지만 두 개를 사용 하는 생성자가 없습니다 (IntPtr, bool) 인수입니다.|
|XA4104|등록자의 반환 값 형식 ' {'이 (가) '{1 \}' 메서드의 서명에 마샬링할 수 없습니다.|
|XA4105|등록자의 형식 ' {'이 (가) '{1 \}' 메서드 서명에서 매개 변수를 마샬링할 수 없습니다.|
|XA4106|등록자 '{1 \}' 메서드의 서명에 ' {'이 (0) 구조에 대 한 반환 값을 마샬링할 수 없습니다.|
|XA4107|등록자의 형식 ' {'이 (가) '{1 \}' 메서드 서명에서 매개 변수를 마샬링할 수 없습니다.|
|XA4108|등록 기관에는 관리 되는 형식 ' {'이 (가)에 대 한 ObjectiveC 형식을 가져올 수 없습니다.|
|XA4109|생성 된 등록자 코드를 컴파일하지 못했습니다. 보관 된 [버그 보고서](http://bugzilla.xamarin.com)합니다.|
|XA4110|'{1 \}' 메서드의 서명에 등록자의 형식 ' {'이 (가) out 매개 변수를 마샬링할 수 없습니다.|
|XA4111|등록자는 메서드 '{1 \}'에서 형식 ' {'이 (가)에 대 한 서명을 만들 수 없습니다.|
|XA4200|'Claas' 형식에 대 한 ACW의만 생성할 수 있습니다.|
|XA4201|{0} 형식의 JNI 이름을 확인할 수 없습니다.|
|XA4203|지정된 된 형식 이름을 정규화 해야 합니다.|
|XA4204|인터페이스 형식 ' {'이 (가) 확인할 수 없습니다. 어셈블리 참조가 있는지 확인하세요.|
|XA4205|[ExportField] 메서드 매개 변수가 0에 사용할 수 있습니다.|
|XA4206|[내보내기] 제네릭 형식에 사용할 수 없습니다.|
|XA4207|[ExportField] 제네릭 형식에 사용할 수 없습니다.|
|XA4208|[Java.Interop.ExportFieldAttribute] void를 반환 하는 메서드를 사용할 수 없습니다.|
|XA4209|클래스에 대 한 JavaTypeInfo를 만들지 못했습니다: {1 \} {0}.|
|XA4210|ExportAttribute 또는 ExportFieldAttribute 사용 하 여 Mono.Android.Export.dll에 대 한 참조를 추가 해야 합니다.|
|XA4211|AndroidManifest.xml //uses-sdk/@android:targetSdkVersion ' {은 (는) ' $(TargetFrameworkVersion) '{1 \}' 보다 작습니다. API-사용 하 여 \ {1 \\} ACW 컴파일에 대 한 합니다.|


### <a name="xa5xxx-errors"></a>XA5xxx 오류

|오류 코드|설명|
|--- |--- |
|XA5101|누락 된 ' {'이 (0) 컴파일러입니다. Android NDK를 설치 하십시오.|
|XA5102|어셈블리를 네이티브 코드로 변환 하지 못했습니다. 보관 된 [버그 보고서](http://bugzilla.xamarin.com)합니다.|
|XA5103|파일 ' {'이 (가) 컴파일하지 못했습니다. 보관 된 [버그 보고서](http://bugzilla.xamarin.com)합니다.|
|XA5201|네이티브 연결에 실패 했습니다. Gcc에 제공 된 사용자 플래그를 검토 하십시오: {0}|
|XA5202|네이티브 연결에 실패 했습니다. 빌드 로그를 검토 하십시오.|
|XA5303|네이티브 연결 경고: {0}.|
|XA5300|Android SDK 찾을 수 없거나 설치 하지 않습니다.|
|XA5301|누락 된 '제거' 도구입니다. Xcode '명령줄 도구' 구성 요소를 설치 하십시오.|
|XA5302|누락 된 'dsymutil' 도구입니다. Xcode '명령줄 도구' 구성 요소를 설치 하십시오.|
|XA5203|디버그 기호 (dSYM 디렉터리)를 생성 하지 못했습니다. 빌드 로그를 검토 하십시오.|
|XA5204|최종 이진 파일을 제거 하지 못했습니다. 빌드 로그를 검토 하십시오.|
|XA5205|누락 된 'aapt' 도구입니다. Android SDK 빌드-도구 패키지를 설치 하십시오.|
|XA5206|{0}. Android 리소스 디렉터리 {1 \} 존재 하지 않습니다.|
|XA5207|{0}. Java 라이브러리 파일 {1 \} 존재 하지 않습니다.|
|XA5208|다운로드에 실패 했습니다. {0}를 다운로드 하 고 {1 \} 디렉터리에 배치 하세요.|
|XA5209|압축을 풀기에 실패 했습니다. {0}를 다운로드 하 고 {1 \} 디렉터리에 추출 하세요.|
|XA5210|{0}. 네이티브 라이브러리 파일 {1 \} 존재 하지 않습니다.|

### <a name="xa6xxx-errors"></a>XA6xxx 오류

|오류 코드|설명|
|--- |--- |
|XA6001|Cecil의 실행 중인 버전을 제거 하는 어셈블리를 지원 하지 않습니다.|
|XA6002|어셈블리 ' {'이 (가) 제거 하지 못했습니다.|
|XA6003|UnauthorizedAccessException 메시지입니다.|

### <a name="xa9xxx-errors"></a>XA9xxx 오류

이러한 오류 코드는 라이선싱 및 정품 인증 오류입니다.


#### <a name="xa9000"></a>XA9000

 **원인:** 라이선스가 만료

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|경고|경고|경고|경고|경고|


#### <a name="xa9001"></a>XA9001

 **원인:** 평가판이 만료

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|경고|경고|경고|경고|경고|



#### <a name="xa9002"></a>XA9002

 **원인:** AndroidJavaSource

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|확인|확인|확인|확인|

 **원인:** AndroidJavaLibrary

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|확인|확인|확인|확인|

 **바인딩 어셈블리에 포함 된.jar 경우 다음이 검색 되었습니다 빌드 시간이 아닌 패키지 시.**

 **원인:** AndroidNativeLibrary

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|확인|확인|확인|확인|


#### <a name="xa9003"></a>XA9003

 **원인:** System.Runtime.Serialization

 **동안 검사:** 패키지

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|확인|확인|확인|

 **Cause:** System.ServiceModel.Web

 **동안 검사:** 패키지

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|확인|확인|확인|

 **원인:** Mono.Data.Tds

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|확인|확인|확인|

 **이 허용 System.Data.dll에서 참조**

 **원인:** Mono.Android.Export

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|확인|확인|확인|확인|



#### <a name="xa9004"></a>XA9004

 **원인:** -프로 파일링

 **동안 검사:** 패키지

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|확인|확인|확인|



#### <a name="xa9005"></a>XA9005

 **원인:** 크기 제한 (32 kb)입니다.

 **동안 검사:** 패키지

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|확인|-|-|-|



#### <a name="xa9006"></a>XA9006

 **원인:** System.Data.SqlClient 네임 스페이스입니다.

 **동안 검사:** 패키지

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|확인|확인|확인|


#### <a name="xa9008"></a>XA9008

 **원인:** 명령줄에서 빌드.

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|확인|확인|확인|


#### <a name="xa9009"></a>XA9009

 **원인:** Missing 일련 번호입니다.

 **동안 검사:** 볼

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|


#### <a name="xa9010"></a>XA9010

 **원인:** ProductId 잘못 되었습니다.

 **동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|

XA9018와 동일 합니다.



#### <a name="xa9011"></a>XA9011

 **원인:** 라이선스 파일 (새 파일 형식)을 업데이트 하지 못했습니다.

 **동안 검사:** 정품 인증

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|

#### <a name="xa9012"></a>XA9012

 **원인:** 인터넷 없음

 **동안 검사:** 정품 인증

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|


#### <a name="xa9013"></a>XA9013

 **원인:** 알 수 없는 오류

 **동안 검사:** 정품 인증

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|


#### <a name="xa9014"></a>XA9014

 **원인:** 잘못 되었습니다. 활성화 코드

 **동안 검사:** 정품 인증

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|


#### <a name="xa9017"></a>XA9017

 **원인:** 정품 인증 서버에서 유효한 라이선스를 반환 하지 않습니다.

 **동안 검사:** 정품 인증

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|오류|오류|오류|오류|오류|


#### <a name="xa9018"></a>XA9018

**원인:** 잘못 된 라이선스

**동안 검사:** 빌드

|시작|Indie|Business(Trial)|비즈니스|엔터프라이즈|
|--- |--- |--- |--- |--- |
|-|-|오류|-|-|


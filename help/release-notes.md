---
title: 릴리스 정보
description: Places Service 릴리스 정보.
exl-id: 76da9548-4e32-4b23-9a15-7012973915f3
source-git-commit: d5c216aebd99ffef01c37c17c62576835b52438b
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 1%

---

# 릴리스 정보 {#release-notes}

## 2020년 7월 8일

* **위치 및 위치 모니터 확장**

   * [React Native 응용 프로그램](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#react-native)에 대한 위치 및 위치 모니터 확장이 추가되었습니다.
   * [Cordova 응용 프로그램](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#cordova)에 대한 위치 및 위치 모니터 확장이 추가되었습니다.
   * 자세한 내용은 [위치 확장 사용](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-extension/places-extension.html)을 참조하세요.


## 2020년 5월 12일

* **장소 서비스**

   * &quot;POI 가져오기&quot; 버튼을 사용하여 CSV 파일에서 POI 대량 가져오기
   * 여러 POI를 선택하고 메타데이터 값을 일괄 편집 또는 추가

## 2020년 5월 6일

* **PlacesMonitor 2.2.1**

   * **Android**

      * 향상된 로깅

## 2020년 5월 5일


* **PlacesMonitor 2.1.3**

   * **iOS**

      * 향상된 로깅

## 2020년 2월 20일

* **ACPPlaces 1.3.1(iOS)**

   * 위치 확장은 이제 Core SDK의 이벤트 허브에 버전 정보를 보고합니다.
   * 이제 디바이스 POI 멤버십 정보에 수집된 시간으로부터 1시간의 기본 TTL(Time-To-Live)이 있습니다. 자세한 내용은 [Places 멤버십 TTL(Time-to-Live) 수정](places-ext-aep-sdks/places-extension/places-extension.md#places-ttl)을 참조하세요.


* **장소 1.4.1(Android)**

   * 위치 확장은 이제 Core SDK의 이벤트 허브에 버전 정보를 보고합니다.
   * 이제 디바이스 POI 멤버십 정보에 수집된 시간으로부터 1시간의 기본 TTL(Time-To-Live)이 있습니다. 자세한 내용은 [Places 멤버십 TTL(Time-to-Live) 수정](places-ext-aep-sdks/places-extension/places-extension.md#places-ttl)을 참조하세요.

## 2020년 1월 27일

* **PlacesMonitor 2.2.0**

   * **Android**

      * 앱이 시작될 때 및 앱이 실행되는 동안 권한 부여가 변경될 때 위치 권한 부여 상태를 수집하려면 새 위치 API를 호출하십시오.
      * setRequestLocationPermission API 및 더 이상 사용되지 않는 setLocationPermission API가 추가되었습니다.

## 2020년 1월 9일

* **위치 1.4.0**

   * **Android**

      * Places Services에 대한 장치 인증 상태를 설정하기 위해 새 API `setAuthorizationStatus`을(를) 추가했습니다. 이 값은 Places shared 상태에 저장되고 사용됩니다.

## 2019년 12월 4일

* **PlacesMonitor 2.1.2**

   * **iOS**

      * Places API를 호출하여 변경 시 장치에서 CLAuthorizationStatus를 수집합니다.

## 2019년 12월 3일

* **ACPPlaces 1.3.0**

   * **iOS**

      * Places Services에 대한 장치 인증 상태를 설정하기 위해 새 API `setAuthorizationStatus`을(를) 추가했습니다. 이 값은 Places shared 상태에 저장되고 사용됩니다.

## 2019년 11월 25일

* **PlacesMonitor 2.1.1**

   * **iOS**

      * 여러 Pod 프로젝트 옵션을 사용하여 Cocoapods 프로젝트에 대한 가져오기 명세서를 수정했습니다.

## 2019년 11월 22일 토요일

* **PlacesMonitor 2.1.1**

   * **Android**

      * 이제 모니터가 Android 장치의 부트를 인식하고 필요한 경우 장치의 현재 위치를 기반으로 OS에 지오펜스를 다시 등록합니다.
      * 경우에 따라 시작/종료 이벤트가 삭제되는 경합 조건을 수정했습니다.

## 2019년 10월 9일

* **PlacesMonitor 2.1.0**

   * **iOS**

      * 사용자에게 표시될 위치 인증 요청의 유형을 설정하기 위해 새 API `setRequestAuthorizationLevel`을(를) 추가했습니다.


   * **Android**

      * 사용자에게 표시될 위치 권한 요청의 유형을 설정하기 위해 새 API `setLocationPermission`을(를) 추가했습니다.
      * 위치 모니터는 이제 Android 10을 지원합니다.

## 2019년 8월 8일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### UI 업데이트

다음은 위치 UI에 대한 업데이트 목록입니다.

#### 새로운 기능

* 맵 없이 POI를 표시하는 새 목록 보기를 추가했습니다.
* 구/군/시, 도, 국가 및 메타데이터에 대한 POI 필터링 옵션이 추가되었습니다.
* 조직의 첫 번째 라이브러리가 자동으로 만들어집니다.
* 목록 보기에 POI 정렬을 추가했습니다.

#### UI 업데이트

* 목록 및 세부 정보 패널을 UI의 오른쪽으로 이동했습니다.
* UI의 맨 위에 새 검색 패널을 추가했습니다.
* 라이브러리가 하나만 있는 경우 POI를 만들 때 이 라이브러리가 자동으로 선택됩니다.
* 라이브러리 관리를 팝업 창으로 이동했습니다.
* 필터 옆에 POI 카운트가 추가되었습니다.

## 2019년 8월 6일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### Launch 확장 2.0.0 모니터링

* 위치 모니터 2.0에 대한 Android 및 iOS 설치 지침이 업데이트되었습니다.

## 2019년 7월 31일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### 위치 모니터 2.0.0

* 이제 모니터링 상태가 실행 간에 유지됩니다.
* 위치 권한 요청으로 인해 발생한 콜백을 처리하면 더 이상 PlacesActivity를 확장할 필요가 없습니다.
* 기존 API를 변경하여 개발자가 장치에서 모든 위치 데이터를 지울 수 있습니다.

  이전 API: `public static void stop();`

  새 API: `public static void stop (final boolean clearData);`

* 오류 시나리오를 보다 효과적으로 처리하기 위해 `getNearbyPointsOfInterest` API의 사용을 업데이트했습니다.

## 2019년 7월 25일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### ACPPlacesMonitor 2.0.0

* 장치에서 모든 위치 데이터를 지우려면

  acpplacesMonitor에서 기존 API `+ (void) stop;`을(를) `+ (void) stop: (BOOL) clearData;`(으)로 바꾸었습니다.

* 오류 시나리오를 보다 효과적으로 처리하기 위해 ACPPlace `getNearbyPointsOfInterest` API의 사용을 업데이트했습니다.

## 2019년 7월 22일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### Android Places 1.3.0

* 공유 상태, 인앱 메모리 및 공유 환경 설정에서 모든 위치 관련 데이터를 지우는 새 API를 추가했습니다.
* 응용 프로그램 시작 중에 공유 상태가 업데이트되지 않는 문제가 해결되었습니다.
* `getNearbyPointsOfInterest` 콜백이 인터넷 없이 오류 코드 `SERVER_RESPONSE_ERROR instead of CONNECTIVITY_ERROR`을(를) 반환하던 버그를 수정했습니다.
* 근처 관심 영역을 검색하는 동안 오류가 발생하면 `getNearbyPointsOfInterest` API(errorCallback 없음)에 빈 poi 목록과 함께 호출되는 `successCallback`이(가) 있습니다.

## 2019년 7월 19일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS Places 1.2.0**

공유 상태, 인앱 메모리 및 `NSUserDefaults`에서 모든 위치 관련 데이터를 지우는 새 API를 추가했습니다.

## 2019년 6월 25일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS 위치 모니터 1.0.2**

* 더 나은 코드 내 설명서 및 로깅을 포함하여 삶의 질이 개선되었습니다.

## 2019년 6월 17일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS Places 1.1.0**

* 근처 위치를 검색하지 못할 때 오류 코드를 반환하는 새 API가 추가되었습니다.
* 개인 정보 상태가 옵트아웃으로 변경되면 이제 모든 위치 관련 데이터가 장치에서 삭제됩니다.
* 첫 번째 실행 후 잘못된 네트워크 조건으로 인해 위치 이벤트가 유실되는 문제가 해결되었습니다.
* POI 입력 이벤트를 빠르게 연속해서 처리할 때 규칙 엔진을 통한 토큰 교체가 경우에 따라 잘못된 POI를 참조하는 문제가 수정되었습니다.

## 2019년 5월 30일

**Android 위치 모니터 1.0.1**

* 위치 모니터링이 시작될 때 POI에 대한 시작 이벤트가 발생하지 않는 문제를 해결했습니다.

## 2019년 5월 28일

위치 UI에서 다음 문제가 해결되었습니다.

* 나머지 Experience Cloud과 일치하도록 위치에 솔루션 전환기 를 업데이트했습니다.
* 등급이 변경되지 않은 인스턴스에서 등급이 저장되는 문제를 해결했습니다.
* UI에서 허용되는 최소 반경이 10미터로 증가했습니다.
* 필드의 모든 숫자를 삭제하면 반경 필드가 20m로 다시 설정되는 문제가 수정되었습니다.

## 2019년 5월 17일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**Android Places 1.2.0**

* 개별 Geofence를 처리하기 위해 새 API를 추가했습니다.
* 여러 개의 연속 시작 이벤트를 방지하는 버그 수정.

**Android 위치 모니터 1.0.0**

Android용 위치 모니터 초기 릴리스.

위치 모니터는 OS 수준의 위치 API를 관리하고 위치 확장과 직접 통신합니다. 두 확장이 모두 설치되어 있으면 고객은 애플리케이션에서 기본 영역 모니터링을 수행할 수 있습니다.
위치 모니터에 대한 자세한 내용을 보려면 여기를 클릭하십시오.


## 2019년 5월 2일

**Android Places 1.1.0**

* errorCallback이 있고 오류 원인을 나타내는 errorCode와 함께 호출되는 getNearByPlaces용 새 API를 도입했습니다.
* 이제 위치 확장은 구성을 가져올 때까지 이벤트를 큐에 추가합니다.
* 환경 인식 구성에 대한 지원이 추가되었습니다.
* 버그 수정 : 영역 시작/종료 이벤트에 대한 키가 수정되었습니다.
* 마지막으로 알려진 위치의 저장은 이제 사용자의 개인 정보 상태를 올바르게 준수합니다


## 2019년 4월 9일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS 위치 모니터 1.0.1**

* 전체 단위 테스트 범위가 추가되었습니다.
* CI 통합(CircleCI)
* 코드 검사 통합(codecov)

## 2019년 25월 3일

iOS Places Monitor 1.0.0

iOS용 위치 모니터 초기 릴리스.

위치 모니터는 OS 수준의 위치 API를 관리하고 위치 확장과 직접 통신합니다. 두 확장이 모두 설치되어 있으면 고객은 애플리케이션에서 기본 영역 모니터링을 수행할 수 있습니다.

## 2019년 2월 28일

### Beta 릴리스

고객이 실제 위치 데이터로 사용자 경험을 강화할 수 있는 도구 세트인 Places Service의 첫 번째 릴리스입니다. 첫 번째 릴리스의 경우 주요 사용 사례는 모바일 앱이 사용자 지정 위치 데이터를 검색하고 Adobe Experience Platform Launch을 통해 해당 데이터에 대해 작동하도록 하는 것입니다.

### 주요 기능

이 릴리스의 주요 기능은 다음과 같습니다.

#### Places Service UI

관심 영역(POI)을 보고 관리할 수 있는 관리 UI가 출시되었습니다. POI를 라이브러리로 구성할 수도 있습니다. 도시, 주 및 카테고리와 같은 표준 메타데이터 외에도 사용자 지정 메타데이터를 POI에 추가하는 기능도 지원합니다.

* UI를 보려면 [https://places.adobe.com](https://places.adobe.com)(으)로 이동하십시오.
* UI를 시작하려면 [시작하기](/help/getting-started.md)를 참조하세요.

#### 위치 확장

위치 확장을 사용하면 Places Service 라이브러리를 모바일 앱에 추가하고 POI를 처리할 수 있습니다. Experience Platform Launch에서 규칙 빌더를 사용하여 사용자가 POI를 입력하거나 종료할 때 실행할 작업을 트리거할 수 있습니다.

위치 확장에서:

* 앱에 포함할 POI 라이브러리를 선택할 수 있습니다.
* POI 시작 또는 종료 시 트리거되는 규칙 이벤트.
* 사용자의 현재 POI를 가리키는 데이터 요소를 만듭니다.

위치 확장에 대한 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md)을 참조하십시오.

#### 위치 API

Places API를 사용하여 다음을 수행할 수 있습니다.

* 개발자가 POI 목록을 채우고 업데이트할 수 있도록 허용합니다.
* 고유한 UI를 구축하거나 기존 POI 데이터베이스와 통합합니다.
* Places API 배치 끝점을 사용하여 POI를 대량으로 가져옵니다.

  제공된 Python 유틸리티를 사용하여 벌크 가져오기를 완료할 수 있습니다.

Places API에 대한 자세한 내용은 [웹 서비스 API](/help/web-service-api/places-web-services.md)를 참조하십시오.

### 곧 출시

#### Analytics 통합

사용자가 POI(수동 호출)에 있을 때 Places Service 데이터베이스의 위치 컨텍스트 데이터를 모든 발신 Analytics 호출에 자동으로 추가하도록 Analytics 확장을 업데이트하는 중입니다. 또한 이 업데이트를 통해 규칙을 만들어 POI 시작 또는 종료(활성 호출)에서 바로 Analytics 추적 호출을 실행할 수 있습니다.

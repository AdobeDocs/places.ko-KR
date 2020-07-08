---
title: 릴리스 노트
description: 장소 서비스에 대한 릴리스 노트입니다.
translation-type: tm+mt
source-git-commit: 3f986697179eb9c0af1d9b54daf67793a99b8491
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 3%

---


# 릴리스 노트 {#release-notes}

## 2020년 7월 8일

* **위치 및 위치 모니터 확장**

   * 반응형 기본 애플리케이션에 대해 위치 및 장소 모니터 익스텐션이 [추가되었습니다.](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#react-native)
   * Cordova 응용 프로그램에 대해 위치 및 배치 모니터 확장 [기능이 추가되었습니다.](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#cordova)
   * 자세한 내용은 다음을 참조하십시오. [위치 확장 사용](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-extension/places-extension.html)


## 2020년 5월 12일

* **Places Service**

   * &quot;POI 가져오기&quot; 단추를 사용하여 CSV 파일에서 POI 대량 가져오기
   * 여러 POI 선택 및 메타데이터 값 일괄 편집 또는 추가

## 2020년 5월 6일

* **PlacesMonitor 2.2.1**

   * **Android**

      * 향상된 로깅

## 2020년 5월 5일


* **PlacesMonitor 2.1.3**

   * **iOS**

      * 향상된 로깅

## 2020년 2월 20일

* **ACPPlace 1.3.1(iOS)**

   * 이제 확장 기능을 통해 Core SDK의 이벤트 허브에 버전 정보를 보고합니다.
   * 이제 장치 POI 멤버십 정보는 수집일로부터 1시간의 기본 실시간 시간을 갖습니다. 자세한 내용은 [장소 멤버십 기간 수정을 참조하십시오.](places-ext-aep-sdks/places-extension/places-extension.md#places-ttl)


* **Places 1.4.1 (Android)**

   * 이제 확장 기능을 통해 Core SDK의 이벤트 허브에 버전 정보를 보고합니다.
   * 이제 장치 POI 멤버십 정보는 수집일로부터 1시간의 기본 실시간 시간을 갖습니다. 자세한 내용은 [장소 멤버십 기간 수정을 참조하십시오.](places-ext-aep-sdks/places-extension/places-extension.md#places-ttl)

## 2020년 1월 27일

* **PlacesMonitor 2.2.0**

   * **Android**

      * 앱을 실행할 때와 앱이 실행되는 동안 인증이 변경될 때 위치 인증 상태를 수집하려면 새로운 위치 API를 호출합니다.
      * setRequestLocationPermission API와 가치가 떨어진 setLocationPermission API가 추가되었습니다.

## 2020년 1월 9일

* **Places 1.4.0**

   * **Android**

      * 장소 서비스에 대한 장치 인증 상태 `setAuthorizationStatus`를 설정하기 위해 새 API를 추가했습니다. 값이 저장되고 [장소] 공유 상태에서 사용됩니다.

## 2019년 12월 4일

* **PlacesMonitor 2.1.2**

   * **iOS**

      * Places API를 호출하여 장치에서 CLAauthorizationStatus를 수집합니다.

## 2019년 12월 3일

* **ACPPlace 1.3.0**

   * **iOS**

      * 장소 서비스에 대한 장치 인증 상태 `setAuthorizationStatus`를 설정하기 위해 새 API를 추가했습니다. 값이 저장되고 [장소] 공유 상태에서 사용됩니다.

## 2019년 11월 25일

* **PlacesMonitor 2.1.1**

   * **iOS**

      * 여러 창 프로젝트 옵션을 사용하여 코드 프로젝트에 대한 가져오기 문을 수정했습니다.

## 2019년 11월 22일

* **PlacesMonitor 2.1.1**

   * **Android**

      * 이제 모니터가 Android 장치의 부트를 인식하며, 필요한 경우 장치의 현재 위치에 따라 OS에 대상을 다시 등록합니다.
      * 때때로 시작/종료 이벤트가 무시되던 경합 조건을 수정했습니다.

## 2019년 10월 9일

* **PlacesMonitor 2.1.0**

   * **iOS**

      * 사용자에게 묻는 위치 인증 요청 유형 `setRequestAuthorizationLevel`을 설정하기 위해 새 API를 추가했습니다.
   * **Android**

      * 사용자에게 묻는 위치 권한 요청 유형 `setLocationPermission`을 설정하기 위해 새 API를 추가했습니다.
      * 이제 위치 모니터가 Android 10을 지원합니다.



## 2019년 8월 8일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

### UI 업데이트

위치 UI에 대한 업데이트 목록은 다음과 같습니다.

#### 새로운 기능

* 맵이 없는 POI를 표시하는 새 목록 보기가 추가되었습니다.
* 도시, 주, 국가 및 메타데이터에 대한 POI 필터링 옵션이 추가되었습니다.
* 조직의 첫 번째 라이브러리가 자동으로 만들어집니다.
* 목록 보기에 POI 정렬을 추가했습니다.

#### UI 업데이트

* 목록 및 세부 사항 패널을 UI 오른쪽으로 이동했습니다.
* UI 상단에 새 검색 패널을 추가했습니다.
* 라이브러리가 하나만 있으면 POI를 만들 때 이 라이브러리가 자동으로 선택됩니다.
* 라이브러리 관리를 팝업 창으로 이동했습니다.
* 필터 옆에 POI 카운트가 추가되었습니다.

## 2019년 8월 6일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

### Monitor Launch Extension 2.0.0

* Places Monitor 2.0에 대한 Android 및 iOS 설치 지침을 업데이트했습니다.

## 2019년 7월 31일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

### Places Monitor 2.0.0

* 이제 시작 사이에 모니터링 상태가 유지됩니다.
* 위치 권한 요청으로 인한 콜백 처리를 더 이상 PlacesActivity를 확장할 필요가 없습니다.
* 개발자가 장치에서 모든 위치 데이터를 지울 수 있도록 기존 API를 변경했습니다.

   이전 API: `public static void stop();`

   새  API: `public static void stop (final boolean clearData);`

* 오류 시나리오를 보다 효과적으로 처리하도록 `getNearbyPointsOfInterest` API 사용을 업데이트했습니다.

## 2019년 7월 25일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

### ACPPlacesMonitor 2.0.0

* 장치에서 모든 위치 데이터를 지우려면

   acppLaysMonitor에서 기존 API를 로 `+ (void) stop;` 대체했습니다`+ (void) stop: (BOOL) clearData;`.

* 오류 시나리오를 보다 효과적으로 처리하도록 ACPPlaces `getNearbyPointsOfInterest` API의 사용을 업데이트했습니다.

## 2019년 7월 22일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

### Android Places 1.3.0

* 공유 상태, 인앱 메모리 및 공유 환경 설정에서 모든 위치 관련 데이터를 삭제하는 새로운 API가 추가되었습니다.
* 응용 프로그램을 시작하는 동안 공유 상태가 업데이트되지 않는 문제가 해결되었습니다.
* 콜백이 인터넷 상에서 오류 코드 `getNearbyPointsOfInterest` `SERVER_RESPONSE_ERROR instead of CONNECTIVITY_ERROR` 를 반환하는 버그를 수정했습니다.
* `getNearbyPointsOfInterest` API(errorCallback 없이)에는 인근 관심 영역을 검색하는 동안 오류가 발생하는 경우 빈 poi 목록이 있는 `successCallback` 호출자가 있습니다.

## 2019년 7월 19일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

**iOS Places 1.2.0**

공유 상태, 인앱 메모리 등에서 모든 위치 관련 데이터를 삭제하는 새로운 API가 추가되었습니다 `NSUserDefaults`.

## 2019년 6월 25일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

**iOS Places Monitor 1.0.2**

* 향상된 in-code 문서 및 로깅(logging) 등 향상된 삶의 질

## 2019년 6월 17일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

**iOS Places 1.1.0**

* 인근 위치를 검색하지 못할 때 오류 코드를 반환하는 새 API를 추가했습니다.
* 개인 정보 상태가 옵트아웃으로 변경되면 이제 장치에서 모든 위치 관련 데이터가 지워집니다.
* 첫 번째 실행 후 네트워크 상태가 불량하여 장소 이벤트가 손실되는 문제가 해결되었습니다.
* POI 항목 이벤트를 빠르게 연속으로 처리할 때 규칙 엔진을 통한 토큰 대체가 가끔씩 잘못된 POI를 참조하는 문제가 해결되었습니다.

## 2019년 5월 30일

**Android Places Monitor 1.0.1**

* 장소 모니터링을 시작할 때 POI에 대한 시작 이벤트가 발생하지 않던 문제를 수정했습니다.

## 2019년 5월 28일

위치 UI에서 다음 문제를 수정했습니다.

* 다른 Experience Cloud에 맞게 위치(Places)의 솔루션 전환기를 업데이트했습니다.
* 등급 변경 사항이 없는 경우 등급이 저장되던 문제를 수정했습니다.
* UI에서 허용된 최소 반경을 10m로 늘렸습니다.
* 필드의 숫자를 모두 삭제하면 반경 필드가 다시 20m로 재설정되던 문제가 해결되었습니다.

## 2019년 5월 17일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

**Android Places 1.2.0**

* 개별 Geofence를 처리하는 새 API가 추가되었습니다.
* 연속적인 여러 시작 이벤트를 방지하기 위한 버그 수정.

**Android Places Monitor 1.0.0**

Android용 장소 모니터의 초기 릴리스.

위치 모니터는 OS 수준 위치 API를 관리하고 위치 확장 프로그램과 직접 통신합니다. 두 익스텐션이 모두 설치되어 있는 고객은 애플리케이션에서 즉시 사용 가능한 지역 모니터링을 수행할 수 있습니다.
위치 모니터에 대한 자세한 내용을 보려면 여기를 클릭하십시오.


## 2019년 5월 2일

**Android Places 1.1.0**

* errorCallback이 있고 오류 이유를 나타내는 errorCode를 사용하여 호출되는 getNearByPlaces에 대한 새 API를 도입했습니다.
* 이제 위치 확장 기능은 구성을 얻을 때까지 이벤트의 대기열을 유지합니다.
* 환경 인식 구성에 대한 지원을 추가했습니다.
* 버그 수정: 지역 시작/종료 이벤트의 키 수정
* 마지막으로 알려진 위치의 저장은 이제 사용자의 개인 정보 상태를 준수합니다.


## 2019년 9월 4일

이 릴리스에서는 다음 업데이트가 수행되었습니다.

**iOS Places Monitor 1.0.1**

* 전체 단위 테스트 범위를 추가했습니다.
* CI 통합(CircleCI)
* 코드 검사 통합(codecov)

## 2019년 3월 25일

iOS Places Monitor 1.0.0

iOS용 위치 모니터의 초기 릴리스.

위치 모니터는 OS 수준 위치 API를 관리하고 위치 확장 프로그램과 직접 통신합니다. 두 익스텐션이 모두 설치되어 있는 고객은 애플리케이션에서 즉시 사용 가능한 지역 모니터링을 수행할 수 있습니다. 위치 모니터에 대한 자세한 내용은 위치 모니터 확장 [을 참조하십시오](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

## 2019년 2월 28일

### 베타 릴리스

Places Service의 첫 번째 릴리스입니다. 이 툴셋은 고객이 실제 위치 데이터를 통해 사용자 경험을 개선할 수 있도록 해줍니다. 첫 번째 릴리스에서는 모바일 앱이 사용자 지정 위치 데이터를 검색하고 Adobe Experience Platform 시작을 통해 해당 데이터에 대해 작동할 수 있도록 하는 것이 주된 사용 사례입니다.

### 주요 기능

이 릴리스의 주요 기능은 다음과 같습니다.

#### 배치 서비스 UI

관심 영역(POI)을 보고 관리할 수 있는 관리 UI를 발표했습니다. 또한 POI를 라이브러리에 구성할 수 있습니다. 도시, 주 및 카테고리와 같은 표준 메타데이터 외에도 사용자 정의 메타데이터를 POI에 추가하는 기능도 지원합니다.

* UI를 보려면 https://places.adobe.com으로 [이동합니다](https://places.adobe.com).
* UI를 시작하려면 시작하기를 [참조하십시오](/help/getting-started.md).

#### 위치 확장

Places Extension을 사용하여 모바일 앱에 Places Service 라이브러리를 추가하고 POI에 대해 작업할 수 있습니다. Experience Platform Launch의 규칙 빌더를 사용하면 사용자가 POI에 입장하고 나갈 때 실행할 작업을 트리거할 수 있습니다.

위치 확장:

* 앱에 포함할 POI 라이브러리를 선택할 수 있습니다.
* POI 시작 또는 종료 시 트리거되는 규칙 이벤트.
* 사용자의 현재 POI를 가리키는 데이터 요소를 만듭니다.

위치 확장 기능에 대한 자세한 내용은 위치 확장 [기능을 참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

#### API 배치

위치 API를 사용하여 다음을 수행할 수 있습니다.

* 개발자는 POI 목록을 채우고 업데이트할 수 있습니다.
* 고유한 UI를 만들거나 기존 POI 데이터베이스와 통합할 수 있습니다.
* API 배치 끝점을 사용하여 POI의 벌크 가져오기를 수행합니다.

   제공된 Python 유틸리티를 사용하여 벌크 가져오기를 완료할 수 있습니다.

위치 API에 대한 자세한 내용은 [웹 서비스 API를 참조하십시오](/help/web-service-api/places-web-services.md).

### 제공 예정

#### Analytics 통합

사용자가 POI(수동 호출)에 있을 때 나가는 모든 Analytics 호출에 Places Service 데이터베이스의 위치 컨텍스트 데이터를 자동으로 추가하도록 Analytics 확장이 업데이트됩니다. 또한 이 업데이트를 통해 규칙 만들기에서 POI 시작 또는 종료(활성 호출)에서 직접 Analytics 추적 호출을 실행할 수 있습니다.

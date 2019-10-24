---
title: 릴리스 노트
seo-title: Adobe Experience Platform Places 릴리스 노트.
description: Adobe Experience Platform Places 릴리스 노트.
seo-description: Adobe Experience Platform Places 릴리스 노트.
translation-type: tm+mt
source-git-commit: fd1b37a0f50d93de1efff4cb38fc23253f02d517

---


# 릴리스 노트 {#release-notes}

다음은 장소에 대한 릴리스 노트입니다.

## 2019년 10월 9일

* **PlacesMonitor 2.1.0**

   * **iOS**

      * 사용자에게 메시지가 표시되는 위치 인증 요청 유형을 `setRequestAuthorizationLevel`설정하기 위해 새 API를 추가했습니다.
   * **Android**

      * 사용자에게 메시지가 표시되는 위치 권한 요청 유형을 `setLocationPermission`설정하기 위해 새 API를 추가했습니다.
      * 이제 위치 모니터가 Android 10을 지원합니다.



## 2019년 8월 8일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### UI 업데이트 배치

위치 UI에 대한 업데이트 목록은 다음과 같습니다.

#### 새로운 기능

* 맵 없이 POI를 표시하는 새 목록 보기가 추가되었습니다.
* 도시, 주, 국가 및 메타데이터에 대한 POI 필터링 옵션이 추가되었습니다.
* 조직의 첫 번째 라이브러리가 자동으로 생성됩니다.
* 목록 보기에 POI 정렬을 추가했습니다.

#### UI 업데이트

* 목록 및 세부 사항 패널을 UI 오른쪽으로 이동했습니다.
* UI 상단에 새 검색 패널을 추가했습니다.
* 라이브러리가 하나만 있으면 POI를 만들 때 이 라이브러리가 자동으로 선택됩니다.
* 라이브러리 관리를 팝업 창으로 옮겼습니다.
* 필터 옆에 POI 카운트가 추가되었습니다.

## 2019년 8월 6일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### 위치 모니터 시작 확장 2.0.0

* 위치 모니터 2.0에 대한 Android 및 iOS 설치 지침을 업데이트했습니다.

## 2019년 7월 31일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### 위치 모니터 2.0.0

* 이제 시작 사이에 모니터링 상태가 유지됩니다.
* 위치 권한 요청에서 발생한 콜백의 처리를 더 이상 PlacesActivity를 확장할 필요가 없습니다.
* 개발자가 장치에서 모든 위치 데이터를 지울 수 있도록 기존 API를 변경했습니다.

   이전 API: `public static void stop();`

   새 API: `public static void stop (final boolean clearData);`

* 위치 API의 사용을 `getNearbyPointsOfInterest` 업데이트하여 오류 시나리오를 보다 효과적으로 처리합니다.

## 2019년 7월 25일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### AcplaysMonitor 2.0.0

* 장치에서 모든 위치 데이터를 지우려면

   acplaysMonitor에서 기존 API를 `+ (void) stop;` 로`+ (void) stop: (BOOL) clearData;`대체했습니다.

* 오류 시나리오를 보다 효과적으로 처리하도록 ACPPlays API `getNearbyPointsOfInterest` 사용을 업데이트했습니다.

## 2019년 7월 22일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

### Android Places 1.3.0

* 공유 상태, 인앱 메모리 및 공유 환경 설정에서 모든 위치 관련 데이터를 삭제하는 새로운 API가 추가되었습니다.
* 응용 프로그램을 시작하는 동안 공유 상태가 업데이트되지 않는 문제가 해결되었습니다.
* 콜백이 인터넷 상에서 오류 코드를 반환하는 버그를 `getNearbyPointsOfInterest` `SERVER_RESPONSE_ERROR instead of CONNECTIVITY_ERROR` 수정했습니다.
* `getNearbyPointsOfInterest` API(errorCallback 없이)에는 근처 관심 영역을 검색하는 동안 오류가 발생하는 경우 빈 poi 목록과 함께 `successCallback` 호출됩니다.

## 2019년 7월 19일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS Places 1.2.0**

공유 상태, 인앱 메모리 등에서 모든 위치 관련 데이터를 삭제하는 새로운 API가 `NSUserDefaults`추가되었습니다.

## 2019년 6월 25일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS Places Monitor 1.0.2**

* 향상된 in-code 문서 및 로깅(logging) 등 향상된 삶의 질

## 2019년 6월 17일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS Places 1.1.0**

* 근처 위치를 검색하는 데 오류가 있을 때 오류 코드를 반환하는 새 API를 추가했습니다.
* 개인 정보 상태가 옵트아웃으로 변경되면 이제 장치에서 모든 위치 관련 데이터가 지워집니다.
* 첫 번째 실행 후 때때로 잘못된 네트워크 조건으로 인해 장소 이벤트가 손실되는 문제를 해결했습니다.
* POI 항목 이벤트를 빠르게 연속하여 처리할 때 규칙 엔진을 통한 토큰 교환이 가끔씩 잘못된 POI를 참조하는 문제가 해결되었습니다.

## 2019년 5월 30일 (장소)

**Android Places Monitor 1.0.1**

* 위치 모니터링이 시작될 때 POI에 대한 시작 이벤트가 발생하지 않던 문제를 수정했습니다.

## 2019년 5월 28일

위치 UI에서 다음 문제가 해결되었습니다.

* Experience Cloud의 나머지 솔루션과 일치하도록 [위치]의 솔루션 전환기가 업데이트되었습니다.
* 등급 변경 사항이 없는 경우 등급이 저장되던 문제를 수정했습니다.
* UI에서 허용된 최소 반경을 10m로 늘렸습니다.
* 필드의 숫자를 모두 삭제하면 반경 필드가 다시 20m로 재설정되는 문제가 해결되었습니다.

## 2019년 5월 17일 (장소)

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**Android Places 1.2.0**

* 개별 Geofence를 처리하는 새 API가 추가되었습니다.
* 여러 연속 시작 이벤트를 방지하기 위한 버그 수정.

**Android Places Monitor 1.0.0**

Android용 위치 모니터의 초기 릴리스.

위치 모니터는 OS 수준 위치 API를 관리하고 위치 확장 프로그램과 직접 통신합니다. 두 익스텐션이 모두 설치되어 있는 경우 고객은 애플리케이션에서 즉시 사용할 수 있는 지역 모니터링을 수행할 수 있습니다.
위치 모니터에 대한 자세한 내용을 보려면 여기를 클릭하십시오.


## 2019년 5월 2일

**Android Places 1.2.0**

* errorCallback이 있고 오류 이유를 나타내는 errorCode와 함께 호출되는 getNearByPlaces에 대한 새 API를 도입했습니다.
* 이제 위치 확장 기능은 구성을 얻을 때까지 이벤트를 대기시킵니다.
* 환경 인식 구성에 대한 지원이 추가되었습니다.
* 버그 수정:지역 시작/종료 이벤트에 대한 키 수정
* 마지막으로 알려진 위치의 저장은 이제 사용자의 개인 정보 상태를 적절히 유지합니다.


## 2019년 9월 4일

이 릴리스에서는 다음과 같은 업데이트가 수행되었습니다.

**iOS Places Monitor 1.0.1**

* 전체 단위 테스트 범위를 추가했습니다.
* CI 통합(CircleCI)
* 코드 검사 통합(codecov)

## 2019년 3월 25일

iOS Places Monitor 1.0.0

iOS용 위치 모니터의 초기 릴리스.

위치 모니터는 OS 수준 위치 API를 관리하고 위치 확장 프로그램과 직접 통신합니다. 두 익스텐션이 모두 설치되어 있는 경우 고객은 애플리케이션에서 즉시 사용할 수 있는 지역 모니터링을 수행할 수 있습니다. 위치 모니터에 대한 자세한 내용은 위치 모니터 [확장을](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md)참조하십시오.

## 2019년 2월 28일

### 베타 릴리스

Places의 첫 번째 릴리스로서, 고객은 실제 위치 데이터를 통해 사용자 경험을 강화할 수 있는 다양한 툴을 제공합니다. 첫 번째 릴리스에서는 모바일 앱이 사용자 지정 위치 데이터를 검색하고 Adobe Experience Platform Launch를 통해 해당 데이터에 대한 조치를 취할 수 있도록 하는 것이 주된 사용 사례입니다.

### 주요 기능

다음은 이번 릴리스의 주요 기능입니다.

#### 위치 UI

관심 영역(POI)을 보고 관리할 수 있는 관리 UI를 발표했습니다. 또한 POI를 라이브러리에 구성할 수 있습니다. 도시, 주 및 카테고리와 같은 표준 메타데이터 외에도 사용자 정의 메타데이터를 POI에 추가할 수 있습니다.

* 위치 UI를 보려면 https://places.adobe.com으로 [이동하십시오](https://places.adobe.com).
* 위치 UI를 시작하려면 시작하기를 [참조하십시오](/help/getting-started.md).

#### 위치 확장

위치 확장 기능을 사용하여 위치 라이브러리를 모바일 앱에 추가하고 POI에 따라 작업할 수 있습니다. Experience Platform Launch의 규칙 빌더를 사용하면 사용자가 POI에 들어가서 나갈 때 실행할 작업을 트리거할 수 있습니다.

위치 확장:

* 앱에 포함할 POI 라이브러리를 선택할 수 있습니다.
* POI 시작 또는 종료 시 트리거되는 규칙 이벤트.
* 사용자의 현재 POI를 가리키는 데이터 요소를 만듭니다.

위치 확장 기능에 대한 자세한 내용은 위치 확장을 [참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

#### API 배치

위치 API를 사용하여 다음을 수행할 수 있습니다.

* 개발자는 POI 목록을 채우고 업데이트할 수 있습니다.
* 고유한 UI를 만들거나 기존 POI 데이터베이스와 통합할 수 있습니다.
* API 배치 끝점을 사용하여 POI를 벌크 가져오십시오.

   API에는 Python 유틸리티가 제공됩니다.

위치 API에 대한 자세한 내용은 웹 [서비스](/help/places-web-service-api/places-web-services.md)배치를 참조하십시오.

### 출시 예정

#### Analytics 통합

사용자가 POI(수동 호출) 내에 있을 때 장소 데이터베이스의 위치 컨텍스트 데이터를 모든 나가는 Analytics 호출에 자동으로 추가하도록 Analytics 확장 기능이 업데이트됩니다. 또한 이 업데이트를 사용하면 POI 시작 또는 종료(활성 호출)에서 직접 Analytics 추적 호출을 실행할 수 있습니다.


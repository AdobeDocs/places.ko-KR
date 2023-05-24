---
title: Places 이벤트 참조
description: 위치 확장에서 처리되는 이벤트의 목록입니다.
exl-id: 98210ef4-5ff1-4792-b97b-2845ce02e78a
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 28%

---

# Places 이벤트 참조 {#places-event-reference}

다음은 위치 확장에서 처리되는 이벤트의 목록입니다.

## GetCurrentPointOfInterest

**이벤트 세부 사항**

| 유형 | 소스 | 이름 | 연결됨 |
| :--- | :--- | :--- | :--- |
| 위치 | REQUEST_CONTENT | `requestgetuserwithinplaces` | True |

**이벤트 설명**

이 이벤트는 디바이스가 현재 위치한 POI를 검색하기 위한 요청입니다.

**데이터 페이로드 정의**

해당 없음

## GetNearbyPointsOfInterest

**이벤트 세부 사항**

| 유형 | 소스 | 이름 | 연결됨 |
| :--- | :--- | :--- | :--- |
| 위치 | REQUEST_CONTENT | `requestgetnearbyplaces` | True |

**이벤트 설명**

이 이벤트는 현재 장치 위치와 구성된 위치 라이브러리를 고려하여 인근 POI를 가져오라는 요청입니다.

**데이터 페이로드 정의**

| 키 | 값 유형 | 필수 여부 | 기본값 | 설명 |
| :--- | :--- | :--- | :--- | :--- |
| latitude | 더블 | true | 해당 없음 | 주변 POI를 검색할 때의 중앙에 대한 위도 값을 보유합니다. |
| longitude | 더블 | true | 해당 없음 | 주변 POI를 검색할 중심의 경도 값을 보유합니다. |
| 반경 | 정수 | false | 해당 없음 | 주변 POI 검색에 사용되는 반경(미터 단위). |
| count | 정수 | false | 10 | 결과 응답 이벤트에서 반환할 최대 POI 수. |

## ProcessRegionEvent

**이벤트 세부 사항**

| 유형 | 소스 | 이름 | 연결됨 |
| :--- | :--- | :--- | :--- |
| 위치 | REQUEST_CONTENT | `requestprocessregionevent` | False |

**이벤트 설명**

이 이벤트를 사용하면 위치 확장에서 지오펜스 시작 또는 종료 이벤트를 처리합니다.

**데이터 페이로드 정의**

| 키 | 값 유형 | 필수 여부 | 설명 |
| :--- | :--- | :--- | :--- |
| 지역 | 문자열 | true | 이벤트를 생성하는 영역 ID입니다. |
| regioneventtype | int | true | 생성 중인 지역 이벤트 유형. 진입의 경우 1, 종료의 경우 2. |

## Places 확장에서 발송한 이벤트

이 정보는 현재 진행 중입니다.

---
title: 이벤트 참조 배치
description: '위치 확장이 처리하는 이벤트 목록입니다. '
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 24%

---


# 이벤트 참조 배치 {#places-event-reference}

위치 확장자가 처리하는 이벤트 목록입니다.

## GetCurrentPointsOfInterest

**이벤트 세부 사항**

| 유형 | 소스 | 이름 | 연결됨 |
| :--- | :--- | :--- | :--- |
| PLACES | REQUEST_CONTENT | `requestgetuserwithinplaces` | True |

**이벤트 설명**

이 이벤트는 장치가 현재 있는 POI를 검색하기 위한 요청입니다.

**데이터 페이로드 정의**

n/a

## GetNearlyPointsOfInterest

**이벤트 세부 사항**

| 유형 | 소스 | 이름 | 연결됨 |
| :--- | :--- | :--- | :--- |
| PLACES | REQUEST_CONTENT | `requestgetnearbyplaces` | True |

**이벤트 설명**

이 이벤트는 현재 장치 위치와 구성된 장소 라이브러리를 고려하여 가까운 POI를 가져오기 위한 요청입니다.

**데이터 페이로드 정의**

| 키 | 값 유형 | 필수 여부 | 기본값 | 설명 |
| :--- | :--- | :--- | :--- | :--- |
| latitude | 이중 | true | n/a | 가까운 POI에 대한 검색 중심에 대한 위도 값을 보유합니다. |
| longitude | 이중 | true | n/a | 근처 POI에 대한 검색 중심에 대한 경도 값을 유지합니다. |
| 반경 | 정수 | false | n/a | 주변 POI를 검색하는 데 사용되는 반경(미터 단위) |
| count | 정수 | false | 10 | 결과 응답 이벤트로 반환할 최대 POI 수입니다. |

## 프로세스 영역 이벤트

**이벤트 세부 사항**

| 유형 | 소스 | 이름 | 연결됨 |
| :--- | :--- | :--- | :--- |
| PLACES | REQUEST_CONTENT | `requestprocessregionevent` | False |

**이벤트 설명**

이 이벤트로 인해 위치 확장이 위치 시작 또는 종료 이벤트를 처리합니다.

**데이터 페이로드 정의**

| 키 | 값 유형 | 필수 여부 | 설명 |
| :--- | :--- | :--- | :--- |
| 지역 | string | true | 이벤트를 생성하는 영역의 ID입니다. |
| region eventtype | int | true | 생성할 지역 이벤트 유형. 1은 시작, 2는 종료. |

## Places 확장자가 전달하는 이벤트

이 정보는 현재 진행 중입니다.


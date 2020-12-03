---
title: 머리글 및 매개 변수
description: Places Service REST API에서 사용할 수 있는 헤더 및 매개 변수
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 12%

---


# Headers and parameters {#headers-and-parameters}

다음은 Places Service REST API에서 사용할 수 있는 헤더 및 매개 변수에 대한 세부 정보입니다.

## 지원되는 헤더

| Header | 설명 | 메서드 | 예 |
| :--- | :--- | :--- | :--- |
| `Authorization` | 모바일 토큰 | 모두 |  |
| `x-api-key` | API 키 | 모두 | `19776964b4cde49e08d8f62e5824f777b` |
| `x-gw-ims-org-id` | 조직 ID | 모두 | `18FB61145BAC2FFB0A494777@AdobeOrg` |
| `Content-Type` | 전송 또는 수신된 컨텐츠의 형식 | PUT, POST | `application/json` |
| `Accept-Language` | 오류 메시지에 사용되는 언어 | 선택 사항입니다 | `en-US` |

## 라이브러리 매개 변수

| 매개 변수 | 설명 | 유형 | 제한 | 요청 또는 응답 | 예 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | 라이브러리의 ID | 할당됨 | n/a | 응답 | `"id": "b2488788-2d2a-462b-b1a2-305272777dda"` |
| `name` | 라이브러리의 이름 | string | 256자 | both, required | `"name": "Amazing Places"` |
| `orgID` | 조직의 Experience Cloud 조직 ID | 할당됨 | n/a | 응답 | `"orgID": "777F20F55BACA09E0A495D8F@AdobeOrg"` |
| `poiCount` | 라이브러리의 POI 수 | 정수 | 최대 150,000개 | 응답 | `"poiCount": 25149` |
| `metadataDescriptors` | 각 고유한 POI 메타데이터 키 값 쌍에 대해 카운트 | 혼합 | n/a | 응답 |  |
| `poiCountInCities` | 각 고유한 POI 도시 값에 대해 계산 | 혼합 | n/a | 응답 |  |

## POI 매개 변수

| 매개 변수 | 설명 | 유형 | 제한 | 요청 또는 응답 | 예 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Poi 데이터 | POI 세부 정보 배열 | n/a | both |  |
| `id` | POI의 ID | 할당됨 | n/a | response | `"id": "1455462b-7f9c-4220-9f42-5bbce777a0d1"` |
| `name` | POI의 이름 | string | 512자 | both, optional\* | `"name": "My Favorite Place"` |
| `description` | POI에 대한 설명 | string | 512자 | both, optional\* | `"description": "This is a very good place."` |
| `location` | POI의 형식 및 좌표 배열 | array(혼합) | n/a | both | `"location": {"type": "Point", "coordinates": [-122.201007, 37.604713]` |
| `type` | POI 유형 | string | 현재 &quot;Point&quot;만 지원됨 | both, required | `"type": "Point"` |
| `coordinates` | POI의 경도 및 위도 | array(float) | 위도:-180 - 180, latitude -85 - 85 | both, required | `"coordinates": [-122.201007, 37.604713]` |
| `radius` | POI 주위의 원형 지오펜스 크기 | float | 10 - 2000미터 | both, required | `"radius": 100` |
| `country` | POI 국가 | string | 32자 | both, 옵션* | `"country": "United States"` |
| `state` | POI 주 | string | 32자 | both, 옵션* | `"state": "California"` |
| `city` | POI를 위한 도시 | string | 32자 | both, 옵션* | `"city": "San Jose"` |
| `street` | POI의 주소 | string | 256자 | both, 옵션* | `"street": "122 Woz Way"` |
| `category` | POI 카테고리 | string | 100자 | both, 옵션* | `"category": "cafe"` |
| `icon` | POI 아이콘 | string | 50자 | both, 옵션* | `"icon": "star"` |
| `color` | POI용 색상 | string | 8자 | both, 옵션* | `"color": "blue"` |
| `metadata` | POI에 대한 키/값 쌍의 배열 | array(string) | key:256자, 값:256자, 최대 10쌍 | both, 옵션* | `"metadata": {"region": "Equator"}` |
| `lib_id` | POI가 있는 라이브러리의 ID | n/a | n/a | both, required | `"lib_id": "ac7a0b25-c6c2-43ba-bbc6-2b1777b80fe9"` |

* 매개 변수 값이 포함되지 않으면 이 값이 데이터베이스에 `empty` 로 설정됩니다. 기존 키/값 쌍이 포함되지 않으면 데이터베이스의 해당 POI에 대한 키/값 쌍이 제거됩니다.


---
title: 헤더 및 매개 변수
description: Places Service REST API에서 사용할 수 있는 헤더 및 매개 변수.
exl-id: 3c7e76de-f0ff-4966-a3ec-7f64d819c140
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 14%

---

# 헤더 및 매개 변수 {#headers-and-parameters}

다음은 Places Service REST API에서 사용할 수 있는 헤더 및 매개 변수에 대한 세부 사항입니다.

## 지원되는 헤더

| Header | 설명 | 메서드 | 예 |
| :--- | :--- | :--- | :--- |
| `Authorization` | 전달자 토큰 | 모두 |  |
| `x-api-key` | API 키 | 모두 | `19776964b4cde49e08d8f62e5824f777b` |
| `x-gw-ims-org-id` | 조직 ID | 모두 | `18FB61145BAC2FFB0A494777@AdobeOrg` |
| `Content-Type` | 전송 또는 수신한 콘텐츠의 형식 | PUT, POST | `application/json` |
| `Accept-Language` | 오류 메시지에 사용되는 언어 | 선택 사항입니다 | `en-US` |

## 라이브러리 매개 변수

| 매개변수 | 설명 | 유형 | 제한 | 요청 또는 응답 | 예 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | 라이브러리 ID | 할당됨 | 해당 사항 없음 | 응답 | `"id": "b2488788-2d2a-462b-b1a2-305272777dda"` |
| `name` | 라이브러리 이름 | 문자열 | 256자 | 둘 다 요청에 필요 | `"name": "Amazing Places"` |
| `orgID` | 조직의 Experience cloud orgID | 할당됨 | 해당 사항 없음 | 응답 | `"orgID": "777F20F55BACA09E0A495D8F@AdobeOrg"` |
| `poiCount` | 라이브러리의 POI 수 | 정수 | 최대 150,000 | 응답 | `"poiCount": 25149` |
| `metadataDescriptors` | 각 고유 POI 메타데이터 키 값 쌍의 개수 | 혼합 | 해당 사항 없음 | 응답 |  |
| `poiCountInCities` | 각 고유 POI 도시 값에 대한 카운트 | 혼합 | 해당 사항 없음 | 응답 |  |

## POI 매개 변수

| 매개변수 | 설명 | 유형 | 제한 | 요청 또는 응답 | 예 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Poi 데이터 | POI 세부 정보 배열 | 해당 사항 없음 | 모두 |  |
| `id` | POI ID | 할당됨 | 해당 사항 없음 | 응답 | `"id": "1455462b-7f9c-4220-9f42-5bbce777a0d1"` |
| `name` | POI 이름 | 문자열 | 512자 | 모두, 선택 사항\* | `"name": "My Favorite Place"` |
| `description` | POI에 대한 설명 | 문자열 | 512자 | 모두, 선택 사항\* | `"description": "This is a very good place."` |
| `location` | POI 유형 및 좌표 배열 | 배열(혼합) | 해당 사항 없음 | 모두 | `"location": {"type": "Point", "coordinates": [-122.201007, 37.604713]` |
| `type` | POI 유형 | 문자열 | 현재 &quot;포인트&quot;만 지원됨 | 둘 다 요청에 필요 | `"type": "Point"` |
| `coordinates` | POI의 경도 및 위도 배열 | 배열(부동 소수점) | 경도: -180 ~ 180, 위도 -85 ~ 85 | 둘 다 요청에 필요 | `"coordinates": [-122.201007, 37.604713]` |
| `radius` | POI 주변 원형 지오펜스 크기 | 부동 | 10 - 2000미터 | 둘 다 요청에 필요 | `"radius": 100` |
| `country` | POI 국가 | 문자열 | 32자 | 모두, 옵션* | `"country": "United States"` |
| `state` | POI 주 | 문자열 | 32자 | 모두, 옵션* | `"state": "California"` |
| `city` | POI를 위한 도시 | 문자열 | 32자 | 모두, 옵션* | `"city": "San Jose"` |
| `street` | POI의 상세 주소 | 문자열 | 256자 | 모두, 옵션* | `"street": "122 Woz Way"` |
| `category` | POI에 대한 범주 | 문자열 | 100자 | 모두, 옵션* | `"category": "cafe"` |
| `icon` | POI용 아이콘 | 문자열 | 50자 | 모두, 옵션* | `"icon": "star"` |
| `color` | POI의 색상 | 문자열 | 8자 | 모두, 옵션* | `"color": "blue"` |
| `metadata` | POI에 대한 키/값 쌍 배열 | array(string) | 키: 256자, 값: 256자, 최대 10쌍 | 모두, 옵션* | `"metadata": {"region": "Equator"}` |
| `lib_id` | POI가 있는 라이브러리의 ID | 해당 사항 없음 | 해당 사항 없음 | 모두, 필수 | `"lib_id": "ac7a0b25-c6c2-43ba-bbc6-2b1777b80fe9"` |

* 매개 변수 값이 포함되지 않으면 데이터베이스에서 값이 `empty`(으)로 설정됩니다. 기존 키/값 쌍이 포함되지 않으면 데이터베이스의 해당 POI에 대해 키/값 쌍이 제거됩니다.

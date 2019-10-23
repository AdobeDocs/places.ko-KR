---
title: 여러 POI 업데이트
seo-title: 여러 POI 업데이트
description: 일괄 처리 API를 사용하여 여러 POI를 업데이트합니다.
seo-description: 일괄 처리 API를 사용하여 여러 POI를 업데이트합니다.
translation-type: tm+mt
source-git-commit: 26b0cab7bdada26a7598b20623095b72f7c8d334

---


# 여러 POI 업데이트 {#update-multiple-pois}

여러 POI를 업데이트할 수 있는 POST 메서드입니다.

## 요청

```text
POST https://api-places.adobe.io/places/placesapi/v1/pois/batchUpdate
```

## 머리글

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 본문

```text
{    "updates": [        {            "id": "<POIID>,            ""lib_id": "<lIBRARYID>",            "name": "string",            "description": "string",            "location": {                "type": "Point",                "coordinates": [<LONGITUDE>, <LATITUDE>]            },            "radius": integer,            "country": "string",            "state": "string",            "city": "string",            "street": "string",            "category": "string",            "icon": "string",            "color": "string",            "metadata": {                "ownership": "string",                "brand": "string"            }        },        {            "id": "<POIID>,            "lib_id": "<lIBRARYID>",            "name": "string",            "description": "string",            "location": {                "type": "Point",                "coordinates": [<LONGITUDE>, <LATITUDE>]            },            "radius": integer,            "country": "string",            "state": "string",            "city": "string",            "street": "string",            "category": "string",            "icon": "string",            "color": "string",            "metadata": {                "ownership": "string",                "brand": "string"            }        },        .        .        .        {            "id": "<POIID>,            "lib_id": "<lIBRARYID>",            "name": "string",            "description": "string",            "location": {                "type": "Point",                "coordinates": [<LONGITUDE>, <LATITUDE>]            },            "radius": integer,            "country": "string",            "state": "string",            "city": "string",            "street": "string",            "category": "string",            "icon": "string",            "color": "string",            "metadata": {                "ownership": "string",                "brand": "string"            }        },        {            "id": "<POIID>,            "lib_id": "<lIBRARYID>",            "name": "string",            "description": "string",            "location": {                "type": "Point",                "coordinates": [<LONGITUDE>, <LATITUDE>]            },            "radius": integer,            "country": "string",            "state": "string",            "city": "string",            "street": "string",            "category": "string",            "icon": "string",            "color": "string",            "metadata": {                "ownership": "string",                "brand": "string"            }        }    ]}
```

## 샘플 응답

```text
{    "ids": [        "558360b5-5b4b-4c8a-777f-5e3f4b60e4cb",        "ac01c21c-6274-4922-86d5-7777b59dc9b0",        .        .        .        "acf0fde0-22ee-470a-bfa9-b760777cefdc",        "d3cf8338-520f-49a5-8ee7-3777df69be91"    ],    "_links": {        "pois": {            "href": "https://api-places-dev.adobe.io/places/placesapi/v1/pois/{poi_id}",            "templated": true        }    }}
```

## CURL 명령

다음 CURL 명령을 사용하여 API를 테스트합니다.

```text
curl -X POST 'https://api-places.adobe.io/places/placesapi/v1/pois/batchUpdate' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' --data-binary "@<PATHTOBATCHUPDATEJSONFILE>" -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>실제 값으로 `<API KEY>``<TOKEN>`, `<ORGID>`및 `<PATHTOBATCHUPDATEJSONFILE>` 바꿀 수 있습니다.

## 샘플 JSON 파일

다음은 API용 샘플 JSON `batchUpdate` 파일입니다.

```text
updates":[{"id":"31a49d5c-c6ad-46ae-b88d-a6912a8a6b2f","name":"Updated POI 1","description":"1","location":{"type":"Point","coordinates":[0.0000000,0.0000000]},"radius":25.0,"country":"Ghana","state":"Ghana","city":"Accra","street":"","category":"cafe","icon":"nice","color":"red","metadata":{"region":"Equator"},"lib_id":"42b4d03c-672c-4deb-83e0-134ef070c2af"},{"id":"6a78a729-7973-4373-9199-36da18cc5b8c","name":"Updated POI 2","description":"2","location":{"type":"Point","coordinates":[0.0250000,0.0250000]},"radius":50.0,"country":"Ghana","state":"Ghana","city":"Accra","street":"","category":"cafe","icon":"nice","color":"red","metadata":{"region":"Equator"},"lib_id":"42b4d03c-672c-4deb-83e0-134ef070c2af"},{"id":"74eaa3da-2464-4298-9b6d-5376fa7ea00f","name":"Updated POI 3","description":"3","location":{"type":"Point","coordinates":[0.0500000,0.0500000]},"radius":100.0,"country":"Ghana","state":"Ghana","city":"Accra","street":"","category":"cafe","icon":"nice","color":"red","metadata":{"region":"Equator"},"lib_id":"42b4d03c-672c-4deb-83e0-134ef070c2af"}]}
```

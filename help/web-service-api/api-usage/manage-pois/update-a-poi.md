---
title: POI 업데이트
description: REST API를 사용하여 POI를 업데이트합니다.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e

---


# POI 업데이트 {#update-a-poi}

POI를 업데이트할 수 있는 PUT 메서드입니다.

## 요청

```text
PUT https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>
```

## 머리글

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 본문

```text
{  "id": "string",  "name": "string",  "description": "string",  "location": {    "type": Point",    "coordinates": [<LONGITUDE>, <LATITUDE>]  },  "radius": 0,  "country": "string",  "state": "string",  "city": "string",  "street": "string",  "category": "string",  "icon": "string",  "color": "string",  "metadata": {          "brand": "string",          "owndership": "string"          },  "lib_id": "{libraryID}"}
```

## 샘플 응답

```text
{    "id": "66e3c0fb-12fe-4af2-863e-16e0e777d777",    "name": "New Name",    "description": "18827",    "location": {        "type": "Point",        "coordinates": [            -123.000507,            37.698029        ]    },    "radius": 66,    "country": "US",    "state": "CA",    "city": "Small City",    "street": "1 Island Road",    "category": "",    "icon": "",    "color": "",    "metadata": {        "ownership": "LS",        "brand": "Island station"    },    "lib_id": "6efd87bc-c9c4-4ff3-9503-051bfbc81777"}
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X PUT 'https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '<SINGLEPOIDATA>' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>Replace `<POIID>`, `<API KEY>`, `<TOKEN>``<ORGID>`, and `<SINGLEPOIDATA>` with actual values.
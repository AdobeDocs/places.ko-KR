---
title: POI 읽기
description: REST API를 사용하여 POI를 읽습니다.
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2

---


# POI 읽기

POI에 대한 세부 정보를 반환하는 GET 메서드입니다.

## 요청

```text
GET https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>
```

## 머리글

```text
-H' Content-Type: application/json'  
-H 'Authorization: Bearer <TOKEN>'  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## 샘플 응답

```text
{
    "id": "66e3c0fb-12fe-4af2-863e-16e0e578d777",
    "name": "Train Station Road",
    "description": "18827",
    "location": {
        "type": "Point",
        "coordinates": [
            -121.902498,
            37.331087
        ]
    },
    "radius": 66,
    "country": "PH",
    "state": "41",
    "city": "Quezon City",
    "street": "No. 10 Train Station Road",
    "category": "",
    "icon": "",
    "color": "",
    "metadata": {
        "ownership": "LS",
        "brand": "Train station"
    },
    "lib_id": "6efd87bc-c9c4-4ff3-9503-051bfbc81777"
}
```

## CURL 명령

다음 CURL 명령을 사용하여 API를 테스트합니다.

```text
curl -X GET 'https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>실제 값으로 `<POIID>`, `<API KEY>`, `<TOKEN>`및 `<ORIGIN>` 바꿀 수 있습니다.


---
title: 라이브러리 보기
seo-title: 라이브러리 보기
description: Places REST API를 사용하여 라이브러리를 확인합니다.
seo-description: Places REST API를 사용하여 라이브러리를 확인합니다.
translation-type: tm+mt
source-git-commit: 6ae0c8d90cad4c437e1db7f562a0bc9c6b072ce6

---



# 라이브러리 보기

라이브러리의 세부 정보를 반환하는 GET 메서드입니다.

## 요청

```text
GET https://api-places.adobe.io/places/placesapi/v1/libraries/<LIBRARYID>
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
    "id": "9aa7f663-35cc-4de6-8643-ae7779f3bb87",
    "name": "Facinating places",
    "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",
    "poiCount": 30,
    "metadataDescriptors": [
        {
            "key": "region",
            "type": "string",
            "value": "Equator",
            "count": 29
        },
        {
            "key": "ownership",
            "type": "string",
            "value": "LS",
            "count": 1
        },
        {
            "key": "brand",
            "type": "string",
            "value": "Coffee Cafe",
            "count": 1
        },
        {
            "key": "Color",
            "type": "string",
            "value": "Blue",
            "count": 1
        }
    ],
    "poiCountInCities": [
        {
            "country": "Ghana",
            "state": "Ghana",
            "city": "Accra",
            "count": 29
        },
        {
            "country": "CN",
            "state": "91",
            "city": "Hong Kong",
            "count": 1
        }
    ]
}
```

## CURL 명령

다음 CURL 명령을 사용하여 API를 테스트합니다.

```text
curl -X GET 'https://api-places.adobe.io/places/placesapi/v1/libraries/<LIBRARYID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>실제 값으로 `<LIBRARYID>`, `<API KEY>`, `<TOKEN>`및 `<ORGID>` 바꿀 수 있습니다.


---
title: 조직의 모든 라이브러리 읽기
description: Places REST API를 사용하여 조직의 모든 라이브러리를 읽습니다.
exl-id: 3384e1f2-9626-498d-85f7-84569d869c2c
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: d8704da9c84a066f72471421290d4b46c65f41e1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 3%
---
# 조직의 모든 라이브러리 읽기 {#read-all-lib-in-org}

조직의 모든 라이브러리에 대한 세부 정보를 반환하는 GET 메서드입니다.

## 요청

```text
GET https://api-places.adobe.io/places/placesapi/v1/libraries
```

## 헤더

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 샘플 응답

```text
[    {        "id": "5abb5c6d-ce4f-43f3-a253-120ae883777f",        "name": "Restaurants",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 1    },    {        "id": ""9aa7f663-35cc-4de6-8643-ae7779f3bb87",        "name": "Gas stations",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 30    },    {        "id": "6efd87bc-c9c4-4ff3-9503-051bfbc81777",        "name": "Coffee shops",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 25151    },    {        "id": "d1330287-79bd-44fb-b777-5e59ec37faad",        "name": "Theatres",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 0    }]
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X GET 'https://api-places.adobe.io/places/placesapi/v1/libraries' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>`<API KEY>`, `<TOKEN>,` 및 `<ORGID>` 등의 변수를 실제 값으로 바꾸십시오.

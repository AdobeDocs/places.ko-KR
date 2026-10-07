---
title: 라이브러리 만들기
description: Places REST API를 사용하여 라이브러리를 만듭니다.
exl-id: 155cc6e6-9254-4389-bb02-e526d15908f4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: d8704da9c84a066f72471421290d4b46c65f41e1
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 18%
---
# 라이브러리 만들기 {#create-a-library}

라이브러리를 만들 수 있는 POST 메서드입니다.

## 요청

```text
POST https://api-places.adobe.io/places/placesapi/v1/libraries
```

## 헤더

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 본문

```text
{"name": "<LIBRARY_NAME>"}
```

## 샘플 응답

```text
{       "id": "449f08f3-eff5-4658-9329-2d9687af777e",       "name": "Facinating places",      "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",       "poiCount": 0  }
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X POST 'https://api-places.adobe.io/places/placesapi/v1/libraries' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"name":"New Library Name"}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>`<API KEY>`, `<TOKEN>` 및 `<ORGID>` 등의 변수를 실제 값으로 바꾸십시오.

---
title: 라이브러리에 대한 순위 설정
description: Places REST API를 사용하여 라이브러리에 대한 등급을 설정합니다.
exl-id: c922bddc-1587-4da8-acb4-c2d69ce11808
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: d8704da9c84a066f72471421290d4b46c65f41e1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 3%
---
# 라이브러리에 대한 순위 설정 {#set-rank-on-libraries}

모든 라이브러리에서 등급 순서를 설정할 수 있는 PUT 메서드입니다.

## 요청

`PUT https://api-places-dev.adobe.io/places/placesapi/v1/libraries/rank`

## 헤더

```-H Content-Type: application/json'
-H 'Authorization: Bearer <TOKEN>`  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## PUT 데이터

```
"library_rank_order": ["dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b","ea45781f-26af-44b1-b4f8-43baf5f0fe28"]  
}
```

## 샘플 응답

```
{"library_rank_order" ["dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b","ea45781f-26af-44b1-b4f8-43baf5f0fe28"]}
```

## CURL 명령

```
curl -X PUT `'https://api-places.adobe.io/places/placesapi/v1/libraries/rank'` -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"library_rank_order": ["dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b","ea45781f-26af-44b1-b4f8-43baf5f0fe28"]}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>`<API KEY>`, `<TOKEN>` 및 `<ORGID>` 등의 변수를 실제 값으로 바꾸십시오.

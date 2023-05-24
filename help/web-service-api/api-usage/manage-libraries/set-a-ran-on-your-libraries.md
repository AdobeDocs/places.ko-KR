---
title: 라이브러리에 대한 순위 설정
description: Places REST API를 사용하여 라이브러리에 대한 등급을 설정합니다.
exl-id: c922bddc-1587-4da8-acb4-c2d69ce11808
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 7%

---

# 라이브러리에 대한 순위 설정 {#set-rank-on-libraries}

모든 PUT에서 등급 순서를 설정할 수 있는 라이브러리 방법입니다.

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
>다음과 같은 변수 바꾸기 `<API KEY>`, `<TOKEN>`, 및 `<ORGID>` (실제 값 포함)

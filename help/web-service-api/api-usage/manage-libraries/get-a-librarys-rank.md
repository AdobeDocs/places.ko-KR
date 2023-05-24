---
title: 라이브러리의 등급 가져오기
description: Places REST API를 사용하여 라이브러리의 등급을 가져옵니다.
exl-id: c0abedd0-5ff4-4a01-9f8d-e3d17ea53a97
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '41'
ht-degree: 9%

---

# 라이브러리의 등급 가져오기 {#get-library-rank}

라이브러리 등급을 지정할 수 있는 GET 방법입니다.

## 요청

`GET https://api-places.adobe.io/places/placesapi/v1/libraries/rank`

## 헤더

```
-H Content-Type: application/JSON  
-H 'Authorization: Bearer <TOKEN>'  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## 샘플 응답

```
{"library_rank_order":["ea45781f-26af-44b1-b4f8-43baf5f0fe28","dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b"]}
```

## CURL 명령

```
curl -X GET 'https://api-places.adobe.io/places/placesapi/v1/libraries/rank ' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>다음과 같은 변수 바꾸기 `<API KEY>`, `<TOKEN>`, 및 `<ORGID>` (실제 값 포함)

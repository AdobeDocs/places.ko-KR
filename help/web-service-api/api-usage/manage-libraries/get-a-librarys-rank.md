---
title: 라이브러리 등급 가져오기
description: Places REST API를 사용하여 라이브러리의 등급을 가져옵니다.
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2

---


# 라이브러리 등급 가져오기

라이브러리의 등급을 지정할 수 있는 GET 메서드입니다.

## 요청

`GET https://api-places.adobe.io/places/placesapi/v1/libraries/rank`

## 머리글

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
>변수(예: `<API KEY>`, `<TOKEN>`및)를 실제 값으로 `<ORGID>` 바꿉니다.


---
title: 라이브러리의 등급 설정
description: Places REST API를 사용하여 라이브러리의 등급을 설정합니다.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e

---


# 라이브러리의 등급 설정 {#set-rank-on-libraries}

모든 라이브러리에서 등급 순서를 설정할 수 있는 PUT 메서드입니다.

## 요청

`PUT https://api-places-dev.adobe.io/places/placesapi/v1/libraries/rank`

## 머리글

```-H Content-Type: application/json'
-H 'Authorization: Bearer <TOKEN>`  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## 데이터 입력

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
>변수(예: `<API KEY>`, `<TOKEN>`및)를 실제 값으로 `<ORGID>` 바꿉니다.


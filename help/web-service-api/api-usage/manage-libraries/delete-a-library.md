---
title: 라이브러리 삭제
description: REST API를 사용하여 라이브러리를 삭제합니다.
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2

---


# 라이브러리 삭제

라이브러리를 삭제할 수 있는 DELETE 메서드입니다.

## 요청

```text
DELETE https://api-places.adobe.io/places/placesapi/v1/libraries/<lIBRARYID>
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
If successful a Status of "204 No Content" is returned.
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X DELETE 'https://api-places.adobe.io/places/placesapi/v1/libraries/<LIBRARYID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>변수(예: `<lIBRARYID>`, `<API KEY>`, `<TOKEN>`및)를 실제 값으로 `<ORGID>`바꿉니다.


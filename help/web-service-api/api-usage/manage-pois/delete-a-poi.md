---
title: POI 삭제
description: REST API를 사용하여 POI를 삭제합니다.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e

---


# POI 삭제 {#delete-a-poi}

POI를 삭제할 수 있는 DELETE 메서드입니다.

## 요청

```text
DELETE https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>
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

다음 CURL 명령을 사용하여 API를 테스트합니다.

```text
curl -X DELETE 'https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>실제 값으로 `<POIID>`, `<API KEY>`, `<TOKEN>`및 `<ORGID>` 바꿀 수 있습니다.


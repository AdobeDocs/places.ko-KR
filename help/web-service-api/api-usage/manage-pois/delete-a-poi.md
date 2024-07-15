---
title: POI 삭제
description: 위치 REST API를 사용하여 POI를 삭제합니다.
exl-id: 0325eb3b-f9b2-4b21-bed8-e318e8072a69
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '44'
ht-degree: 4%

---

# POI 삭제 {#delete-a-poi}

POI를 삭제할 수 있는 DELETE 방법입니다.

## 요청

```text
DELETE https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>
```

## 헤더

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
>`<POIID>`, `<API KEY>`, `<TOKEN>` 및 `<ORGID>`을(를) 실제 값으로 바꿉니다.

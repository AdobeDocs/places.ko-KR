---
title: 여러 POI 삭제
description: 배치 API를 사용하여 여러 POI를 삭제합니다.
exl-id: f170b722-e6f4-42a2-b3a6-1bf56965eb17
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 8%

---

# 여러 POI 삭제 {#delete-multiple-pois}

여러 POI를 삭제할 수 있는 POST 방법입니다.

## 요청

```text
POST https://api-places.adobe.io/places/placesapi/v1/pois/batchDelete
```

## 헤더

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 본문

```text
{  "ids": [    "<POIID>",    "<POIID>",    .    .    .    "<POIID>",    "<POIID>"  ]}
```

## 샘플 응답

```text
If successful a Status of "204 No Content" is returned.
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X POST 'https://api-places.adobe.io/places/placesapi/v1/pois/batchDelete' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' --data-binary "@<PATHTOBATCHDELETEJSONFILE>" -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>바꾸기 `<API KEY>`, `<TOKEN>`, `<ORGID>`, 및 `<PATHTOBATCHDELETEJSONFILE>` 실수 값 포함.

## 샘플 JSON 파일

다음은 의 샘플 JSON 파일입니다. `batchDelete` API:

```text
{​"ids":["31a49d5c-c6ad-46ae-b88d-a6912a8a6b2f","6a78a729-7973-4373-9199-36da18cc5b8c","74eaa3da-2464-4298-9b6d-5376fa7ea00f"]​}
```

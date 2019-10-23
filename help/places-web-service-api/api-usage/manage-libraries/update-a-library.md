---
title: 라이브러리 업데이트
seo-title: 라이브러리 업데이트
description: Places REST API를 사용하여 라이브러리를 업데이트합니다.
seo-description: Places REST API를 사용하여 라이브러리를 업데이트합니다.
translation-type: tm+mt
source-git-commit: 26b0cab7bdada26a7598b20623095b72f7c8d334

---


# 라이브러리 업데이트

라이브러리를 업데이트할 수 있는 PUT 메서드입니다.

## 요청

```text
PUT https://api-places.adobe.io/places/placesapi/v1/libraries/<lIBRARYID>
```

## 머리글

```text
-H' Content-Type: application/json'  -H 'Authorization: bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 본문

```text
{"name": "<NEW_LIBRARY_NAME>"}
```

## 샘플 응답

```text
{       "id": "449f08f3-eff5-4658-9329-2d9687af777e",       "name": "Really facinating places",      "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",       "poiCount": 0  }
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X PUT 'https://api-places.adobe.io/places/placesapi/v1/libraries/<LIBRARYID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"name":"Updated Library Name"}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>변수(예: `<lIBRARYID>`, `<API KEY>`, `<TOKEN>`및 `<ORGID>` )를 실제 값으로 바꿉니다.


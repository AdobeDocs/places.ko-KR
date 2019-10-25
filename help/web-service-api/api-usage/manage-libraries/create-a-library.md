---
title: 라이브러리 만들기
seo-title: 라이브러리 만들기
description: Places REST API를 사용하여 라이브러리를 만듭니다.
seo-description: Places REST API를 사용하여 라이브러리를 만듭니다.
translation-type: tm+mt
source-git-commit: 6ae0c8d90cad4c437e1db7f562a0bc9c6b072ce6

---


# 라이브러리 만들기

라이브러리를 만들 수 있는 POST 메서드입니다.

## 요청

```text
POST https://api-places.adobe.io/places/placesapi/v1/libraries
```

## 머리글

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 본문

```text
{"name": "<LIBRARY_NAME>"}
```

## 샘플 응답

```text
{       "id": "449f08f3-eff5-4658-9329-2d9687af777e",       "name": "Facinating places",      "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",       "poiCount": 0  }
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X POST 'https://api-places.adobe.io/places/placesapi/v1/libraries' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"name":"New Library Name"}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>변수(예: `<API KEY>`, `<TOKEN>`및)를 실제 값으로 `<ORGID>` 바꿉니다.


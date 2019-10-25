---
title: 조직의 모든 라이브러리 보기
seo-title: 조직의 모든 라이브러리 보기
description: Places REST API를 사용하여 조직의 모든 라이브러리를 확인합니다.
seo-description: Places REST API를 사용하여 조직의 모든 라이브러리를 확인합니다.
translation-type: tm+mt
source-git-commit: 6ae0c8d90cad4c437e1db7f562a0bc9c6b072ce6

---


# 조직의 모든 라이브러리 보기

조직의 모든 라이브러리에 대한 세부 정보를 반환하는 GET 메서드입니다.

## 요청

```text
GET https://api-places.adobe.io/places/placesapi/v1/libraries
```

## 머리글

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## 샘플 응답

```text
[    {        "id": "5abb5c6d-ce4f-43f3-a253-120ae883777f",        "name": "Restaurants",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 1    },    {        "id": ""9aa7f663-35cc-4de6-8643-ae7779f3bb87",        "name": "Gas stations",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 30    },    {        "id": "6efd87bc-c9c4-4ff3-9503-051bfbc81777",        "name": "Coffee shops",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 25151    },    {        "id": "d1330287-79bd-44fb-b777-5e59ec37faad",        "name": "Theatres",        "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",        "poiCount": 0    }]
```

## CURL 명령

다음 CURL 명령을 사용하여 이 API를 테스트합니다.

```text
curl -X GET 'https://api-places.adobe.io/places/placesapi/v1/libraries' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>및 같은 변수를 `<API KEY>`실제 `<TOKEN>,` 값으로 `<ORGID>` 바꿉니다.
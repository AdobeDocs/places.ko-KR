---
title: 개요
seo-title: 쿼리 API
description: 쿼리 API 이해 및 사용
seo-description: 쿼리 API 이해 및 사용
translation-type: tm+mt
source-git-commit: 6ae0c8d90cad4c437e1db7f562a0bc9c6b072ce6

---



# 쿼리 API

호출자와 가장 가까운 POI를 쿼리할 수 있는 GET 메서드입니다.

## 요청

```text
GET https://query.places.adobe.com/placesedgequery
```

다음 입력을 통해 서비스는 호출자와 가장 가까운 POI 목록을 반환합니다.

* 호출자의 위치 \(위도, 경도\)입니다.
* 검색에 포함할 POI 라이브러리의 ID입니다.
* 반환할 최대 POI 수입니다.  기본값은 100입니다.

   발신자와 POI 사이의 거리는 발신자에서 POI 지오펜스 사이의 거리로 정의됩니다. 응답에서 호출자가 포함된 POI는 호출자가 있는 것으로 표시됩니다.

인수는 다음 쿼리 매개 변수로 제공됩니다.

* (**필수 여부**) `latitude`

   발신자의 위도입니다. 위도는 -85에서 85 사이여야 합니다.
* (**필수 여부**) `longitude`

   호출자의 경도이며 -180에서 180 사이여야 합니다.

* (**선택 사항입니다**) `limit`

   반환할 최대 POI 수입니다.

* (**필수 여부**) `library`

   쿼리할 라이브러리의 ID입니다. 여러 라이브러리를 쿼리하려면 쿼리에 라이브러리 매개 변수의 복사본을 여러 개 포함해야 합니다.

다음은 성공적으로 반환된 JSON 형식의 예입니다.

```markup
{
    "places": {
        "userWithin": [
            {
                "p": [
                    "poi id",
                    "poi name",
                    "poi center's latitude",
                    "poi center's longitude",
                    poiRadius,
                    rank
                ],
                "x": {
                    "country": "US",
                    "city": "Fremont",
                    "street": "Vineyard Heights",
                    "Color": "Blue",
                    "state": "CA",
                    <other POI metadata>
                }
            }
        ],
        "pois": [
            {
                "p": [
                    "poi id",
                    "poi name",
                    "poi center's latitude",
                    "poi center's longitude",
                    poiRadius,
                    rank
                ],
                "x": {
                    "country": "US",
                    "city": "Milpitas",
                    "street": null,
                    "state": "CA"
                }
            },
            {
                "p": [
                    "poi id",
                    "poi name",
                    "poi center's latitude",
                    "poi center's longitude",
                    poiRadius,
                    rank
                ],
                "x": {
                    "country": "US",
                    "city": "Fremont",
                    "street": null,
                    "state": "CA"
                }
            }
        ]
    }
}
```

아래의 POI는 발신자에서 POI의 가장자리까지의 거리별로 `places.pois` 정렬됩니다. POI에는 발신자가 `places.userWithin` 포함되어 있으며, 이 POI는 등급별로 정렬된 다음 반경을 늘립니다.

## 샘플 호출

다음은 통화의 예입니다.

```text
GET https://query.places.adobe.com/placesedgequery?latitude=<userLatitude>&longitude=<userLongitude>&library=<libID1>&library=<libID2>&limit=20
```
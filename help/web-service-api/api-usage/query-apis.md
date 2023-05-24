---
title: 개요
description: 쿼리 API 이해 및 사용.
exl-id: cc61a49c-1cf2-407f-b81a-3d38fcb622cc
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---

# 쿼리 API

호출자에게 가장 가까운 POI를 쿼리할 수 있는 GET 방법입니다.

## 요청

```text
GET https://query.places.adobe.com/placesedgequery
```

다음 입력을 통해 서비스는 호출자에게 가장 가까운 POI 목록을 반환합니다.

* 발신자의 위치(위도, 경도)입니다.
* 검색에 포함할 POI 라이브러리의 ID입니다.
* 반환할 최대 POI 수.  기본값은 100입니다.

   발신자와 POI 사이의 거리는 발신자로부터 POI의 지오펜스의 엣지까지의 거리로 정의된다. 응답에서 호출자가 포함된 POI는 호출자가 있는 것으로 표시됩니다.

인수는 다음 쿼리 매개 변수로 제공됩니다.

* (**필수 여부**) `latitude`

   발신자의 위도이며, -85에서 85 사이여야 합니다.
* (**필수 여부**) `longitude`

   발신자의 경도이며, -180과 180 사이여야 합니다.

* (**선택 사항**) `limit`

   반환할 최대 POI 수.

* (**필수 여부**) `library`

   쿼리할 라이브러리의 ID입니다. 여러 라이브러리를 쿼리하려면 쿼리에 라이브러리 매개 변수의 여러 복사본을 포함해야 합니다.

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

아래 POI `places.pois` 은 호출자에서 POI의 가장자리까지의 거리별로 정렬되어 있습니다. 아래 POI `places.userWithin` 에는 발신자가 포함되며 이러한 POI는 등급별로 정렬된 다음 반경 증가로 정렬됩니다.

## 샘플 호출

다음은 호출의 예입니다.

```text
GET https://query.places.adobe.com/placesedgequery?latitude=<userLatitude>&longitude=<userLongitude>&library=<libID1>&library=<libID2>&limit=20
```

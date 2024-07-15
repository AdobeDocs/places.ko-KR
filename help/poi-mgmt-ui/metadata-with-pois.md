---
title: POI에 메타데이터 사용
description: 이 섹션에서는 POI와 함께 메타데이터를 사용하는 방법에 대한 정보 및 전략을 제공합니다.
exl-id: e669e560-a999-43ff-aeb4-06e6308b0d5c
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# POI와 함께 메타데이터를 사용하기 위한 전략 {#using-metadata-pois}

위치 서비스에서 새 POI를 만들 때 필요한 요소는 이름, 반경, 위도 및 경도뿐입니다. POI 만들기에 대한 자세한 내용은 [POI 만들기](/help/poi-mgmt-ui/create-a-poi-ui.md)를 참조하십시오. 그러나 최소 정보만 입력하는 경우에는 추가 가치를 창출할 기회를 놓치게 됩니다.

POI 메타데이터는 다양한 방식으로 사용할 수 있습니다. POI 관리 관점에서 메타데이터 값을 추가하면 잠재적으로 수천 개의 POI 목록을 검색하거나 필터링할 수 있습니다. POI와 관련된 주요 속성에 대한 메타데이터를 만들면 다운스트림 워크플로우에서 가치를 높일 수 있습니다. 예를 들어, 각 속성에 대한 POI를 생성하는 호텔 체인은 호텔 속성에 수영장이 있는지 여부, 레스토랑 및 바, 체육관 시설이 있는지 여부 등의 메타데이터를 포함할 수 있습니다. 이 메타데이터는 Analytics에 컨텍스트 데이터로 포함될 수 있으며 타깃팅된 오퍼 또는 메시징에도 사용할 수 있습니다.

## Launch에 서비스 메타데이터 배치

Experience Platform Launch에서 추적 또는 메시지 목적으로 중요한 각 Places Service 메타데이터 필드에 대한 데이터 요소를 만들 수 있습니다.

체육관 시설의 ![데이터 요소](/help/assets/gymfacility.png)

그런 다음 Analytics 확장을 사용하여 컨텍스트 데이터로 사용할 메타데이터를 포함하는 새 히트를 만드는 작업을 만들 수 있습니다.

체육관 시설의 ![작업](/help/assets/Analytics-gym.png)

## Adobe Campaign의 인앱 메시지

메타데이터는 Adobe Campaign Standard에 정의된 로컬 알림 및 인앱 메시지에 대한 필터로 사용할 수 있습니다. 메타데이터를 필터로 사용하면 실제 위치와 상황에 맞는 보다 관련성이 높은 메시지를 만들 수 있습니다.

![ACS에서 로컬 알림 및 인앱 메시지 필터링](/help/assets/ACS_gym_metadata.png)

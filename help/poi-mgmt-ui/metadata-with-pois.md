---
title: POI에서 메타데이터 사용
description: 이 섹션에서는 POI에서 메타데이터를 사용하는 방법에 대한 정보 및 전략을 제공합니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# POI에서 메타데이터 사용 전략 {#using-metadata-pois}

위치 서비스에서 새 POI를 만들 때 필요한 요소는 이름, 반경, 위도 및 경도뿐입니다. POI 만들기에 대한 자세한 내용은 POI [만들기를 참조하십시오](/help/poi-mgmt-ui/create-a-poi-ui.md). 그러나 최소 정보만 입력할 경우 추가 값을 만들 수 있는 기회를 잃게 됩니다.

POI 메타데이터는 다양한 방법으로 사용할 수 있습니다. POI 관리 측면에서 메타데이터 값을 추가하면 잠재적으로 수천 개의 POI 목록을 검색하거나 필터링할 수 있습니다. POI와 관련된 주요 속성에 대한 메타데이터를 만들면 다운스트림 워크플로우에서 값을 산출할 수 있습니다. 예를 들어, 각 속성에 대해 POI를 생성하는 호텔 체인은 호텔 속성에 수영장이 있는지 여부에 따라 레스토랑 및 바가 있는지 또는 피트니스 짐 시설이 설치되어 있는지 등의 메타데이터를 포함할 수 있습니다. 이 메타데이터는 분석에서 컨텍스트 데이터로 포함할 수 있으며 타깃팅된 오퍼 또는 메시징에도 사용할 수 있습니다.

## 서비스 메타데이터를 론치에 배치

Experience Platform Launch에서는 추적 또는 메시지 전달에 중요한 각 장소 서비스 메타데이터 필드에 대한 데이터 요소를 만들 수 있습니다.

![체육시설 데이터 요소](/help/assets/gymfacility.png)

그런 다음 Analytics 확장 기능을 사용하여 작업을 만들어 컨텍스트 데이터로 원하는 메타데이터를 포함하는 새로운 히트를 만들 수 있습니다.

![체육시설 운동](/help/assets/Analytics-gym.png)

## Adobe Campaign의 인앱 메시지

메타데이터는 Adobe Campaign Standard에 정의된 로컬 알림 및 인앱 메시지에 대한 필터로 사용할 수 있습니다. 메타데이터를 필터로 사용하면 실제 위치에 컨텍스트 기반의 보다 연관성 있는 메시지를 만들 수 있습니다.

![ACS에서 로컬 알림 및 인앱 메시지 필터링](/help/assets/ACS_gym_metadata.png)
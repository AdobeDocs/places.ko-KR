---
title: 위치 모니터 확장
description: 위치 모니터 익스텐션은 운영 체제와의 상호 작용을 처리하여 사용자와 가장 가까운 POI를 등록하고 모니터링합니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 위치 모니터 확장 {#places-monitor-extension}

위치 모니터 익스텐션은 운영 체제와의 상호 작용을 처리하여 사용자와 가장 가까운 POI를 등록하고 모니터링합니다. 이 익스텐션은 장소 확장 프로그램에서 등록해야 하는 POI를 검색하여 시작 및 종료 알림을 위치 확장 프로그램에 전달합니다. 이러한 알림은 Experience Platform Launch 규칙에서 이벤트로 사용할 수 있습니다.

일부 고객이 이미 운영 체제에서 지역을 모니터링하고 있을 수 있으므로 모니터 익스텐션은 선택 사항입니다. 이러한 경우 위치 확장 API를 추가하여 위치 서비스 데이터베이스에서 가장 가까운 POI를 받고 적절한 작업을 수행할 수 있도록 시작 및 종료 이벤트를 전달해야 합니다.

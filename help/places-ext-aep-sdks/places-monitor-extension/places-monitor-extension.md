---
title: 위치 모니터 확장
description: 위치 모니터 확장은 사용자에게 가장 가까운 POI를 등록하고 모니터링하는 운영 체제와의 상호 작용을 처리합니다.
exl-id: 254b33a0-79c4-4d51-8835-16e60f5c055e
source-git-commit: 8dcd777acf5d578b748afae9aa609c2349ea94a9
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 위치 모니터 확장 {#places-monitor-extension}

위치 모니터 확장은 사용자에게 가장 가까운 POI를 등록하고 모니터링하는 운영 체제와의 상호 작용을 처리합니다. 이 확장은 위치 확장에서 등록해야 하는 POI를 검색하고 시작 및 종료 알림을 위치 확장으로 전달합니다. 이러한 알림은 Experience Platform Launch 규칙에서 이벤트로 사용할 수 있습니다.

일부 고객이 이미 운영 체제에서 지역을 모니터링하고 있을 수 있으므로 모니터 확장은 선택 사항입니다. 이런 경우 위치 확장 API를 추가하여 위치 서비스 데이터베이스에서 가장 가까운 POI를 수신하고 적절한 작업을 수행할 수 있도록 시작 및 종료 이벤트도 전달해야 합니다.

## 위치 모니터 사용 중단

2021년 8월 31일부터 Adobe Experience Platform Mobile SDK용 위치 모니터 확장은 더 이상 사용되지 않습니다. 위치 모니터 확장에서는 8월 31일 이후에 추가 업데이트나 지원을 받지 않습니다.

현재 위치 모니터 확장을 사용하는 고객은 Adobe을 통해 추가 업데이트나 지원을 사용할 수 없다는 점을 파악하여 이 확장 프로그램을 계속 사용할 수 있습니다.

위치 모니터 확장의 사용 중단은 개선 사항 및 업데이트로 계속 지원되는 위치 서비스 확장에 영향을 주지 않거나 부정적인 영향을 주지 않습니다.

위치 모니터 확장에서 자체 모니터링 솔루션으로 전환하려는 고객은 다음 사항에 대한 설명서를 검토해야 합니다.[고유한 모니터링 솔루션과 함께 위치 서비스 사용](https://experienceleague.adobe.com/docs/places/using/using-your-own-monitor.html?lang=en). 이 문서에서는 iOS에서 [핵심 위치 서비스](https://developer.apple.com/documentation/corelocation) 또는 Google Play에서 [위치 서비스](https://developers.google.com/android/reference/com/google/android/gms/location/package-summary)를 구현하여 위치 서비스와 상호 작용하는 방법을 설명합니다.

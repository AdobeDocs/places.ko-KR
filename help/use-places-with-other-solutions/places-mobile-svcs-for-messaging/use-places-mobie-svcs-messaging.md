---
title: Mobile Services에서 Places Service를 사용한 메시지
description: 이 섹션에서는 메시징을 위해 Mobile Services와 함께 Places Service를 사용하는 방법을 보여줍니다.
exl-id: dfa6b8bb-6bf2-44eb-8bfc-87294807ec3b
source-git-commit: d5c216aebd99ffef01c37c17c62576835b52438b
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# Adobe Mobile Services {#places-mobile-services}

Mobile Services 확장을 사용하여 메시지를 보내려면 먼저 다음 전제 조건을 검토하십시오.

* 관심 영역이 Places Service에 만들어졌습니다. 자세한 내용은 [POI 만들기](/help/poi-mgmt-ui/create-a-poi-ui.md).

  >[!IMPORTANT]
  >
  >위치 서비스에는 기존 Mobile Services UI 외부에 있는 조직에 대한 새롭고 개선된 POI 데이터베이스가 포함되어 있습니다. Mobile Service에 있는 POI *위치 관리* 페이지 탐색은 SDK 버전 4에서만 작동합니다.

* 다음 *위치 관리* 이전 버전의 SDK에 대한 레거시 Mobile Services UI의 POI 관리 페이지:

  ![레거시 UI](/help/assets/legacy-location-v4-ui.png)

* 다음은 장소 서비스 UI입니다.

  ![장소 서비스 POI 관리 UI](/help/assets/places-ui.png)

* ACP SDK가 Places 확장으로 올바르게 구성되었습니다.

  즉, 데이터는 모바일 앱의 Experience Platform Launch 규칙 엔진에서 이벤트 및/또는 조건으로 사용할 수 있습니다. 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md).

* 모바일 앱에서 ACP SDK에 Experience Platform Launch 규칙을 만들고 게시하는 방법에 익숙해집니다.

  자세한 내용은 [규칙 엔진](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine).

* Experience Platform Launch 데이터 요소는 규칙 엔진에서 사용될 위치 확장 데이터에서 만들어집니다.

  자세한 내용은 [데이터 요소](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#data-elements).

## 보고

보고를 사용하려면 먼저 다음 전제 조건을 완료하십시오.

* Places Service 데이터를 Adobe Analytics 보고서 세트로 보냈습니다.

  자세한 내용은 [Adobe Analytics에서 장소 서비스 사용](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md).

* Mobile Services 보고에 익숙해지십시오.

  자세한 내용은 [보고서](https://experienceleague.adobe.com/docs/discontinued/using/mobile-services.html).

## 보고 시각화

Adobe Analytics으로 전송되는 Places Service 데이터를 사용하여 모바일 서비스 보고서를 실행할 수 있습니다. 다음 예에서는 사용자가 POI 중 하나에 항목이 있을 때 이벤트가 전송됩니다. 이 보고서에서 POI 항목 이벤트의 필터가 기본 제공 사용자 보고서에 추가되었습니다.

![보고서 시각화](/help/assets/report-visualize.png)

위치 서비스 데이터를 시각화하는 추가 유연성은 Adobe Analytics 인터페이스에서 사용할 수 있습니다.

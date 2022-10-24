---
title: 메시징에 Mobile Services에서 Places Service 사용
description: 이 섹션에서는 메시징에 Mobile Services와 함께 Places Service를 사용하는 방법을 보여줍니다.
exl-id: dfa6b8bb-6bf2-44eb-8bfc-87294807ec3b
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# Adobe Mobile Services {#places-mobile-services}

메시지에 Mobile Services 확장을 사용하려면 먼저 다음 전제 조건을 검토하십시오.

* 관심 영역이 Places Service에서 만들어졌습니다. 자세한 내용은 [POI 만들기](/help/poi-mgmt-ui/create-a-poi-ui.md).

   >[!IMPORTANT]
   >
   >위치 서비스 에는 기존 Mobile Services UI 외부에 있는 조직을 위한 새롭고 개선된 POI 데이터베이스가 포함되어 있습니다. Mobile Service에 있는 POI *배치 관리* 페이지 탐색은 SDK 버전 4에서만 작동합니다.

* 다음은 입니다 *위치 관리* 이전 버전의 SDK용 레거시 Mobile Services UI의 POI 관리 페이지:

   ![레거시 UI](/help/assets/legacy-location-v4-ui.png)

* 다음은 Places Service UI입니다.

   ![Places Service POI 관리 UI](/help/assets/places-ui.png)

* ACP SDK는 위치 확장으로 올바르게 구성됩니다.

   즉, 데이터는 모바일 앱에 대한 Experience Platform Launch 규칙 엔진에서 이벤트 및/또는 조건으로 사용할 수 있습니다. 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md).

* 모바일 앱에서 ACP SDK에 Experience Platform Launch 규칙을 만들고 게시하는 것에 익숙해지십시오.

   자세한 내용은 [규칙 엔진](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine).

* Experience Platform Launch 데이터 요소는 규칙 엔진에서 사용할 위치 확장 데이터에서 만들어집니다.

   자세한 내용은 [데이터 요소](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#data-elements).

## 보고

보고를 사용하려면 먼저 다음 전제 조건을 완료하십시오.

* 위치 서비스 데이터를 Adobe Analytics 보고서 세트에 성공적으로 보냈습니다.

   자세한 내용은 [Adobe Analytics에서 위치 서비스 사용](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md).

* Mobile Services 보고에 익숙해지십시오.

   자세한 내용은 [보고서](https://docs.adobe.com/content/help/en/mobile-services/using/reports-ug/usage.html).

## 보고 시각화

Adobe Analytics으로 전송되는 Places Service 데이터를 사용하여 Mobile Service 보고서를 실행할 수 있습니다. 다음 예에서는 사용자가 POI 중 하나에 항목이 있을 때 이벤트가 전송됩니다. 이 보고서에서 기본 사용자 보고서를 통해 POI 항목 이벤트 필터가 추가되었습니다.

![보고서 시각화](/help/assets/report-visualize.png)

Adobe Analytics 인터페이스에서 위치 서비스 데이터를 시각화하는 데 추가적인 유연성을 사용할 수 있습니다.

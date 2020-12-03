---
title: 메시지에 Mobile Services와 Places Service 사용
description: 이 섹션에서는 메시지에 Mobile Services와 함께 Places Service를 사용하는 방법을 보여 줍니다.
translation-type: tm+mt
source-git-commit: 5a21e734c0ef56c815389a9f08b445bedaae557a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---


# Adobe Mobile Services {#places-mobile-services}

메시지에 Mobile Services 확장 기능을 사용하려면 먼저 다음 사전 요구 사항을 검토하십시오.

* 관심 영역은 장소 서비스에서 만들어졌습니다. For more information, see [Create a POI](/help/poi-mgmt-ui/create-a-poi-ui.md).

   >[!IMPORTANT]
   >
   >장소 서비스에는 기존 Mobile Services UI 외부에 있는 조직을 위한 새롭고 향상된 POI 데이터베이스가 포함되어 있습니다. Mobile Service 배치 *관리* 페이지 탐색에 있는 POI는 SDK 버전 4에서만 작동합니다.

* 이전 버전의 SDK에 *대한 이전 Mobile Services UI의 위치* 관리 페이지는 다음과 같습니다.

   ![레거시 UI](/help/assets/legacy-location-v4-ui.png)

* 위치 서비스 UI는 다음과 같습니다.

   ![서비스 POI 관리 UI 배치](/help/assets/places-ui.png)

* ACP SDK는 배치 서비스 및/또는 배치 모니터 확장 기능으로 올바르게 구성됩니다.

   즉, 데이터는 모바일 앱의 Experience Platform Launch 규칙 엔진에서 이벤트 및/또는 조건으로 사용할 수 있습니다. 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md) 또는 [위치 모니터 확장](/help/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.md)기능을 참조하십시오.

* 모바일 앱에서 ACP SDK에 Experience Platform Launch 규칙을 만들고 게시하는 것에 익숙해지십시오.

   For more information, see [Rules engine](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine).

* Experience Platform Launch 데이터 요소는 규칙 엔진에서 사용될 위치 확장 데이터에서 만들어집니다.

   For more information, see [Data elements](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#data-elements).

## 보고

보고를 사용하려면 먼저 다음 전제 조건을 완료하십시오.

* 위치 서비스 데이터를 Adobe Analytics 보고서 세트에 성공적으로 전송했습니다.

   자세한 내용은 Adobe Analytics과 함께 [장소 서비스 사용을 참조하십시오](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md).

* Mobile Services 보고에 익숙해지십시오.

   For more information, see [Reports](https://docs.adobe.com/content/help/en/mobile-services/using/reports-ug/usage.html).

## 보고 시각화

Adobe Analytics으로 전송된 장소 서비스 데이터를 사용하여 모바일 서비스 보고서를 실행할 수 있습니다. 다음 예에서는 사용자가 POI 중 하나에 항목이 있을 때 이벤트가 전송됩니다. 이 보고서에서 기본 사용자 보고서에 POI 항목 이벤트 필터가 추가되었습니다.

![보고서 시각화](/help/assets/report-visualize.png)

Places Service 데이터를 시각화하는 데 추가적인 유연성은 Adobe Analytics 인터페이스에서 사용할 수 있습니다.


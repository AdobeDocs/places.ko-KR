---
title: 메시지에 Mobile Services와 위치 서비스 사용
description: 이 섹션에서는 메시지에 위치 서비스를 사용하는 방법을 보여줍니다.
translation-type: tm+mt
source-git-commit: 5a21e734c0ef56c815389a9f08b445bedaae557a

---


# Adobe Mobile Services {#places-mobile-services}

메시지에 Mobile Services 확장을 사용하려면 먼저 다음 전제 조건을 검토하십시오.

* 위치 서비스에서 관심 영역이 만들어졌습니다. For more information, see [Create a POI](/help/poi-mgmt-ui/create-a-poi-ui.md).

   >[!IMPORTANT]
   >
   >장소 서비스에는 기존 Mobile Services UI 외부에 있는 조직에 대한 새롭고 향상된 POI 데이터베이스가 포함되어 있습니다. Mobile Service 배치 관리 *페이지 탐색에* 있는 POI는 SDK 버전 4에서만 작동합니다.

* 다음은 이전 *버전의 SDK용* 이전 Mobile Services UI의 위치 관리 페이지입니다.

   ![기존 UI](/help/assets/legacy-location-v4-ui.png)

* 위치 서비스 UI는 다음과 같습니다.

   ![서비스 POI 관리 UI 배치](/help/assets/places-ui.png)

* ACP SDK는 위치 서비스 및/또는 위치 모니터 익스텐션으로 올바르게 구성됩니다.

   즉, 데이터는 모바일 앱용 Experience Platform 시작 규칙 엔진에서 이벤트 및/또는 조건으로 사용할 수 있습니다. 자세한 내용은 위치 확장 [또는](/help/places-ext-aep-sdks/places-extension/places-extension.md) 위치 모니터 [확장](/help/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.md)기능을 참조하십시오.

* 모바일 앱의 ACP SDK에 Experience Platform 시작 규칙을 만들고 게시하는 것에 익숙해지십시오.

   For more information, see [Rules engine](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine).

* 경험 플랫폼 시작 데이터 요소는 규칙 엔진에서 사용될 위치 확장 데이터에서 만들어집니다.

   For more information, see [Data elements](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#data-elements).

## 보고

보고를 사용하려면 먼저 다음 전제 조건을 완료하십시오.

* 위치 서비스 데이터를 Adobe Analytics 보고서 세트로 전송했습니다.

   자세한 내용은 Adobe Analytics에서 [위치 서비스 사용을 참조하십시오](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md).

* Mobile Services 보고에 익숙해지십시오.

   For more information, see [Reports](https://docs.adobe.com/content/help/en/mobile-services/using/reports-ug/usage.html).

## 보고 시각화

Adobe Analytics로 전송된 위치 서비스 데이터를 사용하여 Mobile Service 보고서를 실행할 수 있습니다. 다음 예제에서는 사용자가 POI 중 하나에 항목을 입력하면 이벤트가 전송됩니다. 이 보고서에서는 기본 사용자 보고서에 POI 항목 이벤트 필터가 추가되었습니다.

![보고서 시각화](/help/assets/report-visualize.png)

Adobe Analytics 인터페이스에서 Places Service 데이터를 시각화하는 데 추가적인 유연성을 사용할 수 있습니다.


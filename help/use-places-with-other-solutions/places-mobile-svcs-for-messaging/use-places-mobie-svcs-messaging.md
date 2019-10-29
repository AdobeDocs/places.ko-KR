---
title: 메시지에 Mobile Services와 위치 사용
seo-title: 메시지에 Mobile Services와 위치 사용
description: 이 섹션에서는 메시지에 Mobile Services와 함께 위치를 사용하는 방법을 보여줍니다.
seo-description: 이 섹션에서는 메시지에 Mobile Services와 함께 위치를 사용하는 방법을 보여줍니다.
translation-type: tm+mt
source-git-commit: accfa6ba009ad3419481d9bd3b498143228099fc

---


# Adobe Mobile Services {#places-mobile-services}

메시지에 Mobile Services 확장을 사용하려면 먼저 다음 전제 조건을 검토하십시오.

* 위치 서비스에서 관심 영역이 만들어졌습니다. 필요한 경우 설명서를 참조하십시오. (POI 만들기 링크)참고:위치 서비스에는 기존 AMS 인터페이스 외부에 있는 조직에 대한 새롭고 향상된 관심 영역 데이터베이스가 포함되어 있습니다. AMS의 '위치 관리' 탐색에 있는 모든 POI는 SDK 버전 4에서만 작동합니다.
   * 다음은 이전 버전의 SDK를 위한 AMS 내의 기존 위치 POI 관리 인터페이스입니다.

      ![기존 UI](/help/assets/legacy-location-v4-ui.png)

   * 다음은 Location Service POI 관리 인터페이스입니다.

      ![위치 서비스 POI 관리 UI](/help/assets/places-ui.png)

* ACP SDK는 위치 및/또는 위치 모니터 확장 기능으로 올바르게 구성됩니다. 즉, 데이터는 모바일 앱용 Launch 규칙 엔진에서 이벤트 및/또는 조건으로 사용할 수 있습니다. 필요한 경우 설명서를 참조하십시오. (https://aep-sdks.gitbook.io/docs/beta/adobe-places)

* 모바일 앱의 ACP SDK에 Launch 규칙을 만들고 게시하는 방법에 대해 잘 알고 있습니다. 필요한 경우 설명서를 참조하십시오. (https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine)

* 시작 데이터 요소는 Places SDK 확장 데이터에서 생성되며, 이 데이터는 규칙에 사용됩니다. 설명서 참조(https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#data-elements)

## 보고

보고를 사용하려면 먼저 다음 전제 조건을 완료하십시오.

* 위치 서비스 데이터를 Adobe Analytics 보고서 세트로 전송했습니다. 필요한 경우 Adobe Analytics 설명서를 참조하십시오(Steve의 문서에 대한 링크).
* AMS 보고에 익숙합니다. 필요한 경우 설명서를 참조하십시오(https://docs.adobe.com/content/help/en/mobile-services/using/reports-ug/usage.html).

## 보고 시각화

Adobe Analytics로 전송된 위치 서비스 데이터를 사용하여 AMS 보고서를 실행할 수 있습니다. 예를 들어 사용자가 내 POI 중 하나에 항목을 가지고 있을 때 이벤트를 전송했습니다. 이 보고서에서 기본 사용자 보고서 위에 POI 항목 이벤트 필터를 추가했습니다.

![보고서 시각화](/help/assets/report-visualize.png)

Adobe Analytics 인터페이스에서 위치 서비스 데이터를 시각화하는 데 추가적인 유연성을 사용할 수 있습니다.


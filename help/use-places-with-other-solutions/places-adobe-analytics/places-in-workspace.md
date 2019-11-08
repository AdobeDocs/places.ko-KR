---
title: Analytics 작업 공간의 위치 데이터에 대한 보고서
seo-title: Analytics 작업 공간의 위치 데이터에 대한 보고서
description: 이 섹션에서는 Analytics 작업 공간에서 위치 데이터를 보고하는 방법에 대한 정보를 제공합니다.
seo-description: 이 섹션에서는 Analytics 작업 공간에서 위치 데이터를 보고하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 7609711db8b53dfbf0a387632c47133e9b9d0f07

---


# Analytics 작업 공간의 위치 데이터에 대한 보고서 {#places-in-workspace}

이 문서는 Analytics 작업 공간에서 위치 데이터를 보고하는 방법의 예를 보여줍니다. 각 단계에는 다른 문서 페이지에 대한 참조를 통해 제공된 세부 사항과 함께 수준 높은 요약이 포함됩니다.

## 전제 조건

이 문서에서는 다음 사항을 가정합니다.

1. Adobe Places 익스텐션은 애플리케이션에서 구현됩니다. Adobe Places 구현에 대한 자세한 내용은 Places [확장을](/help/places-ext-aep-sdks/places-extension/places-extension.md)참조하십시오.

1. Adobe Analytics 사용자는 관리자이며 처리 규칙에 액세스할 수 있습니다. 처리 규칙에 대한 자세한 내용은 [처리 규칙 개요](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html)를 참조하십시오.

1. 론치 속성에서 원하는 위치 서비스 변수에 대한 데이터 요소가 생성되었습니다. 론치의 데이터 요소에 대한 자세한 내용은 데이터 [요소](/help/use-places-launch-workflow/define-data-elements.md)정의를 참조하십시오.


## 1.론치 규칙 만들기

장치가 POI에 들어올 때 SDK가 Analytics로 데이터를 보내도록 하는 규칙을 만듭니다. 이러한 유형의 규칙 만들기에 대해서는 Analytics로 POI [항목 및 종료 데이터를 보냅니다](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md) .

이 예에서, 규칙의 작업은 Analytics 요청에 대해 정의된 다음 값을 가집니다.

* **[!UICONTROL Action]** 의 값이 **[!UICONTROL Places Entry]**&#x200B;제공됩니다.

* 컨텍스트 데이터 키는 데이터 요소의 값으로 **[!UICONTROL poi.name]** 설정됩니다 **[!UICONTROL {%%POI Name%%}]**.

!["작업 설정"](/help/assets/pt-setAction.png)

## 2.Analytics 변수 만들기

컨텍스트 데이터(1단계에서 전송됨)를 매핑하려면 먼저 Analytics 보고서 세트에 대해 변수를 만들어야 합니다. Analytics에서 변수를 만드는 방법에 대한 자세한 내용은 전환 [변수 \(eVar\)](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-conversion-variables-evar.html)를 참조하십시오.

이 예에서는 전환 변수가 **[!UICONTROL Evar2]**&#x200B;생성되어 이름이 **[!UICONTROL Places POI Name]**&#x200B;지정됩니다. 보고에 표시할 각 위치 변수에 대해 추가 변수를 만들어야 합니다.

!["분석 변수 만들기"](/help/assets/aa-evar.png)

## 3.처리 규칙 만들기

이 단계는 컨텍스트 데이터(1단계)를 Analytics 변수(2단계)에 매핑하는 데 필요합니다. For more information on creating processing rules, see [Processing rules overview](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

이 예에서, 컨텍스트 데이터 값을 **[!UICONTROL poi.name]** 에 매핑하기 위해 처리 규칙이 **[!UICONTROL Places POI Name \(eVar2\)]**&#x200B;만들어졌습니다. 생성된 각 위치 변수에 대해 추가 처리 규칙을 만들어야 합니다.

!["처리 규칙 만들기"](/help/assets/aa-processing-rule.png)

## 4.작업 공간에서 보고서 생성

이 단계는 1-3단계에서 수집된 데이터를 보기 위한 분석 작업 공간의 기본 보고서를 보여줍니다. Analytics 작업 공간을 사용하는 방법에 대한 자세한 내용은 Analytics 작업 [공간 개요를](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/analysis-workspace-features.html)참조하십시오.

이 예에서는 보고서에 다음 설정이 있습니다.

* Metric - **[!UICONTROL Occurrences]**

* Dimension - **[!UICONTROL Action Name]**

   * 차원별 분류 - **[!UICONTROL Places POI Name]**

!["작업 공간에서 보고서 만들기"](/help/assets/aa-workspace.png)

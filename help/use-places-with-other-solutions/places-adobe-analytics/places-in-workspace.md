---
title: Analytics Workspace의 위치 데이터에 대한 보고서
description: 이 섹션에서는 Analytics Workspace에서 위치 데이터에 대해 보고하는 방법에 대해 설명합니다.
exl-id: 45ca3c80-71b7-41de-9b00-645504061935
source-git-commit: d5c216aebd99ffef01c37c17c62576835b52438b
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---

# Analytics Workspace의 위치 데이터에 대한 보고서 {#places-in-workspace}

이 문서에서는 Analytics Workspace에서 위치 데이터에 대해 보고하는 방법의 예를 보여 줍니다. 각 단계에는 다른 설명서 페이지를 참조하여 제공되는 세부 정보와 함께 높은 수준의 요약이 포함됩니다.

## 사전 요구 사항

이 문서에서는 다음과 같은 내용을 가정합니다.

1. 위치 확장은 애플리케이션에 구현됩니다.

   위치 확장 구현에 대한 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md).

1. Adobe Analytics 사용자는 관리자이며 처리 규칙에 액세스할 수 있습니다.

   처리 규칙에 대한 자세한 내용은 [처리 규칙 개요](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html)를 참조하십시오.

1. Launch 속성에서 원하는 Places Service 변수에 대한 데이터 요소가 생성되었습니다.

   Launch의 데이터 요소에 대한 자세한 내용은 [데이터 요소 정의](/help/use-places-launch-workflow/define-data-elements.md).


## 1. Launch 규칙 만들기

디바이스가 POI에 들어갈 때 SDK가 데이터를 Analytics에 보내도록 하는 규칙을 만듭니다. 이러한 종류의 규칙을 만드는 방법은에 설명되어 있습니다 [Analytics에 POI 시작 및 종료 데이터 보내기](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md) 페이지를 가리키도록 업데이트하는 중입니다.

이 예에서 규칙의 작업에는 Analytics 요청에 대해 다음 값이 정의되어 있습니다.

* **[!UICONTROL 작업]** 다음 값이 제공됨: **[!UICONTROL 위치 항목]**.

* 컨텍스트 데이터 키 **[!UICONTROL poi.name]** 는 데이터 요소의 값으로 설정됩니다. **[!UICONTROL {%%POI 이름%}]**.

![&quot;작업 설정&quot;](/help/assets/pt-setAction.png)

## 2. Analytics 변수 만들기

컨텍스트 데이터(1단계에서 전송됨)를 매핑하려면 먼저 Analytics 보고서 세트에 대한 변수를 만들어야 합니다. Analytics에서 변수를 만드는 방법에 대한 자세한 내용은 [전환 변수 (eVar)](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html).

이 예에서는 전환 변수, **[!UICONTROL Evar2]**, 이(가) 만들어지고 이름이 지정됨 **[!UICONTROL 위치 POI 이름]**. 보고에 표시하려는 각 위치 변수에 대해 추가 변수를 만들어야 합니다.

![&quot;analytics 변수 만들기&quot;](/help/assets/aa-evar.png)

## 3. 처리 규칙 만들기

이 단계는 컨텍스트 데이터(1단계)를 Analytics 변수(2단계)에 매핑하는 데 필요합니다. 처리 규칙 만들기에 대한 자세한 내용은 [처리 규칙 개요](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html).

이 예에서는 컨텍스트 데이터 값을 매핑하는 처리 규칙이 작성되었습니다 **[!UICONTROL poi.name]** 대상 **[!UICONTROL 위치 POI 이름(eVar2)]**. 생성된 각 위치 변수에 대해 추가 처리 규칙을 생성해야 합니다.

![&quot;처리 규칙 만들기&quot;](/help/assets/aa-processing-rule.png)

## 4. 작업 영역에서 보고서 생성

이 단계에서는 1-3단계에서 수집된 데이터를 보기 위한 Analytics Workspace의 기본 보고서를 보여줍니다. Analytics Workspace를 사용하는 방법에 대한 자세한 내용은 [Analytics Workspace 개요](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html).

이 예제에서 보고서에는 다음과 같은 설정이 있습니다.

* 지표 - **[!UICONTROL 발생 횟수]**

* DIMENSION - **[!UICONTROL 작업 이름]**

   * Dimension으로 분류 - **[!UICONTROL 위치 POI 이름]**

![&quot;작업 영역에서 보고서 만들기&quot;](/help/assets/aa-workspace.png)

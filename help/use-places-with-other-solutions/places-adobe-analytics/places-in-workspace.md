---
title: Analytics 작업 공간의 위치 데이터에 대한 보고서
description: 이 섹션에서는 Analytics 작업 공간에서 위치 데이터를 보고하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 9%

---


# 분석 작업 공간의 위치 데이터에 대한 보고서 {#places-in-workspace}

이 문서에서는 Analytics 작업 공간에서 위치 데이터를 보고하는 방법의 예를 보여줍니다. 각 단계에는 다른 문서 페이지를 참조하여 제공된 세부 사항과 함께 수준 높은 요약이 포함됩니다.

## 전제 조건

이 문서에서는 다음과 같이 가정합니다.

1. 위치 확장 기능은 애플리케이션에서 구현됩니다.

   위치 확장 구현에 대한 자세한 내용은 [위치 확장을 참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

1. Adobe Analytics 사용자는 관리자이며 처리 규칙에 액세스할 수 있습니다.

   처리 규칙에 대한 자세한 내용은 [처리 규칙 개요](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules.html)를 참조하십시오.

1. 론치 속성에서 원하는 장소 서비스 변수에 대한 데이터 요소가 생성되었습니다.

   론치의 데이터 요소에 대한 자세한 내용은 데이터 요소 [정의를 참조하십시오](/help/use-places-launch-workflow/define-data-elements.md).


## 1. 론치 규칙 만들기

장치가 POI를 입력할 때 SDK가 Analytics로 데이터를 보내는 규칙을 만듭니다. 이러한 유형의 규칙 만들기에 대해서는 Analytics로 POI 항목 [보내기 및 종료 데이터를](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md) 참조하십시오.

이 예에서, 규칙의 작업은 Analytics 요청에 대해 정의된 다음 값을 가집니다.

* **[!UICONTROL Action]** 은 의 값을 제공합니다 **[!UICONTROL Places Entry]**.

* 컨텍스트 데이터 키 **[!UICONTROL poi.name]** 는 데이터 요소의 값으로 설정됩니다 **[!UICONTROL {%%POI Name%%}]**.

![&quot;작업 설정&quot;](/help/assets/pt-setAction.png)

## 2. Analytics 변수 만들기

컨텍스트 데이터를 매핑하려면(1단계에서 전송됨) 먼저 Analytics 보고서 세트에 대해 변수를 만들어야 합니다. Analytics에서 변수를 만드는 방법에 대한 자세한 내용은 [전환 변수(eVar)를 참조하십시오](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-conversion-variables-evar.html).

이 예에서 전환 변수 **[!UICONTROL Evar2]**&#x200B;는 만들어지고 이름이 지정됩니다 **[!UICONTROL Places POI Name]**. 보고에 표시할 각 위치 변수에 대해 추가 변수를 만들어야 합니다.

![&quot;analytics 변수 만들기&quot;](/help/assets/aa-evar.png)

## 3. 처리 규칙 생성

이 단계는 컨텍스트 데이터(1단계)를 Analytics 변수(2단계)에 매핑하는 데 필요합니다. For more information on creating processing rules, see [Processing rules overview](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules.html).

이 예에서는 컨텍스트 데이터 값을 매핑하기 위해 처리 규칙 **[!UICONTROL poi.name]** 이 생성되었습니다 **[!UICONTROL Places POI Name (eVar2)]**. 만들어진 각 위치 변수에 대해 추가 처리 규칙을 만들어야 합니다.

![&quot;처리 규칙 만들기&quot;](/help/assets/aa-processing-rule.png)

## 4. Workspace에서 보고서 생성

이 단계에서는 1-3단계에서 수집된 데이터를 보기 위한 분석 작업 공간의 기본 보고서를 보여줍니다. 분석 작업 공간 사용 방법에 대한 자세한 내용은 [분석 작업 공간 개요를 참조하십시오](https://docs.adobe.com/content/help/ko-KR/analytics/analyze/analysis-workspace/analysis-workspace-features.html).

이 예에서 보고서에는 다음과 같은 설정이 있습니다.

* 지표 - **[!UICONTROL Occurrences]**

* 차원 - **[!UICONTROL Action Name]**

   * Dimension으로 분류 - **[!UICONTROL Places POI Name]**

![&quot;작업 공간에서 보고서 만들기&quot;](/help/assets/aa-workspace.png)

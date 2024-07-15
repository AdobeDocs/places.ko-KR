---
title: Analytics 요청에 위치 컨텍스트 추가
description: 이 섹션에서는 Analytics 요청에 위치 컨텍스트를 추가하는 방법에 대해 설명합니다.
exl-id: bee7b6e3-a75b-4a07-b6e2-f93ce33aa042
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 1%

---

# Analytics 요청에 위치 컨텍스트 추가 {#run-reports-aa-locserv-data}

>[!IMPORTANT]
>
>이 문서에서는 애플리케이션에 Places Service가 구현되어 있다고 가정합니다. 위치 서비스 구현에 대한 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md)을 참조하세요.

Places Service에서 시작 및 종료 이벤트를 보낸 후 Experience Platform Launch에서 규칙을 만들고 Places Service 데이터를 모든 Adobe Analytics 이벤트에 첨부할 수 있습니다. 이 유형의 규칙을 만들려면 Launch에서 속성을 선택하고 다음 단계를 완료하십시오.

## 1. 규칙 만들기

1. **[!UICONTROL 규칙]** 탭에서 **[!UICONTROL 새 규칙 만들기]**&#x200B;를 클릭합니다.

   다음 정보를 숙지하십시오.
   * 이 속성에 대한 기존 규칙이 없는 경우 **[!UICONTROL 새 규칙 만들기]** 단추가 화면 중간에 표시됩니다.
   * 속성에 규칙이 있는 경우 **[!UICONTROL 새 규칙 만들기]** 단추가 화면 오른쪽 상단에 표시됩니다.

## 2. 이벤트 선택

1. 규칙 목록에서 쉽게 인식할 수 있도록 규칙에 의미 있는 이름을 지정합니다.

   이 예제에서는 규칙 이름을 **[!UICONTROL Analytics 추적 작업 이벤트에 위치 서비스 데이터 첨부]**&#x200B;로 지정합니다.

1. **[!UICONTROL 이벤트]** 섹션 아래에서 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL Mobile Core]**&#x200B;를 선택합니다.

1. **[!UICONTROL 이벤트 유형]** 드롭다운 목록에서 **[!UICONTROL 작업 추적]**&#x200B;을 선택합니다.

이제 이 규칙에 포함할 트리거를 결정할 수 있습니다. 이 예제에서 트리거는 모든 `TrackAction` 호출을 기반으로 합니다. 이벤트를 구성한 후 **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

![&quot;이벤트 만들기&quot;](/help/assets/ad-setEvent_use-analytics-data.png)


## 3. 조건 추가

>[!IMPORTANT]
>
>이 절차를 완료하여 규칙에 조건을 추가합니다. 그렇지 않으면 아래의 *작업 정의* 섹션으로 건너뜁니다.

이 예에서는 규칙이 AT&amp;T 고객에 대해서만 트리거되는 조건이 만들어집니다.

1. **[!UICONTROL 조건]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL Mobile Core]**&#x200B;를 선택합니다.

1. **[!UICONTROL 조건 유형]** 드롭다운 목록에서 **[!UICONTROL 통신사 이름]**&#x200B;을 선택합니다.

1. 오른쪽 창에서 **[!UICONTROL AT&amp;T]** 확인란을 선택합니다.

1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

![&quot;조건 만들기&quot;](/help/assets/ad-setCondition_use-analytics-data.png)

## 4. 조치 정의

1. **[!UICONTROL 작업]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL Mobile Core]**&#x200B;를 선택합니다.

1. **[!UICONTROL 작업 유형]** 드롭다운 목록에서 **[!UICONTROL 데이터 첨부]**&#x200B;를 선택합니다.

1. 오른쪽 창의 **[!UICONTROL JSON 페이로드]** 필드에 이 이벤트에 추가할 데이터를 입력하십시오.

1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

오른쪽 창에서는 SDK 이벤트에 데이터를 추가하는 자유 형식 JSON 페이로드를 추가한 후 이 이벤트를 수신 중인 확장에서 이벤트를 들을 수 있습니다. 이 예에서는 Analytics 확장이 처리하기 전에 일부 컨텍스트 데이터가 이 이벤트에 추가됩니다. 추가된 컨텍스트 데이터가 이제 나가는 Analytics 히트에 있습니다.

다음 예제에서는 `poi.city` 및 `poi.name` 값이 Analytics 이벤트의 컨텍스트 데이터에 추가됩니다. 새 키의 값은 이 이벤트가 처리될 때 SDK에 의해 동적으로 결정됩니다.

![&quot;작업 만들기&quot;](/help/assets/ad-setAction_use-analytics-data.png)

## 5. 규칙을 저장하고 속성을 다시 빌드합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![&quot;규칙이 완료되었습니다.&quot;](/help/assets/ad-ruleComplete_use-analytics-data.png)

1. **[!UICONTROL Save]**&#x200B;를 클릭합니다

1. Launch 속성을 다시 빌드하고 올바른 환경에 배포합니다.

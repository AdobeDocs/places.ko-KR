---
title: Analytics 요청에 위치 컨텍스트 추가
description: 이 섹션에서는 Analytics 요청에 위치 컨텍스트를 추가하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---


# Analytics 요청에 위치 컨텍스트 추가 {#run-reports-aa-locserv-data}

>[!IMPORTANT]
>
>이 문서에서는 사용자가 애플리케이션에서 Places Service를 구현했다고 가정합니다. 장소 서비스 구현에 대한 자세한 내용은 [장소 확장을 참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

Places Service가 시작 및 종료 이벤트를 전송하면 Experience Platform Launch에서 규칙을 만들고 Places Service 데이터를 모든 Adobe Analytics 이벤트에 첨부할 수 있습니다. 이 유형의 규칙을 만들려면 론치에서 속성을 선택하고 다음 단계를 완료하십시오.

## 1. 규칙 만들기

1. On the **[!UICONTROL Rules]** tab, click **[!UICONTROL Create New Rule]**.

   다음 정보를 숙지하십시오.
   * 이 속성에 대한 기존 규칙이 없는 경우 **[!UICONTROL Create New Rule]** 단추가 화면 가운데에 표시됩니다.
   * 속성에 규칙이 있는 경우 **[!UICONTROL Create New Rule]** 단추는 화면의 오른쪽 상단에 있습니다.

## 2.이벤트 선택

1. 규칙 목록에서 쉽게 알아볼 수 있도록 의미 있는 이름을 규칙에 지정합니다.

   이 예에서 규칙 이름은 지정됩니다 **[!UICONTROL Attach Places Service Data to Analytics Track Action Events]**.

1. Under the **[!UICONTROL Events]** section, click **[!UICONTROL Add]**.

1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

1. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Track Action]**.

이제 이 규칙에 포함할 트리거를 결정할 수 있습니다. 이 예에서 트리거는 모든 호출을 기반으로 `TrackAction` 합니다. 이벤트를 구성한 후 을 클릭합니다 **[!UICONTROL Keep Changes]**.

![&quot;이벤트 만들기&quot;](/help/assets/ad-setEvent_use-analytics-data.png)


## 3. 조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 절차를 완료하십시오. 그렇지 않은 경우 아래의 작업 *정의* 섹션으로 건너뜁니다.

이 예에서, 규칙이 AT&amp;T 고객에게만 트리거되도록 하는 조건이 만들어집니다.

1. Under the **[!UICONTROL Conditions]** section, click **[!UICONTROL Add]**.

1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

1. 드롭다운 **[!UICONTROL Condition Type]** 목록에서 선택합니다 **[!UICONTROL Carrier Name]**.

1. 오른쪽 창에서 확인란을 **[!UICONTROL AT&T]** 선택합니다.

1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

![&quot;조건 만들기&quot;](/help/assets/ad-setCondition_use-analytics-data.png)

## 4. 작업을 정의합니다.

1. Under the **[!UICONTROL Actions]** section, click **[!UICONTROL Add]**.

1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

1. 드롭다운 **[!UICONTROL Action Type]** 목록에서 선택합니다 **[!UICONTROL Attach Data]**.

1. 오른쪽 창의 **[!UICONTROL JSON Payload]** 필드에 이 이벤트에 추가할 데이터를 입력합니다.

1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

오른쪽 창에서, 이 이벤트를 수신하고 있는 확장이 이벤트를 듣기 전에 SDK 이벤트에 데이터를 추가하는 자유 형식 JSON 페이로드를 추가할 수 있습니다. 이 예에서 일부 컨텍스트 데이터는 Analytics 확장 기능이 처리 전에 이 이벤트에 추가됩니다. 추가된 컨텍스트 데이터는 이제 발신 Analytics 히트에 있습니다.

다음 예에서, `poi.city` 및 `poi.name` 값이 Analytics 이벤트의 컨텍스트 데이터에 추가됩니다. 새 키에 대한 값은 이 이벤트가 처리될 때 SDK에 의해 동적으로 결정됩니다.

![&quot;작업 만들기&quot;](/help/assets/ad-setAction_use-analytics-data.png)

## 5. 규칙을 저장하고 속성을 다시 작성합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![&quot;규칙이 완료되었습니다.&quot;](/help/assets/ad-ruleComplete_use-analytics-data.png)

1. **[!UICONTROL Save]**&#x200B;를 클릭합니다.

1. Launch 속성을 다시 빌드하고 올바른 환경에 배포합니다.

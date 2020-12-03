---
title: POI 항목 및 종료 데이터를 Analytics로 보내기
description: 이 섹션에서는 POI 시작 및 종료 데이터를 Analytics로 보내는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 2%

---


# POI 항목 및 종료 데이터를 Analytics로 보내기 {#places-data-analytics}


>[!IMPORTANT]
>
>이 섹션에서는 애플리케이션에서 배치 서비스를 구현했다고 가정합니다. 장소 서비스 구현에 대한 자세한 내용은 [장소 확장을 참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

Places Service가 시작 및 종료 이벤트를 전송하면 Experience Platform Launch에서 규칙을 만들어 Places Service 데이터를 Adobe Analytics으로 보낼 수 있습니다. 이 유형의 규칙을 만들려면 론치에서 속성을 선택하고 다음 단계를 완료하십시오.

## 1. 규칙 만들기

1. On the **[!UICONTROL Rules]** tab, click **[!UICONTROL Create New Rule]**.

   다음 정보를 숙지하십시오.

   * 이 속성에 대한 기존 규칙이 없는 경우 **[!UICONTROL Create New Rule]** 단추가 화면 가운데에 표시됩니다.
   * 속성에 규칙이 있는 경우 **[!UICONTROL Create New Rule]** 단추는 화면의 오른쪽 상단에 있습니다.

## 2. 이벤트를 선택합니다.

1. 규칙의 의미 있는 이름을 입력합니다.

   이렇게 하면 규칙 목록에서 규칙을 쉽게 인식할 수 있습니다. 이 예에서 규칙 이름은 지정됩니다 **[!UICONTROL Send Data to Analytics]**.

1. In the **[!UICONTROL Events]** section, click **[!UICONTROL Add]**.

1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places Service]**.

1. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Enter POI]**.

1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

   ![&quot;이벤트 선택&quot;](/help/assets/pt-selectEvent.png)


## 3. 조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 단계를 완료하십시오. 그렇지 않은 경우 *아래의 작업* 정의로 건너뜁니다.

이 예에서 현재 POI의 이름이 같은 경우에만 규칙이 트리거되도록 하는 조건이 만들어집니다 **[!UICONTROL My POI]**.

1. Under the **[!UICONTROL Conditions]** section, click **[!UICONTROL Add]**.

1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places Service]**.

1. 드롭다운 **[!UICONTROL Condition Type]** 목록에서 선택합니다 **[!UICONTROL Name]**.

1. 오른쪽 창의 텍스트 필드에 을 입력합니다 **[!UICONTROL My POI]**.

1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

   ![&quot;조건 설정&quot;](/help/assets/pt-setCondition.png)


## 4. 작업을 정의합니다.

1. Under the **[!UICONTROL Actions]** section, click **[!UICONTROL Add]**.

1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Adobe Analytics]**.

1. 드롭다운 **[!UICONTROL Action Type]** 목록에서 선택합니다 **[!UICONTROL Track]**.

1. 오른쪽 창에서 Analytics로 전송할 작업 또는 상태를 추가합니다.

   이 요청에 컨텍스트 데이터를 더 추가하도록 선택할 수도 있습니다. 데이터 요소를 사용하여 SDK에서 이 데이터를 동적으로 가져올 수 있습니다.

1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

   다음 예에서, 이 `TrackAction` 시작 이벤트를 트리거한 POI의 이름과 `poi.name` 동일한 추가 컨텍스트 데이터를 사용하여 Analytics로 호출이 전송됩니다.

   ![&quot;작업 설정&quot;](/help/assets/pt-setAction.png)

## 5. 규칙을 저장하고 속성을 다시 작성합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![&quot;규칙이 만들어짐&quot;](/help/assets/pt-ruleComplete.png)

1. **[!UICONTROL Save]**&#x200B;를 클릭합니다.

1. Launch 속성을 다시 빌드하고 올바른 환경에 배포합니다.

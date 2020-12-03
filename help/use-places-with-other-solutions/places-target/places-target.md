---
title: Adobe Target
description: 이 섹션에서는 Adobe Target에서 장소 서비스를 사용하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: d33e4e2d798c7048bdd275cdf6c0aabf3434f789
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---


# Adobe Target과 함께 위치 서비스 사용 {#places-target}

이 문서에서는 애플리케이션에서 위치 확장 기능을 구현했다고 가정합니다. 위치 확장 구현에 도움이 필요한 경우 위치 확장을 [참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

시작 및 종료 이벤트를 Places Extension에서 보낸 후 Launch의 규칙을 활용하여 Places Service 데이터를 Adobe Target SDK 이벤트에 첨부할 수 있습니다. 론치에서 원하는 속성을 선택한 상태에서 다음 작업을 완료하여 이 유형의 규칙을 만들 수 있습니다.

## 1. 규칙 만들기

1. On the **[!UICONTROL Rules]** tab, click **[!UICONTROL Create New Rule]**.

   다음 정보를 숙지하십시오.

   * 이 속성에 대한 기존 규칙이 없는 경우 단추가 화면 가운데에 표시됩니다.
   * 속성에 규칙이 있으면 화면의 오른쪽 상단에 단추가 표시됩니다.

## 2. 이벤트를 선택합니다.

1. 규칙 목록에서 쉽게 알아볼 수 있도록 의미 있는 이름을 규칙에 지정합니다.

   이 예에서 규칙 이름은 지정됩니다 **[!UICONTROL Attach Places Service Data to Target Content Requested]**.

1. Under the **[!UICONTROL Events]** section, click **[!UICONTROL Add]**.
1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Adobe Target]**.
1. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Content Requested]**.
1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

![이벤트 추가](/help/assets/ad-setEvent_target.png)

## 3. 조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 단계를 완료하십시오. 그렇지 않은 경우 아래 작업 *정의로* 건너뜁니다.

다음 예에서, 규칙이 앱을 5회 이상 실행한 사용자만 트리거되도록 하는 조건이 만들어집니다.

1. Under the **[!UICONTROL Conditions]** section, click **[!UICONTROL Add]**.
1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.
1. 드롭다운 **[!UICONTROL Condition Type]** 목록에서 선택합니다 **[!UICONTROL Launches]**.
1. 오른쪽 창에서 조건이 읽도록 드롭다운 목록 및 번호 컨트롤을 수정합니다 **[!UICONTROL User has launched the app greater than or equal to 5 times]**.
1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

![조건 추가](/help/assets/ad-setCondition_target.png)

## 4. 작업 정의

1. Under the **[!UICONTROL Actions]** section, click **[!UICONTROL Add]**.
1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.
1. 드롭다운 **[!UICONTROL Action Type]** 목록에서 선택합니다 **[!UICONTROL Attach Data]**.
1. 오른쪽 창의 **[!UICONTROL JSON Payload]** 필드에 이 이벤트에 추가할 데이터를 입력합니다.
1. **[!UICONTROL Keep Changes]**&#x200B;을 클릭합니다.

오른쪽 창에서, 이 이벤트에 대한 익스텐션에서 수신하기 전에 SDK 이벤트에 데이터를 추가하는 자유 형식 JSON 페이로드를 추가할 수 있습니다.

다음 예에서, `poiCity` 및 `poiName` 값은 Target 이벤트에서 처리되는 각 **[!UICONTROL mboxparameters]** 요청에 대해 추가됩니다. 새 키에 대한 값은 이 이벤트가 처리되는 시간에 SDK에 의해 동적으로 결정됩니다.

>[!TIP]
>
>이 JSON 페이로드는 개체에 대한 특수 표기법을 `request` 사용합니다. 원래 이벤트 `request` 에서는 익명 개체의 배열입니다. 데이터 첨부를 사용하여 배열의 모든 개체에 데이터를 첨부할 때, 배열이 포함된 것으로 알려진 키의 `[*]` 표기법으로 인해 페이로드가 해당 배열의 모든 개체에 적용됩니다.
>
>이 표기법은 배열에 있는 각 개체 `request[*]` 에 대해 소리내어 읽을 수 _있습니다 `request`_.

![작업 정의](/help/assets/ad-setAction-target.png)

## 5. 규칙을 저장하고 속성을 다시 작성합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![완료된 규칙](/help/assets/ad-ruleComplete-target.png)

1. **[!UICONTROL Save]**&#x200B;를 클릭합니다.
1. Launch 속성을 다시 빌드하고 올바른 환경에 배포합니다.

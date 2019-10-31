---
title: Adobe Target
seo-title: Adobe Target
description: 이 섹션에서는 Adobe Target에서 위치 서비스를 사용하는 방법에 대한 정보를 제공합니다.
seo-description: '이 섹션에서는 Adobe Target에서 위치 서비스를 사용하는 방법에 대한 정보를 제공합니다. '
translation-type: tm+mt
source-git-commit: 7ca51580a4cfa9c00431ad3972bd10e2a12dfbd1

---


# Adobe Target {#places-target}

이 문서에서는 애플리케이션에서 위치 확장을 구현했다고 가정합니다. 위치 확장 구현에 도움이 필요한 경우 위치 확장을 [참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

Places 확장 프로그램이 시작 및 종료에 대한 이벤트를 전송하면 Launch의 규칙을 활용하여 Places 데이터를 Adobe Target SDK 이벤트에 첨부할 수 있습니다. 론치에서 원하는 속성을 선택한 상태에서 다음 작업을 완료하여 이 유형의 규칙을 만들 수 있습니다.

## 1.규칙 만들기

1. 탭에서 을 **[!UICONTROL Rules]** 클릭합니다 **[!UICONTROL Create New Rule]**.

   다음 정보를 숙지하십시오.

   * 이 속성에 대한 기존 규칙이 없는 경우 이 단추는 화면 가운데에 있게 됩니다.
   * 속성에 규칙이 있는 경우 이 단추는 화면의 오른쪽 상단에 있습니다.

## 2.이벤트 선택

1. 규칙 목록에서 쉽게 알아볼 수 있도록 규칙에 의미 있는 이름을 지정합니다.

   이 예에서는 규칙의 이름이 **[!UICONTROL Attach Places Data to Target Content Requested]**&#x200B;지정됩니다.

2. 섹션에서 **[!UICONTROL Events]** 을 클릭합니다 **[!UICONTROL Add]**.

3. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Adobe Target]**.

4. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Content Requested]**.

5. 클릭 **[!UICONTROL Keep Changes]**.

![이벤트 추가](/help/assets/ad-setEvent_target.png)

## 3.조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 단계를 완료하십시오. 그렇지 않으면 *아래 작업 정의로* 건너뜁니다.

다음 예제에서는 앱을 5회 이상 실행한 사용자만 규칙이 트리거되도록 하는 조건이 만들어집니다.

1. 섹션에서 **[!UICONTROL Conditions]** 을 클릭합니다 **[!UICONTROL Add]**.

2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

3. 드롭다운 **[!UICONTROL Condition Type]** 목록에서 선택합니다 **[!UICONTROL Launches]**.

4. 오른쪽 창에서 **[!UICONTROL 사용자가 앱을 5배**&#x200B;이상 실행했다고 인식하도록 드롭다운 목록 및 번호 컨트롤을 수정합니다.

5. 클릭 **[!UICONTROL Keep Changes]**.

![이벤트 추가](/help/assets/ad-setCondition_target.png)

## 4.작업 정의

1. 섹션에서 **[!UICONTROL Actions]** 을 클릭합니다 **[!UICONTROL Add]**.

2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

3. 드롭다운 **[!UICONTROL Action Type]** 목록에서 선택합니다 **[!UICONTROL Attach Data]**.

4. 오른쪽 창의 **[!UICONTROL JSON Payload]** 필드에 이 이벤트에 추가될 데이터를 입력합니다.

5. 클릭 **[!UICONTROL Keep Changes]**.

오른쪽 창에서, 이 이벤트에 대한 익스텐션에서 수신하기 전에 SDK 이벤트에 데이터를 추가하는 자유 형식 JSON 페이로드를 추가할 수 있습니다.

다음 예에서 `poiCity` 및 `poiName` 값은 Target 이벤트에서 처리되는 각 요청에 **[!UICONTROL mboxparameters]** 대해 에 추가됩니다. 새 키에 대한 값은 이 이벤트 처리 시 SDK에서 동적으로 결정됩니다.

>[!TIP
>]
>이 JSON 페이로드에 `request` 개체에 대한 특수 표기법이 사용됩니다. 원래 이벤트에서 익명 `request` 개체의 배열입니다. 데이터 첨부를 사용하여 배열의 모든 개체에 데이터를 연결할 때 배열이 포함되어 있다고 알려진 키의 `[*]` 표기법으로 인해 페이로드가 해당 배열의 모든 개체에 적용됩니다.
>
>의 표기법은 `request[*]` 배열의 각 개체에 대해 _for으로 소리내어 읽을 `request` 수 있습니다.

![이벤트 추가](/help/assets/ad-setCondition_target.png)

## 5.규칙 저장 및 속성 다시 빌드

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![완료된 규칙](/help/assets/ad-ruleComplete_target.png)

1. 클릭 **[!UICONTROL Save]**

2. Launch 속성을 다시 빌드하여 올바른 환경에 배포합니다.

---
title: Adobe Target
description: 이 섹션에서는 Adobe Target에서 Places Service를 사용하는 방법에 대해 설명합니다.
exl-id: 6ee91fca-ea48-4de2-8dcf-87981813c678
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 3%

---

# Adobe Target에서 장소 서비스 사용 {#places-target}

이 문서에서는 사용자가 애플리케이션에 위치 확장 기능이 구현되어 있다고 가정합니다. 위치 확장 구현에 도움이 필요한 경우 다음을 참조하십시오. [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md).

위치 확장에서 시작 및 종료에 대한 이벤트를 전송한 후 Launch의 규칙을 활용하여 위치 서비스 데이터를 Adobe Target SDK 이벤트에 첨부할 수 있습니다. Launch에서 원하는 속성을 선택하면 다음 작업을 완료하여 이 유형의 규칙을 만들 수 있습니다.

## 1. 규칙 만들기

1. 다음에서 **[!UICONTROL 규칙]** 탭을 클릭하고 **[!UICONTROL 새 규칙 만들기]**.

   다음 정보를 숙지하십시오.

   * 이 속성에 대한 기존 규칙이 없는 경우 버튼이 화면 중간에 표시됩니다.
   * 속성에 규칙이 있는 경우 버튼이 화면 오른쪽 상단에 있습니다.

## 2. 이벤트 선택

1. 규칙 목록에서 쉽게 인식할 수 있도록 규칙에 의미 있는 이름을 지정합니다.

   이 예제에서 규칙 이름은 입니다 **[!UICONTROL 요청된 Target 컨텐츠에 Places Service 데이터 첨부]**.

1. 아래 **[!UICONTROL 이벤트]** 섹션, 클릭 **[!UICONTROL 추가]**.
1. 다음에서 **[!UICONTROL 확장]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL Adobe Target]**.
1. 다음에서 **[!UICONTROL 이벤트 유형]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 컨텐츠 요청됨]**.
1. **[!UICONTROL 변경사항 유지]**&#x200B;를 클릭합니다.

![이벤트 추가](/help/assets/ad-setEvent_target.png)

## 3. 조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 단계를 완료하십시오. 그렇지 않으면 *작업 정의* 아래요.

다음 예제에서는 앱을 5회 이상 시작한 사용자에 대해서만 규칙이 트리거되는 조건이 만들어집니다.

1. 아래 **[!UICONTROL 조건]** 섹션, 클릭 **[!UICONTROL 추가]**.
1. 다음에서 **[!UICONTROL 확장]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 모바일 코어]**.
1. 다음에서 **[!UICONTROL 조건 유형]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 론치]**.
1. 오른쪽 창에서 조건이 읽히도록 드롭다운 목록과 숫자 컨트롤을 수정합니다 **[!UICONTROL 사용자가 앱을 5회 이상 실행했습니다.]**.
1. **[!UICONTROL 변경사항 유지]**&#x200B;를 클릭합니다.

![조건 추가](/help/assets/ad-setCondition_target.png)

## 4. 조치 정의

1. 아래 **[!UICONTROL 작업]** 섹션, 클릭 **[!UICONTROL 추가]**.
1. 다음에서 **[!UICONTROL 확장]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 모바일 코어]**.
1. 다음에서 **[!UICONTROL 작업 유형]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 데이터 첨부]**.
1. 오른쪽 창의 **[!UICONTROL JSON 페이로드]** 필드에 이 이벤트에 추가할 데이터를 입력합니다.
1. **[!UICONTROL 변경사항 유지]**&#x200B;를 클릭합니다.

오른쪽 창에서는 이 이벤트를 수신하는 확장에서 듣기 전에 SDK 이벤트에 데이터를 추가하는 자유 형식 JSON 페이로드를 추가할 수 있습니다.

다음 예제에서는 `poiCity` 및 `poiName` 값이 다음에 추가됩니다 **[!UICONTROL mboxparameters]** Target 이벤트에서 처리되는 각 요청에 대해. 새 키의 값은 이 이벤트가 처리할 때 SDK에 의해 동적으로 결정됩니다.

>[!TIP]
>
>이 JSON 페이로드에서는 `request` 개체. 원래 이벤트에서는 `request` 는 익명 개체의 배열입니다. 데이터 첨부 를 사용하여 배열의 모든 객체에 데이터를 첨부할 때 `[*]` 배열이 포함된 것으로 알려진 키의 표기법으로 인해 페이로드가 해당 배열의 모든 개체에 적용됩니다.
>
>의 표기법 `request[*]` 다음과 같이 큰 소리로 읽을 수 있습니다. _의 각 개체에 대해 `request` 배열_.

![작업 정의](/help/assets/ad-setAction-target.png)

## 5. 규칙을 저장하고 속성을 다시 빌드합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![완료된 규칙](/help/assets/ad-ruleComplete-target.png)

1. **[!UICONTROL Save]**&#x200B;를 클릭합니다
1. Launch 속성을 다시 빌드하고 올바른 환경에 배포합니다.

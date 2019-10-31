---
title: 위치 데이터를 포함하는 Adobe Analytics에서 보고서 실행
seo-title: 위치 데이터를 포함하는 Adobe Analytics에서 보고서 실행
description: 이 섹션에서는 위치 데이터를 포함하는 Analytics에서 보고서를 실행하는 방법에 대한 정보를 제공합니다.
seo-description: 이 섹션에서는 위치 데이터를 포함하는 Analytics에서 보고서를 실행하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: a76e91775efd92ce56f2dc5cbdcc65786855b5c3

---


# 위치 데이터를 포함하는 Adobe Analytics에서 보고서 실행 {#run-reports-aa-locserv-data}

>[!IMPORTANT]
>
>이 문서에서는 애플리케이션에 Adobe Places가 구현되었다고 가정합니다. Adobe Places 구현에 대한 자세한 내용은 Places [확장을](/help/places-ext-aep-sdks/places-extension/places-extension.md)참조하십시오.

After Places가 시작 및 종료 이벤트를 전송하면 Experience Platform Launch에서 규칙을 만들고 위치 데이터를 모든 Adobe Analytics 이벤트에 첨부할 수 있습니다. 이 유형의 규칙을 만들려면 론치에서 속성을 선택하고 다음 단계를 완료하십시오.

## 1.규칙 만들기

1. 탭에서 을 **[!UICONTROL Rules]** 클릭합니다 **[!UICONTROL Create New Rule]**.

   다음 정보를 숙지하십시오.
   * 이 속성에 대한 기존 규칙이 없는 경우 **[!UICONTROL Create New Rule]** 단추가 화면 가운데에 표시됩니다.
   * 속성에 규칙이 있는 경우 **[!UICONTROL Create New Rule]** 단추는 화면의 오른쪽 상단에 있습니다.

## 1.이벤트 선택

1. 규칙 목록에서 쉽게 알아볼 수 있도록 규칙에 의미 있는 이름을 지정합니다.

   이 예에서는 규칙의 이름이 **[!UICONTROL Attach Places Data to Analytics Track Action Events]**&#x200B;지정됩니다.

2. 섹션에서 **[!UICONTROL Events]** 을 클릭합니다 **[!UICONTROL Add]**.

3. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

4. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Track Action]**.

이제 이 규칙에 포함할 트리거를 결정할 수 있습니다. 이 예에서는 트리거가 모든 `TrackAction` 호출을 기반으로 합니다. 이벤트를 구성한 후 을 클릭합니다 **[!UICONTROL Keep Changes]**.

!["이벤트 만들기"](/help/assets/ad-setEvent.png)


## 2.조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 절차를 완료하십시오. 그렇지 않은 경우 아래 작업 *정의* 섹션으로 건너뜁니다.

이 예에서는 규칙이 AT&amp;T 고객에 대해서만 트리거되도록 하는 조건이 생성됩니다.

1. 섹션에서 **[!UICONTROL Conditions]** 을 클릭합니다 **[!UICONTROL Add]**.

2. 드롭다운 **[!UICONTROL Extension]** 목록에서 모바일 **[!UICONTORL 코어를 선택합니다]**.

3. 드롭다운 **[!UICONTROL Condition Type]** 목록에서 선택합니다 **[!UICONTROL Carrier Name]**.

4. 오른쪽 창에서 **[!UICONTROL AT&T]** 확인란을 선택합니다.

5. 클릭 **[!UICONTROL Keep Changes]**.

!["조건 만들기"](/help/assets/ad-setCondition.png)

## 3.작업 정의

1. 섹션에서 **[!UICONTROL Actions]** 을 클릭합니다 **[!UICONTROL Add]**.

2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Mobile Core]**.

3. 드롭다운 **[!UICONTROL Action Type]** 목록에서 선택합니다 **[!UICONTROL Attach Data]**.

4. 오른쪽 창의 **[!UICONTROL JSON Payload]** 필드에 이 이벤트에 추가될 데이터를 입력합니다.

5. 클릭 **[!UICONTROL Keep Changes]**.

오른쪽 창에서, 이 이벤트를 수신하는 확장이 이벤트를 듣기 전에 SDK 이벤트에 데이터를 추가하는 자유 형식 JSON 페이로드를 추가할 수 있습니다. 이 예에서 일부 컨텍스트 데이터는 Analytics 확장에서 처리하기 전에 이 이벤트에 추가됩니다. 추가된 컨텍스트 데이터는 이제 나가는 Analytics 히트에 있습니다.

다음 예에서 `poi.city` 및 `poi.name` 값은 Analytics 이벤트의 컨텍스트 데이터에 추가됩니다. 새 키에 대한 값은 이 이벤트가 처리될 때 SDK에 의해 동적으로 결정됩니다.

!["작업 만들기"](/help/assets/pt-setAction.png)

## 4.규칙을 저장하고 속성을 다시 빌드합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

!["규칙이 완료되었습니다."](/help/assets/pt-ruleComplete.png)

1. 클릭 **[!UICONTROL Save]**

2. Launch 속성을 다시 빌드하여 올바른 환경에 배포합니다.

---
title: Adobe Analytics로 위치 데이터 보내기
seo-title: Adobe Analytics로 위치 데이터 보내기
description: 이 섹션에서는 위치 데이터를 Analytics로 보내는 방법에 대한 정보를 제공합니다.
seo-description: '이 섹션에서는 위치 데이터를 Analytics로 보내는 방법에 대한 정보를 제공합니다. '
translation-type: tm+mt
source-git-commit: fd98249c01fba93250dc7111798c76f3c96c6e20

---


# Adobe Analytics로 위치 데이터 보내기 {#places-data-analytics}


>[!IMPORTANT]
>
>이 문서에서는 애플리케이션에서 위치를 구현했다고 가정합니다. 위치 구현에 대한 자세한 내용은 위치 확장을 [참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

After Places가 시작 및 종료 이벤트를 전송하면 Experience Platform Launch에서 규칙을 만들어 위치 데이터를 Adobe Analytics로 보낼 수 있습니다. 이 유형의 규칙을 만들려면 론치에서 속성을 선택하고 다음 단계를 완료하십시오.

## 1.규칙 만들기

1. 탭에서 을 **[!UICONTROL Rules]** 클릭합니다 **[!UICONTROL Create New Rule]**.

   다음 정보를 숙지하십시오.

   * 이 속성에 대한 기존 규칙이 없는 경우 이 단추는 화면 가운데에 있게 됩니다.
   * 속성에 규칙이 있는 경우 이 단추는 화면의 오른쪽 상단에 있습니다.

## 2.이벤트 선택

1. 규칙 목록에서 쉽게 알아볼 수 있도록 규칙에 의미 있는 이름을 지정합니다. 이 예에서, 규칙의 이름은 Analytics로 **데이터 보내기입니다**.

2. In the **[!UICONTROL Events]** section, click **[!UICONTROL Add]**.

3. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places]**.

4. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Enter POI]**.

5. 클릭 **[!UICONTROL Keep Changes]**.

   !["이벤트 선택"](/help/assets/pt-selectEvent.png)


## 3.조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 단계를 완료하십시오. 그렇지 않으면 *아래 작업 정의로* 건너뜁니다.


이 예에서는 현재 POI의 이름이 같은 경우에만 규칙이 트리거되도록 하는 조건이 **[!UICONTROL My POI]**&#x200B;만들어집니다.

1. 섹션에서 **[!UICONTROL Conditions]** 을 클릭합니다 **[!UICONTROL Add]**.

2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places]**.

3. 드롭다운 **[!UICONTROL Condition Type]** 목록에서 선택합니다 **[!UICONTROL Name]**.

4. 오른쪽 창의 텍스트 필드에 을 입력합니다 **[!UICONTROL My POI]**.

5. 클릭 **[!UICONTROL Keep Changes]**.

   !["조건 설정"](/help/assets/ad-setCondition.png)


## 4.작업 정의

1. 섹션에서 **[!UICONTROL Actions]** 을 클릭합니다 **[!UICONTROL Add]**.

2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Adobe Analytics]**.

3. 드롭다운 **[!UICONTROL Action Type]** 목록에서 선택합니다 **[!UICONTROL Track]**.

4. 오른쪽 창에서 Analytics로 전송할 작업 또는 상태를 추가합니다. 이 요청에 컨텍스트 데이터를 더 추가하도록 선택할 수도 있습니다. 데이터 요소를 사용하여 SDK에서 이 데이터를 동적으로 가져올 수 있습니다.

5. 클릭 **[!UICONTROL Keep Changes]**.

다음 예제에서는 이 시작 이벤트를 트리거한 POI의 이름과 `TrackAction` 같은 추가 컨텍스트 데이터를 **** 사용하여 Analytics로 호출이 전송됩니다.

!["작업 설정"](/help/assets/pt-setAction.png)

## 5.규칙 저장 및 속성 다시 작성

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

!["규칙이 만들어짐"](/help/assets/pt-ruleComplete.png)


1. 클릭 **[!UICONTROL Save]**

2. Launch 속성을 다시 빌드하여 올바른 환경에 배포합니다.


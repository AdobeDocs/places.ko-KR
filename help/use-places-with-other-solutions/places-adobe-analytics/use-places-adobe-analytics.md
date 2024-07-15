---
title: Analytics에 POI 시작 및 종료 데이터 보내기
description: 이 섹션에서는 POI 시작 및 종료 데이터를 Analytics에 전송하는 방법에 대한 정보를 제공합니다.
exl-id: 69e96261-4902-47dd-a930-a8f3d19c179c
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# Analytics에 POI 시작 및 종료 데이터 보내기 {#places-data-analytics}


>[!IMPORTANT]
>
>이 섹션에서는 사용자가 애플리케이션에 Places Service가 구현되어 있다고 가정합니다. 위치 서비스 구현에 대한 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md)을 참조하세요.

Places Service에서 시작 및 종료 이벤트를 보낸 후 Experience Platform Launch에서 규칙을 만들어 Places Service 데이터를 Adobe Analytics으로 보낼 수 있습니다. 이 유형의 규칙을 만들려면 Launch에서 속성을 선택하고 다음 단계를 완료하십시오.

## 1. 규칙 만들기

1. **[!UICONTROL 규칙]** 탭에서 **[!UICONTROL 새 규칙 만들기]**&#x200B;를 클릭합니다.

   다음 정보를 숙지하십시오.

   * 이 속성에 대한 기존 규칙이 없는 경우 **[!UICONTROL 새 규칙 만들기]** 단추가 화면 중간에 표시됩니다.
   * 속성에 규칙이 있는 경우 **[!UICONTROL 새 규칙 만들기]** 단추가 화면 오른쪽 상단에 표시됩니다.

## 2. 이벤트 선택

1. 규칙에 의미 있는 이름을 입력합니다.

   이렇게 하면 규칙 목록에서 규칙을 쉽게 인식할 수 있습니다. 이 예제에서 규칙 이름은 **[!UICONTROL Analytics에 데이터 보내기]**&#x200B;입니다.

1. **[!UICONTROL 이벤트]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL 장소 서비스]**&#x200B;를 선택합니다.

1. **[!UICONTROL 이벤트 유형]** 드롭다운 목록에서 **[!UICONTROL POI 입력]**&#x200B;을 선택합니다.

1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

   ![&quot;이벤트 선택&quot;](/help/assets/pt-selectEvent.png)


## 3. 조건 추가

>[!IMPORTANT]
>
>규칙에 조건을 추가하려면 이 단계를 완료하십시오. 그렇지 않으면 아래의 *작업 정의*&#x200B;로 건너뜁니다.

이 예제에서는 현재 POI의 이름이 **[!UICONTROL 내 POI]**&#x200B;인 경우에만 규칙이 트리거되도록 하는 조건이 만들어집니다.

1. **[!UICONTROL 조건]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL 장소 서비스]**&#x200B;를 선택합니다.

1. **[!UICONTROL 조건 유형]** 드롭다운 목록에서 **[!UICONTROL 이름]**&#x200B;을(를) 선택합니다.

1. 오른쪽 창의 텍스트 필드에 **[!UICONTROL 내 POI]**&#x200B;를 입력합니다.

1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

   ![&quot;조건 설정&quot;](/help/assets/pt-setCondition.png)


## 4. 조치 정의

1. **[!UICONTROL 작업]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL Adobe Analytics]**&#x200B;을(를) 선택합니다.

1. **[!UICONTROL 작업 유형]** 드롭다운 목록에서 **[!UICONTROL 추적]**&#x200B;을 선택합니다.

1. 오른쪽 창에서 Analytics에 전송할 작업 또는 상태를 추가합니다.

   이 요청에 추가 컨텍스트 데이터를 추가하도록 선택할 수도 있습니다. 데이터 요소를 사용하여 SDK에서 이 데이터를 동적으로 가져올 수 있습니다.

1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

   다음 예제에서는 이 항목 이벤트를 트리거한 POI의 이름과 같은 `poi.name`의 추가 컨텍스트 데이터와 함께 `TrackAction` 호출이 Analytics로 전송됩니다.

   ![&quot;동작 설정&quot;](/help/assets/pt-setAction.png)

## 5. 규칙을 저장하고 속성을 다시 빌드합니다.

구성을 완료한 후 규칙이 다음 이미지와 같은지 확인합니다.

![&quot;규칙이 만들어짐&quot;](/help/assets/pt-ruleComplete.png)

1. **[!UICONTROL Save]**&#x200B;를 클릭합니다

1. Launch 속성을 다시 빌드하고 올바른 환경에 배포합니다.

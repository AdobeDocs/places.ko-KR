---
title: Places Service 속성에 대한 규칙 만들기
description: 위치 SDK는 현재 위치를 추적하고, 현재 위치 주변에 구성된 POI를 모니터링하고, 이러한 POI에 대한 시작 및 종료 이벤트를 추적합니다.
exl-id: dd5aa7ac-55f9-44dc-8632-e483ef3b91a0
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 15%

---

# 시작 및 종료 규칙 만들기 {#create-entry-exit-rules}

모바일 애플리케이션에 설치된 위치 확장 및 지역 모니터링 솔루션을 사용하면 위치 시작 및 종료 이벤트를 포함하여 위치 데이터를 트리거하거나 조건화한 규칙을 Adobe Experience Platform Launch에서 만들 수 있습니다.

## 규칙

이벤트, 조건 및 작업으로 구성된 규칙을 구성할 수 있습니다. 각 규칙은 다음과 같이 구성됩니다.

* 하나 이상의 이벤트
* (선택 사항) 조건
* 하나 이상의 작업

### 위치 서비스 이벤트

위치 서비스는 규칙을 실행할 수 있는 다음 이벤트를 제공합니다.

* **POI 입력**: 고객이 구성한 POI를 입력할 때 위치 SDK에 의해 트리거됩니다.
* **POI 종료**: 고객이 구성한 POI를 종료할 때 위치 SDK에 의해 트리거됩니다.

### Places 서비스 조건

조건은 작업을 수행하기 위해 이벤트와 연결된 데이터 또는 해당 인스턴스에서 확장의 공유 상태가 충족해야 하는 기준을 정의합니다. 예를 들어, 샌프란시스코 시에만 있는 커피숍 입구에서 작업을 트리거하는 조건을 설정할 수 있습니다.

위치 SDK는 다음 상태를 유지 관리합니다.

* 현재 POI: 고객이 현재 위치한 POI를 가리킵니다.
* 마지막으로 종료한 POI: 고객이 종료한 가장 최근 POI를 가리킵니다.
* 마지막으로 입력한 POI(고객이 입력한 POI 중 가장 최근 POI를 나타냄)

각 POI에는 다음 데이터 요소가 포함되어 있습니다.

* ID
* 이름
* 위도/경도
* 반경
* 도시, 국가, 주, 범주 등 메타데이터

### 작업

작업은 실행된 이벤트에 대한 규칙 조건이 충족되면 앱에서 응답하는 작업을 정의합니다. 예를 들어 고객이 POI를 입력할 때 모바일 장치에 표시할 시작 메시지를 구성할 수 있습니다.

## 규칙 만들기: 예

>[!CAUTION]
>
>이 예에서는 사용자가 미국의 모든 커피숍에 대한 POI 라이브러리를 생성한 것으로 가정합니다. POI 및 라이브러리 생성에 대한 자세한 내용은 [POI 만들기](/help/poi-mgmt-ui/create-a-poi-ui.md) 및 *라이브러리 만들기* 위치: [여러 라이브러리 관리](https://docs.adobe.com/content/help/en/places/using/poi-mgmt-ui/manage-libraries-in-the-places-ui.html).

다음 절차는 San Francisco에서 커피숍에 들어갈 때 Slack에게 다시 게시물을 보내는 규칙을 만드는 방법의 예입니다.

이벤트, 조건 및 작업은 다음 방법으로 정의됩니다.

* **이벤트**: 시작 이벤트를 배치합니다.
* **조건**: **현재 POI**&#x200B;를 위한 도시는 샌프란시스코임
* **작업**: 고객이 입력한 커피숍의 이름을 Slack 하기 위해 포스트백을 보냅니다.

### 전제 조건

규칙을 만들기 전에 Adobe Experience Platform Launch에서 데이터 요소를 만들어야 합니다. 데이터 요소는 포스트백 메시지에서 POI에 대해 필요한 정보를 자동으로 채웁니다.

Experience Platform Launch에서 데이터 요소를 만들려면 다음을 수행하십시오.

1. 다음을 클릭합니다. **데이터 요소** 탭.
1. 클릭 **데이터 요소 추가**.
1. 이름을 입력합니다(예: ). **현재 커피숍 이름**.
1. 다음에서 **확장** 드롭다운 목록에서 다음을 선택합니다. **장소 - Beta**.
1. **데이터 요소**&#x200B;에서 **구/군/시**&#x200B;를 선택합니다.
1. 오른쪽 창에서 을(를) 선택합니다 **현재 POI**.
1. **저장**&#x200B;을 클릭합니다.

### Places Service Experience Platform Launch에 규칙 만들기

![규칙 만들기](/help/assets/placesrule.png)

1. Experience Platform Launch에서 **[!UICONTROL 규칙]**&#x200B;탭을 클릭합니다.
1. **[!UICONTROL 규칙 추가]**&#x200B;를 클릭합니다.
1. 규칙의 이름을 입력합니다(예: ). **[!UICONTROL SF에서 커피숍 항목 추적]**.

### 이벤트를 만듭니다

1. 이벤트 섹션에서 다음을 클릭합니다. **[!UICONTROL + 추가]**. 이벤트는 규칙을 언제 실행할지 결정합니다.
1. 다음에서 **[!UICONTROL 확장]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 장소 - Beta]**.
1. **[!UICONTROL 이벤트 유형]** 드롭다운 목록에서 **[!UICONTROL POI 입력]**&#x200B;을 선택합니다.
1. **[!UICONTROL 이름]**&#x200B;에 이벤트의 이름을 입력합니다(예: **[!UICONTROL 커피숍 입력]**).
1. **[!UICONTROL 변경사항 유지]**&#x200B;를 클릭합니다.

### 조건 만들기

1. Conditions 섹션에서 다음을 클릭합니다. **[!UICONTROL +추가]**. 조건은 수행할 작업에 대해 어떤 기준을 충족해야 하는지 결정합니다.
1. **[!UICONTROL 논리 유형]**&#x200B;에서 일반을 선택합니다. 그러면 조건이 충족되는 경우 작업을 실행할 수 있습니다.
1. 다음에서 **[!UICONTROL 확장]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 장소 - Beta]**.
1. **[!UICONTROL 조건 유형]**&#x200B;에서 **[!UICONTROL 구/군/시]**&#x200B;를 선택합니다.
1. 조건 이름을 입력합니다(예: ). **[!UICONTROL 커피숍]**.
1. 오른쪽 창에서 **[!UICONTROL 현재 POI]**&#x200B;를 클릭하고 드롭다운 목록에서 **[!UICONTROL 샌프란시스코]**&#x200B;를 도시 중 하나로 선택합니다.
1. **[!UICONTROL 변경사항 유지]**&#x200B;를 클릭합니다.

### 동작 만들기

1. 다음에서 **[!UICONTROL 작업]** 섹션, 클릭 **[!UICONTROL + 추가]**.
1. 다음에서 **[!UICONTROL 확장]** 드롭다운 목록에서 기본값을 그대로 둡니다. **[!UICONTROL 모바일 코어]** 옵션이 선택되었습니다.
1. 다음과 같은 작업 유형을 선택합니다. **[!UICONTROL 포스트백 보내기]**.

   a. 의 **[!UICONTROL URL]**, Slack에 대한 포스트백 URL을 입력합니다(예: ). `https://hooks.slack.com/services/`.

   b. 게시물 본문을 보내려면 **[!UICONTROL 게시물 본문 추가]** 확인란.

   c. 시작 **[!UICONTROL 게시물 본문]**&#x200B;게시물 본문을 추가합니다. 예: `{ "text": "A customer has entered" }`

   c. 예를 들어 컨텐츠 유형을 입력합니다 **[!UICONTROL application/json]**.

   d. 시간 초과 값(예: ) 선택 **[!UICONTROL 5]**.

1. **[!UICONTROL 변경사항 유지]**&#x200B;를 클릭합니다.

### 규칙 게시

1. 규칙을 활성화하려면 게시해야 합니다. Experience Platform Launch에 규칙을 게시하는 방법에 대한 자세한 내용은 [게시](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/overview.html).

### 시작 및 종료 이상의 사고

Places Service 지오펜스 시작 및 종료로 Experience Platform Launch에서 규칙을 트리거하는 방법은 매우 강력하지만 위치 데이터를 다른 이벤트가 실행되는 조건으로 사용할 수도 있습니다. 예를 들어 앱 내의 특정 trackAction 호출 이벤트를 기반으로 Mobile Core Track Action 이벤트 트리거를 실행할 준비가 되도록 할 수 있습니다. 이 이벤트를 기반으로 작업을 수행하기 전에 이벤트에 추가 위치 조건을 배치할 수 있습니다. 예를 들어 구매 시 인앱 설문 조사를 엽니다 `trackAction` 이벤트가 발생하지만 **전용** 사용자의 현재 위치에 특정 위치 서비스 메타데이터가 포함된 경우.

![조건 만들기](/help/assets/places-condition.png)

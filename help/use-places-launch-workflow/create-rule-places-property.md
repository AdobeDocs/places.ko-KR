---
title: 위치 속성에 대한 규칙 만들기
seo-title: 위치 속성에 대한 규칙 만들기
description: '위치 SDK는 현재 위치를 추적하고, 현재 위치에 대해 구성된 POI를 모니터링하며, 이러한 POI에 대한 시작 및 종료 이벤트를 추적합니다. '
seo-description: '위치 SDK는 현재 위치를 추적하고, 현재 위치에 대해 구성된 POI를 모니터링하며, 이러한 POI에 대한 시작 및 종료 이벤트를 추적합니다. '
translation-type: tm+mt
source-git-commit: 84b23934a6e9f9fd61c068693bae3daca24de253

---


# 시작 및 종료 규칙 만들기 {#create-entry-exit-rules}

모바일 애플리케이션에 위치 및 위치 모니터 확장 기능이 설치되어 있는 경우 Adobe Experience Platform Launch에서 위치 시작 및 종료 이벤트를 비롯한 위치 데이터를 트리거하거나 조건부로 지정한 규칙을 만들 수 있습니다.

## 규칙

이벤트, 조건 및 작업으로 구성된 규칙을 구성할 수 있습니다. 각 규칙은 다음과 같이 구성됩니다.

* 하나 이상의 이벤트
* (선택 사항) 조건
* 하나 이상의 작업

### 이벤트 배치

규칙을 실행할 수 있는 다음 이벤트를 제공합니다.

* **POI를**&#x200B;입력합니다. 이 POI는 고객이 구성한 POI에 들어올 때 위치 SDK에 의해 트리거됩니다.
* **POI를**&#x200B;종료합니다. POI는 고객이 구성된 POI를 종료할 때 위치 SDK에 의해 트리거됩니다.

### 위치 조건

조건은 이벤트와 연관된 데이터 또는 해당 인스턴스의 확장 기능의 공유 상태가 작업을 수행하기 위해 충족해야 하는 기준을 정의합니다. 예를 들어 조건이 설정되면 샌프란시스코 시에만 있는 커피숍에 대한 입장 작업을 트리거할 수 있습니다.

위치 SDK는 다음 상태를 유지합니다.

* 현재 POI로, 고객이 현재 있는 POI를 나타냅니다.
* 마지막으로 종료한 POI는 고객이 종료한 가장 최근 POI를 나타냅니다.
* 마지막으로 입력한 POI는 고객이 입력한 최신 POI를 의미합니다.

각 POI에는 다음 데이터 요소가 포함되어 있습니다.

* ID
* 이름:
* 위도/경도
* 반경
* 도시, 국가, 주, 카테고리 등의 메타데이터

### 작업

작업은 실행된 이벤트에 대한 규칙의 조건에 응답하여 앱이 수행할 작업을 정의합니다. 예를 들어 고객이 POI에 입장할 때 해당 모바일 장치에 표시할 환영 메시지를 구성할 수 있습니다.

## 규칙 만들기:예

>[!CAUTION]
>
>이 예에서는 미국의 모든 커피숍의 POI 라이브러리를 만들었다고 가정합니다. POI 및 라이브러리 만들기에 대한 자세한 내용은 [POI 만들기](/help/poi-mgmt-ui/create-a-poi-ui.md) 및 *여러 라이브러리* 관리에서 라이브러리 [만들기를](https://docs.adobe.com/content/help/en/places/using/poi-mgmt-ui/manage-libraries-in-the-places-ui.html)참조하십시오.

다음 절차는 샌프란시스코에 커피숍에 들어갈 때 Slack으로 다시 게시물을 보내는 규칙을 만드는 방법의 예입니다.

이벤트, 조건 및 작업은 다음과 같은 방법으로 정의됩니다.

* **이벤트**:응모 이벤트를 배치합니다.
* **조건**:현재 POI를 **위한** 도시는 샌프란시스코
* **작업**:고객이 입력한 커피숍 이름을 Slack으로 포스트백을 보내십시오.

### 전제 조건

규칙을 만들기 전에 Adobe Experience Platform Launch에서 데이터 요소를 만들어야 합니다. 데이터 요소는 포스트백 메시지에 POI에 대한 필요한 정보를 자동으로 채웁니다.

경험 플랫폼 론치에서 데이터 요소를 만들려면:

1. 데이터 요소 **탭을** 클릭합니다.
2. Click **Add Data Element**.
3. 예를 들어 현재 커피숍 **이름과**&#x200B;같은 이름을 입력합니다.
4. 확장 **프로그램** 드롭다운 목록에서 위치 - 베타 **를 선택합니다**.
5. 데이터 **요소에서**&#x200B;시를 **선택합니다**.
6. 오른쪽 창에서 현재 POI를 **선택합니다**.
7. **저장**&#x200B;을 클릭합니다.

### Experience Platform Launch for Places에서 규칙 만들기

![규칙 만들기](/help/assets/placesrule.png)

1. 경험 플랫폼 론치에서 **[!UICONTROL Rules]** 탭을 클릭합니다.
2. 클릭 **[!UICONTROL Add Rule]**.
3. 예를 들어 규칙의 이름을 입력합니다 **[!UICONTROL Track entry for coffee shop in SF]**.

### 이벤트를 만듭니다

1. 이벤트 섹션에서 을 클릭합니다 **[!UICONTROL + Add]**. 이벤트는 규칙을 실행할 시기를 결정합니다.
2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places – Beta]**.
3. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Enter POI]**.
4. 에서 **[!UICONTROL Name]**&#x200B;이벤트의 이름을 입력합니다(예: **[!UICONTROL Entering a coffee shop]**).
5. 클릭 **[!UICONTROL Keep Changes]**.

### 조건 만들기

1. 조건 섹션에서 을 **[!UICONTROL +Add]**&#x200B;클릭합니다. 조건은 수행할 작업에 대해 충족해야 하는 기준을 결정합니다.
2. 에서 **[!UICONTROL Logic Type]**&#x200B;조건이 충족되는 경우 작업을 실행할 수 있도록 하는 [일반]을 선택합니다.
3. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places – Beta]**.
4. 에서 **[!UICONTROL Condition Type]**&#x200B;을 선택합니다 **[!UICONTROL City]**.
5. Type a condition name, for example, **[!UICONTROL Coffee shop in SF]**.
6. 오른쪽 창에서 을 클릭하고 **[!UICONTROL Current POI]**&#x200B;드롭다운 목록에서 도시 **[!UICONTROL San Francisco]** 중 하나로 선택합니다.
7. 클릭 **[!UICONTROL Keep Changes]**.

### 동작 만들기

1. In the **[!UICONTROL Actions]** section, click **[!UICONTROL + Add]**.
2. 드롭다운 **[!UICONTROL Extension]** 목록에서 기본 **[!UICONTROL Mobile Core]** 옵션을 선택된 상태로 둡니다.
3. 작업 유형(예: )을 선택합니다 **[!UICONTROL Send Postback]**.

   a.에서 **[!UICONTROL URL]** Slack의 포스트백 URL을 입력합니다(예: `https://hooks.slack.com/services/`).

   b.게시물 본문을 전송하려면 **[!UICONTROL Add Post Body]** 확인란을 선택합니다.

   c.에서 게시물 본문을 **[!UICONTROL Post Body]**&#x200B;추가합니다(예: `{ "text": "A customer has entered" }`

   c.예를 들어 컨텐츠 유형을 입력합니다 **[!UICONTROL application/json]**.

   d.시간 초과 값(예: )을 선택합니다 **[!UICONTROL 5]**.

4. 클릭 **[!UICONTROL Keep Changes]**.

### 규칙 게시

1. 규칙을 활성화하려면 게시해야 합니다. Experience Platform Launch에서 규칙 게시에 대한 자세한 내용은 게시를 [참조하십시오](https://docs.adobelaunch.com/launch-reference/publishing).

### 입장 및 종료 이상의 사고

위치 서비스 geo-fence 항목 및 종료를 사용하여 Experience Platform Launch의 규칙을 트리거하는 것은 매우 강력하지만, 위치 데이터를 다른 이벤트를 실행하기 위한 조건으로 사용할 수도 있습니다. 예를 들어 앱 내의 특정 trackAction 호출 이벤트를 기반으로 모바일 코어 추적 동작 이벤트 트리거를 실행할 수 있습니다. 이 이벤트를 기반으로, 작업이 수행되기 전에 이벤트에 추가 위치 조건을 배치할 수 있습니다. 예를 들어 구매 `trackAction` 이벤트가 발생하면 인앱 설문 조사를 열지만 사용자의 현재 위치에 특정 위치 서비스 메타데이터가 포함된 **경우에만** 열 수 있습니다.

![조건 만들기](/help/assets/places-condition.png)
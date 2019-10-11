---
title: 위치 속성에 대한 규칙 만들기
seo-title: 위치 속성에 대한 규칙 만들기
description: '위치 SDK는 현재 위치를 추적하고, 현재 위치에 대해 구성된 POI를 모니터링하며, 이러한 POI에 대한 시작 및 종료 이벤트를 추적합니다. '
seo-description: '위치 SDK는 현재 위치를 추적하고, 현재 위치에 대해 구성된 POI를 모니터링하며, 이러한 POI에 대한 시작 및 종료 이벤트를 추적합니다. '
translation-type: tm+mt
source-git-commit: ef3d77eba407013e1f701ed001ef9ab7b3818e07

---


# 위치 속성에 대한 규칙 만들기 {#creating-rule-places-property}

위치 서비스 SDK는 현재 위치를 추적하고, 현재 위치에 대해 구성된 POI를 모니터링하며, 이러한 POI에 대한 시작 및 종료 이벤트를 추적합니다.

## 규칙

이벤트, 조건 및 작업으로 구성된 규칙을 구성할 수 있습니다. 각 규칙은 다음과 같이 구성됩니다.

* 하나 이상의 이벤트
* (선택 사항) 조건
* 하나 이상의 작업

### 이벤트

규칙을 실행할 수 있는 다음 이벤트를 제공합니다.

* **[!UICONTROL Enter POI]**&#x200B;를 설정하는 것이 좋습니다.
* **[!UICONTROL Exit POI]**&#x200B;로 설정되는 URL을 표시합니다.

### 조건

조건은 이벤트와 연관된 데이터 또는 해당 인스턴스의 확장 기능의 공유 상태가 작업을 수행하기 위해 충족해야 하는 기준을 정의합니다. 예를 들어 조건이 설정되면 샌프란시스코 시에만 있는 커피숍에 대한 입장 작업을 트리거할 수 있습니다.

위치 서비스 SDK는 다음 상태를 유지합니다.

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
>이 예에서는 미국의 모든 커피숍의 POI 라이브러리를 만들었다고 가정합니다. POI 및 라이브러리 만들기에 대한 자세한 내용은 POI [만들기](https://placesdocs.com/places-services-by-adobe-documentation/places-database-management-1/managing-pois-in-the-places-ui#create-a-poi) 및 라이브러리 [만들기를 참조하십시오](https://placesdocs.com/places-services-by-adobe-documentation/places-database-management-1/manage-libraries#create-a-library).

다음 절차는 샌프란시스코에 커피숍에 들어갈 때 Slack으로 다시 게시물을 보내는 규칙을 만드는 방법의 예입니다.

이벤트, 조건 및 작업은 다음과 같은 방법으로 정의됩니다.

* **이벤트**:위치 서비스 시작 이벤트.
* **조건**:현재 POI를 **위한** 도시는 샌프란시스코
* **작업**:고객이 입력한 커피숍 이름을 Slack으로 포스트백을 보내십시오.

### 전제 조건

규칙을 만들기 전에 경험 플랫폼 론치에서 데이터 요소를 만들어야 합니다. 데이터 요소는 포스트백 메시지에 POI에 대한 필요한 정보를 자동으로 채웁니다.

경험 플랫폼 론치에서 데이터 요소를 만들려면:

1. Click the **[!UICONTROL Data Elements]** tab.
2. 클릭 **[!UICONTROL Add Data Element]**.
3. Type a name, for example, **[!UICONTROL Current coffee shop name]**.
4. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places – Beta]**.
5. 에서 **[!UICONTROL Data Element]**&#x200B;을 선택합니다 **[!UICONTROL City]**.
6. 오른쪽 창에서 현재 POI를 **선택합니다**.
7. 클릭 **[!UICONTROL Save]**.

### Experience Platform Launch for Location Service에서 규칙 만들기

![](//help/assets/create-a-rule.png)

1. 경험 플랫폼 론치에서 **[!UICONTROL Rules]** 탭을 클릭합니다.
2. Click **Add Rule**.
3. 규칙 이름(예: SF의 **커피숍용 트랙 항목)을 입력합니다**.

### 이벤트를 만듭니다

1. 이벤트 섹션에서 을 클릭합니다 **[!UICONTROL + Add]**. 이벤트는 규칙을 실행할 시기를 결정합니다.
2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places – Beta]**.
3. 드롭다운 **[!UICONTROL Event Type]** 목록에서 선택합니다 **[!UICONTROL Enter POI]**.
4. 에서 **[!UICONTROL Name]**&#x200B;이벤트의 이름을 입력합니다(예: **[!UICONTROL Entering a coffee shop]**).
5. 클릭 **[!UICONTROL Keep Changes]**.

### 조건 만들기

1. 조건 섹션에서 을 **[!UICONTROL +Add]**&#x200B;클릭합니다. 조건은 수행할 작업에 대해 충족해야 하는 기준을 결정합니다.
2. 에서 **[!UICONTROL Logic Type]**&#x200B;조건이 충족되는 경우 작업을 실행할 수 있도록 하는 [일반]을 선택합니다.
3. 확장 **프로그램** 드롭다운 목록에서 을 선택합니다 **[!UICONTROL Places – Beta]**.
4. 에서 **[!UICONTROL Condition Type]**&#x200B;을 선택합니다 **[!UICONTROL City]**.
5. Type a condition name, for example, **[!UICONTROL Coffee shop in SF]**.
6. 오른쪽 창에서 을 클릭하고 **[!UICONTROL Current POI]**&#x200B;드롭다운 목록에서 도시 **[!UICONTROL San Francisco]** 중 하나로 선택합니다.
7. 클릭 **[!UICONTROL Keep Changes]**.

### 동작 만들기

1. 섹션에서 **[!UICONTROL Actions]** + 추가를 **[!UICONTRO클릭합니다]**.
2. 확장 **[!UICONTRO 기능]** 드롭다운 목록에서 기본 모바일 코어 **[!UICONTRO 옵션을]** 선택한 상태로 둡니다.
3. 작업 유형(예: 포스트백 보내기) **[!UICONTRO 을 선택합니다]**.

   a.에서 **[!UICONTROL URL]** Slack의 포스트백 URL을 입력합니다(예: `https://hooks.slack.com/services/`).

   b.게시물 본문을 전송하려면 게시물 본문 **[!UICONTRO 추가 확인란을]** 선택합니다.

   c.게시물 **[!UICONTRO 본문에]**&#x200B;게시물 본문을 추가합니다. 예: `{ "text": "A customer has entered" }`

   c.컨텐츠 유형(예: **[!UICONTRO application/json]**)을 입력합니다.

   d.시간 초과 값(예: **5**)을 선택합니다.

4. Click **[!UICONTRO Keep Changes]**.

### 규칙 게시

1. 규칙을 활성화하려면 게시해야 합니다. Experience Platform Launch에서 규칙 게시에 대한 자세한 내용은 게시를 [참조하십시오](https://docs.adobelaunch.com/launch-reference/publishing).
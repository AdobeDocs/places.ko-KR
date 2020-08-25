---
title: Places 서비스를 사용한 푸시 알림
description: 이 섹션에서는 Campaign Standard에서 푸시 알림과 함께 Places Service를 사용하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: fd469358845e14c47a58b40bb18c9144828a8996
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---


# Places 서비스를 사용한 푸시 알림 {#push-notifications}

이 섹션에서는 내역 위치 정보를 사용하여 Adobe Campaign Standard을 통해 전달되는 푸시 알림을 타깃팅하는 방법을 알아봅니다.

## 전제 조건

시작하기 전에 다음 작업을 완료하십시오.

* 모바일 애플리케이션이 [Adobe Campaign Standard 확장 기능을 포함하여 Adobe Experience Platform Mobile SDK로 구성되어 있어야 합니다](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard).

* 앱에 [Adobe Experience Platform Mobile SDK를](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) 통합합니다.
* 모바일 앱 구성에 [Adobe Campaign Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) 익스텐션을 추가합니다.

* [Places Service](/help/poi-mgmt-ui/create-a-poi-ui.md) POI 관리 인터페이스에서 POI를 만듭니다.

* 위치 확장 기능을 [활성화하고 설치합니다](/help/places-ext-aep-sdks/places-extension/places-extension.md).


## Experience Platform Launch에서 데이터 요소 만들기

애플리케이션에서 위치 확장 및 위치 모니터 확장 기능이 제대로 작동하는지 확인한 후 Experience Platform Launch에서 데이터 요소를 만들어야 합니다. 데이터 요소를 사용하면 Mobile SDK 이벤트 허브를 통해 제공되는 익스텐션에서 제공한 정보를 읽을 수 있으며 클라이언트 애플리케이션에서 데이터를 검색할 별칭으로 사용할 수 있습니다. 장소 확장 기능에서 데이터를 검색하고 장소 서비스 정보를 캠페인에 보내려면 몇 개의 데이터 요소를 만들어야 합니다.

데이터 요소를 만들려면:

1. Experience Platform Launch 모바일 속성에서 **[!UICONTROL Data Elements]** 탭을 클릭하고 을 클릭합니다 **[!UICONTROL Add Data Element]**.
1. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places Service]**.
1. 드롭다운 **[!UICONTROL Data Element Type]** 목록에서 선택합니다 **[!UICONTROL Name]**.
1. 오른쪽 창에서 사용자가 현재 있는 POI **[!UICONTROL Current POI]** 의 이름을 검색하는 항목을 선택할 수 있습니다.

   **[!UICONTROL Last Entered]** 사용자가 마지막으로 입력한 POI의 이름을 검색하고 사용자가 마지막으로 남긴 POI의 이름을 **[!UICONTROL Last Exited]** 제공합니다. 이 예에서는 데이터 요소 **[!UICONTROL Last Entered]** 의 이름(예: 클릭 **[!UICONTROL Last Entered POI Name]** 및 클릭)을 선택하고 입력했습니다 **[!UICONTROL Save]**.

   ![&quot;Campaign Standard의 푸시 메시지&quot;](/help/assets/ACS_Push1.png)

1. Repeat the steps 1-4 above and create data elements for *Last Entered POI Latitude*, *Last Entered POI Longitude*, and *Last Entered POI Radius*.

장소 서비스에 대한 데이터 요소 외에 *앱 ID* 및 *Experience Cloud ID에 대한 모바일 코어 데이터 요소를 만들어야 합니다*.

## 위치 데이터를 Adobe Campaign Standard으로 보내는 규칙 만들기

Experience Platform Launch의 규칙을 사용하면 이벤트 트리거를 기반으로 복잡한 다중 솔루션 워크플로우를 만들 수 있습니다. 규칙을 사용하여 새 규칙을 만들거나 기존 규칙을 수정할 수 있으며 업데이트를 모바일 애플리케이션에 동적으로 배포할 수 있습니다. 다음 예에서, 사용자가 지리적 제약을 받는 POI에 들어갈 때 규칙이 트리거됩니다. 규칙이 트리거되면 Experience Cloud ID를 기반으로 특정 사용자에 대한 특정 POI에 대한 항목을 기록하기 위한 업데이트가 Campaign Standard으로 전송됩니다.

1. Experience Platform Launch 모바일 속성의 **[!UICONTROL Rules]** 탭에서 을 클릭합니다 **[!UICONTROL Add Rule]**.
1. 섹션에서 **[!UICONTROL Events]** 을 **[!UICONTROL +]** 클릭하고 확장자로 **[!UICONTROL Places Service]** 선택합니다.
1. For the **[!UICONTROL Event Type]**, select **[!UICONTROL Enter POI]**.
1. 규칙 이름 지정(예: **사용자가 POI를 입력함)**.
1. **[!UICONTROL Keep Changes]**&#x200B;를 클릭합니다.
1. 그 **[!UICONTROL Conditions]** 구역을 비워두세요.

   이 섹션에서는 이 규칙이 실행되어야 하는 시기를 필터링하거나 제한할 수 있습니다.

1. 섹션에서 를 **[!UICONTROL Actions]** 클릭합니다 **[!UICONTROL +]**.
1. 드롭다운 **[!UICONTROL Extension]** 목록에서 **[!UICONTROL Mobile Core]** 을 선택하고 **[!UICONTROL Action Type]** 드롭다운 목록에서 선택합니다 **[!UICONTROL Send Postback]**.
1. 에서 **[!UICONTROL URL]** Campaign Standard 위치 끝점을 구성해야 합니다.

   URL은 과 비슷해야 합니다 `https:///rest/head/mobileAppV5//locations/`.
이전에 캠페인 서버 및 Key용으로 만든 올바른 데이터 요소를 사용해야 합니다.

1. 게시물 본문을 추가하고 다음을 전송하려면 이 상자를 클릭합니다.

   ```
   {
    "locationData": {
    "distances": "{%%Last Entered POI Radius%%}",
    "poiLabel": "{%%Last Entered POI Name%%}",
    "latitude": "{%%Last Entered POI Lat%%}",
    "longitude": "{%%Last Entered POI Long%%}",
    "appId": "{%%AppID%%}",
    "marketingCloudId": “{%%ecid%%}”
    }
   }
   ```

1. 이전 섹션에서 만든 데이터 요소를 사용해야 합니다.
1. 에 **[!UICONTROL Content Type]**&#x200B;를 입력합니다 **[!UICONTROL application/json]**.
1. **[!UICONTROL Keep Changes]**&#x200B;를 클릭합니다.

>[!IMPORTANT]
>
>* 항목이 트리거되고 있으며 올바른 데이터가 수집되고 있는지 확인하는 추가 작업으로 Slack 웹 후크를 설정하는 것이 도움이 될 수 있습니다.
>* 최신 변경 사항을 앱에 게시하여 규칙과 모든 데이터 요소가 구성의 일부로 배포되는지 확인하십시오. 게시한 후 모바일 애플리케이션을 다시 실행하여 최신 구성 업데이트를 얻으십시오.


## 위치 데이터를 사용하여 캠페인 메시지 타깃팅

Adobe Campaign에 채워진 위치 데이터가 있으므로 POI를 대상 세그먼트 도구로 사용할 수 있습니다.

1. Adobe Campaign Standard 인스턴스에서 을 클릭합니다 **[!UICONTROL Create Push Notification]**.
1. 푸시 알림 유형의 경우 을 선택합니다 **[!UICONTROL Send push to Campaign profiles]**.
1. 을 클릭하고 **[!UICONTROL Next]** 일반 세부 사항을 입력합니다.
1. 대상 화면에서 푸시 알림이 전송될 예상 사용자 수 **[!UICONTROL Count]** 를 결정하려면 을 클릭합니다.

   >[!TIP]
   >
   >이 예에서는 응용 프로그램이 테스트되고 있는 세 개의 설치된 장치가 있기 때문에 개수가 3개가 됩니다.

1. 왼쪽 창에서 **[!UICONTROL Profile]** 탭을 확장하고 **[!UICONTROL POI location]** 필터를 주 영역으로 드래그합니다.
1. POI 필터 창에서 타깃팅할 POI의 정확한 이름을 입력합니다.

   >[!TIP]
   >
   >사용자가 이 POI를 이전 방문한 이후 기간을 결정하기 위해 추가로 선택할 수 있습니다.

   ![&quot;ACS의 푸시 메시지 2&quot;](/help/assets/ACS_push2.png)

1. **[!UICONTROL Confirm]**&#x200B;를 클릭합니다.
1. 맨 위에서 카운트를 다시 실행하면 대상자 크기가 변경됩니다.

   카운트 업데이트가 표시되지 않는 경우 어떤 장치도 응모를 트리거하지 않은 POI 이름을 입력했을 수 있습니다. 다양한 테스트 장치에서 POI 항목 목록을 볼 수 있으므로 이러한 상황에서는 Slack 웹 후크를 사용하는 것이 매우 중요합니다.

1. 메시지에 여러 POI를 포함하도록 추가 POI 위치 필터를 끌 수 있습니다.
1. Click **[!UICONTROL Next]** to finish creating the push notification for delivery.

   ![&quot;ACS에서 푸시 메시지 3&quot;](/help/assets/ACS_push3.png)

Adobe Campaign Standard과 함께 위치 서비스를 사용하면 지역 펜스 항목 및 종료를 기반으로 사용자에게 메시지를 세그먼트화하고 타깃팅할 수 있는 강력한 도구가 제공됩니다. 이러한 통합을 통해 보다 개인화된 컨텍스트 기반의 활용 사례를 구축할 수 있습니다.
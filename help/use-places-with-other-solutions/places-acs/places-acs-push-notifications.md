---
title: 푸시 알림
seo-title: 푸시 알림
description: 이 섹션에서는 Campaign Standard에서 푸시 알림과 함께 위치를 사용하는 방법에 대한 정보를 제공합니다.
seo-description: '이 섹션에서는 Campaign Standard에서 푸시 알림과 함께 위치를 사용하는 방법에 대한 정보를 제공합니다. '
translation-type: tm+mt
source-git-commit: a76e91775efd92ce56f2dc5cbdcc65786855b5c3

---


# Experience Platform Location Service를 통한 푸시 알림 {#push-notifications}

이 안내서에서는 내역 위치 정보를 사용하여 Adobe Campaign Standard를 통해 전달된 푸시 알림을 타깃팅하는 방법을 보여줍니다.

## 전제 조건

시작하기 전에 다음 작업을 완료하십시오.

* Adobe Campaign Standard 익스텐션을 포함하여 Adobe Experience Platform Mobile SDK로 모바일 [애플리케이션을](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard)구성합니다.

* Adobe Experience [Platform Mobile](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) SDK를 앱에 통합합니다.
* Adobe Campaign [Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) Extension을 모바일 앱 구성에 추가합니다.

* [위치 POI](/help/poi-mgmt-ui/create-a-poi-ui.md) 관리 인터페이스에서 POI를 만듭니다.

* 위치 확장을 [활성화하고 설치합니다](/help/places-ext-aep-sdks/places-extension/places-extension.md).


## Experience Platform Launch에서 데이터 요소 제작

응용 프로그램에서 위치 서비스용 위치 및 위치 모니터 확장 기능이 제대로 작동하는지 확인한 후 Experience Platform Launch에서 데이터 요소를 만듭니다. 데이터 요소를 사용하면 Mobile SDK 이벤트 허브를 통해 제공되는 익스텐션에서 제공한 정보를 읽을 수 있으며 클라이언트 애플리케이션에서 데이터를 검색할 별칭으로 사용할 수 있습니다. 위치 확장 기능에서 데이터를 검색하고 위치 정보를 캠페인에 보내려면 몇 가지 데이터 요소를 만들어야 합니다.

데이터 요소를 만들려면

1. Experience Platform 시작 모바일 속성에서 **[!UICONTROL Data Elements]** 탭을 클릭하고 데이터 요소 **[!UICONTROLA추가를 클릭합니다]**.
2. 드롭다운 **[!UICONTROL Extension]** 목록에서 선택합니다 **[!UICONTROL Places]**.
3. 드롭다운 **[!UICONTROL Data Element Type]** 목록에서 선택합니다 **[!UICONTROL Name]**.
4. 오른쪽 창에서 사용자가 현재 있는 POI의 이름을 **[!UICONTROL Current POI]** 검색하는 이름을 선택할 수 있습니다.

   **[!UICONTROL Last Entered]** 사용자가 마지막으로 입력한 POI의 이름을 검색하고 사용자가 마지막으로 남긴 POI의 이름을 **[!UICONTROL Last Exited]** 제공합니다. 이 예에서는 데이터 요소의 이름을 선택하고 **[!UICONTROL Last Entered]** 입력합니다(예: **[!UICONTROL Last Entered POI Name]** 클릭한 **[!UICONTROL Save]**&#x200B;경우).

   !["Campaign Standard의 푸시 메시지"](/help/assets/ACS_Push1.png)

5. 위의 1-4 단계를 반복하여 마지막으로 입력한 POI 위도, *마지막으로 입력한 POI 경도*&#x200B;및 *마지막으로 입력한 POI*&#x200B;반경에 대한 데이터 요소를 *만듭니다*.

위치 서비스에 대한 데이터 요소 외에도 앱 ID 및 Experience Cloud ID에 대한 *모바일* 코어 데이터 요소를 *만들어야 합니다*.

## 위치 데이터를 Adobe Campaign Standard로 전송하는 규칙 만들기

Experience Platform Launch의 규칙을 사용하면 이벤트 트리거를 기반으로 복잡한 다중 솔루션 워크플로우를 만들 수 있습니다. 규칙을 사용하여 새 규칙을 만들거나 기존 규칙을 수정하고 업데이트를 모바일 애플리케이션에 동적으로 배포할 수 있습니다. 다음 예에서는 사용자가 지리적 제약을 받는 POI에 들어갈 때 규칙이 트리거됩니다. 규칙이 트리거되면 Adobe Experience Cloud ID를 기반으로 특정 사용자에 대한 특정 POI에 대한 항목을 기록하기 위한 업데이트가 Campaign Standard로 전송됩니다.

1. Launch 모바일 속성의 **[!UICONTROL Rules]** 탭에서 을 클릭합니다 **[!UICONTROL Add Rule]**.
2. 섹션에서 을 클릭하고 확장자로 **[!UICONTROL Events]** **[!UICONTROL +]** **[!UICONTROL Places]** 선택합니다.
3. For the **[!UICONTROL Event Type]**, select **[!UICONTROL Enter POI]**.
4. 규칙 이름 지정(예: 사용자가 POI **를 입력함)**.
5. 클릭 **[!UICONTROL Keep Changes]**.
6. 이 **[!UICONTROL Conditions]** 섹션은 비워두십시오.

   이 섹션에서는 이 규칙이 실행될 시기를 필터링하거나 제한할 수 있습니다.

7. 섹션에서 **[!UICONTROL Actions]** 을 클릭합니다 **[!UICONTROL +]**.
8. 드롭다운 목록에서 **[!UICONTROL Extension]** 선택하고 **[!UICONTROL Mobile Core]** 드롭다운 목록에서 **[!UICONTROL Action Type]** **[!UICONTROL Send Postback]**&#x200B;선택합니다.
9. 에서 **[!UICONTROL URL]**&#x200B;캠페인 표준 위치 끝점을 구성해야 합니다.

   URL은 다음과 유사해야 합니다 `https:///rest/head/mobileAppV5//locations/`.
캠페인 서버 및 Key에 대해 이전에 만든 올바른 데이터 요소를 사용해야 합니다.

10. 상자를 클릭하여 게시물 본문을 추가하고 다음을 전송합니다.

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

11. 이전 섹션에서 만든 데이터 요소를 사용해야 합니다.
12. 에 **[!UICONTROL Content Type]**&#x200B;입력합니다 **[!UICONTROL application/json]**.
13. 클릭 **[!UICONTROL Keep Changes]**.

>[!IMPORTANT]
>
>* 항목이 트리거되고 있으며 올바른 데이터가 수집되고 있는지 확인하는 추가 작업으로 Slack 웹 후크 설정을 사용하는 것이 유용할 수 있습니다.


>* 규칙의 일부로 규칙과 모든 데이터 요소가 배포되도록 최근 변경 내용을 앱에 게시해야 합니다. 게시 후 모바일 애플리케이션을 다시 실행하여 최신 구성 업데이트를 받아야 합니다.


## 위치 데이터를 사용하여 캠페인 메시지 타깃팅

이제 Campaign에 위치 데이터가 입력되었으므로 POI를 대상 세그먼트 도구로 사용할 수 있습니다.

1. Adobe Campaign Standard 인스턴스에서 을 클릭합니다 **[!UICONTROL Create Push Notification]**.
2. 푸시 알림 유형의 경우 을 **[!UICONTROL Send push to Campaign profiles]**&#x200B;선택합니다.
3. 을 **[!UICONTROL Next]** 클릭하고 일반 세부 사항을 입력합니다.
4. 대상 화면에서 푸시 알림을 전송할 예상 사용자 수를 **[!UICONTROL Count]** 결정하려면 을 클릭합니다.

   >[!TIP]
   >
   >이 예에서는 애플리케이션을 테스트하고 있는 세 개의 설치된 장치가 있으므로 카운트가 3이 됩니다.

5. 왼쪽 창에서 **[!UICONTROL Profile]** 탭을 확장하고 **[!UICONTROL POI location]** 필터를 주 영역으로 드래그합니다.
6. POI 필터 창에서 타깃팅할 POI의 정확한 이름을 입력합니다.

   >[!TIP]
   >
   >사용자가 이 POI를 이전 방문한 이후의 기간을 결정하기 위해 추가 항목을 선택할 수 있습니다.

   !["ACS의 푸시 메시지 2"](/help/assets/ACS_push2.png)

7. 클릭 **[!UICONTROL Confirm]**.
8. 맨 위에 있는 카운트를 다시 실행하여 대상자 크기 변경을 확인합니다.

   카운트 업데이트가 표시되지 않으면 POI 이름을 입력했을 수 있습니다. 이 POI에는 어떤 장치도 응모를 트리거하지 않았습니다. 다양한 테스트 장치에서 POI 항목 목록을 볼 수 있으므로 이러한 상황에서는 Slack 웹 후크를 사용하는 것이 중요합니다.
9. 추가 POI 위치 필터를 드래그하여 메시지에 여러 POI를 포함할 수 있습니다.
10. 전달에 대한 푸시 알림 만들기를 **[!UICONTROL Next]** 완료하려면 을 클릭합니다.

   !["ACS의 푸시 메시지 3"](/help/assets/ACS_push3.html)

Adobe Campaign Standard와 함께 위치 서비스를 사용하면 지역 펜스 항목 및 종료를 기반으로 메시지를 세그먼트화하고 사용자에게 타깃팅할 수 있는 강력한 도구를 사용할 수 있습니다. 이러한 통합을 통해 보다 개인화되고 상황에 맞는 활용 사례를 구축할 수 있습니다.
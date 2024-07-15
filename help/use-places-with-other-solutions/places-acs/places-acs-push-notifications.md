---
title: Places Service로 푸시 알림
description: 이 섹션에서는 Campaign Standard에서 푸시 알림과 함께 Places Service를 사용하는 방법에 대해 설명합니다.
exl-id: 4b50f552-deb8-49cd-9221-fbbf33aaa5f9
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# Places Service로 푸시 알림 {#push-notifications}

이 섹션에서는 내역 지리적 위치 정보를 사용하여 Adobe Campaign Standard을 통해 제공되는 푸시 알림을 타깃팅하는 방법에 대해 알아봅니다.

## 전제 조건

시작하기 전에 다음 작업을 완료하십시오.

* [Adobe Campaign Standard 확장](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard)을(를) 포함하여 Adobe Experience Platform Mobile SDK로 모바일 애플리케이션을 구성했습니다.

* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk)를 앱에 통합합니다.
* 모바일 앱 구성에 [Adobe Campaign Standard 확장](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard)을(를) 추가합니다.

* 위치 서비스 POI 관리 인터페이스에서 [POI를 만듭니다](/help/poi-mgmt-ui/create-a-poi-ui.md).

* [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md)을 사용하도록 설정하고 설치하십시오.


## Experience Platform Launch에서 데이터 요소 만들기

Places 확장 및 지역 모니터링 솔루션([iOS용 CoreLocation 설명서](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) 또는 [Android 위치 설명서](https://developer.android.com/training/location/geofencing))이 응용 프로그램에서 올바르게 작동하는지 확인한 후에는 Experience Platform Launch에서 데이터 요소를 만들어야 합니다. 데이터 요소를 사용하면 Mobile SDK 이벤트 허브를 통해 제공되는 확장에서 제공한 정보를 읽고 클라이언트 애플리케이션에서 데이터를 검색하는 별칭 역할을 할 수 있습니다. Places 확장에서 데이터를 검색하고 Places Service 정보를 Campaign으로 전송하려면 몇 가지 데이터 요소를 만들어야 합니다.

데이터 요소를 만들려면 다음 작업을 수행하십시오.

1. Experience Platform Launch 모바일 속성에서 **[!UICONTROL 데이터 요소]** 탭을 클릭하고 **[!UICONTROL 데이터 요소 추가]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL 장소 서비스]**&#x200B;를 선택합니다.
1. **[!UICONTROL 데이터 요소 유형]** 드롭다운 목록에서 **[!UICONTROL 이름]**&#x200B;을(를) 선택합니다.
1. 오른쪽 창에서 사용자가 현재 위치한 POI의 이름을 검색하는 **[!UICONTROL 현재 POI]**&#x200B;를 선택할 수 있습니다.

   **[!UICONTROL 마지막으로 입력한 날짜]**&#x200B;은(는) 사용자가 마지막으로 입력한 POI의 이름을 검색하고 **[!UICONTROL 마지막으로 종료한 날짜]**&#x200B;은(는) 사용자가 마지막으로 남긴 POI의 이름을 제공합니다. 이 예제에서는 **[!UICONTROL 마지막으로 입력한 날짜]**&#x200B;을(를) 선택하고 **[!UICONTROL 마지막으로 입력한 POI 이름]**&#x200B;과(와) 같은 데이터 요소의 이름을 입력한 다음 **[!UICONTROL 저장]**&#x200B;을(를) 클릭했습니다.

   ![&quot;Campaign Standard의 푸시 메시지&quot;](/help/assets/ACS_Push1.png)

1. 위의 1~4단계를 반복하여 *마지막으로 입력한 POI 위도*, *마지막으로 입력한 POI 경도* 및 *마지막으로 입력한 POI 반경*&#x200B;에 대한 데이터 요소를 만듭니다.

Places Service의 데이터 요소 외에 *앱 ID* 및 *Experience Cloud ID*&#x200B;에 대한 Mobile Core 데이터 요소를 만드십시오.

## 위치 데이터를 Adobe Campaign Standard으로 전송하는 규칙 만들기

Experience Platform Launch의 규칙을 사용하면 이벤트 트리거를 기반으로 복잡한 다중 솔루션 워크플로우를 만들 수 있습니다. 규칙을 사용하여 새 규칙을 만들거나 기존 규칙을 수정하고 업데이트를 모바일 애플리케이션에 동적으로 배포할 수 있습니다. 다음 예에서는 사용자가 지리적 기반 POI를 입력할 때 규칙이 트리거됩니다. 규칙이 트리거되면 Experience Cloud ID를 기반으로 특정 Campaign Standard의 특정 POI에 대한 항목을 기록하는 업데이트가 사용자에게 전송됩니다.

1. Experience Platform Launch 모바일 속성에서 **[!UICONTROL 규칙]** 탭에서 **[!UICONTROL 규칙 추가]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 이벤트]** 섹션에서 **[!UICONTROL +]**&#x200B;을(를) 클릭하고 확장으로 **[!UICONTROL 장소 서비스]**&#x200B;를 선택합니다.
1. **[!UICONTROL 이벤트 유형]**&#x200B;에 대해 **[!UICONTROL POI 입력]**&#x200B;을 선택하세요.
1. 규칙 이름을 지정합니다(예: **사용자가 입력한 POI**).
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 조건]** 섹션을 비워 둡니다.

   이 섹션에서는 이 규칙이 실행되는 시기를 필터링하거나 제한할 수 있습니다.

1. **[!UICONTROL 작업]** 섹션에서 **[!UICONTROL +]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL 확장]** 드롭다운 목록에서 **[!UICONTROL Mobile Core]**&#x200B;를 선택하고 **[!UICONTROL 작업 유형]** 드롭다운 목록에서 **[!UICONTROL 포스트백 보내기]**&#x200B;를 선택합니다.
1. **[!UICONTROL URL]**&#x200B;에서 Campaign Standard 위치 끝점을 구성해야 합니다.

   URL은 `https:///rest/head/mobileAppV5//locations/`과(와) 유사해야 합니다.
Campaign 서버 및 pKey에 대해 이전에 만든 올바른 데이터 요소를 사용해야 합니다.

1. 게시물 본문을 추가하고 다음을 전송하려면 상자를 클릭합니다.

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
1. **[!UICONTROL 컨텐츠 유형]**&#x200B;에, **[!UICONTROL application/json]**&#x200B;을 입력합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭합니다.

>[!IMPORTANT]
>
>* 항목이 트리거되고 올바른 데이터가 수집되고 있는지 확인하기 위한 추가 작업으로 Slack 웹 후크를 설정하는 것이 유용할 수 있습니다.
>* 최근 변경 내용을 앱에 게시하여 규칙과 모든 데이터 요소가 구성의 일부로 배포되었는지 확인해야 합니다. 게시 후 모바일 애플리케이션을 다시 실행하여 최신 구성 업데이트를 받습니다.

## 위치 데이터를 사용하여 캠페인 메시지 타겟팅

이제 Campaign에 위치 데이터가 채워졌으므로 POI를 대상 세그먼트 도구로 사용할 수 있습니다.

1. Adobe Campaign Standard 인스턴스에서 **[!UICONTROL 푸시 알림 만들기]**&#x200B;를 클릭합니다.
1. 푸시 알림 유형에 대해 **[!UICONTROL Campaign 프로필로 푸시 보내기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 다음]**&#x200B;을 클릭하고 일반 세부 정보를 입력하십시오.
1. 대상 화면에서 **[!UICONTROL 카운트]**&#x200B;를 클릭하여 푸시 알림을 보낼 예상 사용자 수를 결정합니다.

   >[!TIP]
   >
   >이 예에서는 애플리케이션이 테스트되는 장치가 세 개 설치되어 있으므로 개수는 3개입니다.

1. 왼쪽 창에서 **[!UICONTROL 프로필]** 탭을 확장하고 **[!UICONTROL POI 위치]** 필터를 기본 영역으로 드래그합니다.
1. POI 필터 창에서 타깃팅할 POI의 정확한 이름을 입력합니다.

   >[!TIP]
   >
   >이 POI에 대한 사용자의 이전 방문 이후 기간을 결정하기 위해 추가 선택을 할 수 있습니다.

   ![&quot;ACS의 푸시 메시지 2&quot;](/help/assets/ACS_push2.png)

1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
1. 상단에서 카운트를 다시 실행하여 대상자 크기가 변경된 것을 확인합니다.

   개수 업데이트가 표시되지 않으면 항목을 트리거한 장치가 없는 POI 이름을 입력했을 수 있습니다. 다양한 테스트 장치에서 POI 항목 목록을 볼 수 있으므로 이 상황에서 Slack 웹 후크를 사용하는 것이 유용합니다.

1. 추가 POI 위치 필터를 드래그하여 메시지에 여러 POI를 포함할 수 있습니다.
1. **[!UICONTROL 다음]**&#x200B;을 클릭하여 전송을 위한 푸시 알림 만들기를 완료합니다.

   ![&quot;ACS의 푸시 메시지 3&quot;](/help/assets/ACS_push3.png)

Adobe Campaign Standard과 함께 위치 서비스를 사용하면 지리적 울타리 시작 및 종료에 따라 메시지를 세그먼트화하고 사용자에게 타깃팅할 수 있는 강력한 도구를 사용할 수 있습니다. 이러한 통합을 통해 보다 개인화되고 상황에 맞는 사용 사례를 구축할 수 있습니다.

---
title: Places Service를 사용한 인앱 메시지
description: 이 섹션에서는 Campaign Standard의 인앱 메시지와 함께 Campaign Standard에서 푸시 메시지를 사용하는 방법에 대한 정보를 제공합니다.
exl-id: c80727b8-20c9-4ca0-9f2c-20ec646bb7fa
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 4%

---

# Places Service를 사용한 인앱 메시징 {#in-app-messages-loc-service}

다음 정보는 위치 서비스 정보를 사용하여 인앱 메시지 또는 로컬 알림을 전송하는 방법을 이해하는 데 도움이 됩니다.

## 전제 조건

시작하기 전에 다음 작업을 완료하십시오.

* 다음을 포함하여 Adobe Experience Platform Mobile SDK로 구성된 모바일 애플리케이션을 가지고 있어야 합니다. [Adobe Campaign Standard 확장](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard).

* 통합 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) 참조하십시오.
* 추가 [Adobe Campaign Standard 확장](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) 모바일 앱 구성에 연결합니다.

* [POI 만들기](/help/poi-mgmt-ui/create-a-poi-ui.md) 를 입력합니다.

* 설치 및 구성 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md) 및 지역 모니터링 솔루션([CoreLocation 설명서](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) iOS용 또는 [Android 위치 설명서](https://developer.android.com/training/location/geofencing)) 내의 아무 곳에나 삽입할 수 있습니다.

## 지역 펜스 시작 또는 종료에 따라 인앱 메시지 보내기

1. Adobe Campaign Standard 인스턴스에서 **[!UICONTROL 인앱 메시지 만들기]**.
1. 메시지 유형에 대해 을(를) 선택합니다. **[!UICONTROL 모바일 애플리케이션의 모든 사용자 Target]**.
1. 클릭 **[!UICONTROL 다음]** 일반 세부 사항을 입력합니다.
1. 왼쪽 창에서 위치 서비스와 관련된 다양한 트리거를 사용할 수 있는지 확인합니다.

   * 사용자가 POI 지역 울타리를 입력한 경우 인앱 메시지를 표시하도록 선택할 수 있습니다.
   * 위치 서비스 UI에 정의된 메타데이터를 사용하여 대상을 필터링할 수도 있습니다.

   아래 예에서는 무료 음료 프로그램에 참여하는 휴가 리조트 중 하나를 입력하는 사용자만 표시되는 인앱 메시지를 트리거할 수 있으며 해당 사용자에게 도착 시 쿠폰을 보내려고 합니다.

   ![&quot;인앱 메시지 위치 메타데이터&quot;](/help/assets/last-entered-vacation.png)

1. 을(를) 클릭합니다. **[!UICONTROL 다음]** 을 클릭하여 전송할 인앱 메시지 작성을 완료합니다.

   ![&quot;이벤트 만들기&quot;](/help/assets/prepare-ACS.png)

   인앱 메시지 전달을 테스트하려면 Xcode 또는 Android studio에서 애플리케이션을 실행하고 위치 시뮬레이터를 사용하여 메시징 기준에 맞는 POI를 선택합니다.

   ![&quot;음료 쿠폰&quot;](/help/assets/drink-coupon-on-app.png)

Adobe Campaign Standard에서 위치 서비스를 사용하면 지역 울타리 항목 및 종료에 따라 메시지를 세그먼트화하고 사용자에게 타깃팅할 수 있는 강력한 도구를 제공합니다. 이 통합을 통해 보다 개인화되고 상황에 맞는 활용 사례를 구축할 수 있습니다.

<!--I changed this embed to a link to pass validation. We should not link to youtube videos, so please upload this to MCP-->

[캠페인 메시징이 포함된 Adobe Experience Platform 위치 서비스](https://www.youtube.com/watch?v=ikiTTQw9c-o)

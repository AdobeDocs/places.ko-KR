---
title: 위치 서비스가 있는 인앱 메시지
description: 이 섹션에서는 Campaign Standard에서 인앱 메시지와 함께 Campaign Standard의 푸시 메시지를 사용하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2

---


# 위치 서비스가 있는 인앱 메시지 {#in-app-messages-loc-service}

이 정보는 Adobe Experience Platform 위치 서비스 정보를 사용하여 인앱 메시지 또는 로컬 알림을 전송하는 방법을 이해하는 데 도움이 됩니다.

## 전제 조건

시작하기 전에 다음 작업을 완료하십시오.

* Adobe Campaign Standard 익스텐션을 포함하여 Adobe Experience Platform Mobile SDK로 모바일 [애플리케이션을](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard)구성합니다.

* Adobe Experience [Platform Mobile](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) SDK를 앱에 통합합니다.
* Adobe Campaign [Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) Extension을 모바일 앱 구성에 추가합니다.

* [위치 POI](/help/poi-mgmt-ui/create-a-poi-ui.md) 관리 인터페이스에서 POI를 만듭니다.

* 모바일 애플리케이션에서 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md) 및 위치 [모니터 확장](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md) 기능을 설치하고 구성합니다.

## 지역 펜스 항목 또는 종료를 기반으로 인앱 메시지 보내기

1. Adobe Campaign Standard 인스턴스에서 을 클릭합니다 **[!UICONTROL Create In-App message]**.
1. 메시지 유형에 대해 을 **[!UICONTROL Target all users of a Mobile application]**선택합니다.
1. 을 **[!UICONTROL Next]**클릭하고 일반 세부 사항을 입력합니다.
1. 왼쪽 창에서 위치 서비스와 관련된 다양한 트리거를 사용할 수 있는지 확인합니다.

   * 사용자가 POI 지역 울타리를 입력한 경우 인앱 메시지를 표시하도록 선택할 수 있습니다.
   * 위치 서비스 UI에 정의된 메타데이터를 사용하여 대상을 필터링할 수도 있습니다.
   아래 예에서는 무료 음료 프로그램에 참여하고 있는 휴가 리조트 중 하나에 입장한 사용자만 표시되는 인앱 메시지를 트리거할 수 있고 사용자가 도착할 때 쿠폰을 보내려는 경우

   ![&quot;인앱 메시지 위치 메타데이터&quot;](/help/assets/last-entered-vacation.png)

1. Click the **[!UICONTROL Next]**to finish creating the In-app message for delivery.

   ![&quot;이벤트 만들기&quot;](/help/assets/prepare-ACS.png)

   인앱 메시지 배달을 테스트하려면 Xcode 또는 Android 스튜디오에서 애플리케이션을 실행하고 위치 시뮬레이터를 사용하여 메시징 기준에 맞는 POI를 선택합니다.

   ![&quot;음료 쿠폰&quot;](/help/assets/drink-coupon-on-app.png)

Adobe Campaign Standard와 함께 위치 서비스를 사용하면 지리적 펜스 항목 및 종료를 기반으로 메시지를 세그먼트화하고 사용자에게 타깃팅할 수 있는 강력한 도구를 사용할 수 있습니다. 이러한 통합을 통해 보다 개인화되고 상황에 맞는 활용 사례를 구축할 수 있습니다.

>[!VIDEO](https://www.youtube.com/watch?v=ikiTTQw9c-o)
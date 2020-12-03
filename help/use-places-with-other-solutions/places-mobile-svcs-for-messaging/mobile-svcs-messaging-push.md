---
title: 푸시 알림
description: 이 섹션에서는 푸시 알림과 함께 Places Service를 사용하는 방법을 보여 줍니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 8%

---


# 푸시 알림

Mobile Services를 사용하면 Adobe Analytics 세그먼트에 푸시 알림을 전송할 수 있습니다. 위치 서비스에서 POI와의 내역 상호 작용을 사용하여 푸시 메시지의 대상을 세그먼트화할 수 있습니다. 예를 들어 지난 30일 동안 스토어 중 하나에 있었던 사용자에게 메시지를 보낼 수 있습니다.

시작하기 전에 다음 작업을 완료했는지 확인하십시오.

* 장소 서비스 데이터가 Adobe Analytics에 의해 처리되었습니다.

   즉, 모바일 앱이 Places Service 데이터를 보고서 세트로 성공적으로 전송하고 데이터를 세그멘테이션에 사용할 수 있음을 의미합니다.

* Mobile Services의 푸시 알림 채널이 설정되어 있습니다.

   자세한 내용은 [푸시 메시지 만들기](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/prerequisites-push-messaging.html)를 참조하십시오.

* Mobile Services의 Analytics 세그먼트에 푸시 알림을 전송하는 방법을 이해합니다.

   자세한 내용은 [푸시 메시지 만들기](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/push-messages/t-create-push-message.html)를 참조하십시오.

## 알림 보내기

푸시 알림 **[!UICONTROL Audience]** 만들기 *작업 과정의* 탭에서 다음 방법 중 하나를 사용하여 이 메시지의 대상을 만들 수 있습니다.

* 드롭다운 **[!UICONTROL Analytics Segments]** 목록에서 이전에 만든 Adobe Analytics 세그먼트를 선택합니다.

* 섹션에서 **[!UICONTROL Custom Segment]** 사용 가능한 사용자 지정 세그먼트 매개 변수를 사용하여 대상을 만듭니다.

![푸시 메시지 설정](/help/assets/push-set-up.png)

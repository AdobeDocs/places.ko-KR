---
title: 푸시 메시지
seo-title: 푸시 메시지
description: 이 섹션에서는 푸시 메시지에 위치 사용을 보여 줍니다.
seo-description: 이 섹션에서는 푸시 메시지에 위치 사용을 보여 줍니다.
translation-type: tm+mt
source-git-commit: accfa6ba009ad3419481d9bd3b498143228099fc

---


# 푸시 알림(#places-push-messaging)

푸시 알림:AMS를 사용하면 푸시 알림을 Adobe Analytics 세그먼트에 보낼 수 있습니다. 위치 서비스를 사용하면 푸시 메시지의 대상을 POI와의 내역 상호 작용에 따라 세그먼트화할 수 있습니다. 예를 들어 지난 30일 동안 스토어에 있었던 사용자에게 메시지를 보낼 수 있습니다.

시작하기 전에 다음 작업을 완료했는지 확인합니다.

* 위치 서비스 데이터가 Adobe Analytics에서 처리되었습니다.

   즉, 모바일 앱이 위치 서비스 데이터를 보고서 세트로 성공적으로 전송하고 데이터를 세그멘테이션에 사용할 수 있습니다.

* Mobile Services의 푸시 알림 채널이 설정되었습니다.

   자세한 내용은 [푸시 메시지 만들기](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/prerequisites-push-messaging.html)를 참조하십시오.

* Mobile Services에서 Analytics 세그먼트에 푸시 알림을 전송하는 방법에 대해 알아보십시오.

   * 자세한 내용은 [푸시 메시지 만들기](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/push-messages/t-create-push-message.html)를 참조하십시오.

## 알림 보내기

푸시 알림 **[!UICONTROL Audience]** 만들기 *워크플로우의* 탭에서 다음 방법 중 하나로 이 메시지의 대상을 만들 수 있습니다.

* 이전에 만든 Adobe Analytics 세그먼트를 선택합니다.

* 사용 가능한 사용자 지정 세그먼트 매개 변수를 사용하여 대상을 만듭니다.

![푸시 메시지 설정](/help/assets/push-set-up.png)


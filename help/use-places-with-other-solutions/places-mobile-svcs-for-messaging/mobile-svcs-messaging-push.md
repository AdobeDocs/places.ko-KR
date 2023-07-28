---
title: 푸시 알림
description: 이 섹션에서는 푸시 알림과 함께 위치 서비스를 사용하는 방법을 보여줍니다.
exl-id: c094fe9c-6148-45ba-850a-f4c520d3362c
source-git-commit: d5c216aebd99ffef01c37c17c62576835b52438b
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 8%

---

# 푸시 알림

Mobile Services를 사용하면 푸시 알림을 Adobe Analytics 세그먼트로 보낼 수 있습니다. 위치 서비스에서는 POI와의 과거 상호 작용을 사용하여 푸시 메시지에 대한 대상을 세그먼트화할 수 있습니다. 예를 들어 지난 30일 동안 상점 중 하나에 있었던 사용자에게 메시지를 보낼 수 있습니다.

시작하기 전에 다음 작업을 완료했는지 확인하십시오.

* Places Service 데이터가 Adobe Analytics에서 처리되었습니다.

  즉, 모바일 앱에서 Places Service 데이터를 보고서 세트에 성공적으로 보냈으며 해당 데이터를 세그멘테이션에 사용할 수 있습니다.

* Mobile Services의 푸시 알림 채널이 설정됩니다.

  자세한 내용은 [푸시 메시지 만들기](https://experienceleague.adobe.com/docs/discontinued/using/mobile-services.html)를 참조하십시오.

* Mobile Services의 Analytics 세그먼트에 푸시 알림을 전송하는 방법을 이해합니다.

  자세한 내용은 [푸시 메시지 만들기](https://experienceleague.adobe.com/docs/discontinued/using/mobile-services.html)를 참조하십시오.

## 알림 보내기

다음에서 **[!UICONTROL 대상자]** 의 탭 *푸시 알림 만들기* 워크플로우에서는 다음 방법 중 하나로 이 메시지의 대상자를 만들 수 있습니다.

* 다음에서 **[!UICONTROL Analytics 세그먼트]** 드롭다운 목록에서 이전에 만든 Adobe Analytics 세그먼트를 선택합니다.

* 다음에서 **[!UICONTROL 사용자 지정 세그먼트]** 섹션, 사용 가능한 사용자 지정 세그먼트 매개 변수를 사용하여 대상을 작성합니다.

![푸시 메시지 설정](/help/assets/push-set-up.png)

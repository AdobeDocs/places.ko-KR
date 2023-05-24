---
title: 인앱 알림
description: 이 섹션에서는 인앱 메시지와 함께 위치 서비스를 사용하는 방법을 보여줍니다.
exl-id: c655e64b-0737-44d5-b453-2ac02fb9cbcc
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---

# 인앱 알림 {#places-push-messaging}

다음 정보는 위치 서비스 이벤트에서 트리거할 인앱 메시지를 구성하는 방법을 보여 줍니다.

>[!IMPORTANT]
>
>메시지는 Analytics 히트에 있어야 합니다.

## 인앱 메시지

Mobile Services를 사용하면 Analytics로 전송되는 위치 데이터를 인앱 메시지의 트리거 이벤트 및/또는 조건으로 사용할 수 있습니다. SDK에서 인앱 메시지가 실행되어 Analytics에서 데이터가 처리될 때까지 기다리지 않아도 되는 경우 트리거가 발생하는 즉시 메시지가 실시간으로 표시될 수 있습니다.

### 로컬 알림

다음은 사용 가능한 인앱 메시지 유형 목록입니다.

* 전체 화면
* 경고
* 로컬 알림

이러한 유형은 SDK에 의해 트리거되므로 인앱 메시지입니다. 로컬 알림은 앱이 백그라운드에 있을 때 표시되므로 푸시 알림처럼 느껴집니다. 또한 이러한 알림은 앱이 백그라운드에 있는 동안 사용자가 POI를 입력하거나 종료할 때 실시간 알림을 제공합니다.

### 사전 요구 사항

시작하기 전에 Mobile Services에서 인앱 메시지를 보내고 만드는 방법과 트리거가 작동하는 방법을 이해합니다. 자세한 내용은 [인앱 메시지를 만듭니다.](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/inapp-messages/t-in-app-message.html)

##  Experience Platform Launch의 규칙

인앱 메시지 트리거 규칙의 일부로 사용할 수 있게 하려는 데이터를 Analytics에 보내는 Experience Platform Launch 규칙을 만들 수 있습니다. 사용 사례에 따라 Experience Platform Launch 규칙의 위치 확장의 데이터를 이벤트 및/또는 조건으로 사용할 수 있습니다.

* 위치 데이터를 트리거 이벤트로 사용.

   예를 들어 사용자가 POI를 입력하면 Analytics로 데이터를 보낼 수 있습니다.

* 위치 데이터를 트리거 이벤트의 조건으로 사용.

   예를 들어 서로 다른 POI의 날씨에 대해 위치 서비스에서 사용자 지정 메타데이터 태그를 만든 경우 해당 메타데이터를 규칙 조건의 매개 변수로 사용할 수 있습니다. 앞에서 설명한 POI 항목 이벤트와 함께 이 조건을 사용할 수 있지만, 모든 이벤트에 대한 컨텍스트로 이 조건을 사용할 수도 있습니다.

적절한 이벤트 및 조건 매개 변수로 규칙이 설정된 후 데이터를 Analytics에 보내도록 작업을 구성하여 규칙 구성을 완료합니다.

## 동작 만들기

작업을 만들려면 다음 작업을 수행하십시오.

1. 다음 항목 선택 **[!UICONTROL Adobe Analytics]** 확장명.
1. 다음에서 **[!UICONTROL 작업 유형]** 드롭다운 목록에서 다음을 선택합니다. **[!UICONTROL 추적합니다.]**
1. 작업 이름을 입력합니다.
1. 오른쪽 창의 **[!UICONTROL 컨텍스트 데이터]**&#x200B;에 키-값 쌍을 선택하여 Analytics로 전송될 컨텍스트 데이터를 설정합니다.

예를 들어 다음을 선택할 수 있습니다 `poiname` 를 키로 사용하고 `{%%Last Entered POI Name}` 을 값으로 추가합니다.

>[!TIP]
>
>Analytics 처리 규칙을 설정하여 이 컨텍스트 데이터를 선택할 수 있습니다. 자세한 내용은 [처리 규칙](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-processing-rules.html)을 참조하십시오. 의 예에서 *작업 만들기*, 작업이 다음을 전송합니다. `poiname` Analytics로 전송되는 POI 항목 이벤트를 설명하는 컨텍스트입니다.

![작업 만들기](/help/assets/configure-action.png)

다음은 전체 규칙의 예입니다.

![완료된 규칙](/help/assets/create-a-rule.png)

## Mobile Services에서 인앱 메시지 만들기

트리거 매개 변수의 일부로, 다음 방법 중 하나로 장소 서비스의 데이터를 사용하여 메시지 대상자를 만들 수 있습니다.

* 시작 또는 종료와 같은 위치 특정 작업 사용.
* 컨텍스트 데이터로 전송되는 POI 메타데이터를 사용하여 대상자의 범위를 좁힐 수 있습니다.

   이 옵션은 항목과 같은 위치별 작업과 함께 사용하거나 시작 또는 단추 클릭과 같은 다른 이벤트에 대한 컨텍스트로 사용할 수 있습니다.

   다음은 가 있는 POI를 입력하는 사용자를 환영하도록 인앱 메시지를 구성하는 방법의 예입니다 **[!UICONTROL Adobe]** 이름:

   ![트리거 매개 변수](/help/assets/trigger-parameters.png)

* 의 위치 서비스 머리글에 있는 매개 변수 *트리거 및 트레이트* Mobile Services의 페이지가 Places Service의 데이터로 작동하지 않습니다.

   이러한 매개 변수는 Mobile Services에서 만든 레거시 Places Service 데이터베이스에 대해서만 사용됩니다.

---
title: 인앱 알림
description: 이 섹션에서는 인앱 메시지에 위치 서비스를 사용하는 방법을 보여줍니다.
exl-id: c655e64b-0737-44d5-b453-2ac02fb9cbcc
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---

# 인앱 알림 {#places-push-messaging}

다음 정보는 Places Service 이벤트에서 트리거하도록 인앱 메시지를 구성하는 방법을 보여줍니다.

>[!IMPORTANT]
>
>메시지는 Analytics 히트에 있어야 합니다.

## 인앱 메시지

Mobile Services를 사용하면 Analytics로 전송되고 있는 위치 데이터를 인앱 메시지의 트리거 이벤트 및/또는 조건으로 사용할 수 있습니다. In-App 메시지가 SDK에서 실행되며 Analytics에서 데이터를 처리할 때까지 기다릴 필요가 없는 경우 트리거가 발생하는 즉시 메시지가 실시간으로 표시될 수 있습니다.

### 로컬 알림

다음은 사용 가능한 인앱 메시지 유형 목록입니다.

* 전체 화면
* 경고
* 로컬 알림

이러한 유형은 SDK에 의해 트리거되므로 인앱 메시지입니다. 로컬 알림은 앱이 백그라운드에 있을 때 표시되므로 푸시 알림의 모양과 느낌을 줍니다. 또한 앱이 백그라운드에 있을 때 사용자가 POI에 들어오거나 종료할 때 이러한 알림은 실시간 알림을 제공합니다.

### 전제 조건

시작하기 전에 Mobile Services에서 인앱 메시지를 보내고 만드는 방법과 트리거가 작동하는 방식을 이해합니다. 자세한 내용은 [인앱 메시지를 만듭니다.](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/inapp-messages/t-in-app-message.html)

##  Experience Platform Launch의 규칙

인앱 메시지 트리거 규칙의 일부로 사용할 데이터를 Analytics에 전송하는 Experience Platform Launch 규칙을 만들 수 있습니다. 사용 사례에 따라 Experience Platform Launch 규칙의 위치 확장의 데이터를 이벤트 및/또는 조건으로 사용할 수 있습니다.

* 위치 데이터를 트리거 이벤트로 사용합니다.

   예를 들어, 사용자가 POI를 입력하면 데이터를 Analytics로 보낼 수 있습니다.

* 위치 데이터를 조건으로 사용하여 트리거 이벤트에 대한 조건 사용.

   예를 들어, 다른 POI에서 날씨를 위해 위치 서비스에서 사용자 지정 메타데이터 태그를 만든 경우 해당 메타데이터를 규칙 조건의 매개 변수로 사용할 수 있습니다. 앞에서 설명한 POI 입력 이벤트와 함께 이 조건을 사용할 수 있지만, 조건을 모든 이벤트의 컨텍스트에서 사용할 수도 있습니다.

규칙이 적절한 이벤트 및 조건 매개 변수로 설정되어 있으면 데이터를 Analytics에 전송하는 작업을 구성하여 규칙 구성을 완료하십시오.

## 동작 만들기

작업을 만들려면:

1. 을(를) 선택합니다 **[!UICONTROL Adobe Analytics]** 확장.
1. 에서 **[!UICONTROL 작업 유형]** 드롭다운 목록에서 **[!UICONTROL 추적.]**
1. 작업의 이름을 입력합니다.
1. 오른쪽 창에서 **[!UICONTROL 컨텍스트 데이터]**&#x200B;키-값 쌍을 선택하여 Analytics로 전송할 컨텍스트 데이터를 설정합니다.

예를 들어 `poiname` 키 `{%%Last Entered POI Name}` 를 값으로 채우는 방법을 설명합니다.

>[!TIP]
>
>Analytics 처리 규칙을 설정하여 이 컨텍스트 데이터를 선택할 수 있습니다. 자세한 내용은 [처리 규칙](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-processing-rules.html)을 참조하십시오. 의 예에서 *작업 만들기*&#x200B;를 입력하면 `poiname` 를 Analytics로 전송 중인 POI 시작 이벤트를 설명하는 컨텍스트로 사용합니다.

![작업 만들기](/help/assets/configure-action.png)

다음은 전체 규칙의 예입니다.

![완료된 규칙](/help/assets/create-a-rule.png)

## Mobile Services에서 인앱 메시지 만들기

트리거 매개 변수의 일부로, 다음 방법 중 하나로 위치 서비스의 데이터를 사용하여 메시지에 대한 대상자를 만들 수 있습니다.

* 시작 또는 종료와 같은 위치별 작업 사용.
* 대상의 대상을 좁히기 위해 컨텍스트 데이터로 전송되는 POI 메타데이터 사용.

   이 옵션은 시작과 같은 위치 특정 작업과 함께 사용하거나 론치나 단추 클릭과 같은 다른 이벤트의 컨텍스트로 사용할 수 있습니다.

   다음은 POI를 입력한 사용자를 환영하기 위해 인앱 메시지를 구성하는 방법의 예입니다 **[!UICONTROL Adobe]** 이름:

   ![트리거 매개 변수](/help/assets/trigger-parameters.png)

* 위치 서비스 헤딩의 매개변수 *트리거 및 트레이트* mobile Services의 페이지는 위치 서비스의 데이터로 작동하지 않습니다.

   이러한 매개 변수는 Mobile Services에서 생성된 이전 Places Service 데이터베이스에 대해서만 입니다.

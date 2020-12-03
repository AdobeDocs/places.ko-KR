---
title: 인앱 알림
description: 이 섹션에서는 인앱 메시지와 함께 위치 서비스를 사용하는 방법을 보여줍니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 3%

---


# 인앱 알림 {#places-push-messaging}

다음 정보는 Places Service 이벤트에서 트리거하도록 인앱 메시지를 구성하는 방법을 보여줍니다.

>[!IMPORTANT]
>
>메시지는 Analytics 히트에 있어야 합니다.

## 인앱 메시지

Mobile Services에서는 Analytics로 전송되는 위치 데이터를 인앱 메시지에 대한 트리거 이벤트 및/또는 조건으로 사용할 수 있습니다. 인앱 메시지가 SDK에서 실행되어 Analytics에서 데이터를 처리할 때까지 기다릴 필요가 없는 경우 트리거가 발생하는 즉시 메시지가 실시간으로 나타날 수 있습니다.

### 로컬 알림

사용 가능한 인앱 메시지 유형 목록은 다음과 같습니다.

* 전체 화면
* 경고
* 로컬 알림

이러한 유형은 SDK에 의해 트리거되기 때문에 인앱 메시지입니다. 앱이 백그라운드에 있을 때 나타나는 로컬 알림은 푸시 알림과 비슷하고 느껴집니다. 앱이 백그라운드에 있는 동안 사용자가 POI에 입장하거나 종료하면 이러한 알림은 실시간 알림을 제공합니다. 자세한 내용은 위치 모니터 [확장 기능을 참조하십시오](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

### 전제 조건

시작하기 전에 Mobile Services에서 인앱 메시지를 전송하고 만드는 방법 및 트리거가 작동하는 방식을 이해합니다. For more information, see [Create an in-app message.](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/inapp-messages/t-in-app-message.html)

##  Experience Platform Launch의 규칙

인앱 메시지 트리거 규칙의 일부로 사용할 수 있는 데이터를 Analytics로 보내는 Experience Platform Launch 규칙을 만들 수 있습니다. 사용 사례에 따라 Experience Platform Launch 규칙의 위치 확장 데이터를 이벤트 및/또는 조건으로 사용할 수 있습니다.

* 트리거 이벤트로 위치 데이터 사용

   예를 들어, 사용자가 POI를 입력할 때 데이터를 Analytics로 보낼 수 있습니다.

* 위치 데이터를 조건으로 사용하여 이벤트를 트리거합니다.

   예를 들어, 장소 서비스에서 다른 POI의 날씨에 대한 사용자 지정 메타데이터 태그를 만든 경우 해당 메타데이터를 규칙 조건의 매개 변수로 사용할 수 있습니다. 이전에 설명한 POI 입력 이벤트와 함께 이 조건을 사용할 수 있지만, 해당 조건을 모든 이벤트의 컨텍스트로 사용할 수도 있습니다.

적절한 이벤트 및 조건 매개 변수로 규칙을 설정한 후 데이터를 Analytics로 보내는 작업을 구성하여 규칙 구성을 완료하십시오.

## 동작 만들기

작업을 만들려면

1. **[!UICONTROL Adobe Analytics]** 확장을 선택합니다.
1. 드롭다운 **[!UICONTROL Action type]** 목록에서 **[!UICONTROL Track.]**
1. 작업 이름을 입력합니다.
1. 오른쪽 창에서 키-값 쌍 **[!UICONTROL Context Data]**&#x200B;을 선택하여 Analytics로 보낼 컨텍스트 데이터를 설정합니다.

예를 들어 키와 값 `poiname` 으로 선택할 수 `{%%Last Entered POI Name}` 있습니다.

>[!TIP]
>
>이 컨텍스트 데이터를 수집하도록 분석 처리 규칙을 설정할 수 있습니다. 자세한 내용은 [처리 규칙](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-processing-rules.html)을 참조하십시오. 작업 *만들기의 예에서*&#x200B;작업은 Analytics로 전송되는 POI 항목 이벤트를 설명하는 `poiname` 컨텍스트로 이 이벤트를 보냅니다.

![작업 만들기](/help/assets/configure-action.png)

다음은 전체 규칙의 예입니다.

![완료된 규칙](/help/assets/create-a-rule.png)

## Mobile Services에서 인앱 메시지 만들기

트리거 매개 변수의 일부로, 다음 방법 중 하나를 사용하여 Places Service의 데이터가 포함된 메시지의 대상을 만들 수 있습니다.

* 시작 또는 종료와 같은 위치별 작업 사용
* 대상 범위를 좁히기 위해 컨텍스트 데이터로 전송되는 POI 메타데이터 사용

   이 옵션은 시작 등의 위치 관련 동작과 함께 사용하거나, 론치나 단추 클릭과 같은 다른 이벤트의 컨텍스트로 사용할 수 있습니다.

   다음은 이름에 있는 POI를 입력하는 사용자를 환영 받는 사람에게 인앱 메시지 **[!UICONTROL Adobe]** 를 구성하는 방법의 예입니다.

   ![트리거 매개 변수](/help/assets/trigger-parameters.png)

* Mobile Services의 트리거 *및 트레이트* 페이지의 위치 서비스 머리글의 매개 변수는 위치 서비스의 데이터와 작동하지 않습니다.

   이러한 매개 변수는 Mobile Services에서 생성된 레거시 Places Service 데이터베이스에 대해서만 적용됩니다.
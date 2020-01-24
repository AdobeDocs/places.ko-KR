---
title: 인앱 알림
description: 이 섹션에서는 인앱 메시지에 위치 서비스를 사용하는 방법을 보여줍니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b

---


# 인앱 알림 {#places-push-messaging}

다음 정보는 위치 서비스 이벤트에서 트리거하도록 인앱 메시지를 구성하는 방법을 보여줍니다.

>[!IMPORTANT]
>
>메시지는 Analytics 히트에 있어야 합니다.

## 인앱 메시지

Mobile Services를 사용하면 Analytics로 전송되는 위치 데이터를 트리거 이벤트 및/또는 인앱 메시지의 조건으로 사용할 수 있습니다. In-App 메시지가 SDK에서 실행되어 Analytics에서 데이터를 처리할 때까지 기다릴 필요가 없는 경우 트리거가 발생하는 즉시 메시지가 실시간으로 나타날 수 있습니다.

### 로컬 알림

다음은 사용 가능한 인앱 메시지 유형 목록입니다.

* 전체 화면
* 경고
* 로컬 알림

이러한 유형은 SDK에 의해 트리거되기 때문에 인앱 메시지입니다. 앱이 백그라운드에 있을 때 로컬 알림이 표시되므로 푸시 알림의 모양과 느낌이 듭니다. 앱이 백그라운드에 있을 때 사용자가 POI에 들어오거나 종료하면 이러한 알림도 실시간으로 전달됩니다. 자세한 내용은 위치 모니터 [확장을](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md)참조하십시오.

### 전제 조건

시작하기 전에 Mobile Services에서 인앱 메시지를 전송하고 만드는 방법과 트리거가 작동하는 방식을 이해해야 합니다. 자세한 내용은 [인앱 메시지 만들기](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/inapp-messages/t-in-app-message.html)를 참조하십시오.

##  Experience Platform Launch의 규칙

인앱 메시지 트리거 규칙의 일부로 사용할 수 있는 데이터를 Analytics에 전송하는 경험 플랫폼 실행 규칙을 만들 수 있습니다. 사용 사례에 따라 Experience Platform 시작 규칙의 위치 확장 데이터를 이벤트 및/또는 조건으로 사용할 수 있습니다.

* 트리거 이벤트로 위치 데이터 사용

   예를 들어 사용자가 POI를 입력할 때 Analytics로 데이터를 보낼 수 있습니다.

* 위치 데이터를 조건으로 사용하여 이벤트를 트리거합니다.

   예를 들어 Places Service에서 다른 POI의 날씨에 대한 사용자 지정 메타데이터 태그를 만든 경우 해당 메타데이터를 규칙 조건의 매개 변수로 사용할 수 있습니다. 앞에서 설명한 POI 응모 이벤트와 함께 이 조건을 사용할 수 있지만, 조건을 모든 이벤트의 컨텍스트로 사용할 수도 있습니다.

적절한 이벤트 및 조건 매개 변수로 규칙을 설정한 후 데이터를 Analytics로 전송하는 작업을 구성하여 규칙 구성을 완료하십시오.

## 동작 만들기

작업을 만들려면

1. **[!UICONTROL Adobe Analytics]**확장을 선택합니다.
1. 드롭다운 **[!UICONTROL Action type]**목록에서**[!UICONTROL Track.]**
1. 작업 이름을 입력합니다.
1. 오른쪽 창에서 키-값 쌍을 **[!UICONTROL Context Data]**선택하여 Analytics로 전송할 컨텍스트 데이터를 설정합니다.

예를 들어 `poiname` 키와 값으로 선택할 `{%%Last Entered POI Name}` 수 있습니다.

>[!TIP]
>
>Analytics 처리 규칙을 설정하여 이 컨텍스트 데이터를 선택할 수 있습니다. 자세한 내용은 [처리 규칙](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-processing-rules.html)을 참조하십시오. 작업 *만들기의 예에서,*&#x200B;작업은 Analytics로 전송되는 POI 항목 이벤트를 설명하는 `poiname` 컨텍스트로 을 보냅니다.

![작업 만들기](/help/assets/configure-action.png)

다음은 전체 규칙의 예입니다.

![완료된 규칙](/help/assets/create-a-rule.png)

## Mobile Services에서 인앱 메시지 만들기

트리거 매개 변수의 일부로, 다음 방법 중 하나를 사용하여 위치 서비스의 데이터를 사용하여 메시지 대상을 만들 수 있습니다.

* 시작 또는 종료와 같은 위치별 작업 사용
* 컨텍스트 데이터로 전송되는 POI 메타데이터를 사용하여 대상 범위를 좁힙니다.

   이 옵션은 시작과 같은 위치별 동작과 함께 사용하거나 론치나 단추 클릭과 같은 다른 이벤트의 컨텍스트로 사용할 수 있습니다.

   다음은 이름에 있는 POI를 입력하는 사용자를 환영 받기 위해 인앱 메시지를 구성하는 **[!UICONTROL Adobe]**방법의 예입니다.

   ![트리거 매개 변수](/help/assets/trigger-parameters.png)

* Mobile Services의 트리거 *및 트레이트* 페이지의 위치 서비스 머리글의 매개 변수는 위치 서비스의 데이터와 작동하지 않습니다.

   이러한 매개 변수는 Mobile Services에서 생성된 레거시 Places Service 데이터베이스에 대해서만 적용됩니다.
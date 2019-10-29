---
title: 인앱 메시지
seo-title: 인앱 메시지
description: 이 섹션에서는 인앱 메시지에 위치 사용을 보여 줍니다.
seo-description: 이 섹션에서는 인앱 메시지에 위치 사용을 보여 줍니다.
translation-type: tm+mt
source-git-commit: 7985943cef606525401983c4c80862c277f41bf0

---


# 인앱 알림(#places-push-messaging)

장소 이벤트에서 트리거하도록 인앱 메시지를 구성하는 방법;메시지는 Analytics 히트에 있어야 합니다.

## 인앱 메시지

AMS를 사용하면 인앱 메시지에 대한 트리거 이벤트 및/또는 조건으로 Analytics로 전송되는 위치 데이터를 사용할 수 있습니다. 인앱 메시지는 SDK에서 실행되는 경우 트리거와 동시에 실시간으로 사용자에게 표시될 수 있으며 Analytics에서 데이터를 처리할 때까지 기다릴 필요가 없습니다.

로컬 알림:인앱 메시징에는 3가지 유형이 있습니다.

* 전체 화면
* 경고
* 로컬 알림을 참조하십시오.

이러한 유형은 SDK에 의해 트리거되기 때문에 인앱 메시지로 자격을 인정하지만 앱이 포그라운드에 있지 않은 상태에서 로컬 알림이 표시되는 것처럼 보이고 푸시 알림처럼 느껴집니다. 로컬 알림은 앱이 백그라운드에 있을 때 POI를 들어오거나 종료하면 사용자에게 실시간 알림을 전달하기 위한 좋은 옵션입니다. 위치 모니터링을 이해하려면 위치 모니터 확장 설명서를 참조하십시오(https://placesdocs.com/places-services-by-adobe-documentation/configure-places-in-the-sdk/places-monitor-extension).

### 전제 조건

* AMS에서 인앱 메시지를 전송하고 만드는 방법 및 트리거의 작동 방식을 이해합니다.

   자세한 내용은 [인앱 메시지 만들기](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/inapp-messages/t-in-app-message.html)를 참조하십시오.


## Experience Platform Launch에서 규칙 만들기

인앱 메시지 트리거 규칙의 일부로 사용할 수 있도록 Analytics에 올바른 데이터를 전송하는 시작 규칙을 만듭니다. 사용 사례에 따라 시작 규칙의 위치 확장 데이터를 이벤트 및/또는 조건으로 사용할 수 있습니다.

* 트리거 이벤트로 위치 데이터 사용 예를 들어 사용자가 POI를 입력할 때 Analytics로 데이터를 전송하려는 경우

* 위치 데이터를 조건으로 사용하여 이벤트를 트리거합니다. 예를 들어 위치 서비스에서 다른 POI의 날씨에 대한 사용자 지정 메타데이터 태그를 만든 경우, 아래 표시된 대로 해당 메타데이터를 규칙 조건에 대한 매개 변수로 사용할 수 있습니다. 이전에 설명한 POI 응모 이벤트에 이 조건을 사용할 수 있지만 모든 이벤트의 컨텍스트로 사용할 수도 있습니다.

적절한 이벤트 및 조건 매개 변수를 사용하여 규칙을 설정한 후에는 데이터를 Analytics로 보내는 작업을 구성하여 규칙 구성을 완료하십시오. 이렇게 하려면:

* Adobe Analytics를 확장으로 선택
* 작업 유형으로 "추적"을 선택합니다.
* 작업 이름 확인
* 이벤트와 함께 전송할 컨텍스트 데이터를 설정합니다. 컨텍스트 데이터 인터페이스를 사용하여 론치 데이터 요소를 Analytics로 보내려는 키 이름에 매핑합니다.

Analytics 처리 규칙은 이 컨텍스트 데이터를 수집하도록 설정할 수 있습니다. 필요한 경우 Analytics 처리 규칙 참조(https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-processing-rules.html)예를 들어 이 작업은 Analytics로 전송되는 POIentry 이벤트를 설명하는 컨텍스트로 poiname로 전송됩니다.

![작업 만들기](/help/assets/configure-action.png)

다음은 완료된 규칙이 어떻게 표시될지에 대한 예입니다.

![완료된 규칙](/help/assets/create-a-rule.png)

## AMS에서 인앱 메시지 만들기:

트리거 매개 변수의 일부로 위치 서비스의 데이터를 사용하여 메시지의 대상을 만듭니다.

* 시작 또는 종료와 같은 위치별 작업 사용
* 컨텍스트 데이터로 전송된 POI 메타데이터를 사용하여 대상 범위를 좁힙니다. 시작 또는 단추 클릭과 같은 위치 특정 동작과 함께 사용하거나 다른 이벤트의 컨텍스트로 사용할 수 있습니다.

   다음은 이름에 "Adobe"가 있는 POI를 입력하는 사용자를 환영 받기 위해 인앱 메시지를 설정하는 방법의 예입니다.

   ![트리거 매개 변수](/help/assets/trigger-parameters.png)

* AMS의 '위치' 머리글에 있는 매개 변수는 위치 서비스의 데이터와 함께 작동하지 않습니다. 이러한 매개 변수는 AMS에서 만든 레거시 위치 데이터베이스를 위한 것입니다.
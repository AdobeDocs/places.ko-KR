---
title: Places Service
description: '''장소 서비스''는 모바일 사용자의 참여를 이해하는 데 중요한 역할을 합니다. 모바일 앱 개발자는 이러한 컨텍스트를 활용하여 앱 디자인을 향상시키고 보다 개인화되고 매력적인 경험을 제공할 수 있습니다. '
translation-type: tm+mt
source-git-commit: 05b4d29aa7925f7a43e70c644e3cb88045cbe446
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 10%

---


# Places Service {#home}

![&quot;Places Service&quot;](/help/assets/places-service-header.png)

위치는 모바일 사용자를 파악하고 참여를 유도하는 중요한 컨텍스트 중 하나입니다. 모바일 앱 개발자는 이러한 컨텍스트를 활용하여 앱 디자인을 향상시키고 보다 개인화되고 매력적인 경험을 제공할 수 있습니다.

위치 서비스는 이전에 Adobe Experience Platform 위치 서비스라고 알려졌었던 서비스로서, 위치 정보를 가진 모바일 앱이 유연한 관심 영역 데이터베이스(POI)와 함께 사용하기 쉬운 리치 SDK 인터페이스를 사용하여 위치 컨텍스트를 이해할 수 있도록 해주는 지리적 위치 서비스입니다.

위치 서비스를 사용하면 다음을 수행할 수 있습니다.

* 다른 Adobe Experience Cloud 솔루션에서 활용할 수 있는 POI의 데이터베이스를 만들고 관리할 수 있습니다.
* 추가 속성을 지정하여 사용자 지정 메타데이터를 POI에 연결하여 보다 풍부하고 의미 있게 만들 수 있습니다.
* 맵에서 POI를 시각화하여 공간 컨텍스트를 손쉽게 파악하고 메타데이터 속성을 추가/편집할 수 있습니다.
* Adobe Experience Platform Launch에서 SDK를 구성하여 위치 기반 규칙 및 메타데이터 기반 조건을 정의합니다.
* 디바이스의 위치를 모니터링하기 위해 작성해야 하는 코드를 줄이고 위치 확장 기능을 사용하여 위치별 규칙을 자동으로 트리거합니다.

이를 통해 위치 신호로부터 실시간으로, 언제 그리고 어디서 이것이 중요한지를 취할 수 있습니다. 최적의 컨텍스트에 따라 모바일 참여도 향상

다음은 위치를 사용할 수 있는 몇 가지 방법입니다.

* 누군가 POI에 들어가면 실시간 알림 *을 보냅니다.경기장에 오신 것을 환영합니다.&quot;*
* 경쟁업체와 비교하여 자체 스토어의 발 트래픽을 분석할 수 있습니다.
* 위치 컨텍스트와 함께 고객 프로파일을 사용하여 오프라인 행동을 기반으로 고객을 세분화할 수 있습니다.
* 관련 있는 경우 매장 내 경험을 가진 사용자를 Target으로 지정합니다.

## 배치 서비스 구성 요소

Places Service는 다음 구성 요소로 구성됩니다.

* **웹 서비스**

   REST API를 사용하여 POI를 만들고 관리할 수 있습니다. REST API에 대한 자세한 내용은 라이브러리 [관리](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) 및 POI [관리를 참조하십시오](/help/web-service-api/api-usage/manage-pois/manage-pois.md).

* **POI 관리 인터페이스**

   맵에서 POI를 시각화하여 공간 컨텍스트를 파악하고 POI와 사용자 정의 메타데이터를 추가/편집할 수 있습니다.

* **위치 확장**

   모바일 앱의 위치 컨텍스트를 통합하는 멀티 플랫폼 모바일 API 인터페이스 SDK에 대한 자세한 내용은 [위치 확장을 참조하십시오](/help/places-ext-aep-sdks/places-extension/places-extension.md).

* **규칙 실행**

   시작 및 종료 이벤트를 사용하여 작업을 트리거할 수 있는 지능적인 실행 규칙. 또한 이 규칙을 통해 사용자 경험을 개인화하는 조건에 지리 특성을 사용할 수 있습니다.

* **위치 모니터 확장**

   모바일 앱에 임베드하여 사용자의 위치 변경 사항을 자동으로 모니터링하고 위치 규칙을 트리거할 수 있는 멀티 플랫폼 모바일 SDK입니다. 자세한 내용은 위치 모니터 [확장 기능을 참조하십시오](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

## 용어

다음은 이 문서에서 사용되는 몇 가지 일반적인 용어입니다.

* POI( **Point of Interest)** 는 조직의 지리적 위치입니다.

   이름, 반경, 주소, 범주 및 메타데이터 태그와 같은 특성을 사용하여 POI를 정의할 수 있습니다.

* 영어는 **POI의** 한 종류이다.

   이 POI 유형은 위도 및 경도 좌표로 정의된 가상 지리적 경계입니다.

* 비콘 **은** POI 유형입니다.

   이 POI 유형은 저전력 블루투스 신호를 방출하여 위치를 나타내는 물리적 장치입니다. 비콘 지원이 향후 릴리스에 제공될 예정입니다.

* **라이브러리**&#x200B;는 POI의 컬렉션으로, POI 1개가 아닌 세트에 규칙을 쉽게 연결하도록 그룹화됩니다.

* 익스텐션은 **모바일 앱에서 Place SDK를 통합하는 데 필요한 Experience Platform Launch 확장입니다** .

   경험에 위치 컨텍스트를 추가하기 위해 다른 모바일 SDK와 함께 사용하는 확장입니다.

* **조직**&#x200B;은 Adobe Experience Cloud에서 귀사를 식별하는 Adobe 엔티티입니다.

   일반적으로 조직은 회사 이름입니다. 그러나 한 회사는 둘 이상의 조직을 가질 수 있습니다. 조직 관리자는 그룹 및 사용자를 구성하고 단일 사인온 기능을 구성할 수 있습니다.

* **orgID**&#x200B;는 Adobe Experience Platform에서 조직을 나타내는 ID입니다.

   자세한 내용은 orgID [찾기를 참조하십시오](https://forums.adobe.com/thread/2339895).

* The **Experience Cloud ID** service provides a universal, persistent ID that identifies your visitors across all the solutions in the Experience Cloud.

   자세한 내용은 [개요](https://docs.adobe.com/content/help/ko-KR/id-service/using/intro/overview.html)를 참조하십시오.

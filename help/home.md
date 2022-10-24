---
title: 장소 서비스
description: 위치 서비스는 모바일 사용자의 참여를 이해하는 데 중요한 컨텍스트입니다. 이 컨텍스트를 사용하여 모바일 앱 개발자는 앱 디자인을 향상시키고 보다 개인화되고 매력적인 경험을 제공할 수 있습니다.
exl-id: 7369176f-c072-437a-9ee3-b463c5ff1d12
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 10%

---

# 장소 서비스 {#home}

위치는 모바일 사용자를 이해하고 참여하기 위한 중요한 컨텍스트입니다. 이 컨텍스트를 사용하여 모바일 앱 개발자는 앱 디자인을 향상시키고 보다 개인화되고 매력적인 경험을 제공할 수 있습니다.

이전에 Adobe Experience Platform 위치 서비스라고 알려진 위치 서비스는 위치를 인식하는 모바일 앱이 유연한 관심 영역(POI) 데이터베이스를 동반하는 풍부하고 사용하기 쉬운 SDK 인터페이스를 사용하여 위치 컨텍스트를 이해할 수 있도록 해주는 지리적 위치 서비스입니다.

위치 서비스를 사용하면 다음 작업을 수행할 수 있습니다.

* 다른 Adobe Experience Cloud 솔루션에서 활용할 수 있는 POI 데이터베이스를 만들고 관리합니다.
* 사용자 지정 메타데이터를 POI에 추가하여 추가 속성을 지정하여 더 풍부하고 의미 있게 만들 수 있습니다.
* 맵에서 POI를 시각화하여 공간 컨텍스트를 쉽게 이해하고 메타데이터 속성을 추가/편집합니다.
* 위치 트리거된 규칙 및 메타데이터 기반 조건을 정의하도록 Adobe Experience Platform Launch에서 SDK를 구성합니다.
* 장치의 위치를 모니터링하기 위해 써야 하는 코드를 줄이고 위치 확장을 사용하여 위치별 규칙을 자동으로 트리거합니다.

이를 통해 위치 신호로부터 실시간으로, 언제, 어디서 문제가 되는지 등의 작업을 수행할 수 있습니다. 올바른 컨텍스트는 모바일 참여 경험을 더 풍부하게 제공합니다.

위치를 사용할 수 있는 몇 가지 방법은 다음과 같습니다.

* 누군가 POI에 들어올 때 실시간 알림을 전송하고, *&quot;이봐..경기장에 오신 것을 환영합니다.&quot;*
* 경쟁사 매장과 자체 매장의 발 교통량을 분석합니다.
* 위치 컨텍스트에서 대상 프로필을 사용하여 오프라인 동작을 기반으로 대상을 세그먼트화합니다.
* 적절한 경우 매장 내 경험을 가진 Target

## Places Service 구성 요소

Places Service는 다음 구성 요소로 구성됩니다.

* **웹 서비스**

   Places REST API를 사용하여 POI를 만들고 관리할 수 있습니다. REST API에 대한 자세한 내용은 [라이브러리 관리](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) 및 [POI 관리](/help/web-service-api/api-usage/manage-pois/manage-pois.md).

* **POI 관리 인터페이스**

   맵에서 POI를 시각화하여 공간 컨텍스트를 이해하고 POI 및 사용자 지정 메타데이터를 추가/편집합니다.

* **위치 확장**

   다중 플랫폼 모바일 API 인터페이스를 사용하여 모바일 앱에서 위치 컨텍스트를 통합합니다. SDK에 대한 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md).

* **Launch 규칙**

   시작 및 종료 이벤트로 작업을 트리거할 수 있는 지능적인 Launch 규칙. 또한 조건에서는 지역 속성을 사용하여 경험을 개인화할 수 있습니다.

## 용어

다음은 이 설명서에서 사용되는 몇 가지 일반적인 용어입니다.

* A **관심 영역(POI)** 는 조직에 유용한 지리적 위치입니다.

   이름, 반경, 주소, 카테고리 및 메타데이터 태그와 같은 속성을 사용하여 POI를 정의할 수 있습니다.

* A **지오펜스** 는 POI 유형입니다.

   이 POI 유형은 위도 및 경도 좌표로 정의된 가상 지리적 경계입니다.

* A **beacon** 는 POI 유형입니다.

   이 POI 유형은 저전력 블루투스 신호를 방출하여 위치를 나타내는 물리적 장치입니다. 비콘 지원은 향후 릴리스에서 제공될 예정입니다.

* **라이브러리**&#x200B;는 POI의 컬렉션으로, POI 1개가 아닌 세트에 규칙을 쉽게 연결하도록 그룹화됩니다.

* An **확장** 는 모바일 앱에서 Places SDK를 통합하는 데 필요한 Experience Platform Launch 확장입니다.

   다른 모바일 SDK와 함께 사용하여 위치 컨텍스트를 경험에 추가할 수 있습니다.

* **조직**&#x200B;은 Adobe Experience Cloud에서 귀사를 식별하는 Adobe 엔티티입니다.

   일반적으로 조직은 회사 이름입니다. 그러나 한 회사에 두 개 이상의 조직이 있을 수 있습니다. 조직 관리자는 그룹 및 사용자를 구성하고 단일 사인온 기능을 구성할 수 있습니다.

* **orgID**&#x200B;는 Adobe Experience Platform에서 조직을 나타내는 ID입니다.

   자세한 내용은 [orgID 찾기](https://forums.adobe.com/thread/2339895).

* 다음 **Experience Cloud ID** 서비스는 Experience Cloud의 모든 솔루션에서 방문자를 식별하는 범용 영구 ID를 제공합니다.

   자세한 내용은 [개요](https://docs.adobe.com/content/help/ko-KR/id-service/using/intro/overview.html)를 참조하십시오.

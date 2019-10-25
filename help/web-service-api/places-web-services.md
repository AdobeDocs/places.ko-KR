---
title: '웹 서비스 API 개요 '
seo-title: '웹 서비스 API 개요 '
description: Adobe 고객은 Adobe Experience Cloud와 Adobe Experience Platform 솔루션에 적합한 위치 데이터와 적절한 경험을 적시에 적시에 적소에 제공할 수 있는 서비스를 제공합니다.
seo-description: Adobe 고객은 Adobe Experience Cloud와 Adobe Experience Platform 솔루션에 적합한 위치 데이터와 적절한 경험을 적시에 적시에 적소에 제공할 수 있는 서비스를 제공합니다.
translation-type: tm+mt
source-git-commit: e204958ac3acbf5fb45d2347987f35557be70e43

---


# 웹 서비스 API 개요 {#places-web-services-api}

Places는 Adobe 고객이 위치 데이터와 올바른 경험을 적시에 적시에 적시에 적소에 제공할 수 있도록 Adobe Cloud Platform 및 Adobe Experience Platform 솔루션을 보다 손쉽게 활용할 수 있는 일련의 서비스입니다.

웹 서비스 API를 사용하여 다음을 수행할 수 있습니다.

* 환경 관리
* 앱이 백그라운드에 있을 때에도 사용자의 위치 측정
* 중요한 데이터를 실시간으로 사용

이 섹션에서는 조직의 POI 데이터를 포함하는 REST API 및 POI 데이터베이스를 사용하는 방법에 대한 정보를 제공합니다.

## REST API

Places REST API를 사용하면 조직의 POI를 사용하여 프로그래밍 방식으로 작업할 수 있습니다. 이러한 API를 사용하면 라이브러리와 해당 라이브러리의 POI를 만들고, 업데이트하고, 삭제할 수 있습니다. 이러한 API는 JSON(JavaScript Object Notation) 표준을 사용하여 전송 및 수신되는 데이터의 형식을 지정합니다. JSON의 주요 이점은 API 쿼리를 개발자와 시스템에서 손쉽게 작성, 읽기 및 분석할 수 있다는 것입니다.

웹 서비스 API를 사용하려면 먼저 다음 요구 사항이 충족되었는지 확인하십시오.

* 위치는 조직에서 프로비저닝되며 사용자로서의 적절한 액세스 권한이 있습니다.

   자세한 내용은 아래 *조직 요구 사항* 섹션을 참조하십시오.

* 조직에서 [위치]가 프로비저닝되고 액세스 권한이 있으면 [장소]에 대한 Adobe 통합을 만드십시오.

   자세한 내용은 Adobe I/ *O 통합* 개요에서 [위치 통합을](/help/web-service-api/adobe-i-o-integration.md)참조하십시오.

추가 정보:

* 사용 가능한 API와 사용 방법에 대한 자세한 내용은 라이브러리 관리 및 [POI](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) 관리를 [참조하십시오](/help/web-service-api/api-usage/manage-pois/manage-pois.md).
* 이러한 API의 헤더 및 매개 변수에 대한 자세한 내용은 [머리글 및 매개 변수를](/help/web-service-api/api-usage/headers-and-parameters.md)참조하십시오.

## 조직 요구 사항 {#org-requirements}

웹 서비스 REST API에 액세스하려면 시스템 관리자에게 다음 작업이 완료되었는지 확인하십시오.

* 위치가 프로비저닝되어 조직에 표시됩니다.
* 조직에 추가되었습니다.
* 조직의 위치에 추가되었습니다.

   자세한 내용은 FAQ *에서 사용자 추가 및 경험* 플랫폼 시작을 [참조하십시오](/help/places-faqs.md).

* 귀하를 조직에 위치 개발자로 추가했습니다.

   개발자 역할에 대한 자세한 내용은 개발자 [관리를 참조하십시오](https://helpx.adobe.com/enterprise/using/manage-developers.html).
---
title: 웹 서비스 API 개요
description: Places Service는 Adobe 고객이 올바른 시간과 장소에 올바른 사람에게 올바른 경험과 위치 데이터로 Adobe Experience Cloud 및 Adobe Experience Platform 솔루션을 더 쉽게 하이드레이션할 수 있도록 하는 서비스 세트입니다.
exl-id: 9e7358d1-3ba0-4304-aeb2-fed7162afb57
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# 웹 서비스 API 개요 {#places-web-services-api}

Places Service는 Adobe 고객이 올바른 시간과 장소에 올바른 사람에게 올바른 경험과 위치 데이터로 Adobe Cloud Platform 및 Adobe Experience Platform 솔루션을 더 쉽게 하이드레이션할 수 있도록 하는 서비스 세트입니다.

웹 서비스 API를 사용하면 다음 작업을 수행할 수 있습니다.

* 지오펜스 관리
* 앱이 백그라운드에 있는 경우에도 사용자의 위치를 측정합니다.
* 중요한 경우 실시간으로 데이터 사용

이 섹션에서는 REST API 및 조직의 POI 데이터가 포함된 POI 데이터베이스를 사용하는 방법에 대한 정보를 제공합니다.

## REST API

Places Service REST API를 사용하면 조직의 POI를 프로그래밍 방식으로 사용할 수 있습니다. 이러한 API를 사용하면 라이브러리와 해당 라이브러리의 POI를 만들고, 업데이트하고, 삭제할 수 있습니다. 이러한 API는 JavaScript JSON(개체 표기법) 표준을 사용하여 보내고 받는 데이터의 형식을 지정합니다. JSON의 주요 장점은 개발자와 시스템이 API 쿼리를 쉽게 작성하고 읽고 구문 분석할 수 있다는 것입니다.

웹 서비스 API를 사용하기 전에 다음 요구 사항이 충족되었는지 확인하십시오.

* Places Service는 조직에서 프로비저닝되며 사용자는 적절한 액세스 권한을 가지고 있습니다.

  자세한 내용은 [통합 개요 및 필수 구성 요소](/help/web-service-api/adobe-i-o-integration.md)에서 *사용자 액세스를 위한 필수 구성 요소*&#x200B;를 참조하십시오.

* 조직에서 Places Service가 프로비저닝되고 액세스 권한이 있으면 Places Service에 대한 Adobe 통합을 만듭니다.

  자세한 내용은 [통합 개요 및 필수 구성 요소](/help/web-service-api/adobe-i-o-integration.md)의 *Places Service 통합 만들기*&#x200B;를 참조하십시오.

추가 정보:

* 사용 가능한 API 및 사용 방법에 대한 자세한 내용은 [라이브러리 관리](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) 및 [POI 관리](/help/web-service-api/api-usage/manage-pois/manage-pois.md)를 참조하십시오.
* 이러한 API의 헤더 및 매개 변수에 대한 자세한 내용은 [헤더 및 매개 변수](/help/web-service-api/api-usage/headers-and-parameters.md)를 참조하십시오.

---
title: '웹 서비스 API 개요 '
description: Places Service는 Adobe 고객이 Adobe Experience Cloud 및 Adobe Experience Platform 솔루션에 적합한 위치 데이터와 경험을 적시에 적시에 적소에 제공할 수 있도록 해주는 서비스 세트입니다.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---


# 웹 서비스 API 개요 {#places-web-services-api}

Places Service는 Adobe 고객이 Adobe Cloud Platform 및 Adobe Experience Platform 솔루션에 적합한 위치 데이터와 경험을 적시에 적시에 적소에 제공할 수 있도록 해주는 서비스 세트입니다.

웹 서비스 API를 통해 다음을 수행할 수 있습니다.

* 환경 관리
* 앱이 백그라운드에 있을 때에도 사용자의 위치를 측정합니다.
* 중요한 데이터를 실시간으로 사용

이 섹션에서는 조직의 POI 데이터가 포함된 REST API 및 POI 데이터베이스를 사용하는 방법에 대한 정보를 제공합니다.

## REST API

Places Service REST API를 사용하면 조직의 POI에서 프로그래밍 방식으로 작업할 수 있습니다. 이러한 API를 사용하면 해당 라이브러리에서 라이브러리와 POI를 만들고, 업데이트하고, 삭제할 수 있습니다. 이러한 API는 JSON(JavaScript Object Notation) 표준을 사용하여 전송 및 수신되는 데이터의 형식을 지정합니다. JSON의 주요 이점은 API 쿼리를 개발자와 시스템에서 손쉽게 작성, 읽기 및 분석할 수 있다는 것입니다.

웹 서비스 API를 사용하려면 먼저 다음 요구 사항이 충족되었는지 확인하십시오.

* 배치 서비스는 조직에서 프로비저닝되며 사용자로 적절한 액세스 권한을 가집니다.

   자세한 내용은 *통합 개요 및 사전 요구 사항* 에서 사용자 [에 액세스하기 위한 사전 요구 사항을 참조하십시오](/help/web-service-api/adobe-i-o-integration.md).

* 조직에서 [장소 서비스]가 프로비저닝되고 액세스 권한이 있으면 [장소 서비스]에 대한 Adobe 통합을 만듭니다.

   자세한 내용은 *통합 개요와 사전 요구 사항* 에서 장소 서비스 통합 [만들기를 참조하십시오](/help/web-service-api/adobe-i-o-integration.md).

추가 정보:

* 사용 가능한 API에 대한 정보 및 사용 방법에 대한 자세한 내용은 라이브러리 [관리](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) 및 POI [관리를 참조하십시오](/help/web-service-api/api-usage/manage-pois/manage-pois.md).
* 이러한 API의 헤더 및 매개 변수에 대한 자세한 내용은 [머리글 및 매개 변수를 참조하십시오](/help/web-service-api/api-usage/headers-and-parameters.md).
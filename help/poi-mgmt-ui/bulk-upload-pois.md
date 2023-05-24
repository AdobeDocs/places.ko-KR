---
title: POI 일괄 업로드
description: 이 섹션에서는 POI를 대량 업로드하는 방법에 대한 정보를 제공합니다.
exl-id: 72704bfc-5837-4439-bdb2-e77ddf935639
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# POI 일괄 업로드 {#bulk-upload-pois}

다음 **POI 가져오기** 위치 서비스의 버튼을 사용하여 CSV 파일을 사용하여 새 POI를 대량 업로드할 수 있습니다. 필요한 데이터 열과 선택적 사용자 지정 메타데이터를 추가하는 방법을 보여주는 샘플 스프레드시트 템플릿이 제공됩니다.

![일괄 가져오기 화면](/help/assets/Bulk-import.png)

일괄 가져오기 및 일괄 편집 프로세스를 보여 주는 이 비디오 를 참조하십시오.

<!--I changed this embed to a link to pass validation. We should not link to youtube videos, so please upload this to MCP-->

[Places Service 일괄 가져오기 및 편집 POI](https://www.youtube.com/watch?v=75qVtirsXhg)

## Python API 스크립트

웹 서비스 API를 사용하여 .csv 파일의 POI를 POI 데이터베이스로 일괄 가져올 수 있도록 일련의 Python 스크립트가 생성되었습니다. 이러한 스크립트는 이 오픈 소스에서 다운로드할 수 있습니다. [git 리포지토리](https://github.com/adobe/places-scripts).

이러한 스크립트를 실행하기 전에 웹 서비스 API에 액세스하려면 다음을 참조하십시오. *사용자 액세스를 위한 사전 요구 사항* 위치: [통합 개요 및 사전 요구 사항](/help/web-service-api/adobe-i-o-integration.md).

다음은 스크립트에 대한 정보입니다.

>[!TIP]
>
>이 정보는 의 추가 정보 파일에도 포함되어 있습니다. [git 리포지토리](https://github.com/adobe/places-scripts).

## CSV 파일로 내보낼 때 시간별 세부기간이 작동하지 않는 문제를 해결했습니다

샘플 .csv 파일, `places_sample.csv`는 이 패키지의 일부이며 필수 헤더와 샘플 데이터 행을 포함합니다. 이러한 헤더는 모두 소문자이며 위치 데이터베이스에서 사용되는 예약된 메타데이터 키에 해당합니다. .csv 파일에 추가하는 열은 각 POI에 대한 별도의 메타데이터 섹션에서 POI 데이터베이스에 키/값 쌍으로 추가되고 헤더 값이 키로 사용됩니다.

다음은 사용해야 하는 열 및 값 목록입니다.

* `lib_id`

   POI 데이터베이스에서 가져온 유효한 라이브러리 ID입니다.

* `type`

   Point는 현재 유일하게 유효한 값입니다.

* `longitude`

   -180과 180 사이의 값입니다.

* `latitude`

   -85와 85 사이의 값입니다.

* `radius`

   10과 20,000 사이의 값입니다.

### 열 값

Places Service UI에는 다음 열의 값이 사용됩니다.

* 위치 서비스 UI 맵에서 POI의 위치를 나타내는 핀 색상으로 사용되는 색입니다.
   * 유효한 값은 &quot;&quot;, #3E76D0, #AA99E8, #DC2ABA, #FC685B, #FC962E, #F6C436, #BECE5D, #61B56B 및 #3DC8DE, &quot;&quot;입니다.
   * 값을 비워 두면 Places Service UI는 파란색을 기본 색상으로 사용합니다.

      이 값은 각각 파란색(#3E76D0), 보라색(#AA99E8), 푸시아(#DC2ABA), 주황색(#FC685B), 밝은 주황색(#FC962E), 노란색(#F6C436), 연한 녹색(#BECE5D), 녹색(#61B56B) 및 연한 파란색(#3DC8DE)에 해당합니다.

* 아이콘: 위치 서비스 UI 맵에서 POI의 위치를 나타내는 핀에 있는 아이콘으로 사용됩니다.

   * 유효한 값은 &quot;&quot;, shop, hotelbed, car, airplane, train, ship, stadium, amusementpark, anchor, beaker, bell, bid, book, box, 서류 가방, browse, brush, building, calculator, camera, clock, education, flashlight, follow, game, female, male, gift, hammer, heart, home, key, launch, lightbulb, mailbox, money, pin, promote, ribbon, shoppingCart, star, target, teapot, thumbDown, thumbUp, trap, trophy, wrench입니다.

      아이콘 값은 다음 그림에 표시되는 순서대로 나열됩니다.

      ![UI의 아이콘](/help/assets/UI_icons.png)

   * 값을 비워 두면 UI는 별표를 기본 아이콘으로 사용합니다.

* 언급되지 않은 열은 비워 둘 수 있습니다.

## 스크립트 실행

1. 에서 파일 다운로드 [git 리포지토리](https://github.com/adobe/places-scripts) 로컬 디렉터리로 이동합니다.
1. 텍스트 편집기에서 `config.py` 파일을 만들고 다음 작업을 완료하십시오.

   a. 다음 변수 값을 문자열로 편집합니다.

   * `csv_file_path`

      다음으로 이동하는 경로입니다 `.csv`  파일.

   * `access_code`

      Adobe IMS 호출에서 가져온 액세스 코드입니다. 이 액세스 코드를 얻는 방법에 대한 자세한 내용은 *사용자 액세스를 위한 사전 요구 사항* 위치: [통합 개요 및 사전 요구 사항](/help/web-service-api/adobe-i-o-integration.md).

   * `org_id`

      POI를 가져올 Experience Cloud 조직 ID입니다. 조직 ID를 가져오는 방법에 대한 자세한 내용은 *사용자 액세스를 위한 사전 요구 사항* 위치: [통합 개요 및 사전 요구 사항](/help/web-service-api/adobe-i-o-integration.md).

   * `api_key`

      Adobe I/O Places 통합에서 가져온 Places REST API 키입니다. API 키를 가져오는 방법에 대한 자세한 내용은 *사용자 액세스를 위한 사전 요구 사항* 위치: [통합 개요 및 사전 요구 사항](/help/web-service-api/adobe-i-o-integration.md).
   b. 변경 사항을 저장합니다.

1. 터미널 창에서 `…/places-scripts/import/` 디렉토리.
1. 입력 `python ./places_import.py` 을 누르고 **[!UICONTROL 입력]** (**[!UICONTROL 반환]**) 키.


## CSV 검사 미리 가져오기

스크립트는 처음에 .csv 파일에 대해 다음 검사를 완료합니다.

* 여부 `.csv` 파일이 지정되었습니다.
* 파일 경로가 유효한지 여부.
* 예약된 메타데이터 머리글을 포함할지 여부입니다.

   예약된 메타데이터 헤더는 lib_id, 이름, 설명, 유형, 경도, 위도, 반경, 국가, 주, 도시, 거리, 카테고리, 아이콘 및 색입니다.

   >[!TIP]
   >
   >머리글은 모두 소문자이며 순서에 관계없이 나열할 수 있습니다.

* CSV 파일 섹션에 지정된 열의 값을 확인합니다.

오류가 발견되면 스크립트는 오류를 인쇄하고 중단됩니다. 오류가 발견되지 않으면 스크립트는 POI를 1000개 묶음으로 가져오려고 시도합니다. 배치를 성공적으로 가져오면 스크립트는 상태 코드 200을 보고합니다. 배치를 성공적으로 가져오지 못하면 오류가 보고됩니다.

## 단위 테스트

단위 테스트는 `tests.py` 파일, 각 가져오기 요청 전에 실행해야 하며 모두 전달해야 합니다. 새 코드와 함께 추가 테스트를 추가해야 합니다. 테스트를 실행하려면 `…/places-scripts/import/` 디렉토리, 입력 `python ./places_import.py` 터미널에서.

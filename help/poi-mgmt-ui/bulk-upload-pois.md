---
title: POI 일괄 업로드
description: 이 섹션에서는 POI를 일괄 업로드하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 1ffc1f4237dfb872614a4bffd43d3fdaefc62fa9
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# POI 일괄 업로드 {#bulk-upload-pois}

장소 서비스의 **POI** 가져오기 단추를 사용하여 CSV 파일을 사용하여 새 POI를 일괄 업로드할 수 있습니다. 필요한 데이터 열과 선택적 사용자 지정 메타데이터를 추가하는 방법을 보여주는 샘플 스프레드시트 템플릿이 제공됩니다.

![벌크 가져오기 화면](/help/assets/Bulk-import.png)

벌크 가져오기 및 벌크 편집 프로세스를 보여주는 비디오는 다음과 같습니다.

>[!VIDEO](https://www.youtube.com/watch?v=75qVtirsXhg)

## Python API 스크립트

웹 서비스 API를 사용하여 .csv 파일의 POI를 POI 데이터베이스로 일괄 가져오는 작업을 단순화하기 위해 Python 스크립트 세트가 만들어졌습니다. 이러한 스크립트는 이 오픈 소스 git 보고서에서 [다운로드할 수 있습니다](https://github.com/adobe/places-scripts).

이러한 스크립트를 실행하기 전에 웹 서비스 API에 액세스하려면 *통합 개요 및 사전 요구 사항* 에서 사용자 액세스에 대한 사전 요구 사항 [을 참조하십시오](/help/web-service-api/adobe-i-o-integration.md).

다음은 스크립트에 대한 몇 가지 정보입니다.

>[!TIP]
>
>이 정보는 git 보고서의 추가 정보 파일에도 [포함되어 있습니다](https://github.com/adobe/places-scripts).

## CSV 파일로 내보낼 때 시간별 세부기간이 작동하지 않는 문제를 해결했습니다

샘플 .csv 파일 `places_sample.csv`은 이 패키지의 일부이며 필요한 헤더와 샘플 데이터 행을 포함합니다. 이러한 헤더는 모두 소문자이며 위치 데이터베이스에서 사용되는 예약된 메타데이터 키에 해당합니다. .csv 파일에 추가하는 열은 각 POI에 대한 별도의 메타데이터 섹션에 키/값 쌍으로 POI 데이터베이스에 추가되고 헤더 값이 키로 사용됩니다.

다음은 사용해야 하는 열과 값의 목록입니다.

* `lib_id`

   POI 데이터베이스에서 얻은 유효한 라이브러리 ID.

* `type`

   현재 유효한 값은 포인트뿐입니다.

* `longitude`

   -180에서 180 사이의 값입니다.

* `latitude`

   -85에서 85 사이의 값입니다.

* `radius`

   10에서 20,000 사이의 값입니다.

### 열 값

다음 열 값은 위치 서비스 UI에서 사용됩니다.

* 색상에 사용됩니다. 이 색상은 Places Service UI 맵에서 POI의 위치를 나타내는 핀 색상으로 사용됩니다.
   * 유효한 값은 &quot;&quot;, #3E76D0, #AA99E8, #DC2ABA, #FC685B, #FC962E, #F6C436, #BECE5D, #61B56입니다. b, #3DC8DE 및 &quot;&quot;를 참조하십시오.
   * 값을 비워 두면 배치 서비스 UI에서 파란색을 기본 색상으로 사용합니다.

      값은 파란색(#3E76D0), 자주색(#AA99E8), 푸시아(#DC2ABA), 주황(#FC685B), 연한 주황색(#FC962E), 노란색(#F6C436), 연한 녹색( #BECE5D), 녹색(#61B56B) 및 연한 파랑(#3DC8DE)입니다.

* 아이콘 - 배치 서비스 UI 맵에서 POI의 위치를 나타내는 핀의 아이콘으로 사용됩니다.

   * 유효한 값은 &quot;&quot;, 상점, 호텔베드, 자동차, 기차, 배, 스타디움, 오락장, 공원, 앵커, 벨, 입찰, 책, 서류, 서류가방, 찾아보기, 브로셔, 건물, 계산기, 카메라, 시계, 교육, 팔로우, 게임, 여성, 남성, 선물, 햄머, 심장, 열쇠, 실행, lightroom, 사서함, 핀, 홍보, 쇼핑 카트, 스타, 타겟입니다. teapot, thumbDown, thumbUp, trap, trophy, 공구니

      아이콘 값은 다음 그림에 표시된 순서대로 나열됩니다.

      ![ui의 아이콘](/help/assets/UI_icons.png)

   * 값을 비워 두면 UI에서 별을 기본 아이콘으로 사용합니다.

* 언급되지 않은 열은 비워 둘 수 있습니다.

## 스크립트 실행

1. git 보고서에서 [로컬](https://github.com/adobe/places-scripts) 디렉토리로 파일을 다운로드합니다.
1. 텍스트 편집기에서 파일을 열고 `config.py` 다음 작업을 완료합니다.

   a. 다음 변수 값을 문자열로 편집합니다.

   * `csv_file_path`

      이 경로가 `.csv` 파일 경로입니다.

   * `access_code`

      Adobe IMS 호출에서 얻은 액세스 코드입니다. 이 액세스 코드를 얻는 방법에 대한 자세한 내용은 *통합 개요 및 사전 요구 사항* 에서 사용자 액세스 [](/help/web-service-api/adobe-i-o-integration.md)사전 요구 사항을 참조하십시오.

   * `org_id`

      POI를 가져올 Experience Cloud orgID. 조직 ID를 얻는 방법에 대한 자세한 내용은 *통합 개요 및 사전 요구 사항* 에서 사용자 액세스 [를 위한 사전 요구 사항을 참조하십시오](/help/web-service-api/adobe-i-o-integration.md).

   * `api_key`

      Adobe I/O Places 통합에서 가져온 Places REST API 키입니다. API 키를 얻는 방법에 대한 자세한 내용은 *통합 개요 및 사전 요구 사항* 에서 사용자 액세스 [](/help/web-service-api/adobe-i-o-integration.md)사전 요구 사항을 참조하십시오.
   b. 변경 내용을 저장합니다.

1. 터미널 창에서 `…/places-scripts/import/` 디렉토리로 이동합니다.
1. 키 `python ./places_import.py` 를 입력하고 **[!UICONTROL enter]** (**[!UICONTROL return]**) 키를 누릅니다.


## CSV 검사 미리 가져오기

스크립트는 처음에 .csv 파일에서 다음 검사를 완료합니다.

* 파일을 `.csv` 지정했는지 여부.
* 파일 경로가 유효한지 여부.
* 예약된 메타데이터 헤더가 포함되어 있는지 여부.

   예약된 메타데이터 헤더는 lib_id, 이름, 설명, 유형, 경도, 위도, 반경, 국가, 시, 거리, 카테고리, 아이콘 및 색상입니다.

   >[!TIP]
   >
   >헤더는 모두 소문자이며 순서에 관계없이 나열될 수 있습니다.

* CSV 파일 섹션에 지정된 열 값을 확인합니다.

오류가 발견되면 스크립트가 오류를 인쇄하여 중단됩니다. 오류가 없는 경우 스크립트는 POI를 1000개의 배치로 가져오려고 합니다. 배치를 성공적으로 가져오면 스크립트에서 상태 코드 200을 보고합니다. 배치를 성공적으로 가져오지 못하면 오류가 보고됩니다.

## 단위 테스트

단위 테스트는 `tests.py` 파일에 있으며 각 풀 요청 전에 실행되어야 하며 모두 통과해야 합니다. 새로운 코드와 함께 추가 테스트를 추가해야 합니다. 테스트를 실행하려면 `…/places-scripts/import/` 디렉토리로 이동하고 터미널 `python ./places_import.py` 에 입력합니다.

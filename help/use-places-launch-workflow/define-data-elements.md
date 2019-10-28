---
title: 데이터 요소 정의
seo-title: 데이터 요소 정의
description: 이 섹션에서는 Experience Platform Launch for Places에서 데이터 요소를 만들고, 사용하고, 게시하는 방법에 대한 정보를 제공합니다.
seo-description: '이 섹션에서는 Experience Platform Launch for Places에서 데이터 요소를 만들고, 사용하고, 게시하는 방법에 대한 정보를 제공합니다. '
translation-type: tm+mt
source-git-commit: 5d438fdd712c85101d546ed82f8ad155010cfb91

---


# Define a data element {#define-data-elements}

다음 정보는 데이터 요소와 작성 및 게시 방법을 이해하는 데 도움이 됩니다.

## 데이터 요소 정보

데이터 요소는 애플리케이션의 데이터 사전을 위한 기본 요소이며 마케팅 및 광고 기술 전반에 걸쳐 데이터를 수집, 구성 및 전달하는 데 사용됩니다.

데이터 요소는 값을 방문자 ID, 통신사 이름, 광고 ID, 푸시 ID 등에 매핑할 수 있는 변수입니다. Experience Platform Launch에서 변수 이름으로 이 값을 참조할 수 있습니다. 이 데이터 요소 모음은 규칙(이벤트, 조건 및 작업)을 작성하는 데 사용할 수 있는 정의된 데이터의 사전이 되며, 이 사전은 Experience Platform Launch에서 공유되며, 여기에서 이 사전은 속성의 확장자와 함께 사용할 수 있습니다.

위치 확장 기능을 사용하면 다음 타겟의 값을 참조할 수 있습니다.

* 현재 POI로, 고객이 현재 있는 POI를 나타냅니다.

   사용자가 여러 POI에 있는 경우 등급이 높은 라이브러리에 속합니다. 여러 POI가 가장 높은 등급 라이브러리에 속한 경우 반경이 가장 작은 POI가 선택됩니다.
* 사용자가 종료한 가장 최근 POI를 가리키는 마지막 종료한 POI입니다.
* 마지막으로 입력한 POI입니다. POI는 사용자가 입력한 최신 POI를 나타냅니다.

각 POI에는 다음 데이터 참조가 포함되어 있습니다.

* **[!UICONTROL Category]**:POI 부문
* **[!UICONTROL City]**:POI 시
* **[!UICONTROL Country]**:POI 국가
* **[!UICONTROL Latitude]**:POI의 위도
* **[!UICONTROL Longitude]**:POI의 경도
* **[!UICONTROL Metadata]**:POI의 사용자 지정 메타데이터
* **[!UICONTROL Name]**:POI 지역
* **[!UICONTROL Radius]**:POI 반경
* **[!UICONTROL Region ID]**:POI의 ID
* **[!UICONTROL Region/State]**:POI의 지역, 주 또는 주

### 데이터 요소 만들기

1. 앱의 속성 페이지에서 **[!UICONTROL Data Elements]** 탭을 클릭합니다.

2. 클릭 **[!UICONTROL Create New Data Element]**.

3. 설치된 확장 프로그램 목록에서 을 **[!UICONTROL Places]**&#x200B;찾습니다.

4. 드롭다운 **[!UICONTROL Data Element Type]** 목록에서 이 데이터 요소에 대한 데이터 참조를 선택합니다.

5. POI 대상을 선택합니다.

6. 이 데이터 요소가 사용자 지정 메타데이터 참조인 경우 메타데이터 키를 선택합니다.

7. 데이터 요소의 이름을 입력하고 를 **[!UICONTROL Save]**&#x200B;클릭합니다.

   ![데이터 요소 만들기](/help/assets/create-de-7-v3.png)


## 데이터 요소 사용

데이터 요소가 만들어지면 데이터 요소 선택기가 있으면 규칙 구성 요소의 데이터 요소를 사용할 수 있습니다.

![데이터 요소 사용](/help/assets/use-de-v2.png)

데이터 요소 선택기가 규칙 구성 요소에 없는 경우 데이터 요소 이름을 **[!UICONTROL %%]** 토큰으로 래핑하여 데이터 요소를 사용할 수 있습니다.
예를 들어 데이터 요소 이름이 **[!UICONTROL Last POI City]**&#x200B;인 경우 텍스트 입력에 추가할 **[!UICONTROL LAST POI City]** 수 있습니다.


## 데이터 요소 게시

규칙 구성 요소에서 데이터 요소를 사용하는 경우 이러한 데이터 요소도 라이브러리에 포함되고 게시되어야 합니다.

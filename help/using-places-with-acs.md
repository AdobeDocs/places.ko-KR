---
title: Adobe Campaign Standard에서 위치 사용
seo-title: Adobe Campaign Standard에서 위치 사용
description: 고객의 선호도 및 습관에 대한 심층적인 이해는 성공적인 마케팅 캠페인의 핵심입니다. 사용자가 실제 위치를 방문했는지 여부를 알면 소비자와 관계를 형성할 때 매우 중요한 컨텍스트를 추가할 수 있습니다.
seo-description: 고객의 선호도 및 습관에 대한 심층적인 이해는 성공적인 마케팅 캠페인의 핵심입니다. 사용자가 실제 위치를 방문했는지 여부를 알면 소비자와 관계를 형성할 때 매우 중요한 컨텍스트를 추가할 수 있습니다.
translation-type: tm+mt
source-git-commit: d7c5fe5d7a20a647240114d25307373b493ae2f5

---


# Adobe Campaign Standard에서 위치 사용 {#places-with-acs}

*지난 주에 우리를 방문해주셔서 감사합니다, 우리는 다음 방문에 당신을 위해 깜짝 선물을 드리고 싶습니다!*

고객의 선호도 및 습관에 대한 심층적인 이해는 성공적인 마케팅 캠페인의 핵심입니다. 사용자가 검색한 항목과 이전 구매 내역은 고객 타깃팅에 큰 역할을 합니다. 사용자가 실제 위치를 방문했는지 여부를 알면 소비자와 관계를 형성할 때 매우 중요한 컨텍스트를 추가할 수 있습니다.

eMarketer의 최근 보고서에 따르면, 85%의 고실적 리테일 업체는 위치가 마케팅 활동에 매우 중요하다고 생각합니다. 또한 북미 지역의 58% 이상의 리테일 업체는 고객 경험을 향상시키기 위해 근접성/위치 기술에 투자할 계획입니다.

![](/help/assets/using-loc-services-acs_0.png)

스마트폰 사용 경험에 있어 위치가 얼마나 중요한지 생각해 보십시오. 가까운 레스토랑, 주유소, 식료품점 또는 기타 서비스를 찾기 위해 얼마나 자주 스마트폰을 요청하세요.

따라서 브랜드 기업은 마케팅 캠페인에 위치를 활용할 수 있는 방법을 모색해야 합니다. 이 안내서에서는 강력한 Adobe Experience Platform Experience Platform 위치 서비스를 활용하여 Adobe Campaign Standard를 통해 위치 컨텍스트를 메시지에 추가하여 POI(History Point Of Interest) 항목을 기반으로 개인화된 푸시 알림 또는 인앱 메시지를 배포하는 방법을 소개합니다.

시작하기 전에 이 안내서에서는 Adobe Campaign Standard 확장 기능이 있는 Adobe Experience Platform Mobile SDK로 구성된 모바일 애플리케이션이 있다고 가정합니다. Adobe Experience Platform Mobile SDK 및 Campaign Standard 외에도 Experience Platform 위치 서비스를 이용할 수 있어야 합니다.

## 전제 조건

1. Adobe Experience [Platform Mobile](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) SDK를 앱에 통합합니다.
1. Adobe Campaign [Standard](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) Extension을 모바일 앱 구성에 추가합니다.
1. [하나 이상의 POI를 만듭니다](/help/places-database-management-1/managing-pois-in-the-places-ui.md).

>[!TIP]
>
>POI를 일괄 업로드하거나 관리하는 방법을 찾고 있는 경우 이 [스크립트를 참조하여 CSV 파일에서 POI를 업로드하십시오](https://github.com/adobe/places-scripts) . 또한 위치 [API를](/help/places-rest-apis/api-usage/api-usage.md) 사용하여 관심 영역을 만들거나 관리할 수 있습니다.

장소에 대한 액세스 권한이 없는 경우 여기에서 [액세스 권한을](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4fkr821yYptFo-ghlnlXCyhUM0dQVkJCSzVDMFNGWEFXWUUwNEJWSjhSRS4u)요청할 수 있습니다.

### 애플리케이션에서 위치 확장 기능 활성화 및 설치

위치 인터페이스에서 관심 영역을 만든 후 애플리케이션에 위치 기능을 추가해야 합니다.

1. 애플리케이션에서 위치 및 위치 모니터 확장 기능을 활성화하는 방법에 따라 수행합니다.
1. 위치 확장 기능에서 이전에 만든 적절한 POI 라이브러리를 선택했는지 확인합니다.

   추가 라이브러리는 언제든지 확장 구성에 추가할 수 있습니다.

1. 이러한 구성을 라이브러리에 추가하고 Launch에서 구성 변경 사항을 게시했는지 확인합니다.
1. UICONTROL **[시작 환경]** 탭에서 설치 지침 아이콘을 클릭하여 해당 CocoaPod 및 Gradle 파일을 앱 프로젝트로 다운로드하는 지침을 봅니다.
1. 애플리케이션에서 위치 배경 모드를 애플리케이션에 추가하는 지침에 따라 위치 위치 모니터를 시작합니다.
1. 디바이스 시뮬레이터를 통해 애플리케이션을 테스트하여 디바이스 위치 스푸핑에 따라 관심 영역 근처에서 애플리케이션 요청을 볼 수 있습니다.

### Experience Platform Launch에서 데이터 요소 만들기

응용 프로그램에서 [위치 및 위치 모니터] 확장이 올바르게 작동하는지 확인한 후 Experience Platform Launch에서 데이터 요소를 만들어 익스텐션에서 제공되고 Mobile SDK 이벤트 허브를 통해 제공되는 정보를 읽습니다. 데이터 요소는 기본적으로 클라이언트 애플리케이션에서 데이터를 검색하는 별칭으로 작동합니다. 위치 확장 기능을 통해 데이터를 검색할 데이터 요소를 몇 개 만들어 보겠습니다.

1. Experience Platform Launch 모바일 속성에서 **[!UICONTROL Data Elements]** 탭을 클릭하고 **[!UICONTROL Add Data Element]**&#x200B;을 클릭합니다.
1. 확장 메뉴에서 을 **[!UICONTROL Places]**&#x200B;선택합니다.
1. 드롭다운 목록에서 **[!UICONTROL Data Element]** [!UICONTROL 이름} ****&#x200B;을 선택합니다.
1. 오른쪽 창에서 사용자가 현재 있는 POI의 이름을 검색할 **[!UICONTROL Current POI]** 이름을 선택할 수 있습니다.

   * **[!UICONTROL Last Entered]** 사용자가
   * **[!UICONTROL Last Exited]** 에서 사용자가 마지막으로 남긴 POI의 이름을 제공합니다.

1. Select **[!UICONTROL Last Entered]**.
1. 데이터 요소의 이름(예: **[!UICONTROL Last Entered POI Name]**&#x200B;를 입력하고 **[!UICONTROL Save]**&#x200B;클릭합니다.


   ![](/help/assets/using-loc-services-acs_1.png)

1. 위의 동일한 단계를 반복하여 마지막으로 입력한 POI 위도, *마지막으로 입력한 POI 경도*, *마지막으로 입력한 POI*&#x200B;반경에 *대한 데이터 요소를 만듭니다*.

위치에 대한 데이터 요소 외에 앱 ID 및 Experience Cloud ID에 대한 *모바일* 코어 데이터 요소도 *만들었는지 확인하십시오*.

### 위치 데이터를 Adobe Campaign Standard로 전송하는 규칙 만들기

경험 플랫폼 론치의 규칙을 사용하면 이벤트 트리거를 기반으로 복잡한 다중 솔루션 워크플로우를 만들 수 있습니다. 새 규칙을 만들거나 기존 규칙을 변경하고 업데이트를 모바일 애플리케이션에 동적으로 배포할 수 있습니다. 이 예에서는 사용자가 지리적 제약을 받는 POI에 들어갈 때 트리거되는 규칙을 만듭니다. 규칙이 트리거되면 업데이트를 Campaign Standard로 보내 사용자의 특정 POI에 대한 항목을 기록합니다. 이 POI 파섹

1. Experience Platform Launch 모바일 속성에서 **[!UICONTROL Rules]** 탭을 클릭하고 **[!UICONTROL Add Rule]**&#x200B;을 클릭합니다.
1. 섹션에서 **[!UICONTROL Events]** 을 클릭하고 **[!UICONTROL +]** 선택합니다 **[!UICONTROL Places]**.
1. 에서 **[!UICONTROL Event Type]**&#x200B;을 선택합니다 **[!UICONTROL Enter POI]**.
1. 예를 들어 규칙의 이름을 입력합니다 **[!UICONTROL User entered POI]**.
1. 클릭 **[!UICONTROL Keep Changes]**.
1. 이 **[!UICONTROL Conditions]** 섹션은 비워두십시오.

   이 섹션에서는 이 규칙이 실행될 시기를 필터링하거나 제한할 수 있습니다.

1. In the **[!UICONTROL Actions]** section, click **[!UICONTROL +]**.
1. 에서 **[!UICONTROL Extension]**&#x200B;을 **[!UICONTROL Mobile Core]** 선택하고 에서 **[!UICONTROL Action Type]**&#x200B;을 선택합니다 **[!UICONTROL Send Postback]**.

1. URL의 경우 캠페인 표준 위치 끝점을 구성해야 합니다.

   URL은 아래 URL과 유사해야 합니다. 캠페인 서버 및 Key에 대해 이전에 만든 올바른 데이터 요소를 사용해야 합니다.

   `https://{%%camp-server%%}/rest/head/mobileAppV5/{%%pkey%%}/locations/`

1. 상자를 클릭하여 게시물 본문을 추가하고 다음을 전송합니다.

   ```text
   {
   "locationData": {
   "distances": "{%%Last Entered POI Radius%%}",
   "poiLabel": "{%%Last Entered POI Name%%}",
   "latitude": "{%%Last Entered POI Lat%%}",
   "longitude": "{%%Last Entered POI Long%%}",
   "appId": "{%%AppID%%}",
   "marketingCloudId": “{%%ecid%%}”
   }
   }
   ```

1. 이전 섹션에서 만든 특정 데이터 요소를 사용합니다.
1. 에 **[!UICONTROL Content Type]**&#x200B;입력합니다 **[!UICONTROL application/json]**.
1. 이 설정을 **[!UICONTROL Keep Changes]** 설정한 후 을 클릭합니다.

   Slack 웹 후크를 추가 작업으로 설정하여 작업이 트리거되고 있으며 올바른 데이터가 수집되고 있는지 확인하는 것이 도움이 될 수 있습니다.

   >[!IMPORTANT]
   >
   >규칙의 일부로 규칙과 모든 데이터 요소가 배포되도록 최근 변경 내용을 앱에 게시해야 합니다. 게시 후 모바일 애플리케이션을 다시 실행하여 최신 구성 업데이트를 받아야 합니다.

### 위치 데이터를 사용하여 Campaign Standard 메시지 타깃팅

이제 Adobe Campaign에 채워진 위치 데이터가 있으므로 관심 영역을 대상 세그먼트 도구로 사용할 수 있습니다.

1. Adobe Campaign Standard 인스턴스 내에서 UICONTROL 푸시 알림 **[만들기를 클릭합니다]**.
1. 푸시 알림 유형의 경우 UICONTROL **[Send push to app subscribers]**.

   이 푸시 유형은 애플리케이션의 모든 사용자를 타깃팅합니다. 모바일 사용자가 캠페인 프로필에 연결된 경우 UICONTROL Send push **[to Campaign profiles]** i를 선택할 수도 있습니다.

1. 을 클릭하고 다음 화면에 일반 세부 사항을 **[!UICONTROL Next]** 입력합니다.
1. 대상 화면에서 푸시 알림이 전송될 예상 사용자 수를 **[!UICONTROL Count]** 보려면 을 클릭합니다.

   이 경우 테스트 애플리케이션에 세 개의 장치가 설치되어 있으므로 이 수는 3개입니다.

1. 왼쪽 세로 막대에서 **[!UICONTROL Profile]** 탭을 확장하고 주 영역의 **[!UICONTROL POI location]** 필터를 드래그합니다.
1. POI 필터 창에서 타깃팅할 POI의 정확한 이름을 입력합니다.

   사용자가 이 POI를 마지막으로 방문한 이후의 시간 범위를 결정하기 위해 추가 항목을 선택할 수 있습니다.

   ![](/help/assets/using-loc-services-acs_2.png)

1. 클릭 [!**UICONTROL 확인]**.
1. 맨 위에 있는 카운트를 다시 실행하여 대상자 크기 변경을 확인합니다.

   카운트 업데이트가 표시되지 않는 경우, 항목이 트리거되지 않은 POI 이름을 입력했을 수 있습니다. 다양한 테스트 장치에서 POI 항목 목록을 볼 수 있으므로 Slack 웹 후크를 사용하는 것이 중요합니다.
1. 추가 POI 위치 필터를 드래그하여 메시지에 여러 POI를 포함할 수 있습니다.
1. 전달에 대한 푸시 알림 만들기를 **[!UICONTROL Next]** 완료하려면 을 클릭합니다.

   ![](/help/assets/using-loc-services-acs_3.png)

푸시 알림 외에도 위치 데이터를 사용하여 인앱 메시지를 받을 사용자를 세그먼트화할 수 있습니다.

1. Adobe Campaign Standard 인스턴스에서 을 클릭합니다 **[!UICONTROL Create In-App message]**.
1. 메시지 유형에 대해 을 **[!UICONTROL Target all users of a Mobile application]**&#x200B;선택합니다.
1. 을 클릭하고 다음 화면에 일반 세부 사항을 **[!UICONTROL Next]** 입력합니다.
1. 왼쪽 창에서 이제 위치와 관련된 다양한 트리거를 사용할 수 있는지 확인합니다.
1. 사용자가 POI 지역 울타리를 입력한 경우 인앱 메시지를 표시하도록 선택할 수 있습니다.

   장소 UI에서 정의한 메타데이터를 사용하여 대상을 필터링할 수도 있습니다. 이 예에서는 Gym 기능이 있는 POI를 종료한 사용자만 표시하는 앱 내 메시지를 트리거하려고 합니다. 아마도 그들이 체육관을 사용했는지, 좋아하는지 알아보기 위해 그들에게 설문지를 보내고 싶을지도 몰라요.

1. 전달을 위한 인앱 메시지 작성을 **[!UICONTROL Next]** 완료하려면 을 클릭하십시오.

   ![](/help/assets/using-loc-services-acs_4.png)

Adobe Campaign Standard와 함께 위치를 사용하면 내역 위치에 따라 메시지를 세그먼트화하고 사용자에게 타깃팅할 수 있는 매우 강력한 도구를 제공합니다. 이러한 간단한 통합을 통해 보다 개인화되고 상황에 맞는 활용 사례를 구축할 수 있습니다.

Adobe는 위치 및 통합 솔루션을 지속적으로 개선하여 모바일 워크플로우에 맞게 위치를 조정할 수 있게 되었습니다. 장소(Places)를 활용할 하나의 제품은 고객이 위치와 같은 이벤트 트리거를 기반으로 실시간 워크플로우를 만들 수 있는 예정된 트리거 경로 솔루션입니다.

## 권장 링크

자세한 내용은 다음을 참조하십시오.

* [Adobe Experience Location Service](https://www.adobe.com/experience-platform/location-service.html)
* [Adobe Campaign Standard](https://www.adobe.com/marketing/campaign.html)
* [Adobe Places 베타 이용 신청](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4fkr821yYptFo-ghlnlXCyhUM0dQVkJCSzVDMFNGWEFXWUUwNEJWSjhSRS4u)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com/)
* [Adobe Campaign과 Experience Platform SDK 통합](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html)

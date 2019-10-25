---
title: FAQ
seo-title: FAQ
description: 이 항목에서는 일부 FAQ에 대한 추가 정보를 제공합니다.
seo-description: 이 항목에서는 일부 FAQ에 대한 추가 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 6ae0c8d90cad4c437e1db7f562a0bc9c6b072ce6

---


# FAQ

다음은 위치 서비스에 대한 몇 가지 정보와 FAQ입니다.

## 크기 및 안정성

Adobe 또는 일부 기타 서비스를 사용하는 것과 상관없이 모바일 앱의 지역 모니터링에서 사용되는 모든 지표에 대해 주목해야 합니다. 운영 체제에서는 지오펜스 생성 시 몇 가지 매개 변수를 고려해야 합니다. 안정성을 극대화하려면 지오펜스 반경은 최소 100m여야 합니다. 더 작은 영역을 만들 수는 있지만 시작 및 종료 이벤트는 생성되지 않을 수도 있고 사용자가 일정 기간 동안 이동을 중지한 후에 생성할 수도 있습니다.

또한, 와이파이의 전원을 끄거나 사용할 수 없는 것과 같은 하드웨어 조건과 GPS 신호의 방해와 관련하여 장치의 위치를 기반으로 하여 정확도와 안정성을 줄일 수 있습니다. 예를 들어 산악 지역, 도시 설정 및 실내 영역은 iOS 및 Android 운영 체제에서 위치 정확도를 줄일 수 있습니다.

## 종료 이벤트는 어떻게 트리거됩니까?

SDK(위치 모니터)가 인근 POI의 새 목록을 받으면 각 POI의 운영 체제에 지역을 등록합니다. 이제 장치가 모니터링되는 영역 중 하나에 대한 경계(시작 또는 종료)를 교차할 때 운영 체제에서 SDK를 알릴 책임이 있습니다. SDK는 운영 체제에서 이벤트가 발생했음을 SDK에 알릴 때만 종료 이벤트를 트리거합니다. 이 알림의 주요 원인은 위치 데이터의 시간 민감도입니다.

장치가 영역을 떠날 때 운영 체제에서 종료 이벤트를 전달할 수 없는 경우 SDK에서 종료 이벤트를 생략하는 것이 더 안전합니다. SDK가 운영 체제에 의해 트리거되는 이벤트 없이 종료 이벤트를 만드는 경우, 종료 이벤트가 POI에 가까이 있는 기간 동안 잘 처리될 수 있습니다.

## 위치 서비스 및 경험 플랫폼 실행에 사용자 추가 {#adding-user-launch-places}

사용자가 Launch Service [UI에](https://places.adobe.com)액세스할 수 있도록 하려면 관리 콘솔의 Places Core Service에 사용자로 추가해야 합니다. 사용자가 Experience Platform Launch에 액세스할 수 있도록 하고, 모바일 속성을 구성하고, Adobe Experience Platform SDK를 사용하여 위치를 사용하려면, Admin Console에서 Experience Platform Launch에 추가하고, Experience Platform Launch에 대해 다음 권한을 부여받아야 합니다.

* 모든 속성 권한:
   * 개발
   * 승인
   * 게시
   * 확장 기능 관리
   * 환경 관리
* 회사 권한으로 속성 관리 권한

사용자를 처음 추가하는 경우 다음 단계를 완료하여 Experience Platform 시작 및 위치 서비스에 사용자를 추가합니다. 이전에 사용자를 추가한 경우 여러 프로필이 표시될 수 있으므로 올바른 프로필을 선택해야 합니다.

>[!IMPORTANT]
>
>조직 관리자만 관리 콘솔에 액세스하고 사용자를 추가할 수 있습니다.

### 1.위치 서비스 및 경험 플랫폼 시작이 제공되는지 확인

위치 서비스 및 경험 플랫폼 시작이 제공되는지 확인하려면:

1. Experience Cloud 조직에 로그인합니다.
1. 오른쪽 상단에서 Experience Cloud 셸 전환기를 클릭합니다.

   ![셸 전환기](/help/assets/places_shell_switcher1.png)

1. **[!UICONTROL Platform]**&#x200B;에서 **[!UICONTROL Administration]**&#x200B;를 클릭합니다.

   목록에 **관리가** 표시되지 않으면 관리자가 아닙니다. 이 절차를 완료하려면 조직 관리자에게 문의해야 합니다.

1. Experience Cloud 관리 페이지의 **[!UICONTROL Admin Console]** 카드에서 을 클릭합니다 **[!UICONTROL Take me there]**.

1. 관리 콘솔에서 여러 조직에 대한 액세스 권한이 있는 경우 페이지의 오른쪽 상단에 올바른 조직이 선택되어 있는지 확인합니다.

   사용자를 추가할 조직입니다. 올바른 조직을 선택하지 않은 경우 해당 조직을 클릭하고 드롭다운 목록에서 조직을 선택합니다.

   >[!IMPORTANT]
   >
   >조직에 대한 액세스 권한이 없는 경우 해당 조직에 대한 관리자 액세스 권한이 없습니다.

1. 카드의 **[!UICONTROL Adobe Experience Platform Launch]** 및 **[!UICONTROL Places Core Services]** 표시가 나타나는지 확인합니다.

   ![](/help/assets/places_provisioned1.png)

   이 구성 요소가 표시되면 위치 서비스 및 경험 플랫폼 시작이 조직에 프로비저닝된 것입니다. 표시되지 않으면 조직에 대해 프로비저닝해야 합니다.

   >[!IMPORTANT]
   >
   >베타 기간 동안 베타 설문 [조사를](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4fkr821yYptFo-ghlnlXCyhUM0dQVkJCSzVDMFNGWEFXWUUwNEJWSjhSRS4u)완료한 후 Provisioning 팀에 요청을 보냅니다.

### 2.프로필 설정 및 권한 추가

프로필을 설정하고 권한을 추가하려면:

1. 프로필에 추가된 사용자가 Experience Platform Launch와 Experience Platform SDK를 사용하여 Experience Platform Launch와 모바일 속성을 사용할 수 있도록 해주는 Experience Platform Launch 프로필을 설정하십시오.

   a.메뉴 모음에서 을 클릭합니다 **[!UICONTROL Product]**.

   b.왼쪽 창의 제품 목록에서 을 클릭합니다 **[!UICONTROL Adobe Experience Platform Launch]**.

   * Experience Platform Launch 프로필이 오른쪽에 나타납니다.
   * Experience Platform Launch에는 Launch - ( *조직 이름)* 라는 기본 프로필이 있습니다.

      이전에 Experience Platform Launch에 사용자를 추가한 경우 여러 프로필이 나열될 수 있습니다.

2. 올바른 프로필을 선택합니다.

   a.기본 프로필의 이름을 클릭합니다.

   b.탭을 **[!UICONTROL Permissions]** 클릭합니다.

   c.옆에 **[!UICONTROL Edit]** 있는 을 클릭합니다 **[!UICONTROL Property Rights]**.

   d.왼쪽 창에서 을 클릭합니다 **[!UICONTROL + Add all]**.

   이 단계에서는 사용 가능한 모든 권한을 포함된 권한 목록으로 이동합니다.

   e.을 **[!UICONTROL Company Rights]**&#x200B;클릭합니다.

   f.왼쪽 창에서 을 클릭합니다 **[!UICONTROL + Manage Properties]**.

   g.을 **[!UICONTROL Save]**&#x200B;클릭합니다.

>[!IMPORTANT]
>
>위치 서비스의 경우 기본 프로필이 있지만 권한을 추가할 필요는 없습니다.

만든 프로필에 권한을 추가했습니다.

### 3.사용자 또는 개발자를 위치 서비스 및 경험 플랫폼 시작 프로필에 추가

사용자 및/또는 개발자를 위치 서비스 및 경험 플랫폼 시작 프로필에 추가할 수 있습니다.

### 사용자 추가

사용자 위치 서비스 및 경험 플랫폼 시작 프로필에 사용자를 추가하려면:

1. Experience Platform Launch 프로필에 사용자를 추가합니다.

   a.메뉴 모음에서 을 클릭합니다 **[!UICONTROL Overview]**.

   b.카드에서 **[!UICONTROL Adobe Experience Platform Launch]** 다음을 확인합니다.

   * 카드 아래쪽에 두 개의 점이 표시됩니다.
   * 왼쪽에 있는 점은 검은색입니다.

      오른쪽에 점이 검은색이면 개발자만 추가할 수 있습니다. 사용자를 추가하려면 왼쪽의 점을 클릭합니다.
   c.을 **[!UICONTROL + Add Users]**&#x200B;클릭합니다.

   d.사용자의 Adobe ID를 입력합니다.

   e.다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 **[!UICONTROL New user]**&#x200B;사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.
   f.드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 이전에 편집한 프로필을 선택합니다.

   g.을 **[!UICONTROL Save]**&#x200B;클릭합니다.

2. 사용자를 추가할 **[!UICONTROL Places Core Services]**&#x200B;수 있습니다.

   >[!TIP]
   >
   >현재 모든 위치 서비스 사용자는 동일한 권한을 가지므로 권한을 편집할 필요가 없습니다.

   a.카드에서 **[!UICONTROL Places Core Services]** 다음을 확인합니다.

   * 카드 아래쪽에 두 개의 점이 표시됩니다.
   * 왼쪽에 있는 점은 검은색입니다.
   b.을 **[!UICONTROL + Assign Users]**&#x200B;클릭합니다.

   c.사용자의 Adobe ID를 입력합니다.

   d.다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 **[!UICONTROL New user]**&#x200B;사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.
   e.드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 위치 프로필을 선택합니다.

   f.을 **[!UICONTROL Save]**&#x200B;클릭합니다.

### 개발자 추가

웹 서비스 API에 액세스해야 하는 사용자의 경우 개발자로 추가해야 합니다.

개발자를 추가하려면:

1. 카드에서 **[!UICONTROL Places Core Services]** 다음을 확인합니다.

   * 카드 아래쪽에 두 개의 점이 표시됩니다.
   * 오른쪽에 있는 점을 클릭하면 카드 하단에 **[!UICONTROL Assign Developers]** 표시됩니다.

1. 클릭 **[!UICONTROL + Assign Developers]**.

1. 사용자의 Adobe ID를 입력합니다.

1. 다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 **[!UICONTROL New user]** 사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

1. 드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 위치 서비스 프로필을 선택합니다.

1. **저장**&#x200B;을 클릭합니다.

사용자는 Experience Platform Launch에 액세스할 수 있음을 알리는 이메일을 수신하게 됩니다. Experience Platform Launch 또는 [이 조직의 위치](https://launch.adobe.com) UI에 [로그인할](https://places.adobe.com) 수 있습니다. 개발자 **추가 절차의 4단계를 완료한** 경우 사용자는 Adobe I/O 콘솔에 [로그인하여 장소](https://console.adobe.io) 통합을 만들고 REST API를 사용할 수도 있습니다.
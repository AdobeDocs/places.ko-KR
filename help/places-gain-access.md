---
title: Adobe Experience Platform 위치 서비스 액세스
seo-title: Adobe Experience Platform 위치 서비스 액세스
description: 이 섹션에서는 사용자가 위치 서비스에 액세스할 수 있도록 위치 서비스 및 경험 플랫폼 론치에 사용자를 추가하는 방법에 대한 정보를 제공합니다.
seo-description: 이 섹션에서는 사용자가 위치 서비스에 액세스할 수 있도록 위치 서비스 및 경험 플랫폼 론치에 사용자를 추가하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 1b4482c8e4cf825c0182421fe00f8b86b411c11b

---


# Adobe Experience Platform 위치 서비스 액세스 {#adding-user-launch-places}

Adobe Experience Cloud 홈의 [빠른 액세스 메뉴에서 플랫폼 위치](https://experience.adobe.com)서비스에 액세스할 수 있습니다.
사용자 ID에 액세스 권한이 있으면 아래에 표시된 위치 서비스 아이콘이 표시됩니다.

![빠른 액세스 메뉴](/help/assets/quick-access.png)

Adobe Experience Platform 메뉴에서 플랫폼 위치 서비스에 액세스할 수도 있습니다.

![경험 플랫폼 메뉴](/help/assets/exp-platform-menu-sm.png)

이러한 메뉴 중 하나에서 플랫폼 위치 서비스가 표시되지 않는 경우 조직 내의 관리자에게 문의하여 관리 콘솔의 Places Core 서비스에 사용자 ID를 추가해야 합니다.

## 위치 서비스 및 경험 플랫폼 실행에 사용자 추가

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

1. Verify that the cards for **[!UICONTROL Adobe Experience Platform Launch]** and **[!UICONTROL Places Core Services]** are displayed.

   ![](/help/assets/places_provisioned1.png)

   이 구성 요소가 표시되면 위치 서비스 및 경험 플랫폼 시작이 조직에 프로비저닝된 것입니다. 표시되지 않으면 조직에 대해 프로비저닝해야 합니다.


### 2.프로필 설정 및 권한 추가

프로필을 설정하고 권한을 추가하려면:

1. 프로필에 추가된 사용자가 Experience Platform Launch와 Experience Platform SDK를 사용하여 Experience Platform Launch와 모바일 속성을 사용할 수 있도록 해주는 Experience Platform Launch 프로필을 설정하십시오.

   a.메뉴 모음에서 을 클릭합니다 **[!UICONTROL Product]**.

   b.왼쪽 창의 제품 목록에서 을 클릭합니다 **[!UICONTROL Adobe Experience Platform Launch]**.

   * Experience Platform Launch 프로필이 오른쪽에 나타납니다.
   * Experience Platform Launch에는 Launch - ( *조직 이름)* 라는 기본 프로필이 있습니다.

      이전에 Experience Platform Launch에 사용자를 추가한 경우 여러 프로필이 나열될 수 있습니다.

1. 올바른 프로필을 선택합니다.

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

1. 사용자를 추가할 **[!UICONTROL Places Core Services]**&#x200B;수 있습니다.

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

1. On the **[!UICONTROL Places Core Services]** card, verify the following:

   * 카드 아래쪽에 두 개의 점이 표시됩니다.
   * 오른쪽에 있는 점을 클릭하면 카드 하단에 **[!UICONTROL Assign Developers]** 표시됩니다.

1. 클릭 **[!UICONTROL + Assign Developers]**.

1. 사용자의 Adobe ID를 입력합니다.

1. 다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 **[!UICONTROL New user]** 사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

1. 드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 위치 서비스 프로필을 선택합니다.

1. **저장**&#x200B;을 클릭합니다.

사용자는 Experience Platform Launch에 액세스할 수 있음을 알리는 이메일을 수신하게 됩니다. [Experience Platform Launch ](https://launch.adobe.com)또는 이 조직의 위치에 대한 [위치](https://places.adobe.com) UI에 로그인할 수 있습니다. **개발자 추가 절차**&#x200B;의 4단계를 완료한 경우, 사용자는 [Adobe I/O 콘솔](https://console.adobe.io)에 로그인하여 장소 통합을 생성하고 REST API를 사용할 수도 있습니다.

---
title: '장소 서비스 이용 '
description: 이 섹션에서는 사용자가 장소 서비스에 액세스할 수 있도록 위치 서비스 및 Experience Platform Launch에 사용자를 추가하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 26538602a73e806a4822705c7a3aa44d76351030
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 7%

---

# 장소 서비스 이용 {#adding-user-launch-places}

Adobe Experience Cloud 홈의 빠른 액세스 메뉴에서 장소 서비스를 이용할 수 [있습니다](https://experience.adobe.com).
사용자 ID에 액세스할 수 있는 경우 아래와 같이 장소 서비스 아이콘이 표시됩니다.

![빠른 액세스 메뉴](/help/assets/quickaccess.png)

Adobe Experience Platform 메뉴에서 장소 서비스를 이용할 수도 있습니다.

![Experience Platform 메뉴](/help/assets/solutionaccessmenu.png)

이러한 메뉴 중 하나에 위치 서비스가 표시되지 않으면 조직의 관리자에게 연락하여 Admin Console의 위치 코어 서비스에 사용자 ID를 추가하십시오.

## 장소 서비스 및 Experience Platform Launch에 사용자 추가

사용자가 [Experience Platform Launch UI에](https://launch.adobe.com)액세스할 수 있도록 하려면 Admin Console의 핵심 서비스 위치에 사용자로 추가해야 합니다. 사용자가 Experience Platform Launch에 액세스하고, 모바일 속성을 구성하고, Adobe Experience Platform SDK와 함께 [장소]를 사용할 수 있도록 하려면, Admin Console의 Experience Platform Launch에 이들을 추가하고, Experience Platform Launch에 대해 다음 권한을 부여받아야 합니다.

* 모든 속성 권한:
   * 개발
   * 승인
   * 게시
   * 익스텐션 관리
   * 환경 관리
* 회사 권한에 따라 속성 관리 권한

사용자를 처음 추가하는 경우 다음 단계를 완료하여 Experience Platform Launch 및 장소 서비스에 사용자를 추가합니다. 이전에 사용자를 추가한 경우 여러 개의 프로필이 표시될 수 있으므로 올바른 프로필을 선택해야 합니다.

>[!IMPORTANT]
>
>조직 관리자만 Admin Console에 액세스하여 사용자를 추가할 수 있습니다.

### 1. 장소 서비스 및 Experience Platform Launch이 제공되는지 확인합니다.

1. Experience Cloud 조직에 로그인합니다.
1. 오른쪽 상단에서 Experience Cloud 셸 전환기를 클릭합니다.

   ![셸 전환기](/help/assets/places_shell_switcher1.png)

1. **[!UICONTROL Platform]**&#x200B;에서 **[!UICONTROL Administration]**&#x200B;를 클릭합니다.

   목록에 관리 **가** 표시되지 않으면 관리자가 아닙니다. 이 절차를 완료하려면 조직 관리자에게 연락해야 합니다.

1. Experience Cloud 관리 페이지의 **[!UICONTROL Admin Console]** 카드에서 을 클릭합니다 **[!UICONTROL Take me there]**.

1. Admin Console에서 여러 조직에 액세스할 수 있는 경우 페이지의 오른쪽 상단에 올바른 조직이 선택되어 있는지 확인합니다.

   사용자를 추가할 조직입니다. 올바른 조직을 선택하지 않은 경우 해당 조직을 클릭하고 드롭다운 목록에서 해당 조직을 선택합니다.

   >[!IMPORTANT]
   >
   >조직에 대한 액세스 권한이 없는 경우 해당 조직에 대한 관리자 액세스 권한이 없습니다.

1. Verify that the cards for **[!UICONTROL Adobe Experience Platform Launch]** and **[!UICONTROL Places Core Services]** are displayed.

   ![](/help/assets/places_provisioned1.png)

   이러한 항목이 표시되면 조직에 대해 배치 서비스 및 Experience Platform Launch이 프로비저닝된 것입니다. 표시되지 않으면 조직에 대해 프로비저닝해야 합니다.


### 2. 프로필을 설정하고 권한을 추가합니다.

1. 프로필에 추가한 사용자가 Experience Platform Launch 및 해당 모바일 속성을 Experience Platform SDK와 함께 사용할 수 있도록 Experience Platform Launch 프로필을 설정합니다.

   a.메뉴 모음에서 을 클릭합니다 **[!UICONTROL Product]**.

   b.왼쪽 창의 제품 목록에서 을 클릭합니다 **[!UICONTROL Adobe Experience Platform Launch]**.

   * Experience Platform Launch 프로필이 오른쪽에 나타납니다.
   * Experience Platform Launch에는 론치 - *(조직 이름)라는 기본 프로필이 있습니다* .

      이전에 사용자를 Experience Platform Launch에 추가한 경우 여러 개의 프로필이 나열될 수 있습니다.

1. 올바른 프로필을 선택합니다.

   a.기본 프로필의 이름을 클릭합니다.

   b. Click the **[!UICONTROL Permissions]** tab.

   c. 옆에 있는 **[!UICONTROL Edit]** 을 클릭합니다 **[!UICONTROL Property Rights]**.

   d.왼쪽 창에서 을 클릭합니다 **[!UICONTROL + Add all]**.

   이 단계에서는 사용 가능한 모든 권한을 포함된 권한 목록으로 이동합니다.

   e.을 **[!UICONTROL Company Rights]**&#x200B;클릭합니다.

   f.왼쪽 창에서 을 클릭합니다 **[!UICONTROL + Manage Properties]**.

   g.을 **[!UICONTROL Save]**&#x200B;클릭합니다.

>[!IMPORTANT]
>
>위치 서비스의 경우 기본 프로필이 있지만 권한을 추가할 필요는 없습니다.

만든 프로필에 권한을 추가했습니다.

### 3. 사용자 또는 개발자를 장소 서비스 및 Experience Platform Launch 프로파일에 추가합니다.

사용자 및/또는 개발자를 장소 서비스 및 Experience Platform Launch 프로필에 추가할 수 있습니다.

### 사용자 추가

사용자 위치 서비스 및 Experience Platform Launch 프로필에 사용자를 추가하려면:

1. Experience Platform Launch 프로필에 사용자를 추가합니다.

   a.메뉴 모음에서 을 클릭합니다 **[!UICONTROL Overview]**.

   b.카드에서 **[!UICONTROL Adobe Experience Platform Launch]** 다음을 확인합니다.

   * 카드 하단에 두 점이 표시됩니다.
   * 왼쪽의 점은 검정색입니다.

      오른쪽에 점이 검정색이면 개발자만 추가할 수 있습니다. 사용자를 추가하려면 왼쪽의 점을 클릭합니다.
   c. 를 **[!UICONTROL + Add Users]**&#x200B;클릭합니다.

   d.사용자의 Adobe ID을 입력합니다.

   e.다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 사용자 **[!UICONTROL New user]**&#x200B;의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

   f.드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 이전에 편집한 프로필을 선택합니다.

   g.을 **[!UICONTROL Save]**&#x200B;클릭합니다.

1. 사용자를 추가합니다 **[!UICONTROL Places Core Services]**.

   >[!TIP]
   >
   >현재 모든 위치 서비스 사용자는 동일한 권한을 가지므로 권한을 편집할 필요가 없습니다.

   a.카드에서 **[!UICONTROL Places Core Services]** 다음을 확인합니다.

   * 카드 하단에 두 점이 표시됩니다.
   * 왼쪽의 점은 검정색입니다.

   b.을 **[!UICONTROL + Assign Users]**&#x200B;클릭합니다.

   c. 사용자의 Adobe ID을 입력합니다.

   d.다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 사용자 **[!UICONTROL New user]**&#x200B;의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

   e.드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 위치 프로필을 선택합니다.

   f.을 **[!UICONTROL Save]**&#x200B;클릭합니다.

### 개발자 추가

웹 서비스 API에 액세스해야 하는 사용자의 경우 개발자로 추가해야 합니다.

개발자를 추가하려면:

1. On the **[!UICONTROL Places Core Services]** card, verify the following:

   * 카드 하단에 두 점이 표시됩니다.
   * 오른쪽에 있는 점을 클릭하면 카드 하단에 **[!UICONTROL Assign Developers]** 나타납니다.

1. **[!UICONTROL + Assign Developers]**&#x200B;를 클릭합니다.

1. 사용자의 Adobe ID를 입력합니다.

1. 다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 을 클릭하고 사용자 **[!UICONTROL New user]** 의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

1. 드롭다운 **[!UICONTROL Please select a profile for this product]** 목록에서 Places Service 프로필을 선택합니다.

1. **저장**&#x200B;을 클릭합니다.

사용자는 Experience Platform Launch에 액세스할 수 있음을 알리는 이메일을 수신하게 됩니다. They can can log in to the [Experience Platform Launch](https://launch.adobe.com) or the [Places Service](https://places.adobe.com) UIs for this organization. **개발자 추가 절차**&#x200B;의 4단계를 완료한 경우, 사용자는 [Adobe I/O 콘솔](https://console.adobe.io)에 로그인하여 장소 통합을 생성하고 REST API를 사용할 수도 있습니다.

---
title: '장소 서비스 이용 '
description: 이 섹션에서는 사용자가 장소 서비스에 액세스할 수 있도록 위치 서비스 및 Experience Platform Launch에 사용자를 추가하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: ecf50d67d4c08e79d9c3be64480f27d435fd7fcb
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 9%

---

# 장소 서비스 {#adding-user-launch-places} 액세스

[Adobe Experience Cloud 홈](https://experience.adobe.com)의 빠른 액세스 메뉴에서 장소 서비스에 액세스할 수 있습니다.
사용자 ID에 액세스할 수 있는 경우 아래와 같이 장소 서비스 아이콘이 표시됩니다.

![빠른 액세스 메뉴](/help/assets/quickaccess.png)

Adobe Experience Platform 메뉴에서 장소 서비스에 액세스할 수도 있습니다.

![Experience Platform 메뉴](/help/assets/solutionaccessmenu.png)

이러한 메뉴 중 하나에 위치 서비스가 표시되지 않으면 조직의 관리자에게 문의하여 Admin Console의 위치 핵심 서비스에 사용자 ID를 추가하십시오.

## 위치 서비스 및 Experience Platform Launch에 사용자 추가

사용자가 [Experience Platform Launch UI](https://launch.adobe.com)에 액세스할 수 있도록 하려면 Admin Console의 핵심 서비스 위치에 사용자로 추가해야 합니다. 사용자가 Experience Platform Launch에 대한 액세스 권한을 가지고, 모바일 속성을 구성하고, Adobe Experience Platform SDK에서 [위치]를 사용할 수 있도록 하려면 Admin Console의 Experience Platform Launch에 해당을 추가해야 하며 Experience Platform Launch에 대해 다음 권한을 부여받아야 합니다.

* 모든 속성 권한:
   * 개발
   * 승인
   * 게시
   * 확장 관리
   * 환경 관리
* 회사 권한에 따라 속성 관리 권한

사용자를 처음 추가하는 경우에는 다음 단계를 완료하여 Experience Platform Launch 및 장소 서비스에 사용자를 추가합니다. 이전에 사용자를 추가한 경우 여러 프로필이 표시될 수 있으므로 올바른 프로필을 선택해야 합니다.

>[!IMPORTANT]
>
>조직 관리자만 Admin Console에 액세스하여 사용자를 추가할 수 있습니다.

### 1. 장소 서비스 및 Experience Platform Launch이 제공되는지 확인합니다.

1. Experience Cloud 조직에 로그인합니다.
1. 오른쪽 상단에서 Experience Cloud 셸 전환기를 클릭합니다.

   ![셸 전환기](/help/assets/places_shell_switcher1.png)

1. **[!UICONTROL 플랫폼]**&#x200B;에서 **[!UICONTROL 관리]**&#x200B;를 클릭합니다.

   목록에 **[!UICONTROL 관리]**&#x200B;가 표시되지 않으면 관리자가 아닙니다. 이 절차를 완료하려면 조직 관리자에게 연락해야 합니다.

1. Experience Cloud 관리 페이지의 **[!UICONTROL Admin Console]** 카드에서 **[!UICONTROL 나를 그곳에 데려다 주세요]**&#x200B;를 클릭합니다.

1. Admin Console에서 여러 조직에 대한 액세스 권한이 있는 경우 페이지의 오른쪽 상단에 올바른 조직이 선택되어 있는지 확인합니다.

   사용자를 추가할 조직입니다. 올바른 조직을 선택하지 않은 경우 해당 조직을 클릭하고 드롭다운 목록에서 해당 조직을 선택합니다.

   >[!IMPORTANT]
   >
   >조직에 대한 액세스 권한이 없는 경우 해당 조직에 대한 관리자 액세스 권한이 없는 것입니다.

1. **[!UICONTROL Adobe Experience Platform Launch]** 및 **[!UICONTROL Places Core Services]**&#x200B;에 대한 카드가 표시되는지 확인합니다.

   ![](/help/assets/places_provisioned1.png)

   메시지가 표시되면 조직에 대해 장소 서비스 및 Experience Platform Launch이 프로비저닝된 것입니다. 표시되지 않으면 조직에 대해 프로비저닝해야 합니다.


### 2. 프로필을 설정하고 권한을 추가합니다.

1. 프로파일에 추가된 사용자가 Experience Platform Launch 및 해당 모바일 속성을 Experience Platform SDK와 함께 사용할 수 있도록 Experience Platform Launch 프로필을 설정합니다.

   a.메뉴 모음에서 **[!UICONTROL 제품]**&#x200B;을 클릭합니다.

   b.왼쪽 창의 제품 목록에서 **[!UICONTROL Adobe Experience Platform Launch]**&#x200B;을 클릭합니다.

   * Experience Platform Launch 프로필이 오른쪽에 나타납니다.
   * Experience Platform Launch에는 *시작 - (조직 이름)*&#x200B;이라는 기본 프로필이 있습니다.

      이전에 Experience Platform Launch에 사용자를 추가한 경우 여러 개의 프로필이 나열될 수 있습니다.

1. 올바른 프로필을 선택합니다.

   a.기본 프로필의 이름을 클릭합니다.

   b.**[!UICONTROL 권한]** 탭을 클릭합니다.

   c. **[!UICONTROL 속성 권한]** 옆에 있는 **[!UICONTROL 편집]**&#x200B;을 클릭합니다.

   d.왼쪽 창에서 **[!UICONTROL + 모두 추가]**&#x200B;를 클릭합니다.

   이 단계에서는 사용 가능한 모든 권한을 포함된 권한 목록으로 이동합니다.

   e.**[!UICONTROL 회사 권한]**&#x200B;을 클릭합니다.

   f.왼쪽 창에서 **[!UICONTROL + 속성 관리]**&#x200B;를 클릭합니다.

   g.**[!UICONTROL 저장]**&#x200B;을 클릭합니다.

>[!IMPORTANT]
>
>위치 서비스의 경우 기본 프로필이 있지만 권한을 추가할 필요는 없습니다.

만든 프로필에 권한을 추가했습니다.

### 3. 사용자 또는 개발자를 사용자 환경 서비스 및 Experience Platform Launch 프로파일에 추가합니다.

사용자 및/또는 개발자를 Places Service 및 Experience Platform Launch 프로파일에 추가할 수 있습니다.

### 사용자 추가

사용자 위치 서비스 및 Experience Platform Launch 프로파일에 사용자를 추가하려면:

1. Experience Platform Launch 프로필에 사용자를 추가합니다.

   a.메뉴 모음에서 **[!UICONTROL 개요]**&#x200B;를 클릭합니다.

   b.**[!UICONTROL Adobe Experience Platform Launch]** 카드에서 다음을 확인하십시오.

   * 카드 하단에 두 점이 표시됩니다.
   * 왼쪽에 있는 점은 검정색이에요

      오른쪽에 점이 검정으로 표시되면 개발자만 추가할 수 있습니다. 사용자를 추가하려면 왼쪽의 점을 클릭합니다.
   c. **[!UICONTROL + 사용자 추가]**&#x200B;를 클릭합니다.

   d.사용자의 Adobe ID을 입력합니다.

   e.다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 **[!UICONTROL 새 사용자]**&#x200B;를 클릭하고 사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

   f.**[!UICONTROL 이 제품]** 드롭다운 목록에서 이전에 편집한 프로필을 선택하십시오.

   g.**[!UICONTROL 저장]**&#x200B;을 클릭합니다.

1. 사용자를 **[!UICONTROL 핵심 서비스]**&#x200B;에 추가합니다.

   >[!TIP]
   >
   >현재 모든 장소 서비스 사용자는 동일한 권한을 가지므로 권한을 편집할 필요가 없습니다.

   a.**[!UICONTROL 핵심 서비스]** 카드에서 다음을 확인하십시오.

   * 카드 하단에 두 점이 표시됩니다.
   * 왼쪽에 있는 점은 검정색이에요

   b.**[!UICONTROL + 사용자 할당]**&#x200B;을 클릭합니다.

   c. 사용자의 Adobe ID을 입력합니다.

   d.다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 **[!UICONTROL 새 사용자]**&#x200B;를 클릭하고 사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

   e.**[!UICONTROL 이 제품]** 드롭다운 목록에서 위치 프로필을 선택하십시오.

   f. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

### 개발자 추가

웹 서비스 API에 액세스해야 하는 사용자의 경우 개발자로 추가해야 합니다.

개발자를 추가하려면:

1. **[!UICONTROL Places Core Services]** 카드에서 다음을 확인하십시오.

   * 카드 하단에 두 점이 표시됩니다.
   * 오른쪽에 있는 점을 클릭하면 카드 하단에 **[!UICONTROL 개발자 할당]**&#x200B;이 나타납니다.

1. **[!UICONTROL + 개발자 할당]**&#x200B;을 클릭합니다.

1. 사용자의 Adobe ID를 입력합니다.

1. 다음 단계 중 하나를 완료합니다.

   * 새 사용자를 추가하는 경우 **[!UICONTROL 새 사용자]**&#x200B;를 클릭하고 사용자의 이름과 성을 입력합니다.
   * 기존 사용자를 추가하는 경우 표시되는 사용자 이름을 클릭합니다.

1. **[!UICONTROL 이 제품]** 드롭다운 목록에서 Places Service 프로필을 선택하십시오.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

사용자는 Experience Platform Launch에 액세스할 수 있음을 알리는 이메일을 수신하게 됩니다. 이 사용자는 이 조직의 [Experience Platform Launch](https://launch.adobe.com) 또는 [장소 서비스](https://places.adobe.com) UI에 로그인할 수 있습니다. **[!UICONTROL 개발자 추가 절차]**&#x200B;의 4단계를 완료한 경우, 사용자는 [Adobe I/O 콘솔](https://console.adobe.io)에 로그인하여 장소 통합을 생성하고 REST API를 사용할 수도 있습니다.

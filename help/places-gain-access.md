---
title: Places Service 액세스 권한 얻기
description: 이 섹션에서는 사용자가 위치 서비스에 액세스할 수 있도록 위치 서비스 및 Experience Platform Launch에 사용자를 추가하는 방법에 대해 설명합니다.
exl-id: f388945e-cf26-4694-9697-9fe564ae4b69
source-git-commit: c9058e9b70c2ef97151078f43913963471730bd2
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# Places Service 액세스 권한 얻기 {#adding-user-launch-places}

이제 데이터 수집 UI에서 위치 서비스를 사용할 수 있습니다. 의 빠른 액세스 메뉴에서 데이터 수집에 액세스할 수 있습니다 [Adobe Experience Cloud 홈](https://experience.adobe.com).

![빠른 액세스 메뉴](/help/assets/quickaccess.png)

Adobe Experience Platform 메뉴에서 데이터 수집에 액세스할 수도 있습니다.

![Experience Platform 메뉴](/help/assets/solutionaccessmenu.png)

사용자 ID에 액세스할 수 있는 경우 왼쪽 패널에서 데이터 수집의 데이터 관리 아래에 아래에 아래 표시된 대로 위치 서비스 아이콘이 표시됩니다.

![데이터 수집 왼쪽 패널](/help/assets/places_in_data_collection.png)

이 위치에 위치 서비스가 표시되지 않는 경우 조직의 관리자에게 문의하여 Admin Console에서 Adobe Experience Platform에 사용자 ID를 추가하십시오.

## Places Service 및 Experience Adobe Experience Platform 데이터 수집에 액세스할 사용자 추가

이제 위치가 Adobe Experience Platform에 포함되어 있습니다. 사용자가 [Places Service](https://experience.adobe.com/#/data-collection/places)를 추가하면 Admin Console에서 Adobe Experience Platform에 사용자로 추가해야 합니다. 사용자가 모바일 속성을 구성하고 Adobe Experience Platform SDK로 Places를 사용하는 데 필요한 권한이 있는 데이터 수집 Experience Platform에 액세스할 수 있도록 하려면 Admin Console에서 Adobe Experience Platform 데이터 수집에 추가되어야 하며 Adobe Experience Platform 데이터 수집에 대한 다음 권한이 있어야 합니다.

* 속성 권한 아래의 모든 권한:
   * 승인
   * 개발
   * 속성 편집
   * 환경 관리
   * 확장 관리
   * 게시
* 회사 권한에 따른 속성 관리 권한

사용자를 처음 추가하는 경우 다음 단계를 완료하여 Adobe Experience Platform 데이터 수집 및 Adobe Experience Platform에 사용자를 추가합니다. 이전에 사용자를 추가한 경우 여러 프로필이 표시될 수 있으므로 올바른 프로필을 선택해야 합니다.

>[!IMPORTANT]
>
>조직 관리자만 Admin Console에 액세스하고 사용자를 추가할 수 있습니다.

### 1. Adobe Experience Platform 및 Adobe Experience Platform 데이터 수집이 프로비저닝되었는지 확인합니다

1. Experience Cloud 조직에 로그인, [Adobe Experience Cloud 홈](https://experience.adobe.com).
1. 오른쪽 상단에서 Experience Cloud 셸 전환기를 클릭하여 드롭다운 메뉴를 표시합니다.

   ![쉘 전환기](/help/assets/places_shell_switcher1.png)

1. 목록 하단에서 **[!UICONTROL Admin Console]**. (링크: **[!UICONTROL Admin Console]** 빠른 액세스 섹션도 있습니다.)

   표시되지 않으면 **[!UICONTROL Admin Console]** 목록에서 사용자가 관리자가 아닙니다. 이 절차를 완료하려면 조직 관리자에게 문의해야 합니다.

1. Admin Console에서 여러 조직에 대한 액세스 권한이 있는 경우 페이지의 오른쪽 상단에 올바른 조직이 선택되어 있는지 확인합니다.

   사용자를 추가할 조직입니다. 올바른 조직을 선택하지 않은 경우에는 조직을 클릭하고 드롭다운 목록에서 올바른 조직을 선택하십시오.

   >[!IMPORTANT]
   >
   >원하는 조직이 드롭다운 목록에 없는 경우, 해당 조직에 대한 관리자 액세스 권한이 없는 것입니다.

1. Admin Console에서 제품 탭을 클릭하고 **[!UICONTROL Adobe Experience Platform 데이터 수집]** 및 **[!UICONTROL Adobe Experience Platform]** 표시됩니다.

   ![](/help/assets/places_provisioned1.png)

   이 두 제품은 모든 조직에 자동으로 공급되므로 존재해야 합니다.


### 2. 다음 제품에 사용자를 추가합니다

#### Places Service UI에 액세스할 수 있는 사용자 추가

1. 제품 탭에서 **[!UICONTROL Adobe Experience Platform]** 카드.
2. 사용자는 내의 프로필에 추가할 수 있습니다 **[!UICONTROL Adobe Experience Platform]** 위치에 액세스하려면 특정 권한을 설정할 필요가 없습니다.
3. 프로필을 선택하고(프로필이 두 개 이상인 경우) 클릭하여 엽니다.
4. 파란색 클릭 **사용자 추가** 버튼을 클릭하고 AdobeID와 이름을 입력한 다음 저장 을 클릭하여 추가를 완료합니다.

#### 데이터 수집에 사용자 추가

1. 제품 탭에서 **[!UICONTROL Adobe Experience Platform 데이터 수집]** 카드.
2. 기본적으로 이름이 인 프로필 **기본 데이터 수집 모든 액세스** 이(가) 생성되었습니다. 이 프로필에 사용자를 추가하면 Places Service 및 Data Collection에서 작업할 수 있는 적절한 권한이 부여됩니다. 다른 프로필을 선택한 경우 위에 언급된 권한이 포함되어 있는지 확인합니다.
3. 프로필을 선택하고(프로필이 두 개 이상인 경우) 클릭하여 엽니다.
4. 파란색 클릭 **사용자 추가** 버튼을 클릭하고 AdobeID와 이름을 입력한 다음 저장 을 클릭하여 추가를 완료합니다.

#### 사용자를 Places Service 개발자로 추가합니다.

Places Service REST API에 액세스할 수도 있는 사용자의 경우 개발자로 추가해야 합니다.
1. 제품 탭에서 **[!UICONTROL Adobe Experience Platform]** 카드.
2. 사용자가 이미 **[!UICONTROL Adobe Experience Platform]** 위의 지침에 따라 카드를 선택한 후 이전에 사용한 것과 동일한 프로필을 선택하고 클릭합니다.
3. 프로필 내에서 **개발자** 탭
4. 파란색 클릭 **개발자 추가** 버튼을 클릭하고 AdobeID와 이름을 입력한 다음 저장 을 클릭하여 추가를 완료합니다.

위의 단계를 완료하면 사용자는 액세스 권한이 있음을 알리는 이메일을 받게 됩니다 **[!UICONTROL Adobe Experience Platform]** 및 **[!UICONTROL Adobe Experience Platform 데이터 수집]**. 그런 다음에 로그인할 수 있습니다. [Adobe Experience Cloud](https://experience.adobe.com) 이 조직의 경우 Places Service 및 Data Collection에 액세스할 수 있습니다. 단계도 완료하는 경우 **[!UICONTROL 개발자 추가]**&#x200B;에 로그인할 수도 있습니다. [Adobe Developer 콘솔](https://developer.adobe.com/console/home) places Service REST API에 대한 액세스 권한을 제공하는 프로젝트를 만들 수 있습니다.

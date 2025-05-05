---
title: Adobe Developer 프로젝트 개요
description: Adobe Developer API 프로젝트 만들기에 대한 정보입니다.
exl-id: d7d31938-6c0e-40f8-a9d3-30af96043119
source-git-commit: 3d477c6133b74a7e6380d0db1af5125aaa844035
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Places API 액세스 개요 및 사전 요구 사항 {#developer-prereqs}

이 정보는 Adobe Developer Console에서 프로젝트를 만들고 장소 API 요청에 사용할 액세스 토큰을 생성하는 방법을 보여 줍니다.

## 사용자 액세스를 위한 사전 요구 사항

조직의 시스템 관리자에게 다음 작업이 완료되었는지 확인합니다.

* 귀하가 조직에 추가되었습니다.
* Adobe Experience Platform 내의 프로필에 추가되었습니다.

  자세한 내용은 [Places Service 액세스 권한 얻기](/help/places-gain-access.md)에서 *Places Service 및 Experience Platform Launch 프로필에 사용자 또는 개발자 추가*&#x200B;를 참조하십시오.

### REST API 요청

Places Service REST API에 대한 각 요청에는 다음 항목이 필요합니다.

* 조직 ID
* API 키(클라이언트 ID라고도 함)
* 클라이언트 암호
* 전달자 토큰

[Adobe Developer 콘솔](https://developer.adobe.com/console)이 있는 프로젝트에서 이러한 항목을 제공합니다.

* Places Service API용 프로젝트를 만들려면 아래의 *Places Service 프로젝트 만들기* 섹션을 참조하십시오.

>[!IMPORTANT]
>
>[Adobe Developer 콘솔](https://developer.adobe.com/console)에 로그인할 수 없거나 Places Service가 *통합 만들기 페이지*&#x200B;에서 옵션이 아닌 경우 [웹 서비스 API 개요](/help/web-service-api/places-web-services.md)의 *조직 요구 사항*&#x200B;을 참조하세요.

## Places Service API 프로젝트 만들기

Places Service API용 프로젝트를 만들려면 다음을 완료하십시오.

1. Adobe ID으로 [Adobe Developer 웹 사이트](https://developer.adobe.com)에 로그인합니다.
2. 페이지의 오른쪽 상단에 있는 **[!UICONTROL 콘솔]**&#x200B;을 클릭합니다.
3. 둘 이상의 Adobe 조직에 할당되어 있는 경우 페이지의 오른쪽 위 모서리에 있는 드롭다운 목록에서 올바른 조직을 선택합니다.
4. **[!UICONTROL 새 프로젝트 만들기]** 단추를 클릭합니다.
5. 새 프로젝트 시작 섹션에서 **[!UICONTROL API 추가]** 단추를 클릭합니다.
6. Places API를 선택하려면 페이지를 아래로 스크롤하여 Places 카드로 이동하고 카드의 오른쪽 상단에 있는 확인란을 클릭합니다.
7. **[!UICONTROL 다음]** 단추를 클릭합니다.
8. OAuth 서버 간 옵션을 선택합니다(선택 사항이 있는 경우).
9. 자격 증명의 이름을 지정하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
10. 프로필을 선택합니다(둘 이상 있는 경우 모두 작동해야 함).
11. **[!UICONTROL API 저장 및 구성]**&#x200B;을 클릭합니다.
12. 왼쪽 패널에서 자격 증명 아래의 **[!UICONTROL OAuth 서버 간]** 링크를 클릭합니다
13. 이 페이지에서는 다음 정보를 제공합니다.
    * Places Service REST API 요청에 사용할 액세스 토큰을 생성하는 방법입니다.
    * 자체 코드에서 액세스 토큰을 생성하는 방법의 예를 보려면 curl 명령을 확인하십시오.
    * 클라이언트 ID(API 키라고도 함) 보기
    * 클라이언트 암호 보기
    * 조직 ID 보기
    * Places Service REST API에 대한 요청에 모두 필요합니다.
14. 창 왼쪽 위의 경로에서 프로젝트 이름을 클릭하여 프로젝트의 이름을 보다 설명적인 이름으로 바꿀 수 있습니다
15. 그런 다음 페이지의 오른쪽 상단에 있는 **[!UICONTROL 프로젝트 편집]** 단추를 클릭합니다.

>[!IMPORTANT]
>
>Adobe 액세스 토큰은 24시간 동안 **only**&#x200B;만 유효하므로 샘플 CURL 명령을 저장합니다(5단계). 액세스 토큰이 더 이상 유효하지 않으면 토큰을 재생성해야 합니다.

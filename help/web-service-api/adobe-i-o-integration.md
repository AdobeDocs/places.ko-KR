---
title: Adobe I/O 통합 개요
description: Adobe I/O 통합 만들기에 대한 정보입니다.
exl-id: d7d31938-6c0e-40f8-a9d3-30af96043119
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 5%

---

# 통합 개요 및 사전 요구 사항 {#integration-prereqs}

이 정보는 Adobe I/O 및 Places Service 통합을 만드는 방법을 보여줍니다.

## 사용자 액세스를 위한 사전 요구 사항

조직의 시스템 관리자에게 다음 작업이 완료되었는지 확인합니다.

* Places Core Service가 조직의 Admin Console에 표시됩니다.
* 귀하가 조직에 추가되었습니다.
* 조직의 Places Core Service에 사용자로 추가되었습니다.

   자세한 내용은 *Places Service 및 Experience Platform Launch 프로필에 사용자 또는 개발자 추가* 위치: [Places Service 액세스 권한 얻기](/help/places-gain-access.md).

* 조직의 Places Core Service에 개발자로 추가되었습니다.

   개발자 추가에 대한 자세한 내용은 *Places Service 및 Experience Platform Launch 프로필에 사용자 또는 개발자 추가* 위치: [Places Service 액세스 권한 얻기](/help/places-gain-access.md).

   개발자 역할에 대한 자세한 내용은 [개발자 관리](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html).

### REST API 요청

Places Service REST API에 대한 각 요청에는 다음 항목이 필요합니다.

* 조직 ID
* API 키
* 전달자 토큰

Adobe I/O과의 통합은 JSON 웹 토큰(JWT)을 사용하여 전달자 토큰을 요청하는 방법과 이러한 항목을 제공합니다.

* JWT에 대한 자세한 내용은 [JSON 웹 토큰 소개](https://jwt.io/introduction/).
* Places Service에 대한 통합을 만들려면 *Places Service 통합 생성* 아래 섹션.
* API 키 통합, JWT 생성 및 공개 키 인증서를 이해하려면 다음을 참조하십시오. [Adobe I/O 인증 개요](https://www.adobe.io/apis/cloudplatform/console/authentication/gettingstarted.html).

>[!IMPORTANT]
>
>Adobe I/O 콘솔에 로그인할 수 없거나 Places Service가 *통합 생성 페이지*, 참조 *조직 요구 사항* 위치: [웹 서비스 API 개요](/help/web-service-api/places-web-services.md).

## Places Service 통합 만들기

Places Service 통합을 만들려면 다음 작업을 완료하십시오.

### 공개 및 개인 키 쌍 생성

Places Service 통합을 만들려면 공개 키와 개인 키 쌍이 필요합니다. 이러한 쌍을 구매하거나 자체 서명된 키를 생성할 수 있습니다.

자체 서명된 키를 생성하려면 다음을 수행하십시오.

1. 터미널 창에서 다음 줄을 복사하여 붙여 넣은 다음 키를 누릅니다 **[!UICONTROL 입력]** 각 줄을 붙여넣은 후:

   ```text
      mkdir keys
      cd keys
      openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout places_integration_test_private.key -out    places_integration_test_public.crt
   ```

   >[!IMPORTANT]
   >
   >쉽게 참조할 수 있도록 키의 이름을 지정하고 폴더에 저장하는 것이 좋습니다. 여러 통합을 만드는 경우 통합에 속하는 키를 쉽게 식별하고 관리할 수 있습니다.

1. OpenSSL에서 요청하는 정보를 입력합니다.

   ```text
   Country Name (2 letter code:  // Example: US
   State or Province Name (full name):  // Example: California
   Locality Name (eg, city):  // Example: San Jose
   Organization Name (eg, company):  // Example: Places
   Organizational Unit Name (eg, section):  // Example: Engineering
   Common Name (eg, fully qualified host name):  // Example: places.com
   Email Address:  // Example:  poi@places.com
   ```

   OpenSSL에 대한 자세한 내용은 [Openssl](https://www.openssl.org/).

   >[!IMPORTANT]
   >
   >귀하가 제공하는 정보는 키에 통합됩니다.

1. 가 있는 디렉토리로 이동합니다. `.key` 및 `.crt` 파일이 있습니다.

   예를 들어 MacOS에서 **[!UICONTROL Macintosh HD]** > **[!UICONTROL 사용자]** > **[!UICONTROL (사용자 이름)]** > **[!UICONTROL 키]**.

다음 비디오는 키 쌍을 생성하는 과정을 안내합니다.

![통합 비디오](/help/assets/places_integration_video.gif)

### Adobe I/O 콘솔에서 Places Service 통합 만들기

Places Service 통합을 만들려면:

1. 다음으로 이동 [https://console.adobe.io](https://console.adobe.io) Adobe ID으로 로그인합니다.
1. 다음에서 **빠른 시작** 섹션, 클릭 **통합 만들기**.
1. 선택 **[!UICONTROL API 액세스]** 및 클릭 **[!UICONTROL 계속]**.

   **[!UICONTROL API 액세스]** 는 기본 위치입니다.

1. 둘 이상의 Experience Cloud 조직에 대한 액세스 권한을 보유하고 있는 경우 오른쪽 상단의 드롭다운 목록에서 조직을 선택합니다.
1. 아래 **[!UICONTROL Experience Cloud]**, 선택 **[!UICONTROL 장소 서비스]** 를 통합할 Adobe 서비스로 **[!UICONTROL 계속]**.
1. 선택 **[!UICONTROL 새로운 통합]** 및 클릭 **[!UICONTROL 계속]**.
1. 새 통합 만들기 화면에서 이름과 설명을 입력합니다.
1. 을(를) 끌어다 놓기 `xxxx_public.crt` 위에서 만든 파일을 **[!UICONTROL 공개 키 인증서]** 놓기 영역.
1. 제품 프로필을 선택합니다.

   어떤 프로필을 선택해야 할지 모를 경우 시스템 관리자에게 문의하십시오.
1. 페이지 하단에서 **[!UICONTROL 통합 만들기]**.
1. 몇 초 후에 *통합 생성됨* 화면에서 다음 메시지가 표시되는지 확인합니다.

   `Your integration has been created.`

1. 맨 위에 통합 이름이 표시된 통합 세부 정보 페이지가 나타납니다.

   다음 **[!UICONTROL 개요]** 탭은 기본적으로 표시되며 API 키, 조직 ID, 기술 계정 ID 및 통합에 대한 기타 세부 정보를 표시합니다.

### 조직 ID 및 API 키 기록

1. 통합 세부 정보 페이지에서 다음을 클릭합니다. **[!UICONTROL 서비스]** tab 키를 사용하여 다음을 확인합니다. **[!UICONTROL 장소 서비스]** 아래에 표시됨 **[!UICONTROL 구성된 서비스]**.
1. 다음에서 **[!UICONTROL 개요]** 탭에서 API 키(클라이언트 ID)와 조직 ID를 찾아 기록합니다.

   이러한 ID는 각 Places Service REST API 요청에 필요합니다.

![](/help/assets/places_orgid_api-key.png)

### JWT 토큰 생성

통합 세부 정보 페이지에서 다음을 클릭합니다. **[!UICONTROL JWT]** 를 탭하여 jwt를 생성하고 교환 URL을 제공하여 통합을 테스트할 수 있습니다.

JWT 토큰을 생성하려면:

1. 텍스트 편집기에서 `private.key` 위에서 만든 파일입니다.
1. **[!UICONTROL JWT]** 탭에서, 키의 내용을 복사하여 **[!UICONTROL 개인 키 붙여넣기]** 필드에 붙여넣습니다.
1. 클릭 **[!UICONTROL JWT 생성]**.
1. **[!UICONTROL 샘플 CURL 명령]** 섹션에서 **[!UICONTROL 복사]**&#x200B;를 클릭하고 명령 프롬프트 또는 터미널 창에 내용을 붙여 넣습니다.
1. 를 눌러 명령 실행 **[!UICONTROL 입력]** 키보드에서.
1. 를 찾습니다. `"token_type": "bearer"` 및 `"access_token"` 값.

   전달자 액세스 토큰의 값은 Places Service API 요청에 사용할 값입니다.

>[!IMPORTANT]
>
>Adobe 액세스 토큰이 유효합니다. **전용** 24시간 동안 샘플 CURL 명령을 저장합니다(5단계). 액세스 토큰이 더 이상 유효하지 않으면 토큰을 다시 생성해야 합니다.

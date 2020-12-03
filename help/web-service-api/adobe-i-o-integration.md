---
title: Adobe I/O 통합 개요
description: Adobe I/O 통합 만들기에 대한 정보입니다.
translation-type: tm+mt
source-git-commit: c22efc36f2eac6b20fc555d998c3988d8c31169e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---


# Integration overview and prerequisites {#integration-prereqs}

이 정보는 Adobe I/O 및 장소 서비스 통합을 만드는 방법을 보여줍니다.

## 사용자 액세스를 위한 사전 요구 사항

다음 작업이 완료되었는지 조직의 시스템 관리자에게 확인합니다.

* 조직의 관리 콘솔에 핵심 서비스가 나타납니다.
* 조직에 추가되었습니다.
* 조직에서 핵심 서비스를 배치할 사용자로 추가되었습니다.

   자세한 내용은 *장소 서비스 및 Experience Platform Launch 프로필에 사용자 또는 개발자* 추가 [를 참조하십시오](/help/places-gain-access.md).

* 귀사는 귀사에서 핵심 서비스를 제공하기 위한 개발자로 추가되었습니다.

   개발자 추가에 대한 자세한 내용은 *장소 서비스 및 Experience Platform Launch 프로파일에* 사용자 또는 개발자 추가 [를 참조하십시오](/help/places-gain-access.md).

   개발자 역할에 대한 자세한 내용은 개발자 [관리를 참조하십시오](https://helpx.adobe.com/kr/enterprise/using/manage-developers.html).

### REST API 요청

Places Service REST API에 대한 각 요청에는 다음 항목이 필요합니다.

* 조직 ID
* API 키
* 무기명 토큰

Adobe I/O와의 통합에서는 JWT(JSON Web Token)를 사용하여 이러한 항목과 무기명 토큰을 요청하는 방법을 제공합니다.

* JWT에 대한 자세한 내용은 JSON [웹 토큰 소개를 참조하십시오](https://jwt.io/introduction/).
* Places Service에 대한 통합을 만들려면 아래의 *Places Service 통합* 만들기 섹션을 참조하십시오.
* API 키 통합, JWT 및 공개 키 인증서를 생성하려면 [Adobe I/O 인증 개요를 참조하십시오](https://www.adobe.io/apis/cloudplatform/console/authentication/gettingstarted.html).

>[!IMPORTANT]
>
>Adobe I/O 콘솔에 로그인할 수 없거나, 배치 서비스가 통합 *만들기 페이지의*&#x200B;옵션이 아닌 경우, *웹 서비스 API의* 조직 요구 사항 [개요를](/help/web-service-api/places-web-services.md)참조하십시오.

## 장소 서비스 통합 만들기

장소 서비스 통합을 만들려면 다음 작업을 완료하십시오.

### 공개 및 개인 키 쌍 생성

장소 서비스 통합을 만들려면 공개 및 개인 키 쌍이 필요합니다. 이러한 쌍을 구입하거나 자체 서명된 키를 생성할 수 있습니다.

자체 서명된 키를 생성하려면

1. 터미널 창에서 다음 줄을 복사하여 붙여 넣은 다음 각 줄을 **[!UICONTROL Enter]** 누릅니다.

   ```text
      mkdir keys
      cd keys
      openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout places_integration_test_private.key -out    places_integration_test_public.crt
   ```

   >[!IMPORTANT]
   >
   >쉽게 참조할 수 있도록 키의 이름을 지정하고 폴더에 저장하는 것이 좋습니다. 여러 통합을 만들 경우 어느 키가 어느 통합에 속하는지 쉽게 식별하고 관리할 수 있습니다.

1. OpenSSL에서 요청한 정보를 입력합니다.

   ```text
   Country Name (2 letter code:  // Example: US
   State or Province Name (full name):  // Example: California
   Locality Name (eg, city):  // Example: San Jose
   Organization Name (eg, company):  // Example: Places
   Organizational Unit Name (eg, section):  // Example: Engineering
   Common Name (eg, fully qualified host name):  // Example: places.com
   Email Address:  // Example:  poi@places.com
   ```

   OpenSSL에 대한 자세한 내용은 OpenSSL을 [참조하십시오](https://www.openssl.org/).

   >[!IMPORTANT]
   >
   >제공하는 정보는 키에 통합됩니다.

1. 파일과 파일이 있는 디렉토리 `.key` 로 `.crt` 이동합니다.

   예를 들어 MacOS에서 **[!UICONTROL Macintosh HD]** > **[!UICONTROL users]** > **[!UICONTROL (your user name)]** > **[!UICONTROL Keys]**&#x200B;로 이동합니다.

다음 비디오에서는 키 쌍을 생성하는 과정을 안내합니다.

![통합 비디오](/help/assets/places_integration_video.gif)

### Adobe I/O 콘솔에서 위치 서비스 통합 만들기

장소 서비스 통합을 만들려면

1. https://console.adobe.io [으로](https://console.adobe.io) 이동하여 Adobe ID에 로그인합니다.
1. 빠른 **시작** 섹션에서 통합 **만들기를 클릭합니다**.
1. **[!UICONTROL Access an API]**&#x200B;을(를) 선택하고 **[!UICONTROL Continue]**&#x200B;을(를) 클릭합니다 .

   **[!UICONTROL Access an API]** 는 기본 위치입니다.

1. 둘 이상의 Experience Cloud 조직에 액세스할 수 있는 경우 오른쪽 상단의 드롭다운 목록에서 조직을 선택합니다.
1. Under **[!UICONTROL Experience Cloud]**, select **[!UICONTROL Places Service]** as the Adobe service to which you want to integrate and click **[!UICONTROL Continue]**.
1. **[!UICONTROL New integration]**&#x200B;을(를) 선택하고 **[!UICONTROL Continue]**&#x200B;을(를) 클릭합니다 .
1. 새 통합 만들기 화면에서 이름 및 설명을 입력합니다.
1. 위에 만든 `xxxx_public.crt` 파일을 드롭 영역으로 드래그하여 **[!UICONTROL Public keys certificates]** 놓습니다.
1. 제품 프로필을 선택합니다.

   선택할 프로필을 잘 모르는 경우 시스템 관리자에게 문의하십시오.
1. 페이지 하단에서 을 클릭합니다 **[!UICONTROL Create integration]**.
1. 몇 초 후 *통합 만들기* 화면에서 다음 메시지가 나타나는지 확인합니다.

   `Your integration has been created.`

1. 통합 세부 사항 페이지가 맨 위에 통합 이름과 함께 나타납니다.

   이 **[!UICONTROL Overview]** 탭은 기본적으로 표시되며 API 키, 조직 ID, 기술 계정 ID 및 통합에 대한 기타 세부 정보를 표시합니다.

### 조직 ID 및 API 키 기록

1. 통합 세부 사항 페이지에서 **[!UICONTROL Services]** 탭을 클릭하고 아래 **[!UICONTROL Places Service]** 가 표시되는지 확인합니다 **[!UICONTROL Configured Services]**.
1. 탭에서 API 키(클라이언트 ID) 및 조직 ID를 찾아 기록합니다. **[!UICONTROL Overview]**

   이러한 ID는 각 Places Service REST API 요청에 필요합니다.

![](/help/assets/places_orgid_api-key.png)

### JWT 토큰 생성

통합 세부 정보 페이지에서 **[!UICONTROL JWT]** 탭을 클릭하여 JWT를 생성하고 교환 URL을 제공하여 통합을 테스트할 수 있습니다.

JWT 토큰을 생성하려면

1. 텍스트 편집기에서 위에서 만든 `private.key` 파일을 엽니다.
1. On the **[!UICONTROL JWT]** tab, copy the contents of the key and paste it in the **[!UICONTROL Paste private key]** field.
1. **[!UICONTROL Generate JWT]**&#x200B;을 클릭합니다.
1. In the **[!UICONTROL Sample CURL command]** section, click **[!UICONTROL Copy]** and paste the contents in your command prompt or terminal window.
1. 키보드를 눌러 명령을 실행합니다 **[!UICONTROL Enter]** .
1. 및 값 `"token_type": "bearer"` 을 `"access_token"` 찾습니다.

   베어러 액세스 토큰의 값은 Places Service API 요청에서 사용할 값입니다.

>[!IMPORTANT]
>
>Adobe 액세스 토큰은 24시간 **동안만** 유효하므로 샘플 CURL 명령(5단계)을 저장합니다. 액세스 토큰이 더 이상 유효하지 않은 경우 토큰을 다시 생성해야 합니다.
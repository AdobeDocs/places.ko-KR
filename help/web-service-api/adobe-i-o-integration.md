---
title: Adobe I/O 통합 개요
seo-title: Adobe I/O 통합 개요
description: Adobe I/O 통합 만들기에 대한 정보입니다.
seo-description: Adobe I/O 통합 만들기에 대한 정보입니다.
translation-type: tm+mt
source-git-commit: 6ff72eb72ce3ae1abf805b7b542721a7e4915824

---


# Adobe I/O 통합 개요 {#adobeio-integration}

Places REST API에 대한 각 요청에는 다음 항목이 필요합니다.

* 조직 ID
* API 키
* 베어러 토큰

Adobe I/O와의 통합에서는 JWT(JSON Web Token)를 사용하여 이러한 항목과 베어러 토큰을 요청하는 방법을 제공합니다.

## 추가 정보

* JWT에 대한 자세한 내용은 JSON [웹 토큰 소개를 참조하십시오](https://jwt.io/introduction/).
* 위치에 대한 통합을 만들려면 아래 위치 *통합* 만들기 섹션을 참조하십시오.
* API 키 통합, JWT 및 공개 키 인증서 생성에 대한 자세한 내용은 Adobe I/O [인증 개요를 참조하십시오](https://www.adobe.io/apis/cloudplatform/console/authentication/gettingstarted.html).

>[!IMPORTANT]
>
>Adobe I/O 콘솔에 로그인할 수 없거나, Experience Platform Location Service가 통합 만들기 페이지의 **&#x200B;옵션이 아닌 경우, 웹 서비스 API의 *조직 요구 사항* 개요를 [참조하십시오](/help/web-service-api/places-web-services.md).

## 위치 통합 만들기 {#create-places-integration}

위치 통합을 만들려면 다음 작업을 완료하십시오.

### 공개 및 개인 키 쌍 생성

위치 통합을 만들려면 공개 및 개인 키 쌍이 필요합니다. 이러한 쌍을 구입하거나 자체 서명 키를 생성할 수 있습니다.

자체 서명된 키를 생성하려면 다음을 수행합니다.

1. 터미널 창에서 다음 줄을 복사하여 붙여 넣은 다음 각 줄을 붙여넣은 **[!UICONTROL Enter]** 후 누릅니다.

   ```text
      mkdir keys
      cd keys
      openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout places_integration_test_private.key -out    places_integration_test_public.crt
   ```

   >[!IMPORTANT]
   >
   >쉽게 참조할 수 있도록 키 이름을 지정하고 폴더에 저장하는 것이 좋습니다. 여러 통합을 만들 경우 어느 키가 어느 통합에 속하는지 쉽게 식별하고 관리할 수 있습니다.

2. OpenSSL에서 요청한 정보를 입력합니다.

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

3. 파일과 `.key` 파일이 있는 디렉토리로 `.crt` 이동합니다.

   예를 들어 iOS에서 **[!UICONTROL Macintosh HD]** &gt; **[!UICONTROL users]** &gt; **[!UICONTROL (your user name)]** &gt; **[!UICONTROL Keys]**&#x200B;로 이동합니다.

다음 비디오에서는 키 쌍을 생성하는 과정을 안내합니다.

![](/help/assets/places_integration_video.gif)

### Adobe I/O 콘솔에서 위치 통합 만들기

위치 통합을 만들려면

1. https://console.adobe.io [으로](https://console.adobe.io) 이동하여 Adobe ID로 로그인합니다.
2. 두 개 이상의 Experience Cloud 조직에 액세스할 수 있는 경우 왼쪽의 드롭다운 목록에서 조직을 선택합니다.
3. 클릭 **[!UICONTROL New Integration]**.
4. 을 선택하고 **[!UICONTROL Access an API]** 클릭합니다 **[!UICONTROL Continue]**.
5. 아래에서 **[!UICONTROL Experience Cloud]**&#x200B;통합할 Adobe 서비스로 선택하고 **[!UICONTROL Places]** **[!UICONTROL Continue]**&#x200B;클릭합니다.
6. 을 선택하고 **[!UICONTROL New integration]** 클릭합니다 **[!UICONTROL Continue]**.
7. 새 *통합* 만들기 화면에서 이름과 설명을 입력합니다.
8. 위에서 만든 `xxxx_public.crt` 파일을 드래그하여 **[!UICONTROL Public keys certificates]** 놓기 영역으로 놓습니다.
9. At the bottom of the page, click **[!UICONTROL Create integration]**.
10. 몇 초 후 [통합] *작성* 화면에서 다음 메시지가 표시되는지 확인합니다.

   `Your integration has been created.`

11. 클릭 **[!UICONTROL Continue to integration details]**.

   API 키와의 통합 개요, 조직 ID, 기술 계정 ID 및 통합에 대한 기타 세부 사항이 표시됩니다.

### 조직 ID 및 API 키 기록

1. 이 **[!UICONTROL Services]** 탭에서 **[!UICONTROL Places]** 이 메시지가 표시되는지 확인합니다.
2. 탭에서 API 키(클라이언트 ID) 및 조직 ID를 찾아 기록합니다. **[!UICONTROL Overview]**

   이러한 ID는 각 REST API 요청에 필요합니다.

![](/help/assets/places_orgid_api-key.png)

### JWT 토큰 생성

Adobe I/O 콘솔에서는 **[!UICONTROL JWT]** JWT를 생성하고 교환 URL을 제공하여 통합을 테스트할 수 있습니다.

JWT 토큰을 생성하려면

1. 텍스트 편집기에서 위에서 만든 `private.key` 파일을 엽니다.
2. 탭에서 키의 내용을 복사하여 **[!UICONTROL JWT]** **[!UICONTROL Paste private key]** 필드에 붙여 넣습니다.
3. 클릭 **[!UICONTROL Generate JWT]**.
4. 섹션에서 **[!UICONTROL Sample CURL command]** **[!UICONTROL Copy]** 명령 프롬프트 또는 터미널 창에서 내용을 클릭하여 붙여 넣습니다.
5. 키보드를 눌러 명령을 **[!UICONTROL Enter]** 실행합니다.
6. 및 `"token_type": "bearer"` 값을 찾습니다 `"access_token"` .

   베어러 액세스 토큰의 값은 Places API 요청에서 사용할 값입니다.

>[!IMPORTANT]
>
>Adobe 액세스 토큰은 24시간 **동안만** 유효하므로 샘플 CURL 명령(5단계)을 저장합니다. 액세스 토큰이 더 이상 유효하지 않은 경우 토큰을 다시 생성해야 합니다.

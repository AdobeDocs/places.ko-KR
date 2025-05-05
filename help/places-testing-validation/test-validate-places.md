---
title: 위치 서비스 테스트 및 유효성 검사
description: 이 섹션에서는 Places Service를 테스트하고 검증하는 방법에 대해 설명합니다.
exl-id: 8dad6619-566b-4aea-b29c-a89192a66441
source-git-commit: 2b5c53887c9ed0f2a672c377121a39537ee58f01
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 1%

---

# Places Service를 테스트하는 Recommendations {#test-validate-loc-svc}

많은 고객 및 조직에서 전 세계의 POI를 정의할 예정이므로 Places Service가 애플리케이션과 상호 작용하는 방법을 시뮬레이션하고 테스트하는 방법이 중요합니다. 이 정보는 정의된 POI 및 사용자의 현재 위치를 기반으로 올바르게 트리거되는 Places Service 시작 및 종료를 테스트하고 확인하는 방법을 이해하는 데 도움이 됩니다.

환경 변수는 위치 신호 및 정확도의 한 요소가 될 수 있으므로 먼저 개발자 도구 및 시뮬레이션된 위치 항목을 사용하여 로컬에서 작업하여 기준선 결과를 설정하는 것이 좋습니다. 목표는 모든 위치 이벤트가 올바르게 작동하는지 확인하는 것입니다. 위치 이벤트가 올바르게 확인되면 솔루션 통합(예: Analytics, Target 및 Campaign)을 테스트할 수 있습니다. 테스트 활동을 돕기 위해 포스트백을 사용하여 Slack 웹후크를 설정하고 개별 개발 환경에서 GPX 파일을 로드해야 합니다.

>[!IMPORTANT]
>
>이 계획에서는 POI가 [위치 서비스 UI](https://places.adobe.com)에서 만들어졌고 위치 확장의 최신 버전이 설치되고 올바르게 구성되어 있다고 가정합니다. 활성 지역 모니터링을 수행하는 경우, 지역 모니터링 솔루션이 구현되는 경우도 가정한다. 자세한 내용은 iOS용 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md), [CoreLocation 설명서](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) 또는 [Android 위치 설명서](https://developer.android.com/training/location/geofencing)를 참조하십시오.

| 단계 | 설명 | 예상 결과 |
|--- |--- |--- |
| 1 | Android이 추적 위치에 대한 액세스 권한을 부여할 수 있도록 적절한 매니페스트 키가 입력되었는지 확인합니다. | 확인됨 |
| 1a | iOS에 위치 업데이트가 구성되어 있는지 확인합니다. 또한 iOS에서 위치 추적에 대한 사용자 권한을 요청할 적절한 플리스트 키가 설정되어 있는지 확인하십시오. | 확인됨 |
| 2 | iOS에 대해 설정된 모니터링 모드를 확인합니다. 연속 모드는 더 큰 정확도 및 지속성을 허용하지만, 또한 배터리 수명을 더 심하게 소모한다. | 중요한 변경 또는 지속적인 변경 |
| 3 | 둘 이상의 POI 라이브러리를 사용하는 경우 Experience Platform Launch을 위한 위치 확장에서 적절한 라이브러리가 선택되었는지 확인합니다. | 확인됨 |
| 4 | Mobile Core 및 Places 확장의 최신 버전이 Gradle 또는 CocoaPods를 통해 앱과 번들로 제공되었는지 확인합니다. | 확인됨 - 최근 업데이트에 대한 자세한 내용은 [릴리스 정보](/help/release-notes.md)를 참조하세요. |
| 5 | 테스트를 위해 올바른 환경이 구성되어 있는지 확인합니다. Launch 환경 ID는 Launch 개발 환경과 일치해야 합니다. | 확인됨 |
| 6 | 테스트할 각 POI에 대한 GPX 파일을 만듭니다. GPX 파일은 로컬 개발 환경에서 위치 항목을 시뮬레이션하는 데 사용할 수 있습니다. GPX 파일 생성 및 사용에 대한 자세한 내용은 다음을 참조하십시오. <br>[iOS 시뮬레이터용 GPX 파일 [닫힘]](https://stackoverflow.com/questions/17292783/gpx-files-for-ios-simulator)<br>[https://mapstogpx.com/mobiledev.php](https://mapstogpx.com/mobiledev.php)<br>[모바일 앱에서의 위치 테스트](https://qacumtester.wordpress.com/2014/02/27/location-testing-in-mobile-apps/) | GPX 파일이 만들어지고 앱 프로젝트에 로드됩니다. |
| 7 | 다른 작업을 수행하지 않고 Android Studio 또는 XCode에서 애플리케이션을 실행하고 적절한 경고를 확인하여 추적 위치에 대한 액세스를 요청할 수 있습니다. *항상 허용* 권한을 클릭합니다.<br><br>장치 시뮬레이터를 사용하는 대신 컴퓨터에 연결된 실제 장치를 사용하는 것이 좋습니다. | IDE를 통해 로드된 응용 프로그램에 위치 요청 프롬프트가 표시되어야 함 |
| 8 | 위치 권한이 수락되면 위치 SDK는 장치의 현재 위치를 검색하며 지역 모니터링 코드는 현재 위치에서 가장 가까운 20개의 POI를 모니터링해야 합니다 | 표 아래의 로그 샘플을 참조하십시오. |
| 9 | XCode 또는 Android studio에서 서로 다른 위치 간을 전환하면 특정 POI에 대한 시작 이벤트가 생성됩니다. POI 입력 시 아래 로그가 필요합니다. | 표 아래의 로그 샘플을 참조하십시오. |
| 10 | 지역 모니터가 인근 POI를 찾으면 위치 Ping을 전송하여 테스트해야 합니다. Launch에서 위치 확장을 사용하여 지역 펜스 항목을 기반으로 트리거하는 새 규칙을 만듭니다. 그런 다음 Mobile Core를 사용하여 포스트백을 전송하여 새 작업을 만듭니다. Slack Webhook 앱을 생성하면 위치 시작 및 종료를 볼 수 있습니다. Slack 웹후크 앱 만들기에 대한 자세한 내용은 [들어오는 웹후크를 사용하여 메시지 보내기](https://api.slack.com/messaging/webhooks)를 참조하십시오. |  |
| 10a | Launch에서 다음을 포함한 위치 확장에 대한 데이터 요소를 추가했는지 확인합니다. <br>현재 POI 이름<br>현재 POI 위도<br>현재 POI 경도<br>마지막으로 입력한 이름<br>마지막으로 입력한 위도<br>마지막으로 입력한 경도<br>마지막으로 종료한 경도<br>마지막으로 종료한 위도<br>마지막으로 종료한 경도<br>타임스탬프 |  |
| 10b | 이벤트 = Places → Enter POI로 새 규칙 만들기 |  |
| 10c | 작업 만들기 = 모바일 코어 → 포스트백 |  |
| 10d | Slack 앱용 Webhook URL 사용(예: https://hooks.slack.com/services/TKN5FKS68/BNFP7SVD...) |  |
| 10e | 게시물 본문은 `{text: User is in POI -  {%%Last Entered POI Name%%} in {%%Last Entered POI City%%} additional information: Radius:{%%Last Entered POI Radius%%} Timestamp: {%%timestamp%%}}`과(와) 유사합니다. <br>여기에서 만든 특정 데이터 요소를 사용하는지 확인하십시오. |  |
| 10f | Launch에 새 데이터 요소와 규칙 변경 사항을 모두 게시해야 합니다. (Launch 인터페이스의 오른쪽 상단에서 작업 개발 라이브러리를 선택해야 합니다.) |  |
| 11 | 개발자 IDE에서 GPX 위치 사이를 전환하여 애플리케이션을 다시 시작하고 테스트합니다. | 이제 개발 환경에서 서로 다른 위치를 선택하면 각 POI의 항목을 표시하는 Slack 알림이 표시됩니다. |
|  | **빠른 요약 지점**<br>&#x200B;이 테스트는 특정 POI 위치로 이동할 필요 없이 로컬에서 수행할 수 있습니다. 유효성 검사 테스트는 애플리케이션이 올바르게 구성되어 있고 해당 위치에 대한 올바른 권한을 받았는지 확인하는 데 도움이 됩니다. <br><br>또한 이 유효성 검사를 수행하면 정의된 POI가 지역 모니터링 구현에 올바르게 작동하고 있음을 알 수 있습니다.  이 단계 후에는 Campaign에서 메시지를 테스트하여 POI 시작 및 종료에 따라 적절한 메시지가 표시되는지 확인합니다. |  |
|  | **Places Service로 Adobe Campaign Standard 인앱 메시지를 테스트하는 중.** |  |
| 12 | 기본 Campaign 대시보드에서 새 앱 내 메시지를 구성합니다(유형 = broadcast). |  |
| 12a | 트리거에서 **Places 이벤트 유형 - 항목을 트리거로 선택**&#x200B;합니다. |  |
| 12b | **[!UICONTROL 사용자 지정 메타데이터 배치]**&#x200B;를 추가 필터로 선택합니다. POI 유형 = 마지막으로 입력한 POI를 사용합니다.<br>POI 유형으로 **[!UICONTROL 마지막으로 입력한 날짜]**&#x200B;을(를) 사용합니다. 대부분의 경우 **[!UICONTROL 마지막으로 입력한 날짜]**&#x200B;은(는) **[!UICONTROL 현재 POI]**&#x200B;과(와) 동일하기 때문입니다. <br><br>**[!UICONTROL 현재 POI &#x200B;]**&#x200B;는 겹치는 POI 지오펜스가 있는 인스턴스에서만 사용해야 합니다. 이 경우 이러한 POI에 등급을 지정해야 하므로&#x200B;**[!UICONTROL &#x200B;현재 POI &#x200B;]**&#x200B;에는 사용자가 현재 있을 수 있는 2개 또는 3개의 지오펜스 중 상위 순위가 지정된 POI가 표시됩니다. |  |
| 12c | 메시지를 수신할 POI의 범위를 좁히는 데 도움이 되는 사용자 지정 메타데이터 키를 선택합니다. |  |
| 12d | 빈도 및 기간의 경우 기준을 좋아하지 않는 경우 더 짧은 기간 내에 트리거를 만료할 수 있도록 1~2일만 유지합니다. |  |
| 12e | Always/Once 또는 Until 클릭스루의 경우 *ALWAYS*&#x200B;을(를) 선택하여 여러 위치에서 테스트할 수 있습니다. | 적절한 메타데이터 기준을 충족하는 위치 변경을 시뮬레이션하면 인앱 메시지가 항상 표시됩니다. |
| 12f | 표시에서 로컬 알림 이외의 옵션을 선택합니다. 이렇게 하면 앱으로 전경에서 테스트할 때 보다 쉽게 볼 수 있습니다.) |  |
| 12g | 인앱 메시지를 준비/확인하고 배포합니다. |  |
| 13 | 개발 환경에서 새 캠페인 규칙이 다운로드되도록 하려면 애플리케이션을 종료했다가 다시 시작합니다. | 새 Campaign 규칙 파일을 장치에 다운로드하려면 애플리케이션을 다시 완전히 다시 시작해야 한다는 것을 잊지 마십시오. |
| 14 | 개발 애플리케이션에서 이전에 만든 GPX 파일을 사용하여 위치를 전환합니다. | 인앱 메시지가 설정된 이전 기준에 따라 표시되는 것을 볼 수 있습니다. |
| 15 | 다음 테스트에서는 기본적으로 이전과 동일한 단계를 복사하지만 이번에는 로컬 알림을 테스트합니다. | 예상 결과는 일치 기준이 충족될 때마다 로컬 알림이 표시되는 것입니다. |
| 16 | 새 앱 내 메시지를 구성합니다(유형 = broadcast). |  |
| 16a | 트리거에서 **[!UICONTROL Places 이벤트 형식]** - **[!UICONTROL Entry를 트리거로 선택]**&#x200B;합니다. |  |
| 16b | 위치 사용자 지정 메타데이터를 추가 필터로 선택합니다. **[!UICONTROL POI 유형]** = **[!UICONTROL 마지막으로 입력한 POI]**&#x200B;을(를) 사용합니다. |  |
| 16c | 메시지를 수신할 POI의 범위를 좁히는 데 도움이 되는 사용자 지정 메타데이터 키를 선택합니다. |  |
| 16d | 빈도 및 기간의 경우 기준을 좋아하지 않는 경우 더 짧은 기간 내에 트리거를 만료할 수 있도록 1~2일만 유지합니다. |  |
| 16e | Always/Once 또는 클릭스루할 때까지 **[!UICONTROL ALWAYS]**&#x200B;합니다. |  |
| 16f | 표시 유형에 대해 **[!UICONTROL 로컬 알림]**&#x200B;을 선택합니다. |  |
| 16g | 인앱 메시지를 준비/확인하고 배포합니다. |  |
| 17 | 개발자 환경에서 장치를 연결하고 빌드에서 **[!UICONTROL 재생]**&#x200B;을 누릅니다. 해당 위치가 작동하는지 확인한 후 애플리케이션을 백그라운드로 전환하고 Xcode 또는 Android Studio에서 위치를 계속 전환합니다. 위치 변경을 나타내는 콘솔 읽기가 계속 표시되어야 하며 트리거에 설정된 기준에 따라 로컬 알림도 표시되어야 합니다. (1~2초 정도 지연될 수 있습니다.) | 예상 결과는 일치 기준이 충족될 때마다 로컬 알림이 표시되는 것입니다. |
|  | **요약 지점** <br>이 단계에서 로컬 환경에 POI 항목이 표시됩니다. POI 작업을 기반으로 한 Campaign의 메시징도 확인해야 합니다. 오류가 있는 경우 Slack 알림이 발송되지 않았는지 확인합니다. Slack 메시지가 없으면 새 위치 항목이 기록되지 않았을 수 있으므로 응용 프로그램 콘솔을 확인합니다. 결과가 성공적이면 애플리케이션이 올바르게 작동하는지 확인하고 Places Service 및 Campaign 메시징 서비스도 올바르게 작동하는지 확인할 수 있습니다. |  |
|  | **사이트 내 테스트** <br>위치에서 테스트할 때는 크게 변경되지 않습니다. Slack 포스트백을 활성 상태로 유지하면 디바이스가 해당 위치에 대한 시작 및 종료를 가져오는지 이해하는 데 도움이 됩니다. |  |
| 18 | Wi-Fi와 셀룰러 기능이 비활성화된 상태로 장치를 시작한 다음 POI 영역에서 한 번 활성화하여 테스트를 수행합니다. | 오류가 있는 경우 Slack에서 지역 펜스 항목 및 알림을 받는지 여부를 확인합니다. Slack 알림의 타임스탬프는 무엇입니까? |
| 19 | 휴대폰만 활성화한 상태에서 Wi-Fi를 끈 상태로 테스트를 수행합니다. |  |
| 20 | 휴대폰과 Wi-Fi를 모두 켠 상태에서 테스트를 수행합니다. |  |
|  | **요약 지점** <br>사이트 내 테스트는 개발 테스트와 거의 일치해야 합니다. POI 지역 펜스에서 보낸 시간, 셀 신호 가용성 및 인근 Wi-Fi 액세스 포인트의 강도와 같이, 사용자 위치를 결정하는 데 영향을 줄 수 있는 몇 가지 환경 요인이 있다는 점을 명심하십시오. |  |

## 로그 샘플

**8단계 :** 위치를 업데이트하는 동안 iOS 및 Android 로그가 필요합니다.

**iOS**

```
[AdobeExperienceSDK DEBUG <Places>]: Requesting 20 nearby POIs for device location (<lat>, <longitude>)
[AdobeExperienceSDK DEBUG <Places>]: Response from Places Query Service contained <n> nearby POIs   
```

**Android**

```
PlacesExtension - Dispatching nearby places event with n POIs   
```

**9단계 :** 이벤트 중에 iOS 및 Android 로그가 필요합니다.

**iOS**

```
[AdobeExperienceSDK TRACE <Places>]: Dispatching Places region entry event for place ID <poiId>
```

**Android**

```
PlacesExtension -  Dispatching Places Region Event for <poi name> with eventType entry
```

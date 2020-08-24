---
title: 장소 서비스 테스트 및 유효성 검사
description: 이 섹션에서는 Places Service를 테스트하고 검증할 수 있는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 954bd9a12ede841d189138dfbe3d65ad4c1bd3c3
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 2%

---


# Recommendations, 장소 서비스 테스트 {#test-validate-loc-svc}

많은 고객 및 조직은 전 세계 POI를 정의할 수 있으므로 장소 서비스가 애플리케이션과 상호 작용하는 방식을 시뮬레이션하고 테스트할 수 있는 방법이 중요합니다. 이 정보는 정의된 POI와 사용자의 현재 위치를 기반으로 올바르게 트리거되는 장소 서비스 항목 및 종료를 테스트하고 확인하는 방법을 이해하는 데 도움이 됩니다.

환경 변수는 위치 신호 및 정확성의 요소가 될 수 있으므로 먼저 개발자 도구와 시뮬레이트된 위치 항목을 사용하여 로컬에서 작업하여 기준 결과를 설정하는 것이 좋습니다. 목표는 모든 위치 이벤트가 올바르게 작동하는지 확인하는 것입니다. 위치 이벤트가 올바르게 검증되면 솔루션 통합(예: Analytics, Target 및 캠페인)을 테스트할 수 있습니다. 테스트 활동을 돕기 위해 포스트백을 사용하여 Slack Webhook를 설정하고 개별 개발 환경에서 GPX 파일을 로드해야 합니다.

>[!IMPORTANT]
>
>이 플랜에서는 POI가 [장소 서비스 UI에서](https://places.adobe.com) 생성되었으며, 장소 확장 및 위치 모니터 확장 프로그램의 최신 버전이 설치되고 올바르게 구성되어 있다고 가정합니다. 자세한 내용은 [위치 확장](/help/places-ext-aep-sdks/places-extension/places-extension.md) 및 [위치 모니터 확장](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md)기능을 참조하십시오.

| 단계.  | 설명 | 예상 결과 |
|--- |--- |--- |
| 1 | 추적 위치에 대한 액세스 권한을 부여하기 위해 Android에 적절한 매니페스트 키가 입력되었는지 확인합니다. 자세한 내용은 매니페스트에 [권한 추가를 참조하십시오](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.html#add-permissions-to-the-manifest). | 확인 |
| 1a | 위치 업데이트가 iOS에서 구성되었는지 확인합니다. 또한 iOS에서 위치를 추적하기 위한 사용자 권한을 요청하기 위해 적절한 plist keys가 설정되어 있는지 확인하십시오. 자세한 내용은 백그라운드에서 [위치 업데이트 활성화를 참조하십시오.](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.html#enable-location-updates-background) | 확인 |
| 2 | iOS용으로 설정된 모니터링 모드를 확인합니다. 연속 모드를 사용하면 정확도와 지속성이 향상되지만 배터리 수명을 크게 줄일 수 있습니다. 자세한 내용은 [모니터링 모드(iOS만 해당)를 참조하십시오.](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-api-reference.html#monitoring-mode-ios-only) | 중요한 변경 또는 연속 |
| 3 | 두 개 이상의 POI 라이브러리를 사용하는 경우 [Experience Platform Launch용 위치] 확장 기능에서 적절한 라이브러리가 선택되었는지 확인합니다. | 확인 |
| 4 | 최신 버전의 Mobile Core 및 Places/Places Monitor 익스텐션이 Gradle 또는 CocoaPods를 통해 앱과 번들로 제공되었는지 확인합니다. | 확인됨 - 최근 업데이트에 대한 자세한 내용은 [릴리스 노트를 참조하십시오.](/help/release-notes.md) |
| 5 | 테스트를 위해 올바른 환경이 구성되어 있는지 확인합니다. 론치 환경 ID는 론치 개발 환경과 일치해야 합니다. | 확인 |
| 6 | 테스트할 각 POI에 대한 GPX 파일을 만듭니다. 로컬 개발 환경에서 GPX 파일을 사용하여 위치 항목을 시뮬레이션할 수 있습니다. GPX 파일 만들기 및 사용에 대한 자세한 내용은 다음을 참조하십시오. <br>[iOS 시뮬레이터용 GPX 파일 [닫힘]](https://stackoverflow.com/questions/17292783/gpx-files-for-ios-simulator)<br>[https://mapstogpx.com/mobiledev모바일 앱에서](https://mapstogpx.com/mobiledev.php)<br>[phpLOCATION 테스트](https://qacumtester.wordpress.com/2014/02/27/location-testing-in-mobile-apps/) | GPX 파일이 앱 프로젝트에서 만들어지고 로드됩니다. |
| 7 | 다른 작업을 하지 않고 Android Studio 또는 XCode에서 애플리케이션을 실행할 수 있으며 추적 위치에 대한 액세스를 요청하는 적절한 경고를 볼 수 있습니다. 항상 허용 *권한을* 클릭합니다.<br><br>장치 시뮬레이터를 사용하는 대신 컴퓨터에 연결된 실제 장치를 사용하는 것이 좋습니다. | IDE를 통해 로드된 응용 프로그램에 위치 요청 메시지가 표시되어야 합니다. |
| 8 | 위치 권한이 승인되면 위치 SDK는 장치의 현재 위치를 검색할 예정이며 위치 모니터 확장 기능은 현재 위치에서 가장 가까운 20개의 POI를 모니터링합니다 | 표 아래의 로그 샘플을 참조하십시오. |
| 9 | XCode 또는 Android studio에서 서로 다른 위치를 전환하면 특정 POI에 대한 시작 이벤트가 생성됩니다. 아래 로그는 POI에 가입되어 있어야 합니다. | 표 아래의 로그 샘플을 참조하십시오. |
| 10 | 위치 모니터가 가까운 POI를 찾은 경우 위치 전원을 보내 테스트해야 합니다. 론치에서 위치 확장을 사용하여 지역 울타리 항목을 기반으로 트리거하는 새 규칙을 만듭니다. 그런 다음 Mobile Core를 사용하여 포스트백을 전송하여 새 동작을 만듭니다. Slack 웹 후크 앱을 만들면 위치 항목 및 종료를 볼 수 있습니다. Slack 웹 후크 앱 만들기에 대한 자세한 내용은 수신 웹 후크를 [사용하여 메시지 전송을 참조하십시오.](https://api.slack.com/messaging/webhooks) |  |
| 10a | 론치에서 다음을 포함한 위치 확장 기능에 대한 데이터 요소를 추가했는지 확인합니다. <br>현재 POI<br>이름 현재 POI<br>위도<br>경현 POI<br>긴<br>마지막 입력<br>이름<br>마지막 마지막 입력<br>마지막 마지막 긴Last 입력한 마지막긴Last마지막으로 입력한 이름<br>마지막 이후Last Clended마지막 종료긴 타임스탬프 |  |
| 10b | 이벤트 = 장소, POI 입력 |  |
| 10c | 작업 만들기 = 모바일 코어→포스트백 |  |
| 10d | Slack 앱에 대한 웹 후크 URL을 사용합니다(예: https://hooks.slack.com/services/TKN5FKS68/BNFP7SVD....). |  |
| 10e | 게시물 본문은 다음과 비슷합니다. `{text: User is in POI -  {%%Last Entered POI Name%%} in {%%Last Entered POI City%%} additional information: Radius:{%%Last Entered POI Radius%%} Timestamp: {%%timestamp%%}}`. <br>여기에서 만든 특정 데이터 요소를 사용해야 합니다. |  |
| 10f | Launch에서 모든 새 데이터 요소 및 규칙 변경을 게시해야 합니다. (실행 인터페이스의 오른쪽 상단에 있는 작업 개발 라이브러리를 선택해야 합니다.) |  |
| 11 | 개발자 IDE에서 GPX 위치를 뒤집을 수 있어 애플리케이션을 다시 실행하고 테스트할 수 있습니다. | 개발 환경에서 다른 위치를 선택할 때 각 POI에 대한 항목이 표시된 Slack 알림이 표시됩니다. |
|  | **빠른 요약**<br> POI 위치로 이동하지 않고도 모든 테스트를 로컬에서 수행할 수 있습니다. 유효성 검사 테스트는 애플리케이션이 올바르게 구성되어 있고 해당 위치에 대한 올바른 권한을 받았는지 확인하는 데 도움이 됩니다. <br><br>또한 정의된 POI가 위치 모니터 확장 프로그램에서 올바르게 작동하는지 확인할 수 있습니다.  이 단계 후에는 Campaign에서 메시지를 테스트하여 POI 항목 및 종료에 따라 적절한 메시지가 표시되는지 확인합니다. |  |
|  | **Places Service를 사용하여 Adobe Campaign Standard 인앱 메시지 테스트** |  |
| 12 | 기본 캠페인 대시보드에서 새 인앱 메시지를 구성합니다(유형 = 브로드캐스트). |  |
| 12a | 트리거에서 위치 **이벤트 유형 - 항목을 트리거로 선택합니다**. |  |
| 12b | 추가 필터 **[!UICONTROL Places Custom metadata]** 로 선택합니다. POI 유형 = 마지막 입력 POI를 사용합니다.<br>대부분의 경우 **[!UICONTROL Last Entered]** 는 POI와 **[!UICONTROL Last Entered]** 같기 때문에 POI 유형으로 사용합니다 **[!UICONTROL Current POI]**. <br><br>**[!UICONTROL Current POI]**는 겹치는 POI 지역 펜스가 있는 경우에만 사용해야 합니다. 이 경우, 이러한 POI는 등급을 지정해야 하고, 그런 다음 해당 사용자가 현재 있을 수 있는 2 또는 3개의 지역 펜스 중 상위 등급 POI를 표시합니다.**[!UICONTROL Current POI]** |  |
| 12c | 메시지를 받을 POI의 범위를 좁히는 데 도움이 되는 사용자 지정 메타데이터 키를 선택합니다. |  |
| 12d | 빈도 및 기간의 경우, 기준을 좋아하지 않는 경우 트리거 기간을 짧은 기간 내에 만료할 수 있도록 1 또는 2일만 유지하십시오. |  |
| 12e | [항상/한 번] 또는 [클릭스루까지]의 경우 여러 위치에서 테스트할 수 *있도록* [항상]을 선택합니다. | 적절한 메타데이터 기준을 충족하는 위치 변경을 시뮬레이션할 때 인앱 메시지가 ALWAYS로 표시됩니다. |
| 12f | 표시에 대해 로컬 알림 이외의 옵션을 선택합니다. 이를 통해 전경 상태에서 앱을 사용하여 테스트할 때 보다 손쉽게 확인할 수 있습니다.) |  |
| 12g | 인앱 메시지 준비/확인 및 배포 |  |
| 13 | 개발 환경에서 새 캠페인 규칙이 다운로드되었는지 확인하려면 응용 프로그램을 다시 종료하고 시작하십시오. | 새 캠페인 규칙 파일을 장치로 다운로드하려면 응용 프로그램을 다시 실행해야 합니다. |
| 14 | 개발 애플리케이션에서 이전에 만든 GPX 파일을 사용하여 위치를 전환합니다. | 설정된 이전 기준에 따라 인앱 메시지가 표시됩니다. |
| 15 | 다음 테스트의 경우, 기본적으로 이전과 동일한 단계를 복사하지만, 이번에는 LOCAL NOTIFICATION을 테스트합니다. | 예상 결과는 일치 기준이 충족될 때마다 로컬 알림이 표시된다는 것입니다. |
| 16 | 새 인앱 메시지를 구성합니다(type = broadcast). |  |
| 16a | 트리거에서 **[!UICONTROL Places event type]** -를 **[!UICONTROL Entry as the trigger]**&#x200B;선택합니다. |  |
| 16b | 사용자 지정 메타데이터를 추가 필터로 배치합니다(사용 **[!UICONTROL POI type]** = **[!UICONTROL Last Entered POI]**. |  |
| 16c | 메시지를 받을 POI의 범위를 좁히는 데 도움이 되는 사용자 지정 메타데이터 키를 선택합니다. |  |
| 16d | 빈도 및 기간의 경우 기준을 좋아하지 않는 경우 트리거를 짧은 기간 내에 만료할 수 있도록 1~2일만 유지하십시오. |  |
| 16e | [항상/한 번] 또는 [클릭스루까지]의 경우, 를 클릭합니다 **[!UICONTROL ALWAYS]**. |  |
| 16f | 표시 유형에 대해 을 선택합니다 **[!UICONTROL Local Notification]**. |  |
| 16g | 인앱 메시지 준비/확인 및 배포 |  |
| 17 | 개발자 환경에서 장치를 연결하고 빌드를 누릅니다 **[!UICONTROL Play]** . 해당 위치를 설정한 후 응용 프로그램의 배경을 지정하고 Xcode 또는 Android Studio에서 위치를 계속 전환합니다. 위치 변경을 나타내는 콘솔 읽기-아웃이 여전히 표시되고, 트리거에서 설정된 기준에 따라 로컬 알림이 표시됩니다. (1-2초 지연이 있을 수 있습니다.) | 예상 결과는 일치 기준이 충족될 때마다 로컬 알림이 표시된다는 것입니다. |
|  | **요약 지점** <br>이 단계에서는 로컬 환경에서 POI 항목이 표시됩니다. POI 작업을 기반으로 Campaign에서 메시지를 표시해야 합니다. 오류가 있는 경우 Slack 알림이 발송되지 않았는지 확인합니다. Slack 메시지가 없으면 새 위치 항목이 기록되지 않았을 수 있으므로 응용 프로그램 콘솔을 확인하십시오. 결과가 성공적이면, 애플리케이션이 올바로 작동하고 장소 서비스 및 캠페인 메시징 서비스도 제대로 작동하는지 확인할 수 있습니다. |  |
|  | **현장 테스트** 위치 <br>에서 테스트할 때는 크게 변경되어서는 안 됩니다. 슬랙백 포스트백을 활성화하면 장치의 시작 위치에서 나간 후 나간 위치를 이해하는 데 도움이 됩니다. |  |
| 18 | wifi 및 셀룰러 비활성화 상태에서 시작하는 장치로 테스트를 수행한 다음 POI 영역에서 한 번 활성화합니다. | 오류가 있는 경우 Slack에서 지역 펜스 항목 및 알림을 받는지 확인합니다. Slack 알림의 타임스탬프란? |
| 19 | 휴대폰을 사용할 수 있고 와이피가 꺼진 상태에서 테스트를 수행합니다. |  |
| 20 | 셀룰러 및 와이파이 모두 켜진 상태에서 테스트를 실시합니다. |  |
|  | **요약 지점** <br>온사이트 테스트는 개발 테스트와 밀접하게 일치해야 합니다. POI 지역 펜스에서 보낸 시간, 셀 신호 가용성, 인근 wifi 액세스 포인트의 강도와 같이 사용자 위치를 결정하는 데 영향을 줄 수 있는 몇 가지 환경 요인이 있습니다. |  |

## 로그 샘플

**8단계:** 위치 업데이트 중 iOS 및 Android 로그가 필요합니다.

**iOS**

```
[AdobeExperienceSDK DEBUG <com.adobe.placesMonitor>]: Authorization status changed: Always
[AdobeExperienceSDK DEBUG <Places>]: Requesting 20 nearby POIs for device location (<lat>, <longitude>)
[AdobeExperienceSDK DEBUG <Places>]: Response from Places Query Service contained <n> nearby POIs
[AdobeExperienceSDK DEBUG <com.adobe.placesMonitor>]: Received a new list of POIs from Places: (
<ACPPlacePoi: 0x600002b75a40> Name: <poi name>; ID:<poi id>; Center: (<lat>, <long>); Radius: <radius>
..
..)   
```

**Android**

```
PlacesMonitor - All location settings are satisfied to monitor location
PlacesMonitor - PlacesMonitorInternal : New location obtained: <latitude> <longitude> Attempting to get the near by pois
PlacesExtension - Dispatching nearby places event with n POIs
PlacesMonitor - Attempting to Monitor POI with id <poi id> name <poi name> latitude <lat> longitude <longitude>
PlacesMonitor - Attempting to Monitor POI with id <poi id> name <poi name> latitude <lat> longitude <longitude>
PlacesMonitor - Attempting to Monitor POI with id <poi id> name <poi name> latitude <lat> longitude <longitude>
...
...
PlacesMonitor - Successfully added n fences for monitoring
```

**9단계:** 이벤트 도중 iOS 및 Android 로그가 필요합니다.

**iOS**

```
[AdobeExperienceSDK TRACE <Places>]: Dispatching Places region entry event for place ID <poiId>
```

**Android**

```
PlacesExtension -  Dispatching Places Region Event for <poi name> with eventType entry
```

---
title: 위치 확장
description: 위치 확장을 사용하면 사용자의 위치에 따라 작업할 수 있습니다.
exl-id: 09c02753-09b3-4e07-82b2-b6c72c4e0e42
source-git-commit: 795808b38851d5afcedc03f58e9a1d6342830934
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 위치 확장 {#places-extension}

위치 확장을 사용하면 사용자의 위치에 따라 작업할 수 있습니다. 이 확장은 Places Query Service API에 대한 인터페이스입니다. GPS 좌표 및 지오펜스 영역 이벤트가 포함된 이벤트를 수신하면 이 확장은 규칙 엔진에서 처리하는 새 이벤트를 발송합니다. 위치 확장은 API에서 검색하는 앱 데이터에 가장 가까운 POI 목록을 검색하고 전달합니다. API에서 반환되는 영역은 캐시 및 지속성에 저장되며, 이는 제한된 오프라인 처리를 허용합니다.

## Adobe Experience Platform Launch에 위치 확장 설치

1. Experience Platform Launch에서 **[!UICONTROL 확장]** 탭.
1. 설정 **[!UICONTROL 카탈로그]** 탭에서 를 찾습니다 **[!UICONTROL 위치]** 확장을 마우스로 가리킨 다음 **[!UICONTROL 설치]**.
1. 이 속성에서 사용할 위치 라이브러리를 선택합니다. 앱에서 액세스할 수 있는 라이브러리입니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   를 클릭하면 **[!UICONTROL 저장]**&#x200B;를 검색하는 경우, Experience Platform SDK는 선택한 라이브러리에서 POI를 위한 위치 서비스 를 검색합니다. POI 데이터는 앱을 빌드할 때 라이브러리 다운로드에 포함되지 않지만, POI의 위치 기반 하위 집합은 런타임 시 최종 사용자의 장치에 다운로드되고 사용자의 GPS 좌표를 기반으로 합니다.

1. 게시 프로세스를 완료하여 SDK 구성을 업데이트합니다.

   Experience Platform Launch에서 게시에 대한 자세한 내용은 [게시](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/overview.html).

### 위치 확장 구성 {#configure-places-extension}

![](/help/assets/places-extension.png)

## 앱에 위치 확장 추가 {#add-places-to-app}

위치 확장을 Android 및 iOS 앱에 추가할 수 있습니다. iOS 또는 Android 애플리케이션에 위치를 추가하는 단계는 아래에 나와 있습니다. 위치 확장 은 아래의 다음 플랫폼에 대해서도 사용할 수 있습니다. 이러한 플랫폼 중 하나를 사용하여 개발할 때 애플리케이션에 위치 를 추가하는 경우 함께 제공되는 링크를 참조하십시오.

**[Cordova Places 플러그인](https://github.com/adobe/cordova-acpplaces/blob/master/README.md)**

**[React Native Places 플러그인](https://github.com/adobe/react-native-acpplaces/blob/master/README.md)**

**[Flutter Places 플러그인](https://github.com/adobe/flutter-acpplaces_monitor)**

**[Xamarin Places 플러그인](https://github.com/adobe/xamarin-acpcore)**


### Android

Java를 사용하여 앱에 위치 확장 기능을 추가하려면:

1. 앱의 gradle 파일을 사용하여 프로젝트에 위치 확장을 추가합니다.

   ```java
   implementation 'com.adobe.marketing.mobile:places:1.+'
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   ```

1. 애플리케이션의 기본 활동에서 위치 확장을 가져옵니다.

   ```java
   import com.adobe.marketing.mobile.Places;
   ```


### iOS

Objective-C 또는 Swift를 사용하여 앱에 위치 확장 을 추가하려면 다음을 수행합니다.

1. 위치 및 [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) 라이브러리를 프로젝트에 추가합니다. 다음 pod를 `Podfile`:

   ```objective-c
   pod 'ACPPlaces', '~> 1.0'
   pod 'ACPCore', '~> 2.0'    # minimum Core version for Places is 2.0.3
   ```

   또는 Cocoapods를 사용하지 않는 경우 Adobe에서 Mobile 코어 및 위치 라이브러리를 수동으로 포함할 수 있습니다. [릴리스 페이지](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/) 설정

1. Cocoapods를 업데이트합니다.

   ```objective-c
   pod update
   ```

1. Xcode를 열고 AppDelegate 클래스에서 Core 및 Places 헤더를 가져옵니다.

   **Objective-C**

   ```objective-c
   #import "ACPCore.h"
   #import "ACPPlaces.h"
   ```

   **Swift**

   ```swift
   import ACPCore
   import ACPPlaces
   ```

### Mobile Core에 위치 확장 등록 {#register-places-mobile-core}

Android 및 iOS에서 Mobile Core에 위치 확장을 등록해야 합니다.

#### Android

앱의 `OnCreate` 메서드: Places 확장을 등록합니다.

```java
public class PlacesTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);

        try {
            Places.registerExtension();
            MobileCore.start(null);
        } catch (Exception e) {
            Log.e("PlacesTestApp", e.getMessage());
        }
    }
}
```

#### iOS

앱의 `application:didFinishLaunchingWithOptions:` 메서드를 사용하여 Places 확장을 다른 SDK 등록 호출에 등록합니다.

**Objective-C**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // make other sdk registration calls
    [ACPPlaces registerExtension];    
    return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // make other sdk registration calls
    ACPPlaces.registerExtension();
    return true;
}
```

### 위치 멤버십 유지 시간 수정 {#places-ttl}

특히 장치가 백그라운드 위치 업데이트를 받지 않는 경우 위치 데이터가 빠르게 부실해질 수 있습니다.

를 설정하여 장치의 Places 멤버십 데이터에 대한 유지 시간 제어 `places.membershipttl` 구성 설정. 전달된 값은 장치에 대해 유효한 위치 상태가 유지되는 시간(초)을 나타냅니다.

#### Android

의 콜백 내부 `MobileCore.start()` 를 호출하기 전에 필요한 변경 사항으로 구성을 업데이트합니다. `lifecycleStart`:

```java
public class PlacesTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);

        try {
            Places.registerExtension();
            MobileCore.start(new AdobeCallback() {
                @Override
                public void call(Object o) {
                    // switch to your App ID from Launch
                    MobileCore.configureWithAppID("my-app-id");

                    final Map<String, Object> config = new HashMap<>();
                    config.put("places.membershipttl", 30);
                    MobileCore.updateConfiguration(config);

                    MobileCore.lifecycleStart(null);
                }
            });
        } catch (Exception e) {
            Log.e("PlacesTestApp", e.getMessage());
        }
    }
}
```

#### iOS

의 콜백에서 첫 번째 줄 `ACPCore`s `start:` 메서드, 호출 `updateConfiguration:`

**Objective-C**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // make other sdk registration calls

    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
        [ACPCore updateConfiguration:@{@"places.membershipttl":@(30)}];

        if (appState != UIApplicationStateBackground) {
            [ACPCore lifecycleStart:nil];            
        }
    }];

    return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // make other sdk registration calls

    let appState = application.applicationState;            
    ACPCore.start {
        ACPCore.updateConfiguration(["places.membershipttl" : 30])

        if appState != .background {
            ACPCore.lifecycleStart(nil)
        }    
    }

    return true;
}
```

## 구성 키

런타임 시 프로그래밍 방식으로 SDK 구성을 업데이트하려면 다음 정보를 사용하여 Places 확장 구성 값을 변경합니다. 자세한 내용은 [구성 API 참조](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| 키 | 필수 여부 | 설명 |
| :--- | :--- | :--- |
| `places.libraries` | 예 | 모바일 앱용 Places 확장 라이브러리. 라이브러리 ID와 모바일 앱에서 지원하는 라이브러리 이름을 지정합니다. |
| `places.endpoint` | 예 | 라이브러리 및 POI에 대한 정보를 가져오는 데 사용되는 기본 위치 쿼리 서비스 끝점입니다. |
| `places.membershipttl` | 아니요 | 기본값은 3600(1시간 초)입니다. 장치에 대한 위치 멤버십 정보가 유효한 기간(초)을 나타냅니다. |

---
title: 위치 확장
description: 위치 확장 기능을 사용하면 사용자의 위치에 따라 작업을 수행할 수 있습니다.
translation-type: tm+mt
source-git-commit: a7dddb78e1e00a0bde01ea668334932759a9dae8
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 5%

---


# 위치 확장 {#places-extension}

위치 확장 기능을 사용하면 사용자의 위치에 따라 작업을 수행할 수 있습니다. 이 익스텐션은 위치 쿼리 서비스 API에 대한 인터페이스입니다. 이 확장은 GPS 좌표 및 지리 정보 영역 이벤트를 포함하는 이벤트를 수신함으로써 규칙 엔진에서 처리하는 새 이벤트를 전달합니다. 또한 위치 확장 기능은 API에서 검색하는 앱 데이터에 대해 가장 가까운 POI 목록을 검색하여 전달합니다. API가 반환하는 영역은 캐시 및 지속성 내에 저장되므로 제한된 오프라인 처리를 허용합니다.

## Adobe Experience Platform 시작 시 위치 확장 설치

1. In Experience Platform Launch, click the **[!UICONTROL Extensions]** tab.
1. 탭에서 **[!UICONTROL Catalog]** 확장자를 찾아 **[!UICONTROL Places]** 클릭합니다 **[!UICONTROL Install]**.
1. 이 속성에 사용할 위치 라이브러리를 선택합니다. 앱에서 액세스할 수 있는 라이브러리입니다.
1. **[!UICONTROL Save]**&#x200B;를 클릭합니다.

   클릭하면 Experience Platform SDK가 선택한 라이브러리 **[!UICONTROL Save]**&#x200B;에서 위치 서비스에 POI를 검색합니다. 앱을 빌드할 때 POI 데이터는 라이브러리 다운로드에 포함되지 않지만, 위치 기반 POI의 하위 세트가 런타임 시 최종 사용자의 장치로 다운로드되고 사용자의 GPS 좌표를 기반으로 합니다.

1. 게시 프로세스를 완료하여 SDK 구성을 업데이트합니다.

   Experience Platform Launch에서 게시에 대한 자세한 내용은 [게시를 참조하십시오](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/overview.html).

### Configure the Places extension {#configure-places-extension}

![](//help/assets/places-extension.png)

## 앱에 위치 확장 기능 추가 {#add-places-to-app}

Android 및 iOS 앱에 위치 확장을 추가할 수 있습니다. iOS 또는 Android 애플리케이션에 위치를 추가하는 단계는 아래에 나와 있습니다. 위치 확장 기능은 아래의 플랫폼에서도 사용할 수 있습니다. 이러한 플랫폼 중 하나로 개발할 때 애플리케이션에 위치를 추가하는 경우 함께 제공되는 링크를 참조하십시오.

**[Cordova Places Plugin](https://github.com/adobe/cordova-acpplaces/blob/master/README.md)**

**[Responsive Native Places Plugin](https://github.com/adobe/react-native-acpplaces/blob/master/README.md)**

**[Flutter Places Plugin](https://github.com/adobe/flutter-acpplaces_monitor)**

**[Xamarin Places Plugin](https://github.com/adobe/xamarin-acpcore)**


### Android

Java를 사용하여 앱에 위치 확장을 추가하려면:

1. 앱의 등급 파일을 사용하여 프로젝트에 위치 확장을 추가합니다.

   ```java
   implementation 'com.adobe.marketing.mobile:places:1.+'
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   ```

1. 애플리케이션의 기본 활동에서 위치 확장을 가져옵니다.

   ```java
   import com.adobe.marketing.mobile.Places;
   ```


### iOS

Objective-C 또는 Swift를 사용하여 앱에 위치 확장을 추가하려면:

1. 프로젝트에 위치 및 [모바일 코어](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) 라이브러리를 추가합니다. 다음 창을 사용자 창에 추가해야 합니다 `Podfile`.

   ```objective-c
   pod 'ACPPlaces', '~> 1.0'
   pod 'ACPCore', '~> 2.0'    # minimum Core version for Places is 2.0.3
   ```

   또는 코드를 사용하지 않는 경우 Github의 [릴리스 페이지에서](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/) Mobile Core 및 Places 라이브러리를 수동으로 포함할 수 있습니다.

1. 코드 업데이트:

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

### Mobile Core로 Places 확장 등록 {#register-places-mobile-core}

Android 및 iOS에서 Mobile Core에 위치 확장을 등록해야 합니다.

#### Android

앱의 `OnCreate` 메서드에서 위치 확장을 등록합니다.

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

앱의 `application:didFinishLaunchingWithOptions:` 방식에서 다른 SDK 등록 호출을 사용하여 Places 확장을 등록합니다.

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

### 장소 멤버십 기간 수정 {#places-ttl}

특히 장치가 백그라운드 위치 업데이트를 받지 못하는 경우 위치 데이터가 빠르게 오래된 상태가 될 수 있습니다.

구성 설정을 설정하여 장치에 [배치] 멤버십 데이터를 실시간 관리하는 `places.membershipttl` 방법을 살펴봅니다. 전달된 값은 [위치] 상태가 장치에 대해 유효한 상태로 남아 있는 시간(초)을 나타냅니다.

#### Android

호출 전 필요한 변경 사항을 사용하여 구성을 `MobileCore.start()` 업데이트하는 콜백 내부 `lifecycleStart`:

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

On the first line in the callback of `ACPCore`&#39;s `start:` method, `updateConfiguration:`

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

런타임에 프로그래밍 방식으로 SDK 구성을 업데이트하려면 다음 정보를 사용하여 Places 확장 구성 값을 변경합니다. 자세한 내용은 구성 [API 참조를 참조하십시오](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| 키 | 필수 여부 | 설명 |
| :--- | :--- | :--- |
| `places.libraries` | 예 | 모바일 앱용 Places 확장 라이브러리 라이브러리 ID와 모바일 앱이 지원하는 라이브러리 이름을 지정합니다. |
| `places.endpoint` | 예 | 라이브러리 및 POI에 대한 정보를 가져오는 데 사용되는 기본 위치 쿼리 서비스 끝점입니다. |
| `places.membershipttl` | 아니요 | 기본값은 3600(1시간 초)입니다. 장치의 멤버십 정보가 유효한 기간(초)을 나타냅니다. |

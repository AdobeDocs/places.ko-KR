---
title: 위치 모니터 확장 사용
description: 위치 모니터 확장 기능을 설치, 구성 및 사용하는 방법에 대한 정보입니다.
translation-type: tm+mt
source-git-commit: 7fdaace59886225b7fd9b0eba8cc6c2a139fa2d7
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 6%

---


# 위치 모니터 확장 사용 {#using-places-monitor-extension}

위치 모니터 확장 기능을 사용하려면 다음 작업을 완료하십시오.

## Experience Platform Launch에 위치 모니터 확장 설치

1. In Experience Platform Launch, click the **[!UICONTROL Extensions]** tab.
1. 탭에서 **[!UICONTROL Catalog]** 확장 **[!UICONTROL Places Monitor]** 기능을 찾아 설치를 **클릭합니다**.
1. **[!UICONTROL Save]**&#x200B;를 클릭합니다.
1. 게시 프로세스에 따라 SDK 구성을 업데이트합니다.

### 위치 모니터 확장 구성 {#configure-places-monitor-extension}

위치 모니터 확장 기능에 대한 구성 작업이 없습니다.

![위치 모니터](/help/assets/configure_places_monitor.png)구성

## 앱에 위치 모니터 확장 추가 {#add-monitor-extension-to-app}

Android 또는 iOS 애플리케이션에 위치 모니터 확장 기능을 추가하는 방법은 아래에 나와 있습니다.

Places Monitor 익스텐션에 대한 추가 플랫폼 지원은 다음과 같습니다.
**[Cordova 위치 모니터](https://github.com/adobe/cordova-acpplaces-monitor/blob/master/README.md)**

**[반응형 기본 위치 모니터](https://github.com/adobe/react-native-acpplaces-monitor/blob/master/README.md)**

**[Flutter Places Monitor](https://github.com/adobe/flutter_acpplaces_monitor/blob/master/README.md)**


### Android

Android에서 다음 단계를 완료하십시오.

#### Java

1. 앱의 등급 파일을 사용하여 위치 모니터 확장 기능과 위치 확장을 프로젝트에 추가합니다.

1. 또한 최신 Google 위치 서비스를 일반 파일에 포함시킬 수 있습니다.

   ```java
   implementation 'com.adobe.marketing.mobile:places:1.+'
   implementation 'com.adobe.marketing.mobile:places-monitor:1.+'
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   implementation 'com.google.android.gms:play-services-location:16.0.0'
   ```

1. 애플리케이션의 기본 활동에서 위치 모니터 확장 기능을 가져옵니다.

   ```java
   import com.adobe.marketing.mobile.PlacesMonitor;
   ```

### iOS

iOS에서 다음 단계를 완료하십시오.

1. Add the library to your project via your Cocoapods `Podfile` by adding `pod 'ACPPlacesMonitor'`.
1. 위치 및 위치 모니터 라이브러리를 가져옵니다.

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPPlaces.h"
#import "ACPPlacesMonitor.h"
```

#### Swift

```swift
import ACPCore
import ACPPlaces
import ACPPlacesMonitor
```


## 장소 모니터 등록 및 시작 {#register-start-places-monitor}

Android 또는 iOS에서 장소 모니터를 등록하고 시작해야 합니다.

## Android

Android에서 다음 단계를 완료하십시오.

### Java

앱의 `OnCreate` 메서드에서 위치 모니터 확장을 등록합니다.

```java
public class MobileApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.ConfigureWithAppId("yourAppId");
        try {
            PlacesMonitor.registerExtension(); //Register PlacesMonitor with Mobile Core
            Places.registerExtension(); //Register Places with Mobile Core
            MobileCore.start(null);
            PlacesMonitor.start();//Start monitoring the geo-fences
        } catch (Exception e) {
            //Log the exception
        }
    }
}
```

>[!IMPORTANT]
>
>위치 모니터링은 위치 확장명에 따라 다릅니다. 위치 모니터 확장명을 수동으로 설치하는 경우, 프로젝트에 `places.aar` 라이브러리를 추가해야 합니다.

## iOS

iOS 앱에서`application:didFinishLaunchingWithOptions`Mobile Core `PlacesMonitor` 에 등록 및 위치:

### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [ACPPlaces registerExtension];
    [ACPPlacesMonitor registerExtension];
    [ACPCore start:^{            
        // do other initialization required for the SDK
        [ACPPlacesMonitor start];
    }];

    return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ACPCore.configure(withAppId: "yourAppId")
    ACPPlaces.registerExtension()       
    ACPPlacesMonitor.registerExtension()
    ACPCore.start({
        // do other initialization required for the SDK
        ACPPlacesMonitor.start()
    })

    // Override point for customization after application launch.        
    return true
}
```

>[!IMPORTANT]
>
>위치 모니터링은 위치 확장명에 따라 다릅니다. When manually installing the Places Monitor extension, ensure that you also add the `libACPPlaces_iOS.a` library to your project.


## 매니페스트에 권한 추가

### Android

**Java**

모든 버전의 Android에서 앱에 위치 권한이 필요하다고 선언하려면 앱 매니페스트에 `<uses-permission>` 요소를 최상위 `<manifest>` 요소의 자식으로 추가하십시오. API 레벨 29 이상을 대상으로 하는 Android 응용 프로그램의 경우 앱이 백그라운드에서 위치에 액세스할 수 있도록 허용하려면 ACCESS_BACKGROUND_LOCATION 권한을 포함합니다.

```java
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.adobe.placesapp">
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    // Only for Android apps targeting API level 29 and above
  <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
  <application>        
    ...    
  </application>
</manifest>
```


## 백그라운드에서 위치 업데이트 사용  {#enable-location-updates-background}

iOS는 일시 중단되거나 더 이상 실행되지 않는 앱에 위치 이벤트 전달을 지원합니다. 위치 모니터 확장 프로그램의 백그라운드에서 위치 업데이트를 받으려면 앱에서 위치 업데이트 기능을 구성하십시오 `Xcode.background-location-updates`.

![위치 모니터 사용](/help/assets/using-the-places-monitor_1.png)

## plist 키 구성

다음 키가 앱의 `Info.plist` 파일에 포함되어야 합니다.

* `NSLocationWhenInUseUsageDescription` - 전경 상태에서 앱을 실행할 때 앱이 사용자의 위치 정보에 대한 액세스를 요청하는 이유를 설명해야 합니다.
* `NSLocationAlwaysAndWhenInUseUsageDescription` - 텍스트는 앱이 사용자의 위치 정보에 대한 액세스를 항상 요청하는 이유를 설명합니다.

>[!TIP]
>
>앱이 iOS 10 및 이전 버전을 지원하는 경우 `NSLocationAlwaysUsageDescription` 키도 필요합니다.

![](/help/assets/using-the-places-monitor_2.png)

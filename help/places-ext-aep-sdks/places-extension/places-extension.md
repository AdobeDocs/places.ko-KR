---
title: 위치 확장
description: 위치 확장을 사용하면 사용자의 위치에 따라 작업을 수행할 수 있습니다.
feature: Mobile SDK
exl-id: 09c02753-09b3-4e07-82b2-b6c72c4e0e42
source-git-commit: 9f2c6fee6e0d6d075b662cc0b6cbee49cf05ee55
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 10%

---

# 위치 확장 {#places-extension}

Adobe 개발자 포털로 이동하여 [Places SDK 확장](https://developer.adobe.com/client-sdks/documentation/places/).

<!-- 

The Places extension allows you to act based on the location of your users. This extension is the interface to the Places Query Service APIs. By listening for events that contain GPS coordinates and geofence region events, this extension dispatches new events that are processed by the Rules Engine. The Places extension also retrieves and delivers a list of the nearest POI for the app data that retrieves from the APIs. The regions returned by the APIs are stored in cache and persistence, which allows limited offline processing.

## Install the Places extension in Adobe Experience Platform Launch

1. In Experience Platform Launch, click the **[!UICONTROL Extensions]** tab.
1. On the **[!UICONTROL Catalog]** tab, locate the **[!UICONTROL Places]** extension, and click **[!UICONTROL Install]**.
1. Select the Places libraries you want to use in this property. These are the libraries that will be accessible in your app.
1. Click **[!UICONTROL Save]**.

    When you click **[!UICONTROL Save]**, the Experience Platform SDK searches the Places Services for POIs in the libraries that you selected. The POI data is not included in the download of the library when you build the app, but a location-based subset of POIs is downloaded to the end user's device at runtime and is based on the user's GPS coordinates.

1. Complete the publishing process to update the SDK configuration.

   For more information about publishing in Experience Platform Launch, see [Publishing](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html).

### Configure the Places extension {#configure-places-extension}

  ![](/help/assets/places-extension.png)

## Add the Places extension to your app {#add-places-to-app}

You can add the Places extension to your Android and iOS apps. The steps to add Places to your iOS or Android application can be seen below. Places extensions are also available for the following platforms below. For adding Places to your application when developing with one of these platforms see the accompanying links:

**[Cordova Places Plugin](https://github.com/adobe/cordova-acpplaces/blob/master/README.md)** 

**[React Native Places Plugin](https://github.com/adobe/react-native-acpplaces/blob/master/README.md)** 

**[Flutter Places Plugin](https://github.com/adobe/flutter-acpplaces_monitor)**

**[Xamarin Places Plugin](https://github.com/adobe/xamarin-acpcore)**


### Android

To add the Places extension to your app by using Java:

1. Add the Places extension to your project using your app's gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:places:1.+'
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   ```

1. Import the Places extension in your application's main activity.

    ```java
    import com.adobe.marketing.mobile.Places;
    ```


### iOS

To add Places extension to your app by using Objective-C or Swift:

1. Add the Places and [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) libraries to your project. You will need to add the following pods to your `Podfile`:

   ```objective-c
   pod 'ACPPlaces', '~> 1.0'
   pod 'ACPCore', '~> 2.0'    # minimum Core version for Places is 2.0.3
   ```

   Alternatively, if you are not using Cocoapods, you can manually include the Mobile Core and the Places libraries from our [releases page](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/) on Github.

1. Update your Cocoapods:

   ```objective-c
   pod update
   ```

1. Open Xcode, and in your AppDelegate class, import the Core and the Places headers:

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

### Register the Places extension with Mobile Core {#register-places-mobile-core}

You need to register the Places extension with Mobile Core in Android and iOS.

#### Android

In your App's `OnCreate` method register the Places extensions:

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

In your App's `application:didFinishLaunchingWithOptions:` method, register the Places extension with your other SDK registration calls:

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

### Modifying Places membership time-to-live {#places-ttl}

Location data can quickly become stale, especially if the device is not receiving background location updates.

Control the time-to-live for Places membership data on the device by setting the `places.membershipttl` configuration setting. The value passed in represents the number of seconds that the Places state will remain valid for the device.

#### Android

Inside the callback of `MobileCore.start()` update the configuration with the necessary changes prior to calling `lifecycleStart`:

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

On the first line in the callback of `ACPCore`'s `start:` method, call `updateConfiguration:`

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

## Configuration keys

To update the SDK configuration programmatically at runtime, use the following information to change your Places extension configuration values. For more information, see [Configuration API Reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Key | Required | Description |
| :--- | :--- | :--- |
| `places.libraries` | Yes | The Places extension libraries for the mobile app. It specifies the library ID and the name of the library that the mobile app supports. |
| `places.endpoint` | Yes | The default Places Query Service endpoint, which is used to get information about libraries and POIs. |
| `places.membershipttl` | No | Default value of 3600 (seconds in an hour). Indicates how long, in seconds, Places membership information for the device will remain valid. |

-->

---
title: 배치 모니터 API 참조
description: 위치 모니터용 API 목록입니다.
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2

---


# 배치 모니터 API 참조 {#places-api-reference}

## 위치 모니터 확장 등록

위치 모니터 확장을 코어 이벤트 허브에 등록합니다.

### RegisterExtension(Android)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

다음은 Java의 구문입니다.

```java
public static void registerExtension();
```

#### 예

Experience Platform SDK의 나머지 부분을 초기화하는 `onCreate` 메서드에서 이 메서드를 호출합니다.

```java
public class MobileApp extends Application {
  @Override
  public void onCreate(){
     super.onCreate();
     MobileCore.setApplication(this);
     try {
        PlacesMonitor.registerExtension();
     } catch (Exception e) {
       //Log the exception
       }
    }
 }
```

### RegisterExtension(iOS)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

다음은 Objective-C의 구문입니다.

```objective-c
+ (void) registerExtension;
```

#### 예

This method should be called in the `didFinishLaunchingWithOptions` delegate method of the `AppDelegate`.

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [ACPCore configureWithAppId:@"launch-appID"];    
    [ACPPlaces registerExtension];    
    [ACPPlacesMonitor registerExtension];

    [ACPCore start:^{
        // do other initialization of the SDK
    }];

    return YES;
}
```

## 익스텐션 버전

위치 모니터 확장의 현재 버전을 반환합니다.

### ExtensionVersion(Android)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```java
public static String extensionVersion();
```

#### 예

```java
String placesMonitorVersion = PlacesMonitor.extensionVersion();
```

### ExtensionVersion(iOS)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```objective-c
+ (nonnull NSString*) extensionVersion;
```

#### 예

```objective-c
NSString *placesMonitorVersion = [ACPPlacesMonitor extensionVersion];
```

## 디바이스 모니터링 시작

장치의 위치를 추적하고 주변 위치 모니터링을 시작합니다.

### 시작(Android)

사용자가 장치 위치 사용 권한을 부여하지 않은 경우 API에 대한 첫 번째 호출에서 사용자에게 권한을 `start` 입력하라는 메시지가 표시됩니다.

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```java
public static void start();
```

#### 예

```java
PlacesMonitor.start();
```

### 시작(iOS)

>[!IMPORTANT]
>
>모니터링을 시작하려면 위치 서비스에 필요한 인증이 있어야 합니다.
>
>* 응용 프로그램에 위치 서비스에 대한 인증이 제공되지 않은 경우 API에 대한 첫 번째 호출은 응용 프로그램에 대해 구성된 대로 위치 `start` 서비스를 사용할 수 있는 권한을 요청합니다.
>* 장치의 기능에 따라, 인증이 제공된 경우 위치 모니터는 현재 설정을 기준으로 사용자의 위치를 추적합니다. `ACPPlacesMonitorMode` 기본적으로 모니터는 `ACPPlacesMonitorModeSignificantChanges`사용합니다.


>[!CAUTION]
>
>SDK 초기화가 완료되기 전에 모니터링 시작 호출이 수행되면 무시될 수 있습니다.

제공된 콜백에서 SDK `start` 의 초기화가 완료되었는지 확인할 수 `ACPCore::start:`있습니다.

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```objectivec
+ (void) start;
```

#### 예

SDK를 초기화할 때 위치 모니터 시작:

```objective-c
[ACPCore start:^{
    [ACPPlacesMonitor start];
}];
```

앱 실행에서 나중에 위치 모니터 시작:

```objective-c
[ACPPlacesMonitor start];
```

## 장치 모니터링 중지

장치의 위치 추적을 중지합니다.

### 중지(Android)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```java
public static void stop();
```

#### 예

```java
PlacesMonitor.stop();
```

### 중지(iOS)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```objectivec
+ (void) stop;
```

#### 예

```objective-c
[ACPPlacesMonitor stop];
```

## 업데이트 위치

이 API를 사용하여 장치의 위치를 즉시 업데이트합니다. 이 API를 호출하면 장치가 사용자가 지정한 정확도의 위치를 확인하려고 합니다. 또한 이 프로세스는 확장자가 모니터링하는 주변 POI를 새로 고칩니다.

### UpdateLocation(Android)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```java
public static void updateLocation();
```

#### 예

```java
PlacesMonitor.updateLocation();
```

### UpdateLocationNow(iOS)

#### 구문

```objective-c
+ (void) updateLocationNow;
```

#### 예

```objective-c
[ACPPlacesMonitor updateLocationNow];
```

## 앱 위치 권한

이 API를 사용하여 사용자에게 위치 서비스 사용 권한이 표시되고 권한이 부여된 위치 권한 유형을 설정할 수 있습니다.

### SetLocationPermission(Android)

이 API 파섹

>[!TIP]
>
>이 API 파섹
>
>사용자에게 표시할 적절한 권한 부여 프롬프트를 설정하려면 JavaScript 앞에 이 API를 `PlacesMonitor.start()`호출합니다. 이 방법을 호출하면 능동적으로 모니터링하는 동안 위치 권한 수준을 요청된 권한 값으로 업그레이드합니다. 요청한 인증 수준이 이미 제공되었거나 응용 프로그램 사용자가 거부되었거나 또는 권한을 에서 `ALWAYS_ALLOW` 로 다운그레이드하려고 시도해도 `WHILE_USING_APP`이 방법은 적용되지 않습니다.

위치 권한은 다음 값 중 하나로 설정할 수 있습니다.

* `PlacesMonitorLocationPermission.WHILE_USING_APP`

   이 값은 응용 프로그램을 사용하는 동안에만 장치 위치에 액세스하라는 메시지를 표시합니다. 사용자가 장치 화면에서 앱을 보고 있을 때 앱이 사용 중인 것으로 간주됩니다. 예를 들어, 전경에서 활동이 실행 중입니다.

   >[!TIP]
   >
   >ACCESS_FINE_LOCATION 사용자 권한이 앱의 매니페스트 파일에 설정되어 있는지 확인합니다.

* `PlacesMonitorLocationPermission.ALWAYS_ALLOW`

   이 값은 응용 프로그램이 백그라운드로 설정된 경우에도 사용자에게 장치 위치에 액세스하라는 메시지를 표시합니다.

   >[!TIP]
   >
   >ACCESS_BACKGROUND_LOCATION 및 ACCESS_FINE_LOCATION 사용자 권한이 앱의 매니페스트 파일에 설정되어 있는지 확인합니다.

   `PlacesMonitorLocationPermission.ALWAYS_ALLOW` 는 기본 위치 권한 값입니다.

>[!IMPORTANT]
>
>앱 사용자에게 `WHILE_USING_APP` 권한이 부여되면 지오펜스는 운영 체제에 등록되지 않습니다. 따라서 위치 모니터 확장은 백그라운드에서 발생하는 지역에서 시작/종료 이벤트를 트리거하지 않습니다.

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```java
public static void setLocationPermission(final PlacesMonitorLocationPermission placesMonitorLocationPermission)
```

#### 예

권한을 요청하려면 `WHILE_USING_APP` :

```java
// set the location permission
PlacesMonitor.setLocationPermission(PlacesMonitorLocationPermission.WHILE_USING_APP);
// start monitoring
PlacesMonitor.start()
```

사용 권한으로 업그레이드하려면 `ALWAYS_ALLOW` 다음을 수행하십시오.

```java
// upgrade the permission level
PlacesMonitor.setLocationPermission(PlacesMonitorLocationPermission.ALWAYS_ALLOW);
```

### SetRequestAuthorizationLevel(iOS)

이 API 파섹

사용자에게 표시할 적절한 인증 프롬프트를 설정하려면 전화 걸기 `SetRequestAuthorizationLevel` 전에 전화하십시오 `[ACPPlacesMonitor start]`. 사용자에게 표시할 적절한 권한 부여 프롬프트를 설정하려면 JavaScript 앞에 이 API를 `[ACPPlacesMonitor start]`호출합니다. 능동적으로 모니터링하면서 이 방법을 호출하면 위치 인증 수준이 요청된 인증 값으로 업그레이드됩니다. 요청된 인증 수준이 이미 제공 또는 거부되었거나 응용 프로그램 사용자가 권한을 다운그레이드할 `ACPPlacesRequestAuthorizationLevelAlways` 때 이 `ACPPlacesRequestAuthorizationLevelWhenInUse` 방법은 적용되지 않습니다.

인증 수준은 다음 값 중 하나로 설정할 수 있습니다.

* `ACPPlacesRequestAuthorizationLevelWhenInUse`

   앱이 사용 중인 동안 위치 서비스를 사용할 수 있는 사용자의 권한을 요청합니다. 사용자 프롬프트에는 앱 Info.plist 파일의 `NSLocationWhenInUseUsageDescription` 키의 텍스트가 포함되며 이 메서드를 호출할 때는 키가 있어야 합니다. 자세한 내용은 requestWhenInUseAuthorization [에 대한 Apple 설명서를 참조하십시오](https://developer.apple.com/documentation/corelocation/cllocationmanager/1620562-requestwheninuseauthorization).

* `ACPPlacesRequestMonitorAuthorizationLevelAlways`

   앱이 백그라운드에 있을 때에도 위치 서비스를 요청하려면 이 열거형을 사용하십시오. 앱의 Info.plist에 `NSLocationAlwaysUsageDescription` 키와 `NSLocationWhenInUseUsageDescription` 키가 있어야 합니다. 이러한 키는 사용자 프롬프트 동안 표시되는 텍스트를 정의합니다. 자세한 내용은 requestAlwaysAuthorization에 [대한 Apple 설명서를 참조하십시오](https://developer.apple.com/documentation/corelocation/cllocationmanager/1620551-requestalwaysauthorization).

`ACPPlacesRequestAuthorizationLevelAlways` 는 기본 요청 인증 값입니다.

>[!IMPORTANT]
>
>사용 권한을 부여한 응용 프로그램은 백그라운드에서 발생하는 지역에서 시작/종료 이벤트를 트리거할 수 없습니다. `ACPPlacesRequestAuthorizationLevelWhenInUse`

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```objective-c
+ (void) setRequestAuthorizationLevel: (ACPPlacesRequestAuthorizationLevel) requestAuthorizationLevel;
```

#### 예

권한을 요청하려면 `ACPPlacesRequestAuthorizationLevelWhenInUse` :

```objective-c
// set the request authorization level
[ACPPlacesMonitor setRequestAuthorizationLevel: ACPPlacesRequestAuthorizationLevelWhenInUse];
// start monitoring
[ACPPlacesMonitor start];
```

인증으로 업그레이드하려면 다음을 `ACPPlacesRequestAuthorizationLevelAlways` 수행하십시오.

```objective-c
// set the request authorization level
[ACPPlacesMonitor setRequestAuthorizationLevel: ACPPlacesRequestAuthorizationLevelAlways];
```

## 모니터링 모드(iOS만 해당)

모니터링은 다음 값 중 하나로 설정할 수 있습니다.

* `ACPPlacesMonitorModeContinuous`

   모니터링 익스텐션은 위치를 보다 자주 수신하고 처리합니다. 이 모니터링 전략은 많은 전력을 소모하지만 정확도는 더 높습니다. 자세한 내용은 지속적인 모니터링에 [대한 Apple 설명서를 참조하십시오](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423750-startupdatinglocation).

* `ACPPlacesMonitorModeSignificantChanges`

   모니터링 확장 기능은 장치가 이전에 처리된 위치에서 상당히 먼 거리를 이동한 후에만 위치 업데이트를 받고 처리합니다. 이러한 모니터링 전략은 지속적인 모니터링 전략보다 적은 전력을 사용합니다. 자세한 내용은 중요한 [모니터링에 대한 Apple 설명서를 참조하십시오](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423531-startmonitoringsignificantlocati)

### SetPlacesMonitorMode(iOS)

다음은 이 API의 구문 및 예제 코드입니다.

#### 구문

```objective-c
+ (void) setPlacesMonitorMode: (ACPPlacesMonitorMode) monitorMode;
```

#### 예

```objective-c
[ACPPlacesMonitor setPlacesMonitorMode:ACPPlacesMonitorModeSignificantChanges];
```

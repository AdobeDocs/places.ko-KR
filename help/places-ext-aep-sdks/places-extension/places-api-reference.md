---
title: Places API 참조
description: 위치의 API 참조에 대한 정보입니다.
feature: Mobile SDK
exl-id: ce1a113c-dee0-49df-8d2f-789ccc1c8322
source-git-commit: f521d5e3b0b69977877d88382ce41fcb7d1c54b9
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 32%

---

# Places API 참조 {#places-api-reference}

다음은 위치 확장의 API 참조에 대한 정보입니다.

## 영역 이벤트 처리

장치가 앱의 사전 정의된 위치 서비스 지역 경계 중 하나를 넘으면 지역 및 이벤트 유형이 SDK에 전달되어 처리됩니다.

### ProcessGeofence(Android)

프로세스 a `Geofence` 제공된 에 대한 지역 이벤트 `transitionType`.

전달 `transitionType` 출처: `GeofencingEvent.getGeofenceTransition()`. 현재 `Geofence.GEOFENCE_TRANSITION_ENTER` 및 `Geofence.GEOFENCE_TRANSITION_EXIT` 이 지원됩니다.

**구문**

다음은 이 메서드에 대한 구문입니다.

```java
public static void processGeofence(final Geofence geofence, final int transitionType);
```

**예**

에서 이 메서드 호출 `IntentService` android geofence 이벤트 수신을 위해 등록됩니다.

다음은 이 메서드의 코드 샘플입니다.

```java
public class GeofenceTransitionsIntentService extends IntentService {

    public GeofenceTransitionsIntentService() {
        super("GeofenceTransitionsIntentService");
    }

    protected void onHandleIntent(Intent intent) {
        GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);

        List<Geofence> geofences = geofencingEvent.getTriggeringGeofences();

        if (geofences.size() > 0) {
          // Call the Places API to process information
          Places.processGeofence(geofences.get(0), geofencingEvent.getGeofenceTransition());
        }
    }
}
```

### ProcessRegionEvent(iOS)

이 메서드는 `CLLocationManager` 위임 - 사용자가 특정 영역을 입력했는지 또는 종료했는지 여부를 알려줍니다.

**구문**

다음은 이 메서드에 대한 구문입니다.

```objectivec
+ (void) processRegionEvent: (nonnull CLRegion*) region forRegionEventType: (ACPRegionEventType) eventType;
```

**예**

다음은 이 메서드의 코드 샘플입니다.


```objectivec
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```

### ProcessGeofencingEvent(Android)

모두 처리 `Geofences` 다음에서 `GeofencingEvent` 동시에.

**구문**

```java
public static void processGeofenceEvent(final GeofencingEvent geofencingEvent);
```

**예**

에서 이 메서드 호출 `IntentService` android geofence 이벤트 수신을 위해 등록됩니다.

```java
public class GeofenceTransitionsIntentService extends IntentService {

    public GeofenceTransitionsIntentService() {
        super("GeofenceTransitionsIntentService");
    }

    protected void onHandleIntent(Intent intent) {
        GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);
        // Call the Places API to process information
        Places.processGeofenceEvent(geofencingEvent);
    }
}
```

## 가까운 관심 영역 검색

콜백에서 주변 POI의 순서가 지정된 목록을 반환합니다. 이 메서드의 오버로드된 버전은 결과 네트워크 호출에 문제가 있는 경우 오류 코드를 반환합니다.

### GetNearbyPointsOfInterest(Android)

다음은 이 메서드에 대한 구문입니다.

**구문**

```java
public static void getNearbyPointsOfInterest(final Location location, final int limit,
                                             final AdobeCallback<List<PlacesPOI>> callback);

public static void getNearbyPointsOfInterest(final Location location, final int limit,
                                             final AdobeCallback<List<PlacesPOI>> callback,
                                             final AdobeCallback<PlacesRequestError> errorCallback);
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```java
// getNearbyPointsOfInterest without an error callback
Places.getNearbyPointsOfInterest(currentLocation, 10, new AdobeCallback<List<PlacesPOI>>() {
    @Override
    public void call(List<PlacesPOI> pois) {
        // do required processing with the returned nearbyPoi array
        startMonitoringPois(pois);
    }
});

// getNearbyPointsOfInterest with an error callback
Places.getNearbyPointsOfInterest(currentLocation, 10,
    new AdobeCallback<List<PlacesPOI>>() {
        @Override
        public void call(List<PlacesPOI> pois) {
            // do required processing with the returned nearbyPoi array
            startMonitoringPois(pois);
        }
    }, new AdobeCallback<PlacesRequestError>() {
        @Override
        public void call(PlacesRequestError placesRequestError) {
            // look for the placesRequestError and handle the error accordingly
            handleError(placesRequestError);
        }
    }
);
```

### GetNearbyPointsOfInterest(iOS)

**구문**

```objectivec
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback;

+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback
                     errorCallback: (nullable void (^) (ACPPlacesRequestError result)) errorCallback;
```

**예**

```objectivec
// getNearbyPointsOfInterest without an error callback
[ACPPlaces getNearbyPointsOfInterest:location
                               limit:10     
                            callback:^(NSArray<ACPPlacesPoi*>* nearbyPoi) {
    // do required processing with the returned nearbyPoi array
    [self startMonitoringPois:nearbyPOI];
}];

// getNearbyPointsOfInterest with an error callback
[ACPPlaces getNearbyPointsOfInterest:location limit:10
    callback:^(NSArray<ACPPlacesPoi *> * _Nullable nearbyPoi) {
        // do required processing with the returned nearbyPoi array
        [self startMonitoringPois:nearbyPOI];
    } errorCallback:^(ACPPlacesRequestError result) {
        // look for the error and handle accordingly
        [self handleError:result];
    }
];
```

## 현재 장치 관심 영역 검색

장치가 현재 있는 것으로 알려진 POI 목록을 요청하고 콜백에서 반환합니다.

### GetCurrentPointsOfInterest(Android)

다음은 이 메서드에 대한 구문입니다.

**구문**

```java
public static void getCurrentPointsOfInterest(final AdobeCallback<List<PlacesPOI>> callback);
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```java
Places.getCurrentPointsOfInterest(new AdobeCallback<List<PlacesPOI>>() {
    @Override
    public void call(List<PlacesPOI> pois) {
        // use the obtained POIs that the device is within
        processUserWithinPois(pois);        
    }
});
```

### GetCurrentPointsOfInterest(iOS)

**구문**

다음은 이 메서드에 대한 구문입니다.

```objectivec
+ (void) getCurrentPointsOfInterest: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable userWithinPoi)) callback;
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```objectivec
[ACPPlaces getCurrentPointsOfInterest:^(NSArray<ACPPlacesPoi*>* userWithinPoi) {
    // do required processing with the returned userWithinPoi array
    [self processUserWithinPois:userWithinPoi];
}];
```


## 장치 위치 가져오기

위치 확장에서 이전에 알려진 대로 디바이스의 위치를 요청합니다.

>[!TIP]
>
>위치 확장은 호출을 통해 제공된 위치에 대해서만 알고 있습니다. `GetNearbyPointsOfInterest`.


### GetLastKnownLocation(Android)

**구문**

다음은 이 메서드에 대한 구문입니다.

```java
public static void getLastKnownLocation(final AdobeCallback<Location> callback);
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```java
Places.getLastKnownLocation(new AdobeCallback<Location>() {
    @Override
    public void call(Location lastLocation) {
        // do something with the last known location
        processLastKnownLocation(lastLocation);        
    }
});
```

### GetLastKnownLocation(iOS)

**구문**

다음은 이 메서드에 대한 구문입니다.

```objectivec
+ (void) getLastKnownLocation: (nullable void (^) (CLLocation* _Nullable lastLocation)) callback;
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```objectivec
[ACPPlaces getLastKnownLocation:^(CLLocation* lastLocation) {
    // do something with the last known location
    [self processLastKnownLocation:lastLocation];
}];
```

## 클라이언트측 데이터 지우기


### 지우기(Android)

공유 상태, 로컬 저장소 및 인메모리에서 위치 확장에 대한 클라이언트측 데이터를 지웁니다.

**구문**

다음은 이 메서드에 대한 구문입니다.

```java
public static void clear();
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```java
Places.clear();
```

### 지우기(iOS)

공유 상태, 로컬 저장소 및 메모리 내 Places 확장에 대한 클라이언트측 데이터를 지웁니다.

**구문**

다음은 이 메서드에 대한 구문입니다.

```objectivec
+ (void) clear;
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```objectivec
[ACPPlaces clear];
```

## 위치 인증 상태 설정

### setAuthorizationStatus(Android)

*Places v1.4.0부터 사용 가능*

Places 확장에서 인증 상태를 설정합니다.

제공된 상태는 위치 공유 상태에 저장되며 참조용으로만 사용됩니다.
이 메서드를 호출해도 이 장치의 실제 위치 인증 상태는 영향을 받지 않습니다.

**구문**

다음은 이 메서드에 대한 구문입니다.

```java
public static void setAuthorizationStatus(final PlacesAuthorizationStatus status);
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```java
Places.setAuthorizationStatus(PlacesAuthorizationStatus.ALWAYS);
```

### setAuthorizationStatus(iOS)

*ACPPlaces v1.3.0부터 사용 가능*

Places 확장에서 인증 상태를 설정합니다.

제공된 상태는 위치 공유 상태에 저장되며 참조용으로만 사용됩니다.
이 메서드를 호출해도 이 장치의 실제 위치 인증 상태는 영향을 받지 않습니다.

장치 인증 상태가 변경되면 `locationManager:didChangeAuthorizationStatus:` 의 방법 `CLLocationManagerDelegate` 이 호출됩니다. 이 메서드 내에서 새 `CLAuthorizationStatus` ACPPlace 값 `setAuthorizationStatus:` API.

**구문**

다음은 이 메서드에 대한 구문입니다.

```objectivec
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```

**예**

다음은 이 메서드의 코드 샘플입니다.

```objectivec
- (void) locationManager: (CLLocationManager*) manager didChangeAuthorizationStatus: (CLAuthorizationStatus) status {    
    [ACPPlaces setAuthorizationStatus:status];
}
```

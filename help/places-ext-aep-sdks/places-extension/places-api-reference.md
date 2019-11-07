---
title: API 참조 배치
seo-title: API 참조 배치
description: 장소의 API 참조에 대한 정보입니다.
seo-description: 장소의 API 참조에 대한 정보입니다.
translation-type: tm+mt
source-git-commit: 69173bdbd1a69ae1b75ba70e775a4603d1f1b8fc

---


# API 참조 배치 {#places-api-reference}

다음은 장소의 API 참조에 대한 정보입니다.

## 영역 이벤트 처리

장치가 앱의 사전 정의된 위치 영역 경계 중 하나를 교차할 때, 지역과 이벤트 유형이 처리를 위해 SDK로 전달됩니다.

### ProcessGeofence(Android)

제공된 `Geofence` 지역 이벤트를 처리합니다 `transitionType`.

에서 `transitionType` 전달 `GeofencingEvent.getGeofenceTransition()`. 현재 `Geofence.GEOFENCE_TRANSITION_ENTER` 및 `Geofence.GEOFENCE_TRANSITION_EXIT` 지원됩니다.

**구문**

다음은 이 메서드에 대한 구문입니다.

```java
public static void processGeofence(final Geofence geofence, final int transitionType);
```

**예**

이 메서드는 Android geofence 이벤트 수신을 위해 `IntentService` 등록된 사용자 컴퓨터에서 호출합니다.

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

이 메서드는 `CLLocationManager` 대리자에서 호출해야 하며, 이는 사용자가 특정 영역을 입력하거나 종료했는지 여부를 나타냅니다.

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

동시에 모든 `Geofences` 작업을 `GeofencingEvent` 처리할 수 있습니다.

**구문**

```java
public static void processGeofenceEvent(final GeofencingEvent geofencingEvent);
```

**예**

Android geofence 이벤트 수신을 위해 등록된 `IntentService` 앱에서 이 메서드를 호출합니다.

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

콜백에서 주변 POI의 순서가 지정된 목록을 반환합니다. 이 메서드의 오버로드된 버전은 결과 네트워크 호출에 문제가 발생하면 오류 코드를 반환합니다.

### GetNearlyPointsOfInterest(Android)

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

### GetNearlyPointsOfInterest(iOS)

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

## 현재 관심 장치 지점 검색

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


## 장치의 위치 가져오기

장치 위치를 위치 확장명으로 요청합니다.

>[!TIP]
>
>위치 확장 기능은 호출을 통해 제공된 위치만 알고 `GetNearbyPointsOfInterest`있습니다.


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

공유 상태, 로컬 저장소 및 메모리 내 위치에 대한 클라이언트측 데이터를 지웁니다.

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

### clear(iOS)

공유 상태, 로컬 저장소 및 메모리 내 위치에 대한 클라이언트측 데이터를 지웁니다.

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

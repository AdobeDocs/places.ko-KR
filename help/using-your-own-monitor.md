---
title: 자체 모니터 사용
description: 또한 Places Service 확장 API를 사용하여 모니터링 서비스를 사용하고 Places Service와 통합할 수도 있습니다.
exl-id: 8ca4d19b-0f23-4291-b335-af47f03179fa
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 자체 모니터 사용 {#using-your-monitor}

또한 Places 확장 API를 사용하여 모니터링 서비스를 사용하고 Places Service와 통합할 수도 있습니다.

## 지오펜스 등록

모니터링 서비스를 사용하려는 경우 다음 단계를 완료하여 현재 위치 주변에 있는 POI의 위치를 등록하십시오.

### iOS

iOS에서 다음 단계를 완료합니다.

1. iOS의 핵심 위치 서비스에서 가져온 위치 업데이트를 위치 확장에 전달합니다.

1. `getNearbyPointsOfInterest` 위치 확장 API를 사용하여 현재 위치 주변의 `ACPPlacesPoi` 개체 배열을 가져옵니다.

   ```objective-c
   - (void) locationManager: (CLLocationManager*) manager didUpdateLocations: (NSArray<CLLocation*>*) locations {
       [ACPPlaces getNearbyPointsOfInterest:currentLocation limit:10 callback: ^ (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi) {
           [self startMonitoringGeoFences:nearbyPoi];
       }];
   }
   ```

1. 획득한 `ACPPlacesPOI`개의 개체에서 정보를 추출하고 해당 POI를 모니터링하기 시작합니다.

   ```objective-c
   - (void) startMonitoringGeoFences: (NSArray*) newGeoFences {
       // verify if the device supports monitoring geofences
       // check for location permission
   
       for (ACPPlacesPoi * currentRegion in newGeoFences) {
           // make the circular region
           CLLocationCoordinate2D center = CLLocationCoordinate2DMake(currentRegion.latitude, currentRegion.longitude);
           CLCircularRegion* currentCLRegion = [[CLCircularRegion alloc] initWithCenter:center
                                                                                 radius:currentRegion.radius
                                                                             identifier:currentRegion.identifier];
           currentCLRegion.notifyOnExit = YES;
           currentCLRegion.notifyOnEntry = YES;
   
           // start monitoring the new region
           [_locationManager startMonitoringForRegion:currentCLRegion];
       }
   }
   ```

### Android

1. Google Play 서비스 또는 Android 위치 서비스에서 얻은 위치 업데이트를 위치 확장에 전달합니다.

1. `getNearbyPointsOfInterest` 위치 확장 API를 사용하여 현재 위치 주변의 `PlacesPoi` 개체 목록을 가져옵니다.

   ```java
   LocationCallback callback = new LocationCallback() {
       @Override
       public void onLocationResult(LocationResult locationResult) {
           super.onLocationResult(locationResult);
   
           Places.getNearbyPointsOfInterest(currentLocation, 10, new AdobeCallback<List<PlacesPOI>>() {
               @Override
               public void call(List<PlacesPOI> pois) {
                   starMonitoringGeofence(pois);
               }
           });
       }
   };
   ```

1. 획득한 `PlacesPOI`개의 개체에서 데이터를 추출하고 해당 POI를 모니터링하기 시작합니다.

   ```java
   private void startMonitoringFences(final List<PlacesPOI> nearByPOIs) {
       // check for location permission
       for (PlacesPOI poi : nearByPOIs) {
           final Geofence fence = new Geofence.Builder()
               .setRequestId(poi.getIdentifier())
               .setCircularRegion(poi.getLatitude(), poi.getLongitude(), poi.getRadius())
               .setExpirationDuration(Geofence.NEVER_EXPIRE)
               .setTransitionTypes(Geofence.GEOFENCE_TRANSITION_ENTER |
                                   Geofence.GEOFENCE_TRANSITION_EXIT)
               .build();
           geofences.add(fence);
       }
   
       GeofencingRequest.Builder builder = new GeofencingRequest.Builder();
       builder.setInitialTrigger(GeofencingRequest.INITIAL_TRIGGER_ENTER);
       builder.addGeofences(geofences);
       builder.build();
       geofencingClient.addGeofences(builder.build(), geoFencePendingIntent)
   }
   ```


`getNearbyPointsOfInterest` API를 호출하면 현재 위치 주변의 위치를 가져오는 네트워크 호출이 발생합니다.

>[!IMPORTANT]
>
>사용자의 중대한 위치 변경이 있는 경우에만 또는 제한적으로 API를 호출해야 합니다.

## Geofence 이벤트 게시

### iOS

iOS에서 `CLLocationManager` 대리자의 `processGeofenceEvent` Places API를 호출합니다. 이 API는 사용자가 특정 지역을 입력 또는 종료했는지 여부를 알려줍니다.

```objective-c
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```

### Android

Android에서 Geofence 브로드캐스트 수신기에서 적절한 전환 이벤트와 함께 `processGeofence` 메서드를 호출합니다. 중복 시작/종료를 방지하기 위해 받은 지오펜스 목록을 조정할 수 있습니다.

```java
void onGeofenceReceived(final Intent intent) {
    // do appropriate validation steps for the intent
    ...

    // get GeofencingEvent from intent
    GeofencingEvent geoEvent = GeofencingEvent.fromIntent(intent);

    // get the transition type (entry or exit)
    int transitionType = geoEvent.getGeofenceTransition();

    // validate your geoEvent and get the necessary Geofences from the list
    List<Geofence> myGeofences = geoEvent.getTriggeringGeofences();

    // process region events for your geofences
    for (Geofence geofence : myGeofences) {
        Places.processGeofence(geofence, transitionType);
    }
}
```

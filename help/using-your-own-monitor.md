---
title: 자체 모니터 사용
seo-title: 자체 모니터 사용
description: '또한 Places 확장 API를 사용하여 모니터링 서비스를 사용하고 위치와 통합할 수 있습니다. '
seo-description: '또한 Places 확장 API를 사용하여 모니터링 서비스를 사용하고 위치와 통합할 수 있습니다. '
translation-type: tm+mt
source-git-commit: 5d558755d816f4aa05a7a76cad12bab45c1dc282

---


# 자체 모니터 사용 {#using-your-monitor}

또한 Places 확장 API를 사용하여 모니터링 서비스를 사용하고 위치와 통합할 수 있습니다.

## 등록 위치

모니터링 서비스를 사용하려는 경우 다음 단계를 완료하여 현재 위치에 POI의 위치를 등록합니다.

### iOS

iOS에서 다음 단계를 완료하십시오.

1. iOS의 핵심 위치 서비스에서 얻은 위치 업데이트를 위치 확장 프로그램으로 전달합니다.

2. 위치 `getNearbyPointsOfInterest` 확장 API를 사용하여 현재 위치 주위의 *n* 개체 배열을 `ACPPlacesPoi` 가져옵니다.

   ```objective-c
   - (void) locationManager: (CLLocationManager*) manager didUpdateLocations: (NSArray<CLLocation*>*) locations {
   
          [ACPPlaces getNearbyPointsOfInterest:currentLocation limit:10 callback: ^ (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi) {
              [self startMonitoringGeoFences:nearbyPoi];
      }];
   
   }
   ```

3. 가져온 `ACPPlacesPOI` 개체에서 정보를 추출하고 해당 POI를 모니터링합니다.

   ```objective-c
   - (void) startMonitoringGeoFences: (NSArray*) newGeoFences {
       // verify if the device supports monitoring geofences
       // check for location permission
   
       for (ACPPlacesPoi * currentRegion in newGeoFences) {
           // make the circular region
           CLLocationCoordinate2D center = CLLocationCoordinate2DMake(currentRegion.latitude, currentRegion.longitude);
           CLCircularRegion* currentCLRegion = [[CLCircularRegion alloc] initWithCenter:center                                                                                                                              radius:currentRegion.radius                                                                                                                    identifier:currentRegion.identifier];
           currentCLRegion.notifyOnExit = YES;
           currentCLRegion.notifyOnEntry = YES;
   
           // start monitoring the new region
           [_locationManager startMonitoringForRegion:currentCLRegion];
   
       }
   }
   ```

### Android

1. Google Play 서비스 또는 Android 위치 서비스에서 얻은 위치 업데이트를 위치 확장 프로그램으로 전달합니다.

2. Places `getNearbyPointsOfInterest` Extension API를 사용하여 현재 위치 주위의 `PlacesPoi` 개체 목록을 가져옵니다.

   ```java
       LocationCallback callback = new LocationCallback() {
               @Override
               public void onLocationResult(LocationResult locationResult) {
                   super.onLocationResult(locationResult);
   
                   Places.getNearbyPointsOfInterest(currentLocation, 10, new            AdobeCallback<List<PlacesPOI>>() {
               @Override
               public void call(List<PlacesPOI> pois)
                   starMonitoringGeofence(pois);
               }
           });
   
               }
           };
   ```

3. 가져온 `PlacesPOI` 개체에서 데이터를 추출하고 해당 POI를 모니터링합니다.

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


API를 `getNearbyPointsOfInterest` 호출하면 현재 위치 주위의 위치를 가져오는 네트워크 호출이 발생합니다.

>[!IMPORTANT]
>
>API는 제한적으로 호출해야 하며 사용자의 위치가 상당히 변경된 경우에만 호출해야 합니다.

## 위치 이벤트 게시

### iOS

iOS에서 대리자의 `processGeofenceEvent` 위치 API를 `CLLocationManager` 호출합니다. 이 API 파섹

```objective-c
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```
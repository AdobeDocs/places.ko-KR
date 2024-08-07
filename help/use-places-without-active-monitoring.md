---
title: 활성 지역 모니터링 없이 장소 서비스 사용
description: 이 섹션에서는 활성 지역 모니터링 없이 Places Service를 사용하는 방법에 대해 설명합니다.
exl-id: 0ba7949a-447e-4754-9b45-945e58e29541
source-git-commit: 33cbef9b3226be3f013fe82d619b82e093a9752a
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 활성 지역 모니터링 없이 장소 서비스 사용 {#use-places-without-active-monitoring}

응용 프로그램에 대한 사용 사례는 활성 지역 모니터링이 필요하지 않을 수 있습니다. Places Service를 사용하여 사용자의 위치 데이터를 다른 Experience Platform 제품과 통합할 수 있습니다.

## 사전 요구 사항

개발자는 대상 플랫폼의 운영 체제에서 제공하는 API를 사용하여 장치의 위치를 수집합니다.

>[!TIP]
>
>앱의 사용 사례에 활성 지역 모니터링이 필요한 경우 [자체 모니터링 솔루션으로 장소 서비스 사용](/help/using-your-own-monitor.md)을 참조하세요.

활성 지역 모니터링 없이 위치 서비스를 사용하려면

## 1. 사용자의 위치 수집

앱 개발자는 `CoreLocation.framework`(iOS) 또는 Google Play 서비스(Android)에서 제공하는 `Location` API를 사용하여 장치의 현재 위치를 수집해야 합니다.

자세한 내용은 다음 설명서를 참조하십시오.

- [CoreLocation](https://developer.apple.com/documentation/corelocation)(Apple)
- Google Play 서비스의 [위치 API](https://developer.android.com/training/location)(Google)

## 2. SDK에서 가까운 관심 영역 가져오기

사용자의 위치를 가져온 후 SDK에 전달하여 근처 POI 목록을 다시 가져올 수 있습니다.

### Android

다음은 [`BroadcastReceiver`](https://codelabs.developers.google.com/codelabs/background-location-updates-android-o/index.html?index=..%2Findex#5)을(를) 사용하는 Android의 샘플 구현입니다.

```java
public class LocationBroadcastReceiver extends BroadcastReceiver {
    static final String ACTION_LOCATION_UPDATE = "locationUpdate";
    @Override
    public void onReceive(Context context, Intent intent) {
        if (intent == null || context == null) {
            return;
        }

        final String action = intent.getAction();
        if (!ACTION_LOCATION_UPDATE.equals(action)) {
            return;
        }

        LocationResult result = LocationResult.extractResult(intent);
        if (result == null) {
            return;
        }

        Location currentLocation = result.getLastLocation();
        if (currentLocation == null) {
            return;
        }

        // ask the Places SDK for the 10 nearest Points of Interest based on the user's location
        Places.getNearbyPointsOfInterest(currentLocation, 10,
            new AdobeCallback<List<PlacesPOI>>() {
                @Override
                public void call(List<PlacesPOI> pois) {
                    // pois is the 10 nearest POIs based on the location
                }
            }, new AdobeCallback<PlacesRequestError>() {
                @Override
                public void call(PlacesRequestError placesRequestError) {
                    // Look for the placesRequestError and handle the error accordingly
                }
            }
        );
    }
}
```

### Objective-C

다음은 iOS에 대한 샘플 구현입니다. 이 코드는 [`CLLocationManagerDelegate`](https://developer.apple.com/documentation/corelocation/cllocationmanager?language=objc)에서 [`locationManager:didUpdateLocations:`](https://developer.apple.com/documentation/corelocation/cllocationmanagerdelegate/1423615-locationmanager?language=objc) 메서드의 구현을 보여 줍니다.

```objectivec
- (void) locationManager:(CLLocationManager*)manager didUpdateLocations:(NSArray<CLLocation*>*)locations {
    // ask the Places SDK for the 10 nearest Points of Interest based on the user's location
    [ACPPlaces getNearbyPointsOfInterest:[locations lastObject] limit:10 callback:^(NSArray<ACPPlacesPoi *> * _Nullable nearbyPoi) {
        // nearbyPoi is the 10 nearest POIs based on the location
    } errorCallback:^(ACPPlacesRequestError result) {
        // log the error if we got one
        NSLog(@"error: %lu", (unsigned long)result);
    }];
}
```

### Swift

다음은 iOS에 대한 샘플 구현입니다. 이 코드는 [`CLLocationManagerDelegate`](https://developer.apple.com/documentation/corelocation/cllocationmanager)에서 [`locationManager(_:didUpdateLocations:)`](https://developer.apple.com/documentation/corelocation/cllocationmanagerdelegate/1423615-locationmanager) 메서드의 구현을 보여 줍니다.

```swift
func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
    // ask the Places SDK for the 10 nearest Points of Interest based on the user's location
    ACPPlaces.getNearbyPoints(ofInterest: locations.last!, limit: 10, callback: { (nearbyPoi) in
        // nearbyPoi is the 10 nearest POIs based on the location
    }) { (error) in
        // log the error if we have one
        print("error: \(error)")
    }
}
```

## 3. Analytics 요청에 위치 데이터 첨부

위치 SDK는 `getNearbyPointsOfInterest` API를 호출하여 장치에 관련된 모든 POI 데이터를 Launch의 데이터 요소를 통해 사용할 수 있도록 합니다. [데이터 첨부](https://aep-sdks.gitbook.io/docs/resources/user-guides/attach-data) 규칙을 사용하면 위치 데이터를 향후 Analytics 요청에 자동으로 추가할 수 있습니다. 이렇게 하면 디바이스 위치가 수집될 때 Analytics에 대한 일회성 호출이 필요 없습니다.

이 항목에 대한 자세한 내용은 [Analytics 요청에 위치 컨텍스트 추가](use-places-with-other-solutions/places-adobe-analytics/run-reports-aa-places-data.md)를 참조하십시오.

## 선택 사항 - 사용자가 POI에 있을 때 항목 이벤트를 트리거합니다.

>[!TIP]
>
>위치 데이터를 캡처하는 권장 방법은 [Analytics 요청에 위치 데이터를 첨부](#attach-places-data-to-your-analytics-requests)하는 것입니다.
>
>사용 사례에서 SDK에 의해 [지역 항목 이벤트](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent)를 트리거해야 하는 경우 아래 설명된 대로 수동으로 수행해야 합니다.

`getNearbyPointsOfInterest` API에서 반환된 목록에 사용자가 현재 POI 내에 있는지 나타내는 [사용자 지정 개체](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#additional-classes-and-enums)가 포함되어 있습니다. 사용자가 POI에 있는 경우 SDK에서 해당 지역에 대한 시작 이벤트를 트리거하도록 할 수 있습니다.

>[!IMPORTANT]
>
>앱이 한 번의 방문에서 여러 시작 이벤트를 트리거하지 않도록 하려면 사용자가 입력한 것을 알고 있는 영역 목록을 유지합니다. SDK에서 인근 POI의 응답을 처리할 때, 지역이 목록에 없는 경우에만 시작 이벤트를 트리거합니다.
>
>다음 코드 샘플에서는 `NSUserDefaults`(iOS) 및 `SharedPreferences`(Android)을 사용하여 지역 목록을 관리합니다.

### Android

다음 코드 샘플은 `getNearbyPointsOfInterest`, `List<PlacesPOI>`의 콜백에서 제공된 결과를 처리하는 방법을 보여 줍니다.

```java
void handleUpdatedPOIs(final List<PlacesPOI> nearbyPois) {
    // get the list of regions we know the user is already within from SharedPreferences
    SharedPreferences preferences = getApplicationContext().getSharedPreferences("places", 0);
    Set<String> regionsUserIsAlreadyIn = preferences.getStringSet("regionsUserIsAlreadyIn", new HashSet<String>());

    // loop through new placesPOIS and post entry events for pois that aren't already in our list
    // also create the new list of regions that the user is in
    Set<String> updatedRegionsUserIsIn = new HashSet<String>();
    for (PlacesPOI poi : nearbyPois) {
        // check if the user is in this poi
        if (poi.containsUser()) {
            // the user is in the poi, now we need to make sure we haven't already recorded this entry event
            if (!regionsUserIsAlreadyIn.contains(poi.getIdentifier())) {
                Geofence poiGeofence = new Geofence.Builder()
                    .setRequestId(poi.getIdentifier())
                    .setTransitionTypes(Geofence.GEOFENCE_TRANSITION_ENTER)
                    .setCircularRegion(poi.getLatitude(), poi.getLongitude(), poi.getRadius())
                    .setExpirationDuration(Geofence.NEVER_EXPIRE)
                    .build();
                Places.processGeofence(poiGeofence, Geofence.GEOFENCE_TRANSITION_ENTER);
            }

            // add the region to our new list of regions
            updatedRegionsUserIsIn.add(poi.getIdentifier());
        }
    }

    // update SharedPreferences with our new list of regions
    SharedPreferences.Editor editor = getApplicationContext().getSharedPreferences("places", 0).edit();
    editor.putStringSet("regionsUserIsAlreadyIn", updatedRegionsUserIsIn).apply();
}
```

### Objective-C

다음 코드 샘플은 `getNearbyPointsOfInterest:limit:callback:errorCallback:`, `NSArray<ACPPlacesPoi *> *`의 콜백에서 제공된 결과를 처리하는 방법을 보여 줍니다.

```objectivec
- (void) handleUpdatedPOIs:(NSArray<ACPPlacesPoi *> *)nearbyPois {
   // get the list of regions we know the user is already within from user defaults
   NSArray *regionsUserIsCurrentlyWithin = [[NSUserDefaults standardUserDefaults]
                                            arrayForKey:@"regionsUserIsAlreadyIn"];

   // loop through new nearbyPoi and post entry events for pois that aren't already in our list
   // also creating the new list of known regions that the user is in
   NSMutableArray *updatedRegionsUserIsCurrentlyWithin = [@[] mutableCopy];
   for (ACPPlacesPoi *poi in nearbyPois) {
       // check if the user is in this poi
       if (poi.userIsWithin) {
           // the user is in the poi, now we need to make sure we haven't already recorded the entry event
           if (![regionsUserIsCurrentlyWithin containsObject:poi.identifier]) {
               CLCircularRegion *region = [[CLCircularRegion alloc] initWithCenter:CLLocationCoordinate2DMake(poi.latitude, poi.longitude)
                                                                            radius:poi.radius
                                                                        identifier:poi.identifier];
               [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
           }

           // add the region to our updated list
           [updatedRegionsUserIsCurrentlyWithin addObject:poi.identifier];
       }
   }

   // update user defaults with the new list
   [[NSUserDefaults standardUserDefaults] setObject:updatedRegionsUserIsCurrentlyWithin forKey:@"regionsUserIsAlreadyIn"];
}
```

### Swift

다음 코드 샘플은 `getNearbyPoints(_ ofInterest: CLLocation, limit: UInt, callback: (([ACPPlacesPoi]?) -> Void)?, errorCallback: ((ACPPlacesRequestError) -> Void)?)`, `[ACPPlacesPoi]`의 콜백에서 제공된 결과를 처리하는 방법을 보여 줍니다.

```swift
func handleUpdatedPOIs(_ nearbyPois:[ACPPlacesPoi]) {
    // get the list of regions we know the user is already within from user defaults
    let regionsUserIsCurrentlyWithin : [String] = UserDefaults.standard.array(forKey: "regionsUserIsAlreadyIn") as! [String]

    // loop through new nearbyPoi and post entry events for pois that aren't already in our list
    // also creating the new list of known regions that the user is in
    var updatedRegionsUserIsCurrentlyWithin: [String] = []
    for poi in nearbyPois {
        // check if the user is in this poi
        if poi.userIsWithin {
            // the user is in the poi, now we need to make sure we haven't already recorded the entry event
            if !regionsUserIsCurrentlyWithin.contains(poi.identifier!) {
                let region = CLCircularRegion.init(center: CLLocationCoordinate2D.init(latitude: poi.latitude, longitude: poi.longitude), radius: CLLocationDistance(poi.radius), identifier: poi.identifier!)
                ACPPlaces.processRegionEvent(region, for: .entry)
            }

            // add the region to our updated list
            updatedRegionsUserIsCurrentlyWithin.append(poi.identifier!)
        }
    }

    // update user defaults with the new list
    UserDefaults.standard.set(updatedRegionsUserIsCurrentlyWithin, forKey: "regionsUserIsAlreadyIn")
}
```

## 전체 샘플 구현

아래 코드 샘플은 장치의 현재 위치를 검색하고, 필요한 항목 이벤트를 트리거하고, 한 번의 방문으로 동일한 위치에 대해 여러 항목을 가져오지 않도록 하는 방법을 보여 줍니다.

이 코드 샘플에는 사용자가 POI에 있을 때 [시작 이벤트를 트리거하는](#trigger-entry-events-when-the-user-is-in-a-poi) 선택적 단계가 포함되어 있습니다.

>[!IMPORTANT]
>
>이러한 스니펫은 **전용**&#x200B;예입니다. 개발자는 기능을 구현하는 방법을 결정해야 하며, 이 결정에서는 대상 운영 체제에서 권장하는 우수 사례를 고려해야 합니다.

### Android

```java
public class LocationBroadcastReceiver extends BroadcastReceiver {
    static final String ACTION_LOCATION_UPDATE = "locationUpdate";
    @Override
    public void onReceive(Context context, Intent intent) {
        if (intent == null || context == null) {
            return;
        }

        final String action = intent.getAction();
        if (!ACTION_LOCATION_UPDATE.equals(action)) {
            return;
        }

        LocationResult result = LocationResult.extractResult(intent);
        if (result == null) {
            return;
        }

        Location currentLocation = result.getLastLocation();
        if (currentLocation == null) {
            return;
        }

        // ask the Places SDK for the 10 nearest Points of Interest based on the user's location
        Places.getNearbyPointsOfInterest(currentLocation, 10,
            new AdobeCallback<List<PlacesPOI>>() {
                @Override
                public void call(List<PlacesPOI> pois) {
                    // pois is the 10 nearest POIs based on the location
                    handleUpdatedPOIs(pois);
                }
            }, new AdobeCallback<PlacesRequestError>() {
                @Override
                public void call(PlacesRequestError placesRequestError) {
                    // Look for the placesRequestError and handle the error accordingly
                }
            }
        );
    }

    void handleUpdatedPOIs(final List<PlacesPOI> nearbyPois) {
        // get the list of regions we know the user is already within from SharedPreferences
        SharedPreferences preferences = getApplicationContext().getSharedPreferences("places", 0);
        Set<String> regionsUserIsAlreadyIn = preferences.getStringSet("regionsUserIsAlreadyIn", new HashSet<String>());

        // loop through new placesPOIS and post entry events for pois that aren't already in our list
        // also create the new list of regions that the user is in
        Set<String> updatedRegionsUserIsIn = new HashSet<String>();
        for (PlacesPOI poi : nearbyPois) {
            // check if the user is in this poi
            if (poi.containsUser()) {
                // the user is in the poi, now we need to make sure we haven't already recorded this entry event
                if (!regionsUserIsAlreadyIn.contains(poi.getIdentifier())) {
                    Geofence poiGeofence = new Geofence.Builder()
                        .setRequestId(poi.getIdentifier())
                        .setTransitionTypes(Geofence.GEOFENCE_TRANSITION_ENTER)
                        .setCircularRegion(poi.getLatitude(), poi.getLongitude(), poi.getRadius())
                        .setExpirationDuration(Geofence.NEVER_EXPIRE)
                        .build();
                    Places.processGeofence(poiGeofence, Geofence.GEOFENCE_TRANSITION_ENTER);
                }

                // add the region to our new list of regions
                updatedRegionsUserIsIn.add(poi.getIdentifier());
            }
        }

        // update SharedPreferences with our new list of regions
        SharedPreferences.Editor editor = getApplicationContext().getSharedPreferences("places", 0).edit();
        editor.putStringSet("regionsUserIsAlreadyIn", updatedRegionsUserIsIn).apply();
    }
}
```


### Objective-C

```objectivec
- (void) locationManager:(CLLocationManager*)manager didUpdateLocations:(NSArray<CLLocation*>*)locations {
    // ask the Places SDK for the 10 nearest Points of Interest based on the user's location
    [ACPPlaces getNearbyPointsOfInterest:[locations lastObject] limit:10 callback:^(NSArray<ACPPlacesPoi *> * _Nullable nearbyPoi) {
        // nearbyPoi is the 10 nearest POIs based on the location
        [self handleUpdatedPOIs:nearbyPoi];
    } errorCallback:^(ACPPlacesRequestError result) {
        // log the error if we got one
        NSLog(@"error: %lu", (unsigned long)result);
    }];
}

- (void) handleUpdatedPOIs:(NSArray<ACPPlacesPoi *> *)nearbyPois {
   // get the list of regions we know the user is already within from user defaults
   NSArray *regionsUserIsCurrentlyWithin = [[NSUserDefaults standardUserDefaults]
                                            arrayForKey:@"regionsUserIsAlreadyIn"];

   // loop through new nearbyPoi and post entry events for pois that aren't already in our list
   // also creating the new list of known regions that the user is in
   NSMutableArray *updatedRegionsUserIsCurrentlyWithin = [@[] mutableCopy];
   for (ACPPlacesPoi *poi in nearbyPois) {
       // check if the user is in this poi
       if (poi.userIsWithin) {
           // the user is in the poi, now we need to make sure we haven't already recorded the entry event
           if (![regionsUserIsCurrentlyWithin containsObject:poi.identifier]) {
               CLCircularRegion *region = [[CLCircularRegion alloc] initWithCenter:CLLocationCoordinate2DMake(poi.latitude, poi.longitude)
                                                                            radius:poi.radius
                                                                        identifier:poi.identifier];
               [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
           }

           // add the region to our updated list
           [updatedRegionsUserIsCurrentlyWithin addObject:poi.identifier];
       }
   }

   // update user defaults with the new list
   [[NSUserDefaults standardUserDefaults] setObject:updatedRegionsUserIsCurrentlyWithin forKey:@"regionsUserIsAlreadyIn"];
}
```

### Swift

```swift
func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
    // ask the Places SDK for the 10 nearest Points of Interest based on the user's location
    ACPPlaces.getNearbyPoints(ofInterest: locations.last!, limit: 10, callback: { (nearbyPoi) in
        // nearbyPoi is the 10 nearest POIs based on the location
        self.handleUpdatedPOIs(nearbyPoi!)
    }) { (error) in
        // log the error if we have one
        print("error: \(error)")
    }
}

func handleUpdatedPOIs(_ nearbyPois:[ACPPlacesPoi]) {
    // get the list of regions we know the user is already within from user defaults
    let regionsUserIsCurrentlyWithin : [String] = UserDefaults.standard.array(forKey: "regionsUserIsAlreadyIn") as! [String]

    // loop through new nearbyPoi and post entry events for pois that aren't already in our list
    // also creating the new list of known regions that the user is in
    var updatedRegionsUserIsCurrentlyWithin: [String] = []
    for poi in nearbyPois {
        // check if the user is in this poi
        if poi.userIsWithin {
            // the user is in the poi, now we need to make sure we haven't already recorded the entry event
            if !regionsUserIsCurrentlyWithin.contains(poi.identifier!) {
                let region = CLCircularRegion.init(center: CLLocationCoordinate2D.init(latitude: poi.latitude, longitude: poi.longitude), radius: CLLocationDistance(poi.radius), identifier: poi.identifier!)
                ACPPlaces.processRegionEvent(region, for: .entry)
            }

            // add the region to our updated list
            updatedRegionsUserIsCurrentlyWithin.append(poi.identifier!)
        }
    }

    // update user defaults with the new list
    UserDefaults.standard.set(updatedRegionsUserIsCurrentlyWithin, forKey: "regionsUserIsAlreadyIn")
}
```

SDK에서 위치 서비스 시작 이벤트를 트리거하는 것 외에도, 트리거하는 시작 이벤트로 인해 POI를 정의하는 모든 데이터를 Experience Platform Launch의 `data elements`을(를) 통해 나머지 SDK에서 사용할 수 있습니다. Experience Platform Launch `rules`을(를) 사용하면 SDK에서 처리하는 들어오는 이벤트에 Places Service 데이터를 동적으로 연결할 수 있습니다. 예를 들어 사용자가 있는 POI의 메타데이터를 첨부하고 데이터를 Analytics에 컨텍스트 데이터로 보낼 수 있습니다.

자세한 내용은 [다른 Adobe 솔루션에서 Places Service 사용](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-analytics-overview.md)을 참조하세요.

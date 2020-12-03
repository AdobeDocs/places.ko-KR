---
title: 활성 지역 모니터링 없이 위치 서비스 사용
description: 이 섹션에서는 활성 지역 모니터링 없이 위치 서비스를 사용하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 5846577f10eb1d570465ad7f888feba6dd958ec9
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---


# 활성 지역 모니터링 없이 위치 서비스 사용 {#use-places-without-active-monitoring}

응용 프로그램에 대한 사용 사례는 활성 지역 모니터링이 필요하지 않을 수 있습니다. 장소 서비스를 사용하여 사용자의 위치 데이터를 다른 Experience Platform 제품과 통합할 수 있습니다.

## 전제 조건

개발자는 대상 플랫폼의 운영 체제에서 제공하는 API를 사용하여 장치의 위치를 수집합니다.

>[!TIP]
>
>앱의 사용 사례에 활성 지역 모니터링이 필요한 경우 위치 모니터 확장 [사용을 참조하십시오](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

활성 지역 모니터링 없이 위치 서비스를 사용하려면

## 1. 사용자의 위치 수집

앱 개발자는 Google Play 서비스(Android)에서 제공하는 `CoreLocation.framework` (iOS) 또는 `Location` API를 사용하여 장치의 현재 위치를 수집해야 합니다.

자세한 내용은 다음 문서를 참조하십시오.

- [CoreLocation](https://developer.apple.com/documentation/corelocation) (Apple)
- [Google Play Services의 위치](https://developer.android.com/training/location) API(Google)

## 2. SDK에서 가까운 관심 영역 검색

사용자의 위치를 얻은 후 SDK에 전달하여 인근 POI 목록을 가져올 수 있습니다.

### Android

다음은 Android에서 다음을 사용하는 샘플 구현입니다. [`BroadcastReceiver`](https://codelabs.developers.google.com/codelabs/background-location-updates-android-o/index.html?index=..%2F..index#5)

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

다음은 iOS용 샘플 구현입니다. 이 코드에서는 다음 위치의 [`locationManager:didUpdateLocations:`](https://developer.apple.com/documentation/corelocation/cllocationmanagerdelegate/1423615-locationmanager?language=objc) 메서드 구현을 보여 줍니다 [`CLLocationManagerDelegate`](https://developer.apple.com/documentation/corelocation/cllocationmanager?language=objc).

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

다음은 iOS용 샘플 구현입니다. 이 코드에서는 다음 위치의 [`locationManager(_:didUpdateLocations:)`](https://developer.apple.com/documentation/corelocation/cllocationmanagerdelegate/1423615-locationmanager) 메서드 구현을 보여 줍니다 [`CLLocationManagerDelegate`](https://developer.apple.com/documentation/corelocation/cllocationmanager).

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

## 3. 위치 데이터를 Analytics 요청에 첨부

Places SDK는 `getNearbyPointsOfInterest` API를 호출하여 Launch의 데이터 요소를 통해 장치에 대한 모든 POI 데이터를 사용할 수 있도록 합니다. 데이터 [첨부](https://aep-sdks.gitbook.io/docs/resources/user-guides/attach-data) 규칙을 사용하여 위치 데이터를 향후 요청에 자동으로 추가할 수 있습니다. 이렇게 하면 장치의 위치가 수집될 때 Analytics에 대한 일회성 호출이 필요하지 않습니다.

이 [항목에 대한 자세한 내용은 Analytics 요청에](use-places-with-other-solutions/places-adobe-analytics/run-reports-aa-places-data.md) 위치 컨텍스트 추가를 참조하십시오.

## 선택 사항 - 사용자가 POI에 있을 때 시작 이벤트를 트리거합니다.

>[!TIP]
>
>위치 데이터를 캡처하는 권장되는 방법은 Analytics 요청에 위치 [데이터를 첨부하는 것입니다](#attach-places-data-to-your-analytics-requests).
>
>사용 사례에서 SDK에 의해 [지역 응모 이벤트를](places-ext-aep-sdks/places-extension/places-event-ref.md#processregionevent) 트리거해야 하는 경우, 아래에 설명된 대로 수동으로 수행해야 합니다.

API에서 반환되는 목록에는 사용자가 현재 POI 내에 있는지 여부를 나타내는 `getNearbyPointsOfInterest` 사용자 지정 개체가 [](places-ext-aep-sdks/places-extension/cust-places-objects.md) 포함되어 있습니다. 사용자가 POI에 있는 경우 SDK가 해당 영역에 대한 시작 이벤트를 트리거하도록 할 수 있습니다.

>[!IMPORTANT]
>
>앱이 한 번의 방문으로 여러 시작 이벤트를 트리거하지 않도록 사용자가 입력한 지역 목록을 유지합니다. SDK에서 인근 POI의 응답을 처리할 때 해당 지역이 목록에 없는 경우에만 시작 이벤트를 트리거합니다.
>
>다음 코드 샘플에서는 `NSUserDefaults` (iOS) 및 `SharedPreferences` (Android)를 사용하여 지역 목록을 관리합니다.

### Android

다음 코드 샘플은 a의 콜백에서 제공된 결과의 처리 `getNearbyPointsOfInterest`를 보여줍니다. `List<PlacesPOI>`

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

다음 코드 샘플에서는 콜백에서 제공된 결과의 처리 `getNearbyPointsOfInterest:limit:callback:errorCallback:`를 보여 줍니다. `NSArray<ACPPlacesPoi *> *`

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

다음 코드 샘플에서는 콜백에서 제공된 결과의 처리 `getNearbyPoints(_ ofInterest: CLLocation, limit: UInt, callback: (([ACPPlacesPoi]?) -> Void)?, errorCallback: ((ACPPlacesRequestError) -> Void)?)`를 보여 줍니다. `[ACPPlacesPoi]`

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

## 완벽한 샘플 구현

아래 코드 샘플에서는 장치의 현재 위치를 검색하고, 필요한 시작 이벤트를 트리거하며, 한 번의 방문 시 동일한 위치에 대해 여러 항목을 가져오지 않는 방법을 보여 줍니다.

이 코드 샘플에는 사용자가 POI에 있을 [때 시작 이벤트를 트리거하는 선택적 단계가 포함되어 있습니다](#trigger-entry-events-when-the-user-is-in-a-poi).

>[!IMPORTANT]
>
>이러한 코드 조각은 **유일한** 예입니다. 개발자는 해당 기능을 구현할 방법을 결정해야 하며, 이를 위해서는 대상 운영 체제에서 권장하는 우수 사례를 고려해야 합니다.

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

시작 이벤트 트리거로 인해 SDK에서 Places Service 시작 이벤트를 트리거하는 것 외에도, Experience Platform Launch에서 POI를 정의하는 모든 데이터를 나머지 SDK에서 사용할 수 `data elements` 있습니다. Experience Platform Launch `rules`를 사용하면 SDK에서 처리되는 수신 이벤트에 서비스 데이터를 동적으로 첨부할 수 있습니다. 예를 들어, 사용자가 위치한 POI의 메타 데이터를 연결하고 데이터를 Analytics에 컨텍스트 데이터로 전송할 수 있습니다.

자세한 내용은 다른 Adobe 솔루션과 함께 [위치 서비스 사용을 참조하십시오](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-analytics-overview.md).

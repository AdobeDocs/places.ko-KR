---
title: 위치 확장
seo-title: 위치 확장
description: 위치 확장 기능을 사용하면 사용자의 위치를 기반으로 할 수 있습니다.
seo-description: 위치 확장 기능을 사용하면 사용자의 위치를 기반으로 할 수 있습니다.
translation-type: tm+mt
source-git-commit: a2e30282789d9834e5c65502e28ddb25f3c55dfa

---


# 위치 확장 {#places-extension}

위치 확장 기능을 사용하면 사용자의 위치를 기반으로 할 수 있습니다. 이 익스텐션은 위치 쿼리 서비스 API에 대한 인터페이스입니다. 이 확장은 GPS 좌표 및 위치 영역 이벤트가 포함된 이벤트를 수신하여 규칙 엔진에서 처리하는 새 이벤트를 전달합니다. 또한 위치 확장 기능은 API에서 검색하는 앱 데이터에 대해 가장 가까운 POI 목록을 검색하여 제공합니다. API에서 반환되는 영역은 캐시 및 지속성에 저장되므로 제한된 오프라인 처리를 허용합니다.

## Adobe Experience Platform Launch에서 위치 확장 설치

1. 경험 플랫폼 론치에서 **[!UICONTROL Extensions]** 탭을 클릭합니다.
1. 탭에서 **[!UICONTROL Catalog]** 확장자를 찾아 **[!UICONTROL Places]** **[!UICONTROL Install]**&#x200B;클릭합니다.
1. 이 속성에 사용할 위치 라이브러리를 선택합니다. 앱에서 액세스할 수 있는 라이브러리입니다.
1. 클릭 **[!UICONTROL Save]**.

   클릭하면 Experience Platform SDK가 **[!UICONTROL Save]**&#x200B;선택한 라이브러리에서 POI를 배치 서비스를 검색합니다. 앱을 빌드할 때 POI 데이터는 라이브러리 다운로드에 포함되지 않지만, 런타임 시 POI의 위치 기반 하위 세트가 최종 사용자의 GPS 좌표에 다운로드됩니다.

1. 게시 프로세스를 완료하여 SDK 구성을 업데이트합니다.

   Experience Platform Launch에서의 게시에 대한 자세한 내용은 게시를 [참조하십시오](https://docs.adobelaunch.com/launch-reference/publishing).

### Configure the Places extension {#configure-places-extension}

![](//help/assets/places-extension.png)

## 앱에 위치 확장 기능 추가 {#add-places-to-app}

Android 및 iOS 앱에 위치 확장을 추가할 수 있습니다.

### Android

Java를 사용하여 앱에 위치 확장을 추가하려면:

1. 앱의 그래디얼 파일을 사용하여 프로젝트에 위치 확장을 추가합니다.

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

1. 위치 및 [모바일 코어](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) 라이브러리를 프로젝트에 추가합니다. 다음 창을 `Podfile`추가합니다.

   ```objective-c
   pod 'ACPPlaces', '~> 1.0'
   pod 'ACPCore', '~> 2.0'    # minimum Core version for Places is 2.0.3
   ```

   또는 Copods를 사용하지 않는 경우 Github의 [릴리스 페이지에서](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/) Mobile Core 및 Places 라이브러리를 수동으로 포함할 수 있습니다.

1. 코드 업데이트:

   ```objective-c
   pod update
   ```

1. Xcode를 열고 AppDelegate 클래스에서 코어 및 위치 헤더를 가져옵니다.

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

### Mobile Core로 위치 등록 {#register-places-mobile-core}

Android 및 iOS에서 Mobile Core에 위치를 등록해야 합니다.

#### Android

앱의 `OnCreate` 메서드에서 위치 서비스 확장을 등록합니다.

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

앱의 `application:didFinishLaunchingWithOptions:` 방식에서 Places 확장을 다른 SDK 등록 호출에 등록합니다.

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

## 구성 키

런타임에 프로그래밍 방식으로 SDK 구성을 업데이트하려면 다음 정보를 사용하여 위치 구성 값을 변경합니다. 자세한 내용은 구성 API [참조를 참조하십시오](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| 키 | 필수 여부 | 설명 |
| :--- | :--- | :--- |
| `places.libraries` | 예 | 모바일 앱용 라이브러리를 배치합니다. 라이브러리 ID와 모바일 앱이 지원하는 라이브러리 이름을 지정합니다. |
| `places.endpoint` | 예 | 라이브러리 및 POI에 대한 정보를 가져오는 데 사용되는 기본 경험 플랫폼 위치 쿼리 서비스 끝점입니다. |


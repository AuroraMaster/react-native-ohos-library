> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-baidu-map</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lovebing/react-native-baidu-map">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lovebing/react-native-baidu-map/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-baidu-map)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-baidu-map Releases](https://github.com/react-native-oh-library/react-native-baidu-map/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:end -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-baidu-map
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-baidu-map
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from 'react';
import { Text, ScrollView, View, StyleSheet } from 'react-native';
import { MapApp, Location, BaiduMapManager, MapView, Overlay } from 'react-native-baidu-map';


function App({ }): JSX.Element {

    const _onMapClick = (location: Location) => {
        console.log('baidumap _onMapClick location latitude:' + location.latitude);
        console.log('baidumap _onMapClick location longitude:' + location.longitude);
    }

    const _onMapDoubleClick = () => {
        console.log('baidumap _onMapDoubleClick');
    }

    const _onMapLoaded = () => {
        console.log('baidumap _onMapLoaded');
    }


    function _TestTurboModule() {
        console.log('baidumap _TestTurboModule');
        BaiduMapManager.initSDK('test');
        BaiduMapManager.hasLocationPermission().then((hasPermission: boolean) => {
            console.log('baidumap hasLocationPermission:' + hasPermission);
        })
        MapApp.openDrivingRoute({ latitude: 38.914935, longitude: 115.403119, name: "" }, { latitude: 39.914935, longitude: 116.403119, name: "" });
        MapApp.openTransitRoute({ latitude: 36.914935, longitude: 113.403119, name: "" }, { latitude: 37.914935, longitude: 114.403119, name: "" });
        MapApp.openWalkNavi({ latitude: 34.914935, longitude: 111.403119, name: "" }, { latitude: 35.914935, longitude: 112.403119, name: "" });
    }
    return (
    <View >
        <View style={[styles.button, { marginLeft: 100, marginTop: 40 }]}
            onTouchEnd={() => {
             _TestTurboModule();
            }
    }>
    <Text style={styles.buttonText}>_TestTurboModule</Text>
        </View>
        <MapView
    center={{ latitude: 38.914935, longitude: 115.403119 }}
    zoom={12.0}
    mapType={1}
    trafficEnabled={true}
    zoomGesturesEnabled={true}
    scrollGesturesEnabled={true}
    zoomControlsVisible={true}
    showsUserLocation={true}
    locationData={{ latitude: 38.914935, longitude: 115.403119 }}
    onMapClick={_onMapClick}
    onMapLoaded={_onMapLoaded}
    onMapDoubleClick={_onMapDoubleClick}
    style={{ width: '100%', height: '90%' }}
    >
    <Overlay.Circle
    radius={6000}
    fillColor='0000FF'
    stroke={{ width: 12, color: 'AAEEFF11' }}
    center={{ latitude: 38.914935, longitude: 115.403119 }} />
    
        <Overlay.Marker
    location={{ latitude: 39.844935, longitude: 115.603119 }} onClick={() => {
        console.log("baidumap Marker CLICK1")
    }} icon={{ uri: "https://maponline0.bdimg.com/sty/map_icons2x/MapRes/huochezhan.png?udt=20230227" }} />
    
        <Overlay.Marker
    location={{ latitude: 40.044935, longitude: 115.603119 }} onClick={() => {
        console.log("baidumap Marker CLICK2")
    }} icon={{ uri: "https://maponline0.bdimg.com/sty/map_icons2x/MapRes/huochezhan.png?udt=20230227" }} />
    
    
        <Overlay.Polyline
    points={[{ latitude: 38.914935, longitude: 115.403119 }, { latitude: 39.014935, longitude: 115.603119 }, { latitude: 38.814935, longitude: 115.603119 }]}
    stroke={{ width: 5, color: 'AA000000' }} />
    
        <Overlay.Polygon
    points={[{ latitude: 38.914935, longitude: 115.403119 }, { latitude: 38.614935, longitude: 115.203119 }, { latitude: 39.414935, longitude: 115.403119 }]}
    stroke={{ width: 5, color: 'AA000000' }}
    fillColor='0000FF' />
        <Overlay.Text
    location={{ latitude: 38.614935, longitude: 115.403119 }}
    fontColor='0000FF'
    fontSize={32}
    bgColor='888888'
    rotate={10}
    text='overlay Text test' />
        </MapView>
        </View>
    
    )
    }
    
    const styles = StyleSheet.create({
        button: {
            width: 160,
            height: 36,
            backgroundColor: 'hsl(190, 50%, 70%)',
            paddingHorizontal: 16,
            paddingVertical: 8,
            borderRadius: 8,
        },
        buttonText: {
            width: '100%',
            height: '100%',
            fontWeight: 'bold',
        },
    });

export default App;
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
"@rnoh/react-native-openharmony": "file:../react_native_openharmony",
"@react-native-oh-tpl/react-native-baidu-map": "file:../../node_modules/@react-native-oh-tpl/react-native-baidu-map/harmony/baidu_map.har"
}
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing BaiduMapPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-baidu-map/src/main/cpp" ./baidu-map)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_baidu_map)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "BaiduMapPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<BaiduMapPackage>(ctx),
    };
}
```

### 4. Introducing BaiduMapPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {BaiduMapPackage} from '@react-native-oh-tpl/react-native-baidu-map/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BaiduMapPackage(ctx)
  ];
}
```

### 5. Introducing react-native-baidu-map Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets`
or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import {
+  BAIDU_MAP_OVERLAY_CIRCLE_TYPE,
+  BAIDU_MAP_OVERLAY_MARKER_TYPE,
+  BAIDU_MAP_OVERLAY_POLYGON_TYPE,
+  BAIDU_MAP_OVERLAY_POLYLINE_TYPE,
+  BAIDU_MAP_OVERLAY_TEXT_TYPE,
+  BAIDU_MAP_VIEW_TYPE,
+  BaiduMapOverlayCircle,
+  BaiduMapOverlayPolygon,
+  BaiduMapOverlayPolyline,
+  BaiduMapOverlayText,
+  BaiduMapOverlayMarker,
+  BaiduMapView
+} from '@react-native-oh-tpl/react-native-baidu-map';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === BAIDU_MAP_VIEW_TYPE) {
+      BaiduMapView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_CIRCLE_TYPE) {
+      BaiduMapOverlayCircle({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_MARKER_TYPE) {
+      BaiduMapOverlayMarker({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_POLYGON_TYPE) {
+      BaiduMapOverlayPolygon({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_POLYLINE_TYPE) {
+      BaiduMapOverlayPolyline({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_TEXT_TYPE) {
+      BaiduMapOverlayText({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
...
}
...
```

> [!TIP] The repository uses a mixed solution, the component name needs to be added.  

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ BAIDU_MAP_VIEW_TYPE,
+ BAIDU_MAP_OVERLAY_CIRCLE_TYPE,
+ BAIDU_MAP_OVERLAY_MARKER_TYPE,
+ BAIDU_MAP_OVERLAY_POLYGON_TYPE,
+ BAIDU_MAP_OVERLAY_POLYLINE_TYPE,
+ BAIDU_MAP_OVERLAY_TEXT_TYPE
  ];
```

### 6. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-baidu-map Releases](https://github.com/react-native-oh-library/react-native-baidu-map/releases)

### Permission Requirements

#### Add permissions in the module.json5 file under the entry directory.

Open `entry/src/main/module.json5`, add the following permission:

```diff
...
"requestPermissions": [
+      {
+        "name": "ohos.permission.WRITE_USER_STORAGE"
+      },
+      {
+        "name": "ohos.permission.READ_USER_STORAGE"
+      },
+      {
+        "name": "ohos.permission.INTERNET"
+      },
+      {
+        "name": "ohos.permission.GET_BUNDLE_INFO"
+      },
+      {
+        "name": "ohos.permission.LOCATION",
+        "reason": "$string:EntryAbility_desc",
+        "usedScene": {
+          "abilities": [
+            "MainAbility"
+          ],
+          "when": "inuse"
+        }
+      },
+      {
+        "name": "ohos.permission.LOCATION_IN_BACKGROUND",
+        "reason": "$string:EntryAbility_desc",
+        "usedScene": {
+          "abilities": [
+            "MainAbility"
+          ],
+          "when": "inuse"
+        }
+      },
+      {
+        "name": "ohos.permission.APPROXIMATELY_LOCATION",
+        "reason": "$string:EntryAbility_desc",
+        "usedScene": {
+          "abilities": [
+            "MainAbility"
+          ],
+          "when": "inuse"
+        }
+      }
    ]
```

## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### MapView Props

| Name                    | Description                      | Type     | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------|----------|----------|----------|-------------------|
| zoomControlsVisible     | Displays or hides zoom controls.              | Boolean  | no      | Android  | yes               |
| trafficEnabled          | Enables the traffic layer.                         | Boolean  | no      | All      | yes                |
| baiduHeatMapEnabled     | Enables Baidu heatmap.                        | Boolean  | no      | All      | no                |
| zoomGesturesEnabled     | Allows zooming via gestures.                           | Boolean  | no      | All      | yes                |
| scrollGesturesEnabled   | Allows dragging.                             | Boolean  | no      | All      | yes                |
| mapType                 | Type of the map.                              | Number   | no      | All      | partially【Supported values: 1 (NORMAL), 2 (SATELLITE). Unsupported values: 0 (NONE) 】               |
| zoom                    | Zoom level of the map.                              | Number   | no      | All      | yes                |
| showsUserLocation       | Displays the user location.                           | Boolean  | no      | All      | yes                |
| locationData            | Location data {latitude: 0, longitude: 0} | Object   | no      | All      | yes                |
| center                  | {latitude: 0, longitude: 0}      | Object   | no      | All      | yes                |
| onMapStatusChangeStart  | Callback triggered when map status changes start.         | Function | no      | Android  | no                |
| onMapStatusChange       | Callback triggered during map status changes.                     | Function | no      | All      | no                |
| onMapStatusChangeFinish | Callback triggered when map status changes finish.        | Function | no      | Android  | no                |
| onMapLoaded             | Callback triggered when map loading completes.                     | Function | no      | All      | yes                |
| onMapClick              | Callback triggered when the map is clicked.                      | Function | no      | All      | yes                |
| onMapDoubleClick        | Callback triggered when the map is double-clicked.                      | Function | no      | All      | yes                |
| onMarkerClick           | Callback triggered when a marker is clicked.                   | Function | no      | All      | no                |
| onMapPoiClick           | Callback triggered when a point of interest (POI) on the map is clicked.           | Function | no      | All      | no                |

#### Marker Props

| Name         | Description                              | Type     | Required | Platform | HarmonyOS Support |
|--------------|------------------------------------------|----------|----------|----------|-------------------|
| title        | Generates the **InfoWindow** based on the title if no **InfoWindow** is provided. | String   | no       | All      | no                |
| titleOffsetY | Y-axis offset for title when displayed as the **InfoWindow**. | Number   | no       | Android  | no                |
| location     | Longitude and latitude coordinates of a marker.               | Object   | yes      | All      | yes               |
| perspective  | Perspective effect.                   | Boolean  | no       | Android  | no               |
| flat         | Flattens a marker.                     | Boolean  | no       | Android  | yes               |
| rotate       | Rotation angle.                         | Number   | no       | Android  | yes               |
| icon         | Image, which is the same as the **source** property of the **Image** component.                    | Object   | no       | All      | yes               |
| alpha        | Opacity.                         | Number   | no       | Android  | yes               |
| animateType  | Animation effect：drop/grow/jump       | String   | no       | All      | yes               |
| pinColor     | Pin color: red/green/purple.               | String   | no       | IOS      | no                |
| onClick      | Callback triggered when a marker is clicked.     | Function | no       | All      | yes               |

#### Cluster

#### Arc Props 

| Name   | Description    | Type    | Required | Platform | HarmonyOS Support |
|--------|----------------|---------|----------|----------|-------------------|
| stroke | Callback triggered when a marker is clicked.| Object  | yes      | All      | no                |
| points | The value length must be **3**.       | Object  | yes      | All      | no                |
| dash   | Determines if a line is dashed.   | Boolean | yes      | iOS      | no                |

#### Circle Props

| Name      | Description       | Type   | Required | Platform | HarmonyOS Support |
|-----------|-------------------|--------|----------|----------|-------------------|
| radius    | Radius of a circle.             | Number | yes      | All      | yes               |
| fillColor | Fill color of a circle (hexadecimal, with opacity).| String | yes       | All      | yes               |
| stroke    | Stroke style of a circle.           | Object | yes       | All      | yes               |
| center    | Center point coordinates of a circle.          | Object | yes       | All      | yes               |

#### Polyline Props

| Name   | Description | Type   | Required | Platform | HarmonyOS Support |
|--------|-------------|--------|----------|----------|-------------------|
| points | Vertex coordinate array of a polyline.  | Object | yes      | All      | yes               |
| stroke | Stroke style of a polyline.    | Object | yes      | All      | no               |


#### Polygon Props

| Name      | Description          | Type   | Required | Platform | HarmonyOS Support |
|-----------|----------------------|--------|----------|----------|-------------------|
| points    | Vertex coordinate array of a polygon.          | Object | yes      | All      | yes               |
| fillColor | Fill color of a polygon (hexadecimal, with opacity). | String | no      | All      | yes               |
| stroke    | Polygon stroke type.            | Object | no      | All      | yes               |

#### Text Props

| Name      | Description   | Type   | Required | Platform | HarmonyOS Support |
|-----------|---------------|--------|----------|----------|-------------------|
| text      | Text to display.       | String | yes      | All      | yes               |
| fontSize  | Font size of the text.      | Number | no       | All      | yes               |
| fontColor | Font color of the text (hexadecimal).| String | no       | All      | yes               |
| bgColor   | Background color of the text (hexadecimal).| String | no       | All      | yes               |
| rotate    | Rotation angle of the text.      | Number | no       | All      | yes               |
| location  | Coordinates of the text on the map.  | Object | yes      | All      | yes               |

#### MarkerIcon：Using View as a Marker Icon

#### InfoWindow Props

#### The **InfoWindow** must be used as a subcomponent of the **Marker.**

| Name    | Description                    | Type   | Required | Platform | HarmonyOS Support |
|---------|--------------------------------|--------|----------|----------|-------------------|
| offsetY | Y-axis offset relative to the point. | Object | yes      | Android  | no                |

#### HeatMap Props

| Name     | Description | Type   | Required | Platform | HarmonyOS Support |
|----------|-------------|--------|----------|----------|-------------------|
| points   | Points for drawing the heatmap.    | array  | yes      | All      | no                |
| gradient | Gradient color object.     | object | yes      | All      | no                |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### BaiduMapManager

| Name                          | Description | Type | Required | Platform | HarmonyOS Support |
|-------------------------------|-------------|------|----------|----------|-------------------|
| initSDK                       | Initializes the SDK on iOS.| void | no      | All      | yes               |
| Promise hasLocationPermission | Checks if location permission is granted.    | void | no       | All      | yes               |

#### Geolocation Methods

| Name                                              | Description                          | Type | Required | Platform | HarmonyOS Support |
|---------------------------------------------------|--------------------------------------|------|----------|----------|-------------------|
| Promise reverseGeoCode                            | Retrieves address information based on the given coordinates.                 | void | no      | All      | no                |
| Promise reverseGeoCodeGPS                         | Performs reverse geocoding for given coordinates.| void | no       | All      | no                |
| Promise geocode                                   | Calls a geocoding service API.                    | void | no       | All      | no                |
| Promise getCurrentPosition                        | Retrieves the current position. **coorType** can be **bd09ll** (default) or **gcj02**.| void | no       | All      | no                |
| startLocating(function listener, String coorType) | Starts continuous location tracking.                              | void | no       | All      | no                |
| stopLocating                                      | Stops continuous location tracking.                              | void | no       | All      | no                |

#### GetDistance Methods

| Name                        | Description   | Type | Required | Platform | HarmonyOS Support |
|-----------------------------|---------------|------|----------|----------|-------------------|
| Promise getLocationDistance | Calculates the distance between two locations.| no   | no      | All      | no                |

#### MapApp Methods: Opening the Baidu Maps Client

| Name             | Description | Type | Required | Platform | HarmonyOS Support |
|------------------|-------------|------|----------|----------|-------------------|
| openDrivingRoute | Open Baidu Maps for a driving route. | void | no       | All      | yes               |
| openTransitRoute | Open Baidu Maps for a transit route. | void | no       | All      | yes               |
| openWalkNavi     | Open Baidu Maps for a walking route. | void | no       | All      | yes               |

## Known Issues
- [ ] The Arc overlay is not implemented. [#15](https://github.com/react-native-oh-library/react-native-baidu-map/issues/15)
- [ ] The infoWindow overlay is not implemented. [#16](https://github.com/react-native-oh-library/react-native-baidu-map/issues/16)
- [ ] The HeatMap overlay is not implemented. [#17](https://github.com/react-native-oh-library/react-native-baidu-map/issues/17)
- [ ] The Cluster overlay is not implemented. [#18](https://github.com/react-native-oh-library/react-native-baidu-map/issues/18)
- [ ] The MarkerIcon overlay is not implemented. [#19](https://github.com/react-native-oh-library/react-native-baidu-map/issues/19)
- [ ] Some MapView events are not implemented. [#20](https://github.com/react-native-oh-library/react-native-baidu-map/issues/20).
- [ ] The title, pincolor, and perspective properties of the marker are not implemented. [#21](https://github.com/react-native-oh-library/react-native-baidu-map/issues/21).
- [ ] The Geolocation static class function is not implemented. [#22](https://github.com/react-native-oh-library/react-native-baidu-map/issues/22).
- [ ] The GetDistance static class function is not implemented. [#23](https://github.com/react-native-oh-library/react-native-baidu-map/issues/23).
- [ ] The stroke property of Polyline is not implemented. [#21](https://github.com/react-native-oh-library/react-native-baidu-map/issues/29).


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lovebing/react-native-baidu-map/blob/master/LICENSE).
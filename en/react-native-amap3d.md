> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-amap3d</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/qiuxiang/react-native-amap3d">
        <img src="https://img.shields.io/badge/platforms-android%20|%20iOS%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/qiuxiang/react-native-amap3d/blob/main/license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-amap3d)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-amap3d Releases](https://github.com/react-native-oh-library/react-native-amap3d/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-amap3d
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-amap3d
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { ScrollView, Text, View,StyleSheet, Alert } from 'react-native';
import {MapView, Circle, Polygon, Polyline, Marker, LatLng,CameraPosition,voidEvent} from 'react-native-amap3d';

import type * as ReactNative from "react-native";

const points = [
  {
    latitude: 39.806901,
    longitude: 116.397972,
  },
  {
    latitude: 39.806901,
    longitude: 116.297972,
  },
  {
    latitude: 39.906901,
    longitude: 116.397972,
  },
];

const points2 = [
  {
    latitude: 39.836901,
    longitude: 116.497972,
  },
  {
    latitude: 39.836901,
    longitude: 116.397972,
  },
  {
    latitude: 39.936901,
    longitude: 116.497972,
  },
];

const line1 = [
  { latitude: 40.006901, longitude: 116.097972 },
  { latitude: 40.006901, longitude: 116.597972 },
];
const line3 = [
  { latitude: 39.806901, longitude: 116.097972 },
  { latitude: 39.806901, longitude: 116.257972 },
  { latitude: 39.806901, longitude: 116.457972 },
  { latitude: 39.806901, longitude: 116.597972 },
];

function AMapDemo() {
  return (
    <View style={styles.container}>
		<MapView 
    mapType={1}
    myLocationEnabled = {true}
    onPress={(event: ReactNative.NativeSyntheticEvent<LatLng>)=>{
      console.info("AMapViewEventType map3d demo " + event.nativeEvent.latitude + "===" + event.nativeEvent.longitude)
    }}
    onLongPress={(event: ReactNative.NativeSyntheticEvent<LatLng>)=>{
      console.info("AMapViewEventType map3d demo longevent===" + event.nativeEvent.latitude + "===" + event.nativeEvent.longitude)
    }}
    onLoad={(event: ReactNative.NativeSyntheticEvent<voidEvent>) => {
      Alert.alert("onLoad successful")
    }}
    > 
    <Circle
      strokeWidth={5}
      strokeColor="rgba(0, 0, 255, 0.5)"
      fillColor="rgba(255, 0, 0, 0.5)"
      radius={500}
      center={{ latitude: 39.906901, longitude: 116.397972 }}
    />
    <Polygon
      strokeWidth={5}
      strokeColor="rgba(0, 0, 255, 0.5)"
      fillColor="rgba(255, 0, 0, 0.5)"
      points={points}
    />
    <Polyline width={100}  color="rgba(0, 255, 0, 0.5)" points={line1} onPress={() => { console.info("AMapViewEventType map3d polyline onPress width 200")}} />
    <Marker
      draggable={true}
      position={{ latitude: 39.806901, longitude: 116.397972 }}
      onPress={() => Alert.alert("onPress")}
      onDragEnd={({ nativeEvent }) =>
        Alert.alert(`onDragEnd: ${nativeEvent.latitude}, ${nativeEvent.longitude}`)}
    />
    <Marker
        draggable={true}
        flat={false}
        position={{ latitude: 45.806901, longitude: 117.397972 }}
    >
        <Text
            style={{
                color: "#fff",
                backgroundColor: "#ff6977",
                margin:5,
                width:"14%",
            }}
        >
            {"testMarker"}
        </Text>
    </Marker>
    </MapView>
	</View>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#fff',
    flex: 1,
    paddingTop: 24,
  }
});
export default AMapDemo;
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
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
    "@react-native-oh-tpl/react-native-amap3d": "file:../../node_modules/@react-native-oh-tpl/react-native-amap3d/harmony/rn_amap3d.har"
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

### 3. Configuring CMakeLists and Introducing MapViewPackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-amap3d/src/main/cpp" ./rn_amap3d)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_amap3d)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "MapViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<MapViewPackage>(ctx)
    };
}
```


### 4. Introducing react-native-amap3d Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
...
+ import {
+  A_MAP_CIRCLE_VIEW_TYPE,
+  A_MAP_MARKER_TYPE,
+  A_MAP_POLYGON_TYPE,
+  A_MAP_POLYLINE_TYPE,
+  AMapCircle,
+  AMapMarker,
+  AMapPolygon,
+  AMapPolyline,
+  AMapView,
+  GOADE_MAP_VIEW_TYPE
+} from '@react-native-oh-tpl/react-native-amap3d';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+    if (ctx.componentName === GOADE_MAP_VIEW_TYPE) {
+      AMapView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_CIRCLE_VIEW_TYPE) {
+      AMapCircle({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_MARKER_TYPE) {
+      AMapMarker({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_POLYGON_TYPE) {
+      AMapPolygon({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_POLYLINE_TYPE) {
+      AMapPolyline({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.  

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+  A_MAP_CIRCLE_VIEW_TYPE,
+  A_MAP_MARKER_TYPE,
+  A_MAP_POLYGON_TYPE,
+  A_MAP_POLYLINE_TYPE,
+  GOADE_MAP_VIEW_TYPE
  ];
```

### 5. Introducing AMap3DPackage to ArkTS 

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:


```diff  
  ... 
+ import {AMap3DPackage} from '@react-native-oh-tpl/react-native-amap3d/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AMap3DPackage(ctx)
  ];
}
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-amap3d Releases](https://github.com/react-native-oh-library/react-native-amap3d/releases)


## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
### MapView
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| mapType  | Map type         | int  | no | iOS/Android | yes |
| initialCameraPosition  | Initial state         | CameraPosition  | no | iOS/Android | yes |
| myLocationEnabled  | Whether to display the current positioning         | boolean  | no | iOS/Android | no |
| indoorViewEnabled  | Whether to display an indoor map         | boolean  | no | iOS/Android | no |
| buildingsEnabled  | Whether or not to display 3D buildings         | boolean  | no | iOS/Android | no |
| labelsEnabled  | Whether to display the label         | boolean  | no | iOS/Android | yes |
| compassEnabled  | Whether or not to display a compass         | boolean  | no | iOS/Android | yes               |
| zoomControlsEnabled  | Whether to display a zoomed-in button         | boolean  | no | Android | yes |
| scaleControlsEnabled  | Whether to display the scale bar         | boolean  | no | iOS/Android | yes |
| trafficEnabled  | Whether or not to display traffic conditions         | boolean  | no | iOS/Android | yes |
| maxZoom  | Maximum zoom level         | float  | no | iOS/Android | yes |
| minZoom  | Minimum zoom level         | float  | no | iOS/Android | yes |
| zoomGesturesEnabled  | Whether to enable the zoom gesture to zoom in and out         | boolean  | no | iOS/Android | yes |
| scrollGesturesEnabled  | Whether to enable the swipe gesture for panning         | boolean  | no | iOS/Android | yes |
| rotateGesturesEnabled  | Whether to enable the rotate gesture to adjust the orientation         | boolean  | no | iOS/Android | yes |
| tiltGesturesEnabled  | Whether or not to enable the tilt gesture to change the viewing angle         | boolean  | no | iOS/Android | yes |
| distanceFilter  | Sets the minimum update distance for positioning         | float  | no | iOS      | no|
| headingFilter  | Sets the minimum update angle, which defaults to 1 degree         | float  | no | iOS      | no |

### Circle
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| center  | Dotted coordinates         | LatLng  | yes | iOS/Android | yes |
| radius  | Radius (m)         | Float  | yes | iOS/Android | yes |
| strokeWidth  | Edge width         | Float  | no | iOS/Android | yes |
| strokeColor  | Edge color         | string  | no | iOS/Android | yes |
| fillColor  | Fill color         | string  | no | iOS/Android | yes |
| zIndex  | Level         | Float  | no | iOS/Android | yes |

### Marker
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| position  | coordinates         | LatLng  | yes | iOS/Android | yes |
| icon  | icon         | ImageSourcePropType  | no | iOS/Android | yes |
| draggable  | Whether it can be dragged or not         | boolean  | no | iOS/Android | yes |
| flat  | Whether the map is flattened or not         | boolean  | no | Android | yes |
| zIndex  | Level         | Float  | no | iOS/Android | yes |
| anchor  | Mulch anchor point ratio         | Point  | no | Android | no |
| centerOffset  | Cover offset position         | Float  | no | iOS      | no |

### Polygon
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points  | Node coordinates         | LatLng[]  | yes | iOS/Android | yes |
| strokeWidth  | Edge width         | Float  | no | iOS/Android | yes |
| strokeColor  | Edge color         | string  | no | iOS/Android | yes |
| fillColor  | Fill color         | string  | no | iOS/Android | yes |
| zIndex  | Level         | Float  | no | iOS/Android | yes |

### Polyline
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points  | Node coordinates         | LatLng[]  | yes | iOS/Android | yes |
| width  | Edge width         | Float  | no | iOS/Android | yes |
| color  | Segment color         | ColorValue  | no | iOS/Android | yes |
| zIndex  | Level         | Float  | no | iOS/Android | yes |
| colors  | Multi-segment color        | ColorValue[]  | no | iOS/Android | yes |
| gradient  | Whether to use a color gradient        | boolean  | no | iOS/Android | yes |
| geodesic  | Whether or not to draw geodetic lines        | boolean  | no | iOS/Android | no |
| dotted  | Whether or not to draw a dashed line        | boolean  | no | iOS/Android | yes |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
### MapView
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onPress  | Click Events        | LatLng | no | iOS/Android | yes |
| onPressPoi  | Label click events        | Poi | no | iOS/Android | yes |
| onLongPress  | Long press on the event        | LatLng | no | iOS/Android | yes |
| onCameraMove  | Map state change events, which are triggered continuously as the map state changes        | CameraEvent | no | iOS/Android | yes               |
| onCameraIdle  | Map state change events, which are triggered when the change stops        | CameraEvent | no | iOS/Android | no |
| onLoad  | Map Initialization Completion Event        | void | no | iOS/Android | yes |
| onLocation  | Map location update events        | GeolocationPosition | no | iOS/Android | no |
| onCallback  | Callback events        | void | no | iOS/Android | no |
| moveCamera  | Moving perspective        | void | yes | iOS/Android | yes                |
| call  | invoke        | void | no | iOS/Android | no |


### Marker
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onPress  | Click Events        | void | no | iOS/Android | yes |
| onDragStart  | Drag and drop the start event        | void | no | iOS/Android | yes |
| onDrag  | Drag-and-drop events, similar to mousemove, are called continuously until they end        | void | no | iOS/Android | yes |
| onDragEnd  | Drag and drop the end event        | LatLng | no | iOS/Android | yes |
| update  | Trigger a custom view update        | void | no | iOS/Android | no              |

### Polyline
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onPress  | Click Events        | void | no | iOS/Android | yes |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| initSDK  | Initialize AutoNavi SDK         | void  | no | iOS      | no |
| getVersion  | Get version information         | Promise<string>  | no | iOS      | no |

## Known Issues
- [ ] initSDK: Does not support in hramony: [issue#16](https://github.com/react-native-oh-library/react-native-amap3d/issues/16)
- [ ] getVersion: Does not support in hramony: [issue#17](https://github.com/react-native-oh-library/react-native-amap3d/issues/17)
### MapView
- [ ] indoorViewEnabled: Amap SDK is not supported: [issue#6](https://github.com/react-native-oh-library/react-native-amap3d/issues/6)
- [ ] buildingsEnabled: Amap SDK is not supported: [issue#33](https://github.com/react-native-oh-library/react-native-amap3d/issues/33)
- [ ] myLocationEnabled: Amap SDK is not supported: [issue#29](https://github.com/react-native-oh-library/react-native-amap3d/issues/29)
- [ ] distanceFilter: Amap SDK is not supported: [issue#11](https://github.com/react-native-oh-library/react-native-amap3d/issues/11)
- [ ] headingFilter: Amap SDK is not supported: [issue#12](https://github.com/react-native-oh-library/react-native-amap3d/issues/12)
- [ ] geodesic: Amap SDK is not supported: [issue#36](https://github.com/react-native-oh-library/react-native-amap3d/issues/36)
- [ ] onCameraIdle: Amap SDK is not supported: [issue#15](https://github.com/react-native-oh-library/react-native-amap3d/issues/15)
- [ ] onLocation: Amap SDK is not supported: [issue#10](https://github.com/react-native-oh-library/react-native-amap3d/issues/10)
- [ ] onCallback: Amap SDK has partial support: [issue#21](https://github.com/react-native-oh-library/react-native-amap3d/issues/21)
### Marker
- [ ] The marker custom width is adaptive: [issue#64](https://github.com/react-native-oh-library/react-native-amap3d/issues/64)
### Cluster
- [ ] Cluster: Amap SDK does not currently support adding this component: [issue#2](https://github.com/react-native-oh-library/react-native-amap3d/issues/2)
### HeatMap
- [ ] HeatMap: Amap SDK does not currently support adding this component: [issue#3](https://github.com/react-native-oh-library/react-native-amap3d/issues/3)
### MultiPoint
- [ ] MultiPoint: Amap SDK does not currently support adding this component: [issue#4](https://github.com/react-native-oh-library/react-native-amap3d/issues/4)


## Others

## License

This project is licensed under [MIT License (MIT)](https://github.com/qiuxiang/react-native-amap3d/blob/main/license).

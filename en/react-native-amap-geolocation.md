> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-amap-geolocation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/qiuxiang/react-native-amap-geolocation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/qiuxiang/react-native-amap-geolocation/blob/main/license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-amap-geolocation) 

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.2.3-0.0.5@deprecated | [@react-native-oh-tpl/react-native-amap-geolocation Releases(deprecated)](https://github.com/react-native-oh-library/react-native-amap-geolocation/releases) | 0.72       |
| 1.2.4 | [@react-native-ohos/react-native-amap-geolocation Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-amap-geolocation/releases) | 0.72       |
| 1.3.0 | [@react-native-ohos/react-native-amap-geolocation Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-amap-geolocation/releases) | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-amap-geolocation
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-amap-geolocation
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import {
    Button,
    Platform,
    ScrollView,
    StyleSheet,
    Text,
    View,
} from "react-native";
import {
    Geolocation, setInterval, addLocationListener, setAllowsBackgroundLocationUpdates,
    setGeoLanguage, setDistanceFilter, setDesiredAccuracy, init, setNeedAddress, start,
    stop, setLocationTimeout, setOnceLocation, GeoLanguage
} from "react-native-amap-geolocation";


const style = StyleSheet.create({
    body: {
        padding: 16,
        paddingTop: Platform.OS === "ios" ? 48 : 16,
    },
    button: {
        flexDirection: "column",
        marginRight: 8,
        marginBottom: 5,
        marginTop: 5
    },
    result: {
        fontFamily: Platform.OS === "ios" ? "menlo" : "monospace",
    },
});

class AmapGeoLocationDemo extends React.Component {
    state = {
        location: null, needAddressText: "setNeedAddress(false)",
        language: "setLanguage(chinese)", interval: "setInterval(默认2000)", onceText: "setOnceLocation(false) 设置单次定位",
        startText: "start 持续定位", timeoutText: "setLocationTimeout 设置请求定位超时时间",distanceText:"setDistanceFilter(0) 设置定位的最小更新距离"
    };
    watchId = 0;
    needAddress = true;
    currLanguage = GeoLanguage.ZH;
    currInterval = false;
    onceLocationJudge = false;
    timeout5000 = false;
    distanseJudge = true;
    init = () => {
        console.log("rn AMapLocationManagerImpl init");
        init("5f7389b845cbd89b1c32e24f526728f4").then(() => {
            console.log("rn AMapLocationManagerImpl init success");
        });

    };
    addLocationListener = () => {
        console.log("rn AMapLocationManagerImpl addLocationListener");
        addLocationListener((locationData) => {
            console.log("rn AMapLocationManagerImpl callback success:" + JSON.stringify(locationData, null, 2));
            let location = locationData;
            this.setState({ location: location });
        });
    };
    setDistanceFilter = () => {
        console.log("rn AMapLocationManagerImpl setDistanceFilter");
        this.distanseJudge = !this.distanseJudge;
        if (this.distanseJudge) {
            setDistanceFilter(0);
            this.setState({ distanceText: "setDistanceFilter(0) 设置定位的最小更新距离" });
        } else {
            setDistanceFilter(1);
            this.setState({ distanceText: "setDistanceFilter(1) 设置定位的最小更新距离" });
        }

    };
    setLocationTimeout = () => {
        console.log("rn AMapLocationManagerImpl setLocationTimeout");
        this.timeout5000 = !this.timeout5000;
        if (this.timeout5000) {
            setLocationTimeout(5000);
            this.setState({ timeoutText: "setLocationTimeout(5000) 设置请求定位超时时间" });
        } else {
            setLocationTimeout(10000);
            this.setState({ timeoutText: "setLocationTimeout(10000) 设置请求定位超时时间" });
        }
    };
    start = () => {
        console.log("rn AMapLocationManagerImpl start");
        start();
    };
    stop = () => {
        console.log("rn AMapLocationManagerImpl stop");
        stop();
    }
    onceLocation = () => {
        this.onceLocationJudge = !this.onceLocationJudge;
        if (this.onceLocationJudge) {
            setOnceLocation(true);
            this.setState({ onceText: "setOnceLocation(true) 设置单次定位", startText: "start 单次定位" });
        } else {
            setOnceLocation(false);
            this.setState({ onceText: "setOnceLocation(false) 设置单次定位", startText: "start 持续定位" });
        }
        console.log("rn AMapLocationManagerImpl current onceLocation:" + this.onceLocationJudge);
    };
    setInterval = () => {
        if (this.currInterval) {
            setInterval(2000);
            this.setState({ interval: "setInterval:2000" });
        } else {
            setInterval(10000);
            this.setState({ interval: "setInterval:10000" });
        }
        this.currInterval = !this.currInterval;
    }
    setNeedAddress = () => {
        this.needAddress = !this.needAddress;
        console.log("rn AMapLocationManagerImpl setNeedAddress:" + this.needAddress);
        if (this.needAddress) {
            setNeedAddress(true);
            this.setState({ needAddressText: "setNeedAddress(true)" });
        } else {
            setNeedAddress(false);
            this.setState({ needAddressText: "setNeedAddress(false)" });
        }
    }
    setLanguage = () => {
        // default = 0,chinese = 1, engilish=2;
        console.log("rn AMapLocationManagerImpl setLanguage");
        if (this.currLanguage == GeoLanguage.ZH) {
            this.currLanguage = GeoLanguage.EN;
            setGeoLanguage(GeoLanguage.EN);
            this.setState({ language: "setLanguage(engilish)" });
        } else {
            this.currLanguage = GeoLanguage.ZH;
            setGeoLanguage(GeoLanguage.ZH);
            this.setState({ language: "setLanguage(chinese)" });
        }

    }
    updateLocationState(location: any) {
    console.log("rn AMapLocationManagerImpl updateLocationState");
    if (location) {
        this.setState({ location: location });
        console.log(location);
    }
}
getCurrentPosition = () => {
    Geolocation.getCurrentPosition(
        (position) => this.updateLocationState(position),
        (error) => this.updateLocationState(error)
    );
};
watchPosition = () => {
    if (!this.watchId) {
        this.watchId = Geolocation.watchPosition(
            (position) => this.updateLocationState(position),
            (error) => this.updateLocationState(error)
        );
        console.log("rn AMapLocationManagerImpl watchPosition watchId:" + this.watchId);
    }
};
clearWatch = () => {
    if (this.watchId) {
        console.log("rn AMapLocationManagerImpl clearWatch watchId:" + this.watchId);
        Geolocation.clearWatch(this.watchId);
        this.watchId = 0;
    }
    stop();
    this.setState({ location: null });
};
render() {
    const location = this.state.location;
    const needAddressText = this.state.needAddressText;
    const language = this.state.language;
    const currInterval = this.state.interval;
    const onceText = this.state.onceText;
    const startText = this.state.startText;
    const timeoutText = this.state.timeoutText;
    const distanceText = this.state.distanceText;
    return (
        <ScrollView contentContainerStyle={style.body}>
        <View style={style.button}>
        <Button onPress={this.init} title="init 初始化接口" />
        </View>
        <View style={style.button}>
        <Button onPress={this.addLocationListener} title="addLocationListener 设置监听回调,原生接口不设置监听回调,text不会显示数据" />
        </View>
        <View style={style.button}>
        <Button onPress={this.setDistanceFilter} title={distanceText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.setLocationTimeout} title={timeoutText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.onceLocation} title={onceText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.start} title={startText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.stop} title="stop 结束持续定位" />
        </View>
        <View style={style.button}>
        <Button onPress={this.setInterval} title={currInterval} />
        </View>
        <View style={style.button}>
        <Button onPress={this.setNeedAddress} title={needAddressText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.setLanguage} title={language} />
        </View>
        <View style={style.button}>
        <Button onPress={this.getCurrentPosition} title="Geolocation.getCurrentPosition 获取当前位置，相当于单次请求" />
        </View>
        <View style={style.button}>
        <Button onPress={this.watchPosition} title="Geolocation.watchPosition 开启持续定位" />
        </View>
        <View style={style.button}>
        <Button onPress={this.clearWatch} title="Geolocation.clearWatch 结束持续定位" />
        </View>
        <Text style={style.result}>{`${JSON.stringify(location, null, 2)}`}</Text>
    </ScrollView>
);
}

}

export default AmapGeoLocationDemo;
```

##  Usage Notes

There are several important points to note when using this library:

1. **Provide a valid AMap API key**

   **How to obtain the API key:**

   - Go to the official AMap link: [My Applications | AMap Console](https://console.amap.com/dev/key/app)
   - Refer to the guide [Getting Started - HarmonyOS NEXT Map SDK | AMap API](https://lbs.amap.com/api/harmonyosnext-map3d-sdk/gettingstarted#t2) to obtain the appid.
   - Create a new application in the console and click "Add Key." After generating the key, integrate it into your project.

2. **Enable device network services**

3. **Enable device location services**

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.3.0                               |  No                   |  0.77                |
| ~1.2.4                               |  Yes                  |  0.72                |
| <= 1.2.3-0.0.5@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.


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
    "@react-native-ohos/react-native-amap-geolocation": "file:../../node_modules/@react-native-ohos/react-native-amap-geolocation/harmony/amap_geolocation.har"
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

### 3. Configuring CMakeLists and Introducing AmapGeolocationPackage

> If you are using version <= 1.2.3-0.0.5, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-amap-geolocation/src/main/cpp" ./amap_geolocation)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_amap_geolocation)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "AmapGeolocationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<AmapGeolocationPackage>(ctx),
    };
}
```

### 4. Introducing AmapGeolocationPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+  import {AMapGeolocationPackage} from '@react-native-ohos/react-native-amap-geolocation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AMapGeolocationPackage(ctx)
  ];
}
```
</details>

## Running

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

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements

#### Add permissions in the module.json5 file under the entry directory.

Open `entry/src/main/module.json5`, add the following permission：

```
...
"requestPermissions": [
  {
    "name": "ohos.permission.LOCATION",
    "reason": "$string:Access_Location",
    "usedScene": {
      "when":"inuse"
    }
  },
  {
    "name": "ohos.permission.APPROXIMATELY_LOCATION",
    "reason": "$string:Access_AppRoximatelyLocation",
    "usedScene": {
      "when":"inuse"
    }
  },
  {
    "name": "ohos.permission.INTERNET",
  }
]
```

#### Adding the description of location permissions in the entry directory

open `entry/src/main/resources/base/element/string.json`, add the following content：

```
...
{
  "string": [
    {
      "name": "Access_Location",
      "value": "access Location"
    },
    {
      "name": "Access_AppRoximatelyLocation",
      "value": "access AppRoximatelyLocation"
    }
  ]
}
```


## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type          | Required | Platform | HarmonyOS Support |
| ---- | ----------- |---------------|----------| -------- |-------------------|
| init  | Initialize SDK | Promise<void> | yes      | iOS/Android      | yes               |
| addLocationListener  | Add location listener function | void          | yes      | iOS/Android      | yes               |
| isStarted  | Get current location status | boolean       | no       | Android      | no                |
| setAllowsBackgroundLocationUpdates  | Whether to allow background location | void          | no       | iOS      | no                |
| setDesiredAccuracy  | Set desired location accuracy (meters) | void          | no       | iOS     | no                |
| setDistanceFilter  | Set minimum update distance for location (meters) | void          | no       | iOS     | yes               |
| setGeoLanguage  | Set language for reverse geocoding, currently supports Chinese and English | void          | no       | iOS/Android      | yes               |
| setGpsFirst  | Set whether to wait for satellite positioning results for first location | void          | no       | Android      | no                |
| setGpsFirstTimeout  | Set timeout for waiting satellite positioning results when prioritizing satellite location information (milliseconds) | void          | no       | Android      | no                |
| setHttpTimeout  | Set network timeout (milliseconds) | void          | no       | Android      | no                |
| setInterval  | Set time interval for location requests (milliseconds), default 2000, minimum 1000 | void          | no       | Android      | yes               |
| setLocatingWithReGeocode  | Whether continuous positioning returns reverse geocoding | void          | no       | iOS      | no                |
| setLocationCacheEnable  | Set whether to use cache strategy | void          | no      | Android     | no                |
| setLocationMode  | Set positioning mode | void          | no      | Android     | no                |
| setLocationPurpose  | Set positioning scenario | void          | no      | Android      | no                |
| setLocationTimeout  | Specify timeout for single location (seconds) | no          | yes      | iOS      | yes               |
| setMockEnable  | Set whether to allow mock location | void          | no      | Android      | no                |
| setNeedAddress  | Set whether to return address information, returns address information by default | no          | yes      | Android      | yes               |
| setOnceLocation  | Set whether to perform single location | void          | no      | Android      | yes               |
| setOnceLocationLatest  | Set whether location waits for WiFi list refresh | void          | no      | Android      | no                |
| setOpenAlwaysScanWifi  | Set whether to enable continuous WiFi scanning | void          | no      | Android     | no                |
| setPausesLocationUpdatesAutomatically  | Specify whether location will be automatically paused by the system | void          | no      | iOS      | no                |
| setReGeocodeTimeout  | Specify reverse geocoding timeout for single location (seconds), minimum 2s. Note: Set before single location request. | void          | no      | iOS     | no                |
| setSensorEnable  | Set whether to use device sensors | void          | no      | Android      | no                |
| setWifiScan  | Set whether to allow WiFi refresh calls | void          | no      | Android      | no                |
| start  | Start continuous location | void          | no      | iOS/Android      | yes               |
| stop  | Stop continuous location | void          | no      | iOS/Android      | yes               |
| Geolocation.getCurrentPosition  | Get current location information | void          | no      | iOS/Android        | yes               |
| Geolocation.watchPosition  | Register listener for continuous location | void          | no      | iOS/Android      | yes               |
| Geolocation.clearWatch  | Remove location listener | void          | no      | iOS/Android      | yes               |

## Known Issues

- [ ] isStarted() interface: Getting current location status is not supported on HarmonyOS [issue#2](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/2)
- [ ] setGpsFirst() interface: Not supported on HarmonyOS [issue#3](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/3)
- [ ] setGpsFirstTimeout() interface: Not supported on HarmonyOS [issue#4](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/4)
- [ ] setHttpTimeout() interface: Not supported on HarmonyOS [issue#5](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/5)
- [ ] setMockEnable() interface: Not supported on HarmonyOS [issue#6](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/6)
- [ ] setOnceLocationLatest() interface: Not supported on HarmonyOS [issue#7](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/7)
- [ ] setOpenAlwaysScanWifi() interface: Not supported on HarmonyOS [issue#8](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/8)
- [ ] setPausesLocationUpdatesAutomatically() interface: Not supported on HarmonyOS [issue#9](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/9)
- [ ] setReGeocodeTimeout() interface: Not supported on HarmonyOS [issue#10](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/10)
- [ ] setSensorEnable() interface: Not supported on HarmonyOS [issue#11](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/11)
- [ ] setWifiScan() interface: Not supported on HarmonyOS [issue#12](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/12)
- [ ] setLocationCacheEnable() interface: Not supported on HarmonyOS [issue#13](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/13)
- [ ] setLocationMode() interface: Not supported on HarmonyOS [issue#14](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/14)
- [ ] setLocationPurpose() interface: Not supported on HarmonyOS [issue#15](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/15)
- [ ] setLocatingWithReGeocode() interface: Setting whether continuous positioning returns reverse geocoding is not supported on HarmonyOS [issue#19](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/19)
- [ ] setDesiredAccuracy() interface: Setting desired positioning accuracy is not supported on HarmonyOS [issue#22](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/22)
- [ ] setAllowsBackgroundLocationUpdates() interface: Setting whether to allow background location is not supported on HarmonyOS [issue#23](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/23)


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/qiuxiang/react-native-amap-geolocation/blob/main/license).

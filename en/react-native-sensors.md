> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-sensors</code> </h1>
</p>

This project is based on [react-native-sensors@7.2.1-rc.2](https://github.com/react-native-sensors/react-native-sensors/tree/v7.2.1-rc.2).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-sensors`, The version correspondence details are as follows:

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 7.2.1@deprecated     | [@react-native-oh-library/react-native-sensors Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sensors/releases) | 0.72       |
| 7.2.3      | [@react-native-ohos/react-native-sensors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensors/releases) | 0.72       |
| 7.3.7      | [@react-native-ohos/react-native-sensors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensors/releases) | 0.77       |


## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-sensors
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-sensors
```

<!-- tabs:end -->

react-native-sensors is used as an example.

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { Alert } from "react-native";
import { Subscription } from "rxjs";
import { Button, View, Text, TextInput, StyleSheet } from 'react-native';
import { accelerometer, gyroscope, magnetometer, barometer, orientation, gravity, setUpdateIntervalForType, setLogLevelForType } from 'react-native-sensors';
export const App = () => {
    const [value, setValue] = React.useState('15');
    const [sensors, setSensorsValue] = React.useState('');
    const [IsProintLog, setIsProintLog] = React.useState(true);
    const setInterVal = () => {
        if(!sensors) return
        if (IsProintLog) {
            setUpdateIntervalForType(sensors, value);
            setIsProintLog(false)
            let sensorsSubscription: Subscription;
            switch (sensors) {
                case 'accelerometer':
                    sensorsSubscription = accelerometer.subscribe();
                    break;
                case 'gyroscope':
                    sensorsSubscription = gyroscope.subscribe();
                    break;
                case 'magnetometer':
                    sensorsSubscription = magnetometer.subscribe();
                    break;
                case 'barometer':
                    sensorsSubscription = barometer.subscribe();
                    break;
                case 'orientation':
                    sensorsSubscription = orientation.subscribe();
                    break;
                case 'gravity':
                    sensorsSubscription = gravity.subscribe();
                    break;
                default:
            }
            const timer = setTimeout(() => {
                sensorsSubscription.unsubscribe();
                clearTimeout(timer)
                setIsProintLog(true)
            }, 5000);
        }
    }
    const setLogLevel0 = () => {
        setLogLevelForType(sensors, 0)
    }
    const setLogLevel1 = () => {
        setLogLevelForType(sensors, 1)
    }
    const setLogLevel2 = () => {
        setLogLevelForType(sensors, 2)
    }
    const handleChangeText = (text:string) => {
        if (!text) {
            Alert.alert('Please enter the interval time and it cannot be empty!');
            return
        }
        const numericValue = text.replace(/[^0-9]/g, "");
        setValue(numericValue);
    }
    const styles = StyleSheet.create({
        divider: {
            height: 1,
            backgroundColor: '#CCCCCC',
            marginVertical: 5,
        }
    })
    return (
        <View>
            <Text>Operation process: 1. Enter the interval time 2. Select the sensor type 3. Select the output log level 4. Click the log print button. Please ensure that the equipment is supported</Text>
            <View style={styles.divider}></View>
            <Text>setUpdateIntervalForType Set the data collection frequency</Text>
            <TextInput style={{ height: 40, borderColor: 'gray', borderWidth: 1 }} keyboardType="numeric" onChangeText={handleChangeText} value={value} placeholder="The unit is ms"></TextInput>
            <Button onPress={() => { setSensorsValue('accelerometer') }} title="accelerometer"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('gyroscope') }} title="gyroscope"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('magnetometer') }} title="magnetometer"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('barometer') }} title="barometer"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('orientation') }} title="orientation"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('gravity') }} title="gravity"></Button>
            <View style={styles.divider}></View>
            <View style={{ display: 'flex', justifyContent: 'space-around', flexDirection: 'row' }}>
                <View style={{ width: '25%', flex: 1 }}><Button onPress={setLogLevel0} title="Set the logLevel level to 0"></Button></View>
                <View style={{ width: '25%', flex: 1 }}><Button onPress={setLogLevel1} title="Set the logLevel level to 1"></Button></View>
                <View style={{ width: '25%', flex: 1 }}><Button onPress={setLogLevel2} title="Set the logLevel level to 2"></Button></View>
            </View>
            <Button disabled={!IsProintLog} onPress={setInterVal} title="setUpdateIntervalForType log printing"></Button>
        </View>
    )
}
export default App;
```

## 2. Manual Link

Version >= @react-native-ohos/react-native-sensors@7.2.3 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-sensors": "file:../../node_modules/@react-native-ohos/react-native-sensors/harmony/sensors.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 2.3 Configuring CMakeLists and Introducing SensorsPackage Package

> **[!TIP] Version 7.2.2 and above requires.**

Open entry/src/main/cpp/CMakeLists.txt and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-sensors/src/main/cpp" ./sensors)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_sensors)
# RNOH_END: manual_package_linking_2
```

Open entry/src/main/cpp/PackageProvider.cpp and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SensorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<SensorsPackage>(ctx)
    };
}
```

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SensorsPackage} from '@react-native-ohos/react-native-sensors/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SensorsPackage(ctx)
  ];
}
```

### 2.4 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

### 3.2 Permission Requirements (If Any)

Configure the required permissions in module. json 5

accelerometer Required permissions: ohos.permission.ACCELEROMETER

gyroscope Required permissions: ohos.permission.GYROSCOPE

## 4. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description  | Type       | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------ | ---------- | -------- | ----------- | ----------------- |
| accelerometer            | accelerometer     | Observable | no       | ios/Android | yes               |
| gyroscope                | gyroscope       | Observable | no       | ios/Android | yes               |
| magnetometer             | magnetometer       | Observable | no       | ios/Android | yes               |
| barometer                | barometer       | Observable | no       | ios/Android | yes               |
| orientation              | orientation         | Observable | no       | ios/Android | yes               |
| gravity                  | gravity         | Observable | no       | ios/Android | yes               |
| setUpdateIntervalForType | setUpdateIntervalForType     | function   | no       | ios/Android | yes               |
| setLogLevelForType       | setLogLevelForType | function   | no       | ios/Android | yes               |

## 5. Known Issues


## 6. License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-sensors/react-native-sensors/blob/master/LICENSE), Please enjoy and participate freely in open source.
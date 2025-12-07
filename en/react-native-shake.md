> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shake</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Doko-Demo-Doa/react-native-shake">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Doko-Demo-Doa/react-native-shake/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-shake)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 5.6.2-0.0.1@deprecated  | [@react-native-oh-tpl/react-native-shake Releases(deprecated)](https://github.com/react-native-oh-library/react-native-shake/releases) | 0.72       |
| 5.6.3             | [@react-native-ohos/react-native-shake Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-shake/releases)           | 0.72       |
| 6.0.2             | [@react-native-ohos/react-native-shake Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-shake/releases)           | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-shake
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-shake
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from 'react';
import { Text, View, StyleSheet } from 'react-native'
import RNShake from 'react-native-shake';

export function ShakeExample() {
    const [result, setResult] = useState<string>('')
    myComponent(setResult)
    return (
      <View style={styles.container}>
      <Text style={styles.title}>shake（摇晃手机）</Text>
      <Text style={styles.resultText}>{result}</Text>
  </View>
    )
}

export const myComponent = (setResult: React.Dispatch<React.SetStateAction<string>>) => {
    React.useEffect(() => {
        const subscription = RNShake.addListener(() => {
            setResult('shake listen success')
        })
        return () => {
            subscription.remove()
        }
    }, [])
}

const styles = StyleSheet.create({
  container: {
      flex: 1,
      backgroundColor: 'white',
      width: '100%',
      justifyContent: 'center',
      alignItems: 'center',
      padding: 20
  },
  title: {
      fontSize: 18,
      fontWeight: 'bold',
      marginBottom: 15,
      textAlign: 'center'
  },
  resultText: {
      fontSize: 16,
      color: '#2196F3',
      textAlign: 'center',
      marginTop: 10
  }
});
```

## Link

Version >= @react-native-ohos/react-native-shake@5.6.3 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

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
    "@react-native-ohos/react-native-shake": "file:../../node_modules/@react-native-ohos/react-native-shake/harmony/shake_package.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).。

### 3. Introducing ShakePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+ import { ShakePackage } from "@react-native-ohos/react-native-shake/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ShakePackage(ctx)
  ];
}
```

### 4. Configure CMakeLists and import ShakePackge

> If you are using version <=  5.6.2-0.0.1, please skip this chapter.

open `entry/src/main/cpp/CMakeLists.txt`，add：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-shake/src/main/cpp" ./shake_package)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_shake)
# RNOH_END: link_packages
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ShakePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ShakePackage>(ctx)
    };
}
```

### 5. Running

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

此库接口需要 normal 权限：ohos.permission.ACCESS_BLUETOOTH，权限需配置在 entry/src/main 目录下 module.json5 文件中

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCELEROMETER"
      }
    ]
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description               | Type     | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------- | -------- | -------- | ----------- | ----------------- |
| addListener        | add shake event listening | function | yes      | ios/andriod | yes               |
| removeAllListeners | remove event listening    | function | yes      | ios/andriod | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Doko-Demo-Doa/react-native-shake/blob/main/LICENSE).

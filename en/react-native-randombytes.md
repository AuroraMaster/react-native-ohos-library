> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-randombytes</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mvayngrib/react-native-randombytes">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mvayngrib/react-native-randombytes/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-randombytes)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-------| ------------------------------------------------------------ | ---------- |
| <= 3.6.1-0.0.4@deprecated   | [@react-native-oh-tpl/react-native-randombytes Releases(deprecated)](https://github.com/react-native-oh-library/react-native-randombytes/releases) | 0.72                 |
| 3.6.2 | [@react-native-ohos/react-native-randombytes Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-randombytes/releases)                        | 0.72       |
| 3.7.0 | [@react-native-ohos/react-native-randombytes Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-randombytes/releases)                        | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-randombytes
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-randombytes
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```tsx

import React, { useState } from "react";
import { Text, TouchableOpacity, View, TextInput, StyleSheet } from 'react-native';
import { randomBytes } from 'react-native-randombytes';

export default function randomBytesDemo(): JSX.Element {

    const [bytesString, setBytesString] = useState('');
    const [size, setSize] = useState('30');

    const nativeRandom = () => {
        randomBytes(Number(size), (err: any, bytes: any) => {
            setBytesString(JSON.stringify(bytes))
            console.log(err);       
        })
    }

    const jsRandom = () => {
        const bytes = randomBytes(Number(size))
        setBytesString(JSON.stringify(bytes))
    }

    return <View>
        <Text>
            {bytesString}
        </Text>

        <TextInput style={styles.TextInput} value={size} onChangeText={(s) => {
            setSize(s);
        }}></TextInput>
        <TouchableOpacity onPress={nativeRandom} style={styles.btn}>
        <Text
          style={styles.btnText}>
          Native RandomBytes
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={jsRandom} style={styles.btn}>
        <Text
          style={styles.btnText}>
          RandomBytes
        </Text>
      </TouchableOpacity>
    </View>
}

const styles = StyleSheet.create({
  TextInput: { height: 40, borderColor: '#ccc', borderWidth: 1, borderRadius: 4, width: '90%' },
  btn: { borderRadius: 10, display: 'flex', justifyContent: 'center', alignItems: 'center', padding: 10, margin: 10, backgroundColor: 'blue' },
  btnText: { fontWeight: 'bold', color: '#fff', fontSize: 20 }
});

```

## Use Codegen

Version >= @react-native-ohos/react-native-randombytes@3.6.2, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-randombytes@3.6.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
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
    "@react-native-ohos/react-native-randombytes": "file:../../node_modules/@react-native-ohos/react-native-randombytes/harmony/random_bytes.har"
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

### 3. Configuring CMakeLists and Introducing RandomBytesPackage

> If you are using version <= 3.6.1-0.0.4, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-randombytes/src/main/cpp" ./random_bytes)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_randombytes)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RandomBytesPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RandomBytesPackage>(ctx)
    };
}
```

### 4. Introducing RandomBytesPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RandomBytesPackage } from '@react-native-ohos/react-native-randombytes/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RandomBytesPackage(ctx)
  ];
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

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-randombytes](https://gitcode.com/openharmony-sig/rntpc_react-native-randombytes)

| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| randombytes    | generate secure random numbers. | function | No       | IOS/Android | yes               |
| seedSJCL       | Add entropy to the pools.       | function | No       | IOS/Android | yes               |


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mvayngrib/react-native-randombytes/blob/master/LICENSE).


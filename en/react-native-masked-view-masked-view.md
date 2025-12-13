> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-masked-view/masked-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-masked-view/masked-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-masked-view/masked-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github address](https://github.com/react-native-oh-library/masked-view)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 0.2.9-0.2.2@deprecated   | [@react-native-oh-tpl/masked-view Releases(deprecated)](https://github.com/react-native-oh-library/masked-view/releases) | 0.72                 |
| 0.2.11      | [@react-native-ohos/masked-view Releases](https://gitcode.com/openharmony-sig/rntpc_masked-view/releases)                        | 0.72       |
| 0.3.3      | [@react-native-ohos/masked-view Releases](https://gitcode.com/openharmony-sig/rntpc_masked-view/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/masked-view
```

#### **yarn**

```bash
yarn add @react-native-ohos/masked-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { StyleSheet, Text, View } from 'react-native';
import MaskedView from '@react-native-masked-view/masked-view';

const MaskedDemo = () => {
    return (
        <MaskedView
            style={styles.maskedView}
            maskElement={
                <View style={styles.maskElementView}>
                    <Text style={styles.maskElementText}>Basic Mask</Text>
                </View>
            }
        > 
        <View style={{ width:'100%', height: 40, backgroundColor: '#fe4b83' }} />
        <View style={{ width:'100%', height: 40, backgroundColor: '#F5DD90' }} />
        </MaskedView>
    )
}

const styles = StyleSheet.create({
    maskedView: {
        width:'100%',
        height:'40%'
    },
    maskElementView: {
        backgroundColor: 'transparent',
        alignItems: 'center',
        width:'100%',
        height:'100%',
        justifyContent: 'center',
    },
    maskElementText: {
        color: Colors.black,
        width:'100%',
        height:60,
        fontSize: 50,
        fontWeight: 'bold',
    },
    textView: {
        fontSize: 20,
        alignItems: 'center',
        width:'100%',
        height:40,
        flexDirection: 'row',
        justifyContent: 'center',
    },
    text: {
        color: Colors.darkChestnut,
        fontSize: 8,
        width:'100%',
        height:40,
        fontVariant: ['small-caps'],
        fontWeight: 'bold',
    },
});

export default MaskedDemo
```

## Link

|                                      | Is supported autolink | Supported RN Ve
|--------------------------------------|------------------|------------|
| ~0.3.3                               |  No              |  0.77     |
| ~0.2.11                              |  Yes             |  0.72     |
| <= 0.2.9-0.2.2@deprecated            |  No              |  0.72     |

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

    "@react-native-ohos/masked-view": "file:../../node_modules/@react-native-ohos/masked-view/harmony/masked_view.har"
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

### 3. Configuring CMakeLists and Introducing MaskedPackage

> If you are using version <= 0.2.9-0.2.2, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/masked-view/src/main/cpp" ./masked-view)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_masked_view)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "MaskedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<MaskedPackage>(ctx),
    };
}
```

### 4. Introducing MaskedPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {MaskedPackage} from '@react-native-ohos/masked-view/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new MaskedPackage(ctx)
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

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description  | Type               | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------ | ------------------ | -------- | -------- | ----------------- |
| `maskElement`          | 遮罩元素     | element            | yes      | All      | yes               |
| `androidRenderingMode` | 安卓渲染模式 | software, hardware | no       | android  | no                |

## Known Issues


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-masked-view/masked-view/blob/master/LICENSE).

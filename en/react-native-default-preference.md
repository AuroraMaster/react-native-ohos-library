> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-default-preference</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kevinresol/react-native-default-preference">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kevinresol/react-native-default-preference/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-default-preference)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                          | Supported RN Version |
| --------------------------- | ------------------------------------------------------------ | -------------------- |
| <= 1.4.4-0.0.1@deprecated      | [@react-native-oh-tpl/react-native-default-preference Releases](https://github.com/react-native-oh-library/react-native-default-preference/releases) | 0.72       |
| 1.4.5      | [@react-native-ohos/react-native-default-preference Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-default-preference/releases)     | 0.72       |
| 1.5.0      | [@react-native-ohos/react-native-default-preference Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-default-preference/releases) | 0.77       |


For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash

npm install @react-native-ohos/react-native-default-preference
```

#### **yarn**

```bash

yarn add @react-native-ohos/react-native-default-preference
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { Text, View } from "react-native";
import DefaultPreference from 'react-native-default-preference';

const App = () => {
    const handleSetItem = useCallback((key: string, value:  string) => {
        RNDefaultPreference.set(key, value)
    }, []);

    const handleGetItem = useCallback((key: string) => {
        RNDefaultPreference?.get(key).then(res => {
            console.log(res)
        });
    }, []);
  return (
      <View>
        <Button onPress={async () => { handleSetItem('key1', 'value1') }} title={'Add item using setItem'}></Button>
        <Button onPress={async () => { handleGetItem('key1') }} title={'Add item using setItem'}></Button>
     </View>
  );
};

export default App;
```

## Use Codegen

Version >= @react-native-ohos/react-native-default-preference@1.4.5, compatible with codegen-lib for generating bridge code.


If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-default-preference@1.4.5 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
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

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-default-preference": "file:../../node_modules/@react-native-ohos/react-native-default-preference/harmony/react_native_default_preference.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configure CMakeLists and introduce DefaultPreferencePackage

> If you are using version <= 1.4.4-0.0.1, please skip this chapter.

Open the `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-default-preference/src/main/cpp" ./default_preference)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_default_preference)
# RNOH_END: manual_package_linking_2
```

Open the `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "DefaultPreferencePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<DefaultPreferencePackage>(ctx),
    };
}
```

### 4. Introducing RNDefaultPreferencePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import { RNDefaultPreferencePackage } from '@react-native-ohos/react-native-default-preference/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNDefaultPreferencePackage(ctx)
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

| Name          | Description                                | Type     | Required | Platform     | HarmonyOS Support |
| ------------- | ------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| get           | Take out key-value pairs                   | function | yes      | Android、iOS | yes               |
| set           | Set key-value pairs                        | function | yes      | Android、iOS | yes               |
| clear         | Clear key-value pairs                      | function | yes      | Android、iOS | yes               |
| getMultiple   | Take out multiple key-value pairs          | function | yes      | Android、iOS | yes               |
| setMultiple   | Set multiple key-value pairs               | function | yes      | Android、iOS | yes               |
| clearMultiple | Clear multiple key-value pairs             | function | yes      | Android、iOS | yes               |
| getAll        | Take out all key-value pairs               | function | no       | Android、iOS | yes               |
| clearAll      | Clear all key-value pairs                  | function | no       | Android、iOS | yes               |
| getName       | Gets the name of the Preferences instance. | function | no       | Android、iOS | yes               |
| setName       | Sets the name of the Preferences instance. | function | yes      | Android、iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/kevinresol/react-native-default-preference/blob/master/LICENSE).

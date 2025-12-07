> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>@remobile/react-native-toast</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-toast).

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                  | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.0.7-0.0.3@deprecated      | [@react-native-oh-tpl/react-native-toast Releases(deprecated)](https://github.com/react-native-oh-library/react-native-toast/releases) | 0.72       |
| 1.0.8      | [@react-native-ohos/react-native-toast Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-toast/releases)    | 0.72       |
| 1.1.0      | [@react-native-ohos/react-native-toast Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-toast/releases)    | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-toast
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-toast
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, {Component} from 'react';
import {Text, View, Button} from 'react-native';
import Toast from '@remobile/react-native-toast';

function ToastMasterDemo() {
    return (
        <View style={{flex: 2, justifyContent: 'center', alignItems: 'center'}}>
            <Text>Tosat !</Text>
            <Button
                title={'show toast'}
                onPress={() => {
                    Toast.show('This is a toast.');
                }}
            />
            <Button
                title={'short top toast'}
                onPress={() => {
                    Toast.showShortTop('This is a top toast.');
                }}
            />
            <Button
                title={'short center toast'}
                onPress={() => {
                    Toast.showShortCenter('This is a center toast.');
                }}
            />
            <Button
                title={'short bottom toast'}
                onPress={() => {
                    Toast.showShortBottom('This is a bottom toast.');
                }}
            />
            <Button
                title={'long top toast'}
                onPress={() => {
                    Toast.showLongTop('This is a long top toast.');
                }}
            />
            <Button
                title={'long center toast'}
                onPress={() => {
                    Toast.showLongCenter('This is a long center toast.');
                }}
            />
            <Button
                title={'long bottom toast'}
                onPress={() => {
                    Toast.showLongBottom('This is a long bottom toast.');
                }}
            />
        </View>
    );
}

export default ToastMasterDemo;

```

## Use Codegen

Version >= @react-native-ohos/react-native-toast@1.0.8, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-toast@1.0.8 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

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
"@react-native-ohos/react-native-toast": "file:../../node_modules/@react-native-ohos/react-native-toast/harmony/rn_toast.har"
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

### 3. Introducing  ToastPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ToastPackage} from '@react-native-ohos/react-native-toast/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ToastPackage(ctx)
  ];
}
```

### 4. Configure CMakeLists and import ToastPackage

> If you are using version <= 1.0.7-0.0.3, please skip this chapter.

open `entry/src/main/cpp/CMakeLists.txt`，add：

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-toast/src/main/cpp" ./rn_toast)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_toast)
# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ToastPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ToastPackage>(ctx),
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


## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |----------| -------- | ------------------ |
| show()  | Displays the location of the toast, its duration, the content of the message | function  | no      | android      | yes |
| showShortTop()  | Display the top Toast for a short time | function  | no      | android      | yes |
| showShortCenter()  | Display the center Toast for a short time | function  | no      | android      | yes |
| showShortBottom()  | Display the bottom Toast for a short time | function  | no      | android      | yes |
| showLongTop()  | Display the top Toast for a long time | function  | no      | android      | yes |
| showLongCenter()  | Display the center Toast for a long time | function  | no      | android      | yes |
| showLongBottom()  | Display the bottom Toast for a long time | function  | no      | android      | yes |
| hide()  | Hide the toast that is being displayed         | function  | no       | android      | no |

## Known Issues

- [ ] Does not support hide() function to hide toast:[issue#3](https://github.com/react-native-oh-library/react-native-toast/issues/3)

## Others

## License

This project is licensed under [The MIT License](https://github.com/remobile/react-native-toast/blob/master/LICENSE).

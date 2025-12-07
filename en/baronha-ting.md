> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@baronha/ting</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/<Original library source repository address>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/baronha/ting/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github Address](https://github.com/react-native-oh-library/ting)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.2.2-0.0.3@deprecated  | [@react-native-oh-tpl/ting Releases(deprecated)](https://github.com/react-native-oh-library/ting/releases) | 0.72       |
| 1.2.3             | [@react-native-ohos/ting Releases](https://gitcode.com/openharmony-sig/rntpc_ting/releases)   | 0.72       |
| 1.3.0             | [@react-native-ohos/ting Releases](https://gitcode.com/openharmony-sig/rntpc_ting/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/ting
```

#### **yarn**

```bash
yarn add @react-native-ohos/ting
```

<!-- tabs:end -->

The following code demonstrates basic usage scenarios of this library:

> [!WARNING] The library name in the import statement remains unchanged.

```js
import { View, Button } from "react-native";
import {
    ToastOptions,
    toast
} from '@baronha/ting';

function handleToast(options: ToastOptions) {
    toast(options);
}

const App = () => {
  return (
    <View style={{ justifyContent: 'center', alignItems: 'center', flex: 1 }}>
      <Button
        title="defalut"
        onPress={() => {
          const options: ToastOptions = {
            title: 'title-Toast',
            message: 'message-Toast',
          };
          handleToast(options);
        }}
      />
    </View>
  );
};

export default App;
```

## Using Codegen

Version >= @react-native-ohos/ting@1.2.3, compatible with codegen-lib for generating bridge code.

This library has been adapted for `Codegen`. Before use, you need to actively generate the third-party library bridging code. Please refer to the [Codegen Usage Documentation](/en/codegen.md) for details.

## Link

Version >= @react-native-ohos/ting@1.2.3 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

First, use DevEco Studio to open the HarmonyOS project `harmony` within your project.

### 1. Add the overrides field to the root `oh-package.json5`

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Import Native Code

There are currently two methods:

1. Import via har package (This method will be deprecated after IDE features are improved; currently the preferred method);
2. Link source code directly.

Method 1: Import via har package (Recommended)

> [!TIP] The har package is located in the `harmony` folder of the third-party library installation path.

Open `entry/oh-package.json5` and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/ting": "file:../../node_modules/@react-native-ohos/ting/harmony/ting.har"
}
```

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link Source Code Directly

> [!TIP] If you need to link source code directly, please refer to the [Direct Link Source Code Instructions](/en/link-source-code.md).

### 3. Configure CMakeLists and Import RNTingPackage

> If you are using version <=1.2.2-0.0.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/Ting/src/main/cpp" ./ting)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_ting)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
+ #include "TingPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<TingPackage>(ctx)
}
```

### 4. Import RNTingPackage on the ArkTs Side

Open `entry/src/main/ets/RNPackagesFactory.ets` and add:

```diff
  ...
+ import {RNTingPackage} from '@react-native-ohos/ting';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTingPackage(ctx)
  ];
}
```

### 5. Run

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## Constraints and Limitations

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### ToastOptions

| Name                | Description                                                                                                                    | Type    | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| title               | The text for the toast’s title                                                                                                 | string  | no       | All      | yes               |
| message             | The text for the toast’s message                                                                                               | string  | no       | All      | yes               |
| titleColor          | The color of the title text in hexadecimal format                                                                              | string  | no       | All      | yes               |
| messageColor        | The color of the message text in hexadecimal format                                                                            | string  | no       | All      | yes               |
| preset              | The preset style of the toast. Options include done (success), error (error), none (no style), or spinner (loading spinner)    | string  | no       | All      | partially         |
| duration            | The lifetime of the toast (seconds)                                                                                            | number  | no       | All      | yes               |
| haptic              | The type of haptic feedback. Options include success (success), warning (warning), error (error), or none (no haptic feedback) | string  | no       | iOS      | yes               |
| shouldDismissByDrag | Whether the toast can be dismissed by dragging                                                                                 | boolean | no       | All      | yes               |
| position            | Toast is displayed from top or bottom                                                                                          | string  | no       | All      | yes               |
| backgroundColor     | The background color of the toast in hexadecimal format                                                                        | string  | no       | All      | yes               |
| icon                | A custom icon for the toast                                                                                                    | object  | no       | All      | yes               |
| progressColor       | The color of the progress spinner for the spinner preset style                                                                 | string  | no       | Android  | yes               |

### AlertOptions

| Name               | Description                                                                                                                    | Type    | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| title              | The text for the toast’s title                                                                                                 | string  | no       | All      | yes               |
| message            | The text for the toast’s message                                                                                               | string  | no       | All      | yes               |
| titleColor         | The color of the title text in hexadecimal format                                                                              | string  | no       | All      | yes               |
| messageColor       | The color of the message text in hexadecimal format                                                                            | string  | no       | All      | yes               |
| preset             | The preset style of the toast. Options include done (success), error (error), none (no style), or spinner (loading spinner)    | string  | no       | All      | partially         |
| duration           | The lifetime of the toast (seconds)                                                                                            | number  | no       | All      | yes               |
| haptic             | The type of haptic feedback. Options include success (success), warning (warning), error (error), or none (no haptic feedback) | string  | no       | iOS      | yes               |
| shouldDismissByTap | Whether the toast can be dismissed by tapping                                                                                  | boolean | no       | All      | yes               |
| backgroundColor    | The background color of the toast in hexadecimal format                                                                        | string  | no       | All      | yes               |
| borderRadius       | The border radius of the toast box, which determines how rounded the corners are                                               | number  | no       | All      | yes               |
| blurBackdrop       | The intensity of the background blur effect on Android platforms                                                               | number  | no       | Android  | no                |
| backdropOpacity    | The opacity of the background blur effect on Android platforms, with a range from 0 (fully transparent) to 1 (fully opaque)    | number  | no       | All      | yes               |
| icon               | A custom icon for the toast                                                                                                    | object  | no       | All      | yes               |
| progressColor      | The color of the progress spinner for the spinner preset style                                                                 | string  | no       | Android  | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                    | Type     | Required | Platform | HarmonyOS Support |
| ------------ | ---------------------------------------------- | -------- | -------- | -------- | ----------------- |
| toast        | Displays a Toast notification                  | function | yes      | All      | yes               |
| alert        | Displays an Alert dialog                       | function | yes      | All      | yes               |
| dismissAlert | Closes the currently displayed Alert dialog    | function | yes      | All      | yes               |
| setup        | Configures global settings for Toast and Alert | function | yes      | All      | yes               |

## Known Issues

- [ ] preset in AlertOptions and ToastOptions: The animation effect for 'done' is not implemented. [issue#3](https://github.com/react-native-oh-library/ting/issues/3)

## Others

- After configuring the blurBackdrop parameter in AlertOptions, it is not supported on iOS and has no effect on Android.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/baronha/ting/blob/main/LICENSE).

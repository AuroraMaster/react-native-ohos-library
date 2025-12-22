> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-context-menu-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mpiannucci/react-native-context-menu-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mpiannucci/react-native-context-menu-view/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-context-menu-view)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
|-----------------------------| ------------------------------------------------------------ | ---------- |
| <= 1.16.0-0.0.6@deprecated | [@react-native-oh-tpl/react-native-context-menu-view Releases(deprecated)](https://github.com/react-native-oh-library/react-native-context-menu-view/releases) | 0.72       |
| 1.16.1               | [@react-native-ohos/react-native-context-menu-view Releases](https://github.com/react-native-oh-library/react-native-context-menu-view/releases)               | 0.72       |
| 1.19.1               | [@react-native-ohos/react-native-context-menu-view Releases](https://github.com/react-native-oh-library/react-native-context-menu-view/releases)               | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-context-menu-view
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-context-menu-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import ContextMenu from "react-native-context-menu-view";

const Example = () => {
  return (
    <ContextMenu
      actions={[{ title: "Title 1" }, { title: "Title 2" }]}
      onPress={(e) => {
        console.warn(
          `Pressed ${e.nativeEvent.name} at index ${e.nativeEvent.index}`
        );
      }}
    >
      <View style={styles.yourOwnStyles} />
    </ContextMenu>
  );
};
```

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.19.1                              |  No                   |  0.77                |
| ~1.16.1                              |  Yes                  |  0.72                |
| <= 1.16.0-0.0.6@deprecated           |  No                   |  0.72                |

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
    "@react-native-ohos/react-native-context-menu-view": "file:../../node_modules/@react-native-ohos/react-native-context-menu-view/harmony/context_menu.har"
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

### 3. Configuring CMakeLists and Introducing ContextMenuPackage

> If you are using version <= 1.16.0-0.0.6, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-context-menu-view/src/main/cpp" ./context_menu)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_context_menu)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ContextMenuPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ContextMenuPackage>(ctx),
    };
}
```

### 4. Introducing ContextMenuPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ContextMenuPackage} from '@react-native-ohos/react-native-context-menu-view/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ContextMenuPackage(ctx)
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

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                                  | Type     | Required | Platform               | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | -------- | -------- | ---------------------- | ----------------- |
| title                  | The title above the popup menu.                              | string   | no       | Android/iOS            | yes               |
| actions                | Menu props.                                                  | array    | no       | Android(partially)/iOS | partially         |
| previewBackgroundColor | The background color of the preview.                         | string   | no       | NA                     | no                |
| dropdownMenuMode       | When set to true, the context menu is triggered with a single tap instead of a long press. | boolean  | no       | Android/iOS            | yes               |
| disabled               | Disable menu interaction.                                    | boolean  | no       | Android/iOS            | yes               |
| onPress                | When the popup is opened and the user picks an option.       | callback | no       | Android/iOS            | yes               |
| onPreviewPress         | When the context menu preview is tapped.                     | callback | no       | iOS                    | no                |
| onCancel               | When the popup is opened and the user cancels.               | callback | no       | Android/iOS            | yes               |

## actions

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                                                                                    | Type    | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| title          | the title of the action                                                                                                        | string  | no       | Android/iOS | yes               |
| subtitle       | the subtitle of the action                                                                                                     | string  | no       | iOS 15+     | yes               |
| systemIcon     | refers to an icon name within [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/overview/) | string  | no       | iOS         | yes               |
| icon           | Custom Icons.                                                                                                                  | string  | no       | Android/iOS | yes               |
| iconColor      | will change the color of the icon provided to the `icon` prop and has no effect on `systemIcon` (default: black)               | string  | no       | Android/iOS | yes               |
| destructive    | items are rendered in red                                                                                                      | boolean | no       | iOS         | yes               |
| selected       | items have a checkmark next to them                                                                                            | boolean | no       | iOS         | yes               |
| disabled       | marks whether the action is disabled or not                                                                                    | boolean | no       | Android/iOS | yes               |
| inlineChildren | marks whether its children (if any) should be rendered inline instead of in their own child menu                               | boolean | no       | iOS         | partially         |
| actions        | will provide a one level deep nested menu                                                                                      | array   | no       | Android/iOS | partially         |

## Known Issues

## Others

1. The **previewBackgroundColor** property does not take effect on iOS and Android devices.

2. The **actions** property is a struct function and contains other properties listed above, such as **previewBackgroundColor**. Therefore, it is partially supported.

3. The specific logic implementation of the library is to call the corresponding bottom-layer **Menu** API of the OS to perform related operations. Therefore, the animation display varies depending on the OS.

4. The **onPress** callback is as follows: **{ nativeEvent: { index, indexPath, name } }**.

5. When both **systemIcon** and **icon** are configured, **systemIcon** is at a higher priority than **icon** on Harmony Next.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mpiannucci/react-native-context-menu-view/blob/main/LICENSE).

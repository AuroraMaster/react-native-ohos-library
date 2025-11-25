> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/progress-bar-android</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-progress-view/progress-bar-android">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-progress-view/progress-bar-android/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/progress-bar-android)

Please check the corresponding version information at the third-party library's Releases page:

| Library Version	 | Release Info                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.0.4      | [@react-native-oh-tpl/progress-bar-android Releases](https://github.com/react-native-oh-library/progress-bar-android/releases) | 0.72       |
| 1.1.0      | @react-native-ohos/progress-bar-android Releases             | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Enter the project directory and execute the following command:

<!-- tabs:start -->

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/progress-bar-android
# 0.77
yarn add @react-native-ohos/progress-bar-android
```

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/progress-bar-android
# 0.77
npm install @react-native-ohos/progress-bar-android
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { ProgressBar } from '@react-native-community/progress-bar-android';
export default function ProgressBarExample() {
    return (
        <>
            <ProgressBar styleAttr="Horizontal" indeterminate={true} animating={true} />
            <ProgressBar indeterminate={true} />
        </>
    )
}

```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```diff
{
  ...
+ "overrides": {
+  "@rnoh/react-native-openharmony" : "./react_native_openharmony"
+  "@ohos/materialprogressbar": "2.0.3-rc.0"    
+  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

* 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/progress-bar-android": "file:../../node_modules/@react-native-oh-tpl/progress-bar-android/harmony/progress_bar_android.har"
  }
```

* 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/progress-bar-android": "file:../../node_modules/@react-native-ohos/progress-bar-android/harmony/progress_bar_android.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing ProgressBarAndroidPackage

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
# 0.72
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/progress-bar-android/src/main/cpp" ./progress-bar-android)
# 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/progress-bar-android/src/main/cpp" ./progress-bar-android)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_progress_bar_android)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ProgressBarAndroidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ProgressBarAndroidPackage>(ctx)
    };
}
```

### 4.Introducing ProgressBarAndroid Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
# 0.72
+ import { ProgressBarAndroid, PROGRESS_BAR_TYPE } from "@react-native-oh-tpl/progress-bar-android"
# 0.77
+ import { ProgressBarAndroid, PROGRESS_BAR_TYPE } from "@react-native-ohos/progress-bar-android"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === PROGRESS_BAR_TYPE){
+     ProgressBarAndroid({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag
+     })
+   }
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
+ PROGRESS_BAR_TYPE
  ];
```

### 5.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK; IDE：DevEco Studio  6.0.0.868; ROM： 6.0.0.112;


## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                                                                                                                                         | Type                                                                                                                       | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `animating`     | Whether to show the ProgressBar (true, the default) or hide it (false).                                                                             | bool                                                                                                                       | No       | Android  | yes               |
| `color`         | Color of the progress bar.                                                                                                                          | [color](https://reactnative.dev/docs/colors)                                                                               | No       | Android  | yes               |
| `indeterminate` | If the progress bar will show indeterminate progress. Note that this can only be false if styleAttr is Horizontal, and requires a `progress` value. | indeterminateType                                                                                                          | No       | Android  | yes               |
| `progress`      | The progress value (between 0 and 1).                                                                                                               | number                                                                                                                     | No       | Android  | yes               |
| `styleAttr`     | Style of the ProgressBar.                                                                                                                           | One of:<br />Horizontal <br />Normal (default) <br />Small <br />Large <br />Inverse <br />SmallInverse <br />LargeInverse | No       | Android  | yes               |

## Known Issues

- [x] When styleAttr is set to Horizontal, the component cannot fill the entire screen.[issues#4](https://github.com/react-native-oh-library/progress-bar-android/issues/4)。

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-progress-view/progress-bar-android/blob/master/LICENSE).

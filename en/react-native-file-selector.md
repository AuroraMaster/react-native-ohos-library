> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-selector</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/prscX/react-native-file-selector">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/prscX/react-native-file-selector/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-file-selector)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
|<= 1.0.2-0.0.3@deprecated | [@react-native-oh-tpl/react-native-file-selector Releases(deprecated)](https://github.com/react-native-oh-library/react-native-file-selector/releases) | 0.72       |
| 1.0.3 | [@react-native-ohos/react-native-file-selector Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-selector/releases)                        | 0.72       |
| 1.1.0 | [@react-native-ohos/react-native-file-selector Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-selector/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-ohos/react-native-file-selector
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-file-selector
```


The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import FileSelector from 'react-native-file-selector';
import React from 'react';
function App(): React.JSX.Element {
  
  return (
    <FileSelector
      onDone={(path) => {console.log("file selected: " + path);}}
      onCancel={() => {console.log("cancelled");}}
    />)
};
export default App;
```

## Use Codegen


This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.1.0                               |  No                   |  0.77                |
| ~1.0.3                               |  Yes                  |  0.72                |
| <= 1.0.2-0.0.3@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. (Recommended) Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-ohos/react-native-file-selector": "file:../../node_modules/@react-native-ohos/react-native-file-selector/harmony/file_selector.har"
  }
```
Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see[Directly Linking Source Code](/en/link-source-code.md)


### 3.Introducing RNFileSelectorPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNFileSelectorPackage}  from '@react-native-ohos/react-native-file-selector/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNFileSelectorPackage(ctx)
  ];
}
```

### 4.Configuring CMakeLists and Introducing FileSelectorPackage

> If you are using version <= 1.0.2-0.0.3, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-file-selector/src/main/cpp" ./file-selector)


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
+ target_link_libraries(rnoh_app PUBLIC rnoh_file_selector)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FileSelectorPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FileSelectorPackage>(ctx),
    };
}
```
</details>

## Running

Click the sync button in the upper right corner.

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

 FileSelector

| Name              | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| :---------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| filter            | Filter to sort the files                                     | string | no       | All         | yes               |
| path              | Path of directory                                            | string | no       | All         | yes               |
| onDone            | Function called when file is selected                        | func   | no       | All         | yes               |
| onCancel          | Function called when file selector is closed without selecting any file | func   | no       | All         | yes               |
| title             | Title on the toolbar                                         | string | no       | Android iOS | no                |
| closeMenu         | Color of tint                                                | string | no       | Android iOS | no                |
| hiddenFiles       | If true it shows hidden files as well                        | bool   | no       | Android     | no                |
| filterDirectories | Filter should be applied on directories or not               | bool   | no       | Android     | no                |

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description            | Type     | Required | Platform | HarmonyOS Support |
| ---- | ---------------------- | -------- | -------- | -------- | ----------------- |
| Show | present a fileselector | function | no       | All      | yes               |

 Show

```js
Show(filter?: string, path?: string, onDone?: func, onCancel?: func, title?: string, closeMenu?: string, hiddenFiles?: bool, filterDirectories?: bool);
```

| Name              | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| :---------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| filter            | Filter to sort the files                                     | string | no       | All         | yes               |
| path              | Path of directory                                            | string | no       | All         | yes               |
| onDone            | Function called when file is selected                        | func   | no       | All         | yes               |
| onCancel          | Function called when file selector is closed without selecting any file | func   | no       | All         | yes               |
| title             | Title on the toolbar                                         | string | no       | Android iOS | no                |
| closeMenu         | Color of tint                                                | string | no       | Android iOS | no                |
| hiddenFiles       | If true it shows hidden files as well                        | bool   | no       | Android     | no                |
| filterDirectories | Filter should be applied on directories or not               | bool   | no       | Android     | no                |

## Known Issues


- [ ] FileSelector title: Harmony issue: [issue#4](https://github.com/react-native-oh-library/react-native-file-selector/issues/4)
- [ ] FileSelector closeMenu: Harmony issue: [issue#5](https://github.com/react-native-oh-library/react-native-file-selector/issues/5)
- [ ] FileSelector hiddenFiles: Harmony issue: [issue#6](https://github.com/react-native-oh-library/react-native-file-selector/issues/6)
- [ ] FileSelector filterDirectories: Harmony issue: [issue#7](https://github.com/react-native-oh-library/react-native-file-selector/issues/7)

- [ ] Show title: Harmony issue: [issue#4](https://github.com/react-native-oh-library/react-native-file-selector/issues/4)
- [ ] Show closeMenu: Harmony issue: [issue#5](https://github.com/react-native-oh-library/react-native-file-selector/issues/5)
- [ ] Show hiddenFiles: Harmony issue: [issue#6](https://github.com/react-native-oh-library/react-native-file-selector/issues/6)
- [ ] Show filterDirectories: Harmony issue: [issue#7](https://github.com/react-native-oh-library/react-native-file-selector/issues/7)

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/prscX/react-native-file-selector/blob/master/LICENSE).

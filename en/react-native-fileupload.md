> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fileupload</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/PhilippKrone/react-native-fileupload">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/PhilippKrone/react-native-fileupload/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-fileupload)

Check the release notes of the third-party library to pick the matching version:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 1.1.0 | @react-native-oh-tpl/react-native-fileupload | [Github](https://github.com/react-native-oh-library/react-native-fileupload) | [Github Releases](https://github.com/react-native-oh-library/react-native-fileupload/releases) | 0.72 |
| 1.2.0                        | @react-native-ohos/react-native-fileupload       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-fileupload) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-fileupload/releases) | 0.77 |

## Installation and Usage

For legacy versions that are not published to npm, follow the [installation guide](/en/tgz-usage-en.md) to install the TGZ package.

Go to the project directory and run:

### Package Managers

<!-- tabs:start -->

#### **npm**

```bash
# V0.72
npm install @react-native-oh-tpl/react-native-fileupload

# V0.77
npm install @react-native-ohos/react-native-fileupload
```

#### **yarn**

```bash
# V0.72
yarn add @react-native-oh-tpl/react-native-fileupload

# V0.77
yarn add @react-native-ohos/react-native-fileupload
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

This library requires the following permissions to be added in `entry/src/main/module.json5`.

```json
"requestPermissions": [ 
  { 
    "name": "ohos.permission.INTERNET", 
  }
]
```

```tsx
import React, {Component} from 'react';
import { StyleSheet, Text, View } from 'react-native';
import FileUpload from 'react-native-fileupload';
import Toast from '@remobile/react-native-toast';

export default class FileUploadDemo extends Component {

  componentDidMount () {
    var obj = {
        uploadUrl: 'http://1.2.27.230:9990/upload',// The real server Url
        method: 'POST', // default 'POST',support 'POST' and 'PUT'
        headers: {
          
          'Content-Type': 'multipart/form-data',
        },
        fields: {
            name: 'hello',value: 'world',
        },
        files: [
          {
            name: 'file',// optional
            filename: 'assets_placeholder2000x2000.jpg',
            filepath: '/xxx/assets_placeholder2000x2000.jpg',// The real server filepath
            filetype: 'jpg',// optional
          },
          {
            filename: 'one.w4a',
            filepath: '/xxx/one.w4a', // The real server filepath
            filetype: 'audio/x-m4a',// optional
          },
        ]
    };
    FileUpload.upload(obj, function(err,result) {
      console.log("upload",err,result);
      if(err || result) {
        Toast.showShortCenter(err + result)
      }
    })
  }
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
      </View>
    );
  }
}

let styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
});
```

## Use Codegen

> [!TIP] V0.77 does not require running Codegen.

This repository has been adapted to `Codegen`. Generate the third-party bridge code before usage. For details, see the [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

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

- V0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-fileupload": "file:../../node_modules/@react-native-oh-tpl/react-native-fileupload/harmony/fileupload.har"
  }
```

- V0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-fileupload": "file:../../node_modules/@react-native-ohos/react-native-fileupload/harmony/fileupload.har"
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

### 3. Importing FileUpLoadPackage on the ArkTS Side

Open `entry/src/main/ets/RNPackagesFactory.ts` and add the following code:

```diff
  ...
+ // V0.72
+ import {FileUpLoadPackage} from '@react-native-oh-tpl/react-native-fileupload/ts';
+ // V0.77
+ import {FileUpLoadPackage} from '@react-native-ohos/react-native-fileupload/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FileUpLoadPackage(ctx)
  ];
}
```

### 4. Configuring CMakeLists and Adding FileuploadPackage

> [!TIP] This step is required for V0.77.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-fileupload/src/main/cpp" ./fileupload)

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
+target_link_libraries(rnoh_app PUBLIC rnoh_fileupload)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+#include "FileuploadPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+        std::make_shared<FileuploadPackage>(ctx),
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

This repository has been verified with the following configurations:

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0 (API12); DevEco Studio  6.0.0.868; ROM: 5.0.0.107
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| upload | File upload  | void  | yes | iOS/Android  | yes     |

## Known Issues

## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/PhilippKrone/react-native-fileupload/blob/master/LICENSE).

> Template version: v0.2.2

<p align="center">
  <h1 align="center"> @react-native-community/geolocation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/michalchudziak/react-native-geolocation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/michalchudziak/react-native-geolocation/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"/>
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-geolocation/tree/sig)

Please check the matching version information at the Releases page of the third-party library:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 3.1.0 | @react-native-oh-tpl/geolocation | [Github](https://github.com/react-native-oh-library/react-native-geolocation) | [Github Releases](https://github.com/react-native-oh-library/react-native-geolocation/releases) | 0.72 |
| 3.4.1                        | @react-native-ohos/react-native-geolocation       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-geolocation) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-geolocation/releases) | 0.77 |

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/geolocation

# 0.77
npm install @react-native-ohos/geolocation
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/geolocation

# 0.77
yarn add @react-native-ohos/geolocation
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import Geolocation from "@react-native-community/geolocation";
import { Button } from "react-native";
import React from 'react';

export function GeolocationDemo(): JSX.Element {
  const tap = () => {
    Geolocation.setRNConfiguration({
      skipPermissionRequests: true,
      authorizationLevel: "auto",
      enableBackgroundLocationUpdates: true,
      locationProvider: "auto",
    });
    console.log("tap");
  };

  return <Button title='test' onPress={tap} />;
}
```

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

1. Introducing via har package (this method will be deprecated after IDE improves related functions, currently the preferred method);
2. Directly linking source code.

Method 1: Introducing via har package (recommended)

> [!TIP] The har package is located in the `harmony` folder under the third-party library installation path.

Open `entry/oh-package.json5` file and add the following dependencies:

- 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/geolocation": "file:../../node_modules/@react-native-oh-tpl/geolocation/harmony/geolocation.har"
  }
```

- 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/geolocation": "file:../../node_modules/@react-native-ohos/geolocation/harmony/geolocation.har"
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

### 3. Configuring CMakeLists and Introducing geolocation

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/geolocation/src/main/cpp" ./geolocation)

# 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/geolocation/src/main/cpp" ./geolocation)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_geolocation)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "GeoLocationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<GeoLocationPackage>(ctx)
    };
}
```

### 4. Introducing GeolocationPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
// 0.72
+ import {GeoLocationPackage} from '@react-native-oh-tpl/geolocation/ts';

// 0.77
+ import {GeoLocationPackage} from '@react-native-ohos/geolocation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GeoLocationPackage(ctx)
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

Verified on the following versions:

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

### Permission Requirements

1. Include applicable permissions in the module.json5 file within the entry directory.

```diff
...
{
  "module": {
      "requestPermissions": [
+      {
+        "name": "ohos.permission.APPROXIMATELY_LOCATION",
+        "reason": "$string:Access_location",
+        "usedScene": {
+          "abilities": [
+            "EntryAbility"
+          ],
+          "when": "always"
+        }
+      },
+      {
+        "name": "ohos.permission.LOCATION",
+        "reason": "$string:Access_location",
+        "usedScene": {
+          "abilities": [
+            "EntryAbility"
+          ],
+          "when": "always"
+       }
+      },
+     {
+        "name": "ohos.permission.INTERNET"
+      }
    ]
  }
}
```

2. Apply the reasons for applicable permission in the entry directory.

Open the `entry/src/main/resources/base/element/string.json` file and add the following code:

```diff
...
{
  "string": [
+    {
+      "name": "Access_location",
+      "value": "access location"
+    }
  ]
}
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                                            | Type                                            | Required | Platform    | HarmonyOS Support | Notes                                                                                                                                             |
| -------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------- | -------- | ----------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| setRNConfiguration   | Sets configuration options that will be used in all location requests                  | function(config)                                | NO       | iOS Android | partially         | config only supports skipPermissionRequests                                                                                                       |
| requestAuthorization | Request suitable Location permission                                                   | function(success,error)                         | YES      | iOS Android | partially         | error: Only code and message are supported.                                                                                                       |
| getCurrentPosition   | Invokes the success callback once with the latest location info                        | function(success(position),error(error),option) | NO       | iOS Android | partially         | In position, only altitudeAccuracy is not supported. In option, only timeout and maximumAge are supported. In error, only code and message are supported. |
| watchPosition        | Invokes the success callback whenever the location changes. Returns a watchId (number) | function(success(postion),error(error),option)  | NO       | iOS Android | partially         | In position, only altitudeAccuracy is not supported. In error, only code and message are supported. In option, only interval and distanceFilter are supported. |
| clearWatch           | Clears watch observer by id returned by watchPosition()                                | function(watchID)                               | NO       | iOS Android | yes               | watchID supports only the default value 0.                                                                                                        |

## Known Issues

- [ ] Some attributes of @react-native-oh-tpl/geolocation have not been fully implemented for HarmonyOS, and there is a delay issue with maximumAge: [issue#6](https://github.com/react-native-oh-library/react-native-geolocation/issues/6).

## Others

## License

This project is licensed under [The MIT License(MIT)](https://github.com/michalchudziak/react-native-geolocation/blob/master/LICENSE).
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-nitro-modules</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mrousavy/nitro/tree/main/packages/react-native-nitro-modules">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mrousavy/nitro/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Gitcode Address](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-nitro-modules/tree/dev-0.31.10)

## Installation and Usage

Please go to the Releases page of the third-party library to check the matching version information:

| Library Version | Release Info | Supported RN Version |
| --------------- | ------------------------------------------------------------ | -------------------- |
| 0.31.11     | [@react-native-ohos/react-native-nitro-modules Releases](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-nitro-modules/tree/dev-0.31.10) | 0.77     |

For older versions not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Enter the project directory and run the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-nitro-modules
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-nitro-modules
```

<!-- tabs:end -->

The following code shows the basic usage scenarios of this library:

> [!WARNING] The library name imported remains unchanged when using.

```ts
import React from 'react';
import { View, Text, Pressable, StyleSheet } from 'react-native';
import type {TurboModule} from 'react-native/Libraries/TurboModule/RCTExport';
import {TurboModuleRegistry} from 'react-native';
import { type HybridObject, NitroModules } from 'react-native-nitro-modules'

interface Math extends HybridObject<{}> {
    add(a: number, b: number): number
}

export interface Spec extends TurboModule {
    install(): void;
}

const PlatformConstants	= TurboModuleRegistry.get<Spec>('NitroModules');
if(PlatformConstants) {
    PlatformConstants.install()
}

const App = () => {
  const handleButtonClick = () => {
    const math = NitroModules.createHybridObject<Math>("Math")
    const result = math.add(15, 7) // --> 22
    console.info("result:", result) 
  };

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello React Native TSX!</Text>
      <View style={styles.buttonWrapper}>
        <Pressable
          onPress={handleButtonClick}
          style={styles.button}
          android_ripple={{ color: '#ccc' }}
        >
          <Text style={styles.buttonText}>add</Text>
        </Pressable>
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5f5f5',
  },
  text: {
    fontSize: 18,
    color: '#333',
    marginBottom: 20,
  },
  buttonWrapper: {
    paddingVertical: 20,
    paddingHorizontal: 20,
  },
  button: {
    paddingVertical: 8,
    paddingHorizontal: 16,
    backgroundColor: '#007AFF',
    borderRadius: 4,
  },
  buttonText: {
    fontSize: 16,
    color: '#fff',
    textAlign: 'center',
  },
});

export default App;
```
## Link

This step is a guide for manually configuring native dependencies.

First, you need to use DevEco Studio to open the HarmonyOS project `harmony` in the project.

### 1. Add overrides field to `oh-package.json` in the project root directory

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
  ...
}
```

### 2. Introduce Native Code

There are currently two methods:

Import via har package (this method will be deprecated after the IDE improves related functions, and it is the preferred method currently);
Link source code directly.

Method 1: Import via har package (recommended)

> [!TIP] The HAR package can be found in the harmony subfolder of the third-party library's installation directory.

Open the entry/oh-package.json5 file and append the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-nitro-modules": "file:../../node_modules/@react-native-ohos/react-native-nitro-modules/harmony/nitro_modules.har"
  }
```

Click the `sync` button in the upper right corner.

Or run in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link source code directly

> [!TIP] If you need to use direct source code linking, please refer to [Direct Source Code Linking Description](/en/link-source-code.md)

### 3. Configure CMakeLists, Introduce NitroModulesPackage, register HybridObject, and add the new HybridMath.hpp and HybridMath.cpp files on CPP side

open entry/src/main/cpp/CMakeLists.txt, add:

```diff
include(FetchContent)
# BOOST
set(BOOST_ENABLE_CMAKE On)
FetchContent_Declare(
 Boost
 URL /7277/boost-1.82.0.tar.xz
 OVERRIDE_FIND_PACKAGE)
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)


add_subdirectory("${RNOH_CPP_DIR}" ./rn)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-nitro-modules/src/main/cpp" ./nitro_modules)

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
+    "./HybridMath.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

+ target_link_libraries(rnoh_app PUBLIC rnoh_nitro_modules)
```

Open `entry/src/main/cpp/PackageProvider.cpp`, add:

```diff
#include "RNOH/PackageProvider.h"
+ #include "NitroModulesPackage.h"
+ #include "HybridObjectRegistry.hpp"
+ #include "HybridMath.hpp"

using namespace rnoh;
+ using namespace margelo::nitro;
+ using namespace margelo::nitro::test;
std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
+    HybridObjectRegistry::registerHybridObjectConstructor(
+        "Math", []() -> std::shared_ptr<HybridObject> { return std::make_shared<HybridMath>(); });
    return {
+       std::make_shared<NitroModulesPackage>(ctx),
    };
}
```
Open `entry/src/main/cpp/HybridMath.hpp`, add:
```diff
+ #include "HybridObject.hpp"
+ namespace margelo::nitro::test {
+ class HybridMath: public HybridObject {
+ public:
+   HybridMath(): HybridObject(NAME) { }

+ public:
+   double add(double a, double b);

+ protected:
+   void loadHybridMethods() override;

+ private:
+   static constexpr auto NAME = "Math";
+ };
+ }
```
Open `entry/src/main/cpp/HybridMath.cpp`, add：
```diff
+ #include "HybridMath.hpp"
+ namespace margelo::nitro::test {
+ double HybridMath::add(double a, double b) {
+   return a + b;
+ }
+
+ void HybridMath::loadHybridMethods() {
+   // register base methods (toString, ...)
+   HybridObject::loadHybridMethods();
+   // register custom methods (add)
+   registerHybrids(this, [](Prototype& proto) {
+     proto.registerHybridMethod(
+       "add",
+       &HybridMath::add
+     );
+   });
+ }
+ }
```

### 4. Introduce NitroModulesPackage on ArkTs side

Open `entry/src/main/ets/RNPackagesFactory.ts`, add:

```diff
...
+ import { NitroModulesPackage } from '@react-native-ohos/react-native-nitro-modules/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new NitroModulesPackage(ctx)
  ];
}
```

### 5. Run

Click the `sync` button in the upper right corner.

Or run in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## Constraints

### Compatibility

To use this library, you need to use the correct React-Native and RNOH versions.

This document is verified based on the following versions:

1. RNOH: 0.77.33; SDK: HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API
> [!TIP] The "Platform" column shows the platforms supported by the original third-party library.

> [!TIP] The "HarmonyOS Support" column: yes means the property is supported on HarmonyOS; no means not supported; partially means partially supported. The usage is the same across platforms, and the behavior aligns with iOS or Android.

| Name                    | Description                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------------------- | -------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| buildType     | Gets the current build type configuration as defined in the `NITRO_DEBUG`.          | property | No      | iOS/Android | yes               |
| hasHybridObject    | Returns whether a HybridObject under the given {@linkcode name} is registered, or not.       | function | No      | iOS/Android | yes               |
| isHybridObject | Returns whether the given {@linkcode object} is a {@linkcode HybridObject}, or not.                | function | No      | iOS/Android | yes               |
| getAllHybridObjectNames | Get a list of all registered Hybrid Objects.                | function | No      | iOS/Android | yes               |
| version | Gets the native Nitro Modules core runtime version that this app is built with.                | property | No      | iOS/Android | yes               |
| box | Boxes the given {@linkcode hybridObject} into a {@linkcode BoxedHybridObject<T>}, which can later be unboxed in a separate Runtime.                | function | No      | iOS/Android | yes               |
| unbox | Represents a boxed {@linkcode HybridObject} that can later be unboxed again.                | function | No      | iOS/Android | yes               |
| hasNativeState | Returns whether the given {@linkcode object} has NativeState or not.                | function | No      | iOS/Android | yes               |
| updateMemorySize | Re-calculates `memorySize` of the given {@linkcode HybridObject} and notifies the JS VM about the newly updated memory footprint                | function | No      | iOS/Android | yes               |
| AnyHybridObject | Represents a value of the base `HybridObject` type all other HybridObjects inherit from.                | interface | No      | iOS/Android | yes               |
| getHybridObjectConstructor | Get a constructor function for the given `HybridObject` {@linkcode T}.                | function | No      | iOS/Android | yes               |
| toString | Returns a string representation of the given `HybridObject`.                | function | No      | iOS/Android | yes               |
| name | The `HybridObject`'s name.                | property | No      | iOS/Android | yes               |
| equals | Returns whether this `HybridObject` is the same object as {@linkcode other}.                | function | No      | iOS/Android | yes               |
| dispose | Disposes any resources this {@linkcode HybridObject} might hold natively, and releases this {@linkcode HybridObject}'s `NativeState`.                | function | No      | iOS/Android | yes               |
| CustomType | Represents a custom, manually written native type.                | type | No      | iOS/Android | yes               |
| Sync | Marks the given function as _synchronous_, allowing it to be called synchronously on the same Thread.                | type | No      | iOS/Android | yes               |
| createHybridObject | Create a new instance of the `HybridObject` {@linkcode T}.                | function | No      | iOS/Android | yes               |
| HybridView | Represents a Nitro Hybrid View.                | type | No      | iOS/Android | no               |
| getHostComponent | Finds and returns a native view (aka "HostComponent") via the given {@linkcode name}.              | function | No      | iOS/Android | no               |

## Known Issues

## Others
- The react-native-nitro-modules library is not dependent on React Native 0.72. To build Hybrid Views with HybridView and getHostComponent, a minimum React Native version of 0.78 is required.

## License

This project is based on [The MIT License (MIT)](https://github.com/mrousavy/nitro/blob/main/LICENSE), please freely enjoy and participate in open source.


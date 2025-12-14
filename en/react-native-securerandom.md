> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-securerandom</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/robhogan/react-native-securerandom">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/robhogan/react-native-securerandom/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-securerandom)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.0.1-0.0.2@deprecated  | [@react-native-oh-tpl/react-native-securerandom Releases(deprecated)](https://github.com/react-native-oh-library/react-native-securerandom/releases) | 0.72       |
| 1.0.2             | [@react-native-ohos/react-native-securerandom Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-securerandom/releases)           | 0.72       |
| 1.1.0             | [@react-native-ohos/react-native-securerandom Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-securerandom/releases)           | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-securerandom
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-securerandom
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import {
  Text,
  TouchableOpacity,
  View,
  TextInput,
  StyleSheet,
} from "react-native";
import { generateSecureRandom } from "react-native-securerandom";

export default function secureRandomDemo(): JSX.Element {
  const [secureRandom, setSecureRandom] = useState("");
  const [size, setSize] = useState("30");

  return (
    <View>
      <ScrollView style={{ height: 60 }}>
        <Text>{secureRandom}</Text>
      </ScrollView>

      <TextInput
        style={styles.TextInput}
        value={size}
        onChangeText={(s) => {
          setSize(s);
        }}
      ></TextInput>
      <TouchableOpacity
        onPress={() => {
          generateSecureRandom(Number(size))
            .then((myRandom: any) => {
              setSecureRandom(`${JSON.stringify(myRandom?.data)}`);
            })
            .catch((err) => {
              console.log(err, "err");
            });
        }}
        style={styles.btn}
      >
        <Text style={styles.btnText}>secureRandom</Text>
      </TouchableOpacity>
    </View>
  );
}
const styles = StyleSheet.create({
  TextInput: {
    height: 40,
    borderColor: "#ccc",
    borderWidth: 1,
    borderRadius: 4,
    width: "90%",
  },
  btn: {
    borderRadius: 10,
    display: "flex",
    justifyContent: "center",
    alignItems: "center",
    padding: 10,
    margin: 10,
    backgroundColor: "blue",
  },
  btnText: { fontWeight: "bold", color: "#fff", fontSize: 20 },
});
```

### Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).
## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.1.0                               |  No                   |  0.77                |
| ~1.0.2                              |  Yes                  |  0.72                |
| <= 1.0.1-0.0.2@deprecated            |  No                   |  0.72                |

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

### 2.  Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-securerandom": "file:../../node_modules/@react-native-ohos/react-native-securerandom/harmony/secure_random.har"
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

### 3.Configuring CMakeLists and Introducing SecureRandomPackage

> If you are using version <= 1.0.1-0.0.2, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-securerandom/src/main/cpp" ./secure_random)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_secure_random)
# RNOH_END: manual_package_linking_2
```
打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SecureRandomPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SecureRandomPackage>(ctx)
    };
}
```

### 4. Introducing SecureRandomPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { SecureRandomPackage } from '@react-native-ohos/react-native-securerandom/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SecureRandomPackage(ctx)
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

## API

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                 | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | ----------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| generateSecureRandom | A library to generate cryptographically-secure random byte. | Function | No       | ios/Android | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/robhogan/react-native-securerandom/blob/main/LICENSE).

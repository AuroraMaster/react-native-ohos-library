> Template version: v0.2.2

<p align="center">
  <h1 align="center">react-native-ssl-pinning</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/MaxToyberman/react-native-ssl-pinning">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/MaxToyberman/react-native-ssl-pinning/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-ssl-pinning)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.5.7@deprecated  | [@react-native-oh-tpl/react-native-ssl-pinning Releases(deprecated)](https://github.com/react-native-oh-library/react-native-ssl-pinning/releases) | 0.72       |
| 1.5.8             | [@react-native-ohos/react-native-ssl-pinning Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-ssl-pinning/releases)   | 0.72       |
| 1.6.0             | [@react-native-ohos/react-native-ssl-pinning Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-ssl-pinning/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-ssl-pinning
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-ssl-pinning
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] This example relies on react-native-file-selector and is introduced by referring to document [@react-native-ohos/react-native-file-selector](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-file-selector.md).

```js

import React from 'react';
import {
    SafeAreaView,
    StyleSheet,
    ScrollView,
    View,
    Text,
    StatusBar,
    Button,
    Alert,
} from 'react-native';
import {Colors} from 'react-native/Libraries/NewAppScreen';
import {getCookies, fetch, removeCookieByName} from 'react-native-ssl-pinning';
import FileSelector from '@react-native-ohos/react-native-file-selector';
function SslPingDemo() : React.JSX.Element{
    return (
        <>
        <StatusBar barStyle="dark-content" />
            <SafeAreaView>
                <ScrollView contentInsetAdjustmentBehavior="automatic" style={styles.scrollView}>
                    <View style={styles.body}>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>fetch bY Public Key</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={() => {
                                        fetch("https://jsnjlq.cn", {
                                            method: "GET" ,
                                            timeoutInterval: 10000, // milliseconds
                                            pkPinning: true,
                                            sslPinning: {
                                                certs: ["sha256/kPwnudZVhc+iC/fTd3OPph8uugk1YN5ZsJDAeM2P4UU="]
                                            },
                                            headers: {
                                                Accept: "application/json; charset=utf-8", "Access-Control-Allow-Origin": "*", "e_platform": "mobile",
                                            }
                                        }).then(
                                            (result) => {
                                                Alert.alert(JSON.stringify(result));
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>fetch bY Certificate</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={() => {
                                        fetch("https://jsnjlq.cn", {
                                            method: "POST" ,
                                            timeoutInterval: 10000, // milliseconds
                                            sslPinning: {
                                                certs: ["cert"]
                                            },
                                            headers: {
                                                Accept: "application/json; charset=utf-8", "Access-Control-Allow-Origin": "*", "e_platform": "mobile",
                                            }
                                        }).then(response => {
                                            Alert.alert(JSON.stringify(response));
                                        }).catch(err => {
                                            console.log(`error: ${err}`)
                                        })
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <FileSelector
                                onDone={(path: string[]) => {
                                    filePath = path
                                }}
                                onCancel={() => {console.log("cancelled");}}
                            />
                            <Text style={styles.sectionTitle} >Multipart request</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={() => {
                                        let formData = new FormData()
                                        formData.append('username', 'Chris');
                                        let filePathArray = filePath.length > 0 ?filePath[0].split("/") : ["test"]
                                        Alert.alert(JSON.stringify(filePathArray[filePathArray.length - 1]));
                                        formData.append('file', {
                                            name: encodeURIComponent(filePathArray[filePathArray.length - 1]),
                                            fileName: encodeURIComponent(filePathArray[filePathArray.length - 1]),
                                            type: "multipart/form-data",
                                            uri: filePath[0]
                                        })
                                        fetch("http://123.249.28.4:8888/handerOkhttpRequest/parse", {
                                            method: "POST" ,
                                            timeoutInterval: 10000, // milliseconds
                                            body: {
                                                formData: formData,
                                            },
                                            sslPinning: {
                                                certs: ["cert"]
                                            },
                                            headers: {
                                                accept: 'application/json, text/plain, /',
                                            }
                                        })
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>getCookies</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={async () => {
                                        getCookies("jsnjlq.cn").then(
                                            (result) => {
                                                Alert.alert(JSON.stringify(result));
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>remove Cookie</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={async () => {
                                        removeCookieByName("jsnjlq.cn").then(
                                            (result) => {
                                                Alert.alert(JSON.stringify(result));
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                    </View>
                </ScrollView>
            </SafeAreaView>
        </>
    );
};

const styles = StyleSheet.create({
    scrollView: {
        backgroundColor: Colors.lighter,
    },
    engine: {
        position: 'absolute',
        right: 0,
    },
    body: {
        backgroundColor: Colors.white,
    },
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
    sectionTitle: {
        fontSize: 24,
        fontWeight: '600',
        color: Colors.black,
    },
    sectionDescription: {
        marginTop: 8,
        fontSize: 18,
        fontWeight: '400',
        color: Colors.dark,
    },
    highlight: {
        fontWeight: '700',
    },
    footer: {
        color: Colors.dark,
        fontSize: 12,
        fontWeight: '600',
        padding: 4,
        paddingRight: 12,
        textAlign: 'right',
    },
});

export default SslPingDemo;
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.6.0                               |  No                   |  0.77                |
| ~1.5.8                              |  Yes                  |  0.72                |
| <= 1.5.7-0.0.2@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

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

### 2.Introducing Native Code

Currently, two methods are available:

1. Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-ssl-pinning": "file:../../node_modules/@react-native-ohos/react-native-ssl-pinning/harmony/ssl_pinning.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.Configuring CMakeLists and Introducing SslPinningPackage

> If you are using version <= 1.5.7-0.0.2, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-ssl-pinning/src/main/cpp" ./ssl_pinning)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_ssl_pinning)
# RNOH_END: manual_package_linking_2
```
Open `entry/src/main/cpp/PackageProvider.cpp`, and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SslPinningPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SslPinningPackage>(ctx)
    };
}
```

### 4.Introducing SslPinningPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
+ import { SslPinningPackage } from "@react-native-ohos/react-native-ssl-pinning/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SslPinningPackage(ctx),,
  ];
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

### Permission Requirements

#### Add permissions to the module.json5 file in the entry directory.

Open entry/src/main/module.json5 and add the following information:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.INTERNET",
+  }
]
```

## APIs

> [!TIP] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                | Description                                    | Type      | Required | Platform   | HarmonyOS Support |
|-------------------------------------|------------------------------------------------|-----------| -------- |------------|-------------------|
| removeCookieByName(cookieName)      | remove Cookies by cookieName                   | function  | No       | All        | yes               |
| getCookies(domain)                  | query cookies by domain                        | function  | No       | All        | yes               |
| fetch(hostname, options, callback)  | Initiate a fetch request with the certificate. | function  | No       | All        | yes               |


## Known Issues

## Others

If certificate locking is used, the certificate needs to be built into the rawfile folder in the entry directory.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/MaxToyberman/react-native-ssl-pinning/blob/master/LICENSE)

> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-cookies/cookies</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-cookies/cookies/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-cookies/cookies/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-cookies)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 6.2.1-0.0.8@deprecated   | [@react-native-oh-tpl/cookies Releases(deprecated)](https://github.com/react-native-oh-library/react-native-cookies/releases) | 0.72                 |
| 6.2.2            | [@react-native-ohos/cookies Releases](https://gitcode.com/openharmony-sig/rntpc_cookies/releases) | 0.72       |
| 6.3.0            | [@react-native-ohos/cookies Releases](https://gitcode.com/openharmony-sig/rntpc_cookies/releases) | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/cookies
```

#### **yarn**

```
yarn add @react-native-ohos/cookies
```

<!-- tabs:end -->

On HarmonyOS, **react-native-cookies** must be used together with **react-native-webview**. For details, see [@react-native-ohos/react-native-webview](/en/react-native-webview.md).

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useRef } from "react";
import {
  ScrollView,
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
} from "react-native";
import CookieManager from "@react-native-cookies/cookies";
import { WebView } from "react-native-webview";

export interface Cookie {
  name: string;
  value: string;
  path?: string;
  domain?: string;
  version?: string;
  expires?: string;
  secure?: boolean;
  httpOnly?: boolean;
}

export interface Cookies {
  [key: string]: Cookie;
}

export default function CookiesPage() {
  const httpUrl = "https://www.baidu.com";
  const [result, setResult] = useState("Touch the button to perform the operation.");
  const webViewRef = useRef(null);
  return (
    <View style={styles.container}>
      <View style={styles.pageArea}>
        <WebView source={{ uri: httpUrl }} ref={webViewRef} />;
      </View>

      <ScrollView style={styles.resultArea}>
        <Text>{result}</Text>
      </ScrollView>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.clearAll(true);
          let result = cookieResult
            ? "All cookies cleared successfully."
            : "Failed to clear all cookies.";
          setResult(result + "");
        }}
      >
        <Text>clearAll()【Clear all cookies.】</Text>
      </TouchableOpacity>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.get(httpUrl, true);
          setResult(JSON.stringify(cookieResult));
        }}
      >
        <Text>get()【Obtain cookies using the URL.】</Text>
      </TouchableOpacity>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let curCookie: Cookie = { name: "myAddCookie", value: "myNewCookie" };
          let cookieResult = await CookieManager.set(httpUrl, curCookie, true);
          let result = cookieResult
            ? "Cookies set using the URL successfully."
            : "Failed to set the cookies using the URL.";
          setResult(result);
        }}
      >
        <Text>set()【Set cookies using the URL.】</Text>
      </TouchableOpacity>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.clearByName(
            httpUrl,
            "myAddCookie",
            true
          );
          let result = cookieResult
            ? "Cookies deleted by name successfully."
            : "Failed to delete cookies by name.";
          setResult(result);
        }}
      >
        <Text>clearByName()【Delete cookies by name.】</Text>
      </TouchableOpacity>   

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.removeSessionCookies();
          let result = cookieResult
            ? "Session cookies cleared successfully."
            : "Failed to clear session cookies.";
          setResult(result);
        }}
      >
        <Text>removeSessionCookies()【Clear session cookies.】</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: "100%",
    height: "100%",
    alignItems: "center",
  },
  pageArea: {
    width: "95%",
    height: 80,
  },
  resultArea: {
    width: "95%",
    borderWidth: 2,
    borderColor: "gray",
    borderRadius: 10,
    marginTop: 5,
  },
  button: {
    backgroundColor: "#FF0000",
    paddingHorizontal: 16,
    paddingVertical: 10,
    borderRadius: 24,
    alignItems: "center",
    justifyContent: "center",
    elevation: 4,
    width: "80%",
    marginTop: 5,
  },
});
```

## Link

Version >= @react-native-ohos/cookies@6.2.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/cookies": "file:../../node_modules/@react-native-ohos/cookies/harmony/rn_cookies.har",
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

### 3. Configuring CMakeLists and Introducing CookiesPackage

> If you are using version <= 6.2.1-0.0.8, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${OH_MODULES}/rnoh/src/main/cpp")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/cookies/src/main/cpp" ./rn_cookies)
# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_cookies)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
...

+ #include "CookiesPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<CookiesPackage>(ctx),
    };
}
```

### 4.Introducing CookiesPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+ import {CookiesPackage} from '@react-native-ohos/cookies/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    ...
+  	new CookiesPackage(ctx),
  ];
}
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

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                   | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | --------------------------------------------- | ---------|----------| ------------|-------------------|
| clearAll             |  Clear all cookies                            |function  |     NO   |iOS,Android  | yes               |
| get                  |  Get cookies based on url                     |function  |     NO   | iOS,Android | yes               |
| set                  |  Set cookie based on url                      |function  |     NO   | iOS,Android | yes               |
| clearByName          |  Delete cookies by name                       |function  |     NO   | iOS         | yes               |
| flush                |  Refresh cookies                              |function  |     NO   | Android     | no                |
| removeSessionCookies |  Clear session cookies                        |function  |     NO   | iOS,Android | yes               |
| getAll               |  Get all cookies                              |function  |     NO   | iOS         | no                |
| setFromResponse      |  Set cookies from a response header           |function  |     NO   | iOS         | no                |
| getFromResponse      |  Get cookies from a response header           |function  |     NO   | iOS         | no                |

## Known Issues

- [ ] The **getAll**, **setFromResponse**, **getFromResponse**, and **flush** methods are available on iOS, but not on Android. HarmonyOS does not have the corresponding API: [issue#1](https://github.com/react-native-oh-library/react-native-cookies/issues/1).

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-cookies/cookies/blob/master/LICENSE).

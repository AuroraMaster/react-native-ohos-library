> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-apple-authentication</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/invertase/react-native-apple-authentication">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-apple-authentication)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 2.3.0-0.0.1@deprecated      | [@react-native-oh-tpl/react-native-apple-authentication Releases(deprecated)](https://github.com/react-native-oh-library/react-native-apple-authentication/releases) | 0.72       |
| 2.3.1      | [@react-native-ohos/react-native-apple-authentication Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-apple-authentication/releases) | 0.72       |
| 2.4.2      | [@react-native-ohos/react-native-apple-authentication Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-apple-authentication/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-apple-authentication
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-apple-authentication
```

#### **Configuring Sign in with Apple for the Web**

Configure the client ID: [Initial Development Environment Setup](https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md).

Set the service: [Services setup](https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md).

Configure the official Apple description: [Configure Sign in with Apple for the web](https://developer.apple.com/help/account/configure-app-capabilities/configure-sign-in-with-apple-for-the-web)

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React from "react";
import { View } from 'react-native';
import {
  appleAuthHarmony,
  AppleButton,
} from "@invertase/react-native-apple-authentication";

const AppleAuthenticationDemo: React.FC = (): JSX.Element => {
  return (
    <>
      <AppleButton
        onPress={async () => {
          appleAuthHarmony.configure({
            // For the following configuration,please refer to the original library AppleId login document:
            // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md
            // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md
            clientId: "com.example.client",
            redirectUri: "https://example.com",
          });
          const singInRes = await appleAuthHarmony.signIn();
          console.log(singInRes);
        }}
      />
    </>
  );
};

export default AppleAuthenticationDemo;
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~2.4.2                               |  No                   |  0.77                |
| ~2.3.1                               |  Yes                  |  0.72                |
| <= 2.3.0-0.0.1@deprecated            |  No                   |  0.72                |

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
    "@react-native-ohos/react-native-apple-authentication": "file:../../node_modules/@react-native-ohos/react-native-apple-authentication/harmony/react-native-apple-authentication.har"
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

### 3.Configure CMakeLists and import RNOHAppleAuthenticationPackage

> If you are using version <= 2.3.0-0.0.1, please skip this chapter.

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

# (VM) Define a variable and assign it to the current module's cpp directory
set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

# Add the Header File directory, including cpp, cpp/include, and tell cmake to find the Header Files introduced by the code here
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-apple-authentication/src/main/cpp" ./react-native-apple-authentication)
# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp") # this line is needed by codegen v1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC rnoh_apple_authentication)

```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff

#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNOHAppleAuthenticationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx)
{
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+ 			std::make_shared<RNOHAppleAuthenticationPackage>(ctx),
    };
}
```

### 4. Introducing RNAppleAuthPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNAppleAuthPackage } from '@react-native-ohos/react-native-apple-authentication';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAppleAuthPackage(ctx)
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


## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**AppleButton**: Apple authentication button

| Name         | Description        | Type                                                         | Required | Platform | HarmonyOS Support |
| ------------ | ------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| style        | Button style.          | StyleProp< [ViewStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Fview%23props) > | no       | all      | yes               |
| textStyle    | Text style.    | StyleProp< [TextStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Ftext%23props) > | no       | all      | yes               |
| cornerRadius | Corner radius of the border.  | number                                                       | no       | all      | yes               |
| buttonStyle  | Button style (preset enumeration).| [AppleButtonStyle](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonStyle.md) | no       | all      | yes               |
| buttonType   | Button type (preset enumeration).| [AppleButtonType](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonType.md) | no       | all      | yes               |
| onPress      | Touch event.      | () => void                                                   | yes      | all      | yes               |
| leftView     | Left icon of the button.    | ReactNode                                                    | no       | all      | yes               |
| buttonText   | Button text.    | string                                                       | no       | all      | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**appleAuthHarmony**: Apple authentication object, including two methods

| Name      | Description                                             | Type                                                         | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| configure | Configures Apple authentication information. This API must be called before **signIn**.| ([Config](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidConfig.md)) => void | no       | all      | yes               |
| signIn    | Pops up the WebView for Apple authentication.                     | () => Promise< [SigninResponse](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidSigninResponse.md) > | no       | all      | no                |

## Others

## Known Issues

- [ ] Due to Apple developer account authentication issues, the following API is not supported by HarmonyOS: [issue#1](https://github.com/react-native-oh-library/react-native-apple-authentication/issues/1).

## License

This project is licensed under [Apache License 2.0](https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE).

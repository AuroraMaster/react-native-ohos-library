> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-email-link</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tschoffelen/react-native-email-link">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/tschoffelen/react-native-email-link/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-email-link)

## Installation and Usage

Find the matching version information in the release address of a third-party library: 

| Third-party Library Version | Release Information    | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.15.0@deprecated     | [@react-native-oh-tpl/react-native-email-link Releases(deprecated)](https://github.com/react-native-oh-library/react-native-email-link/releases) | 0.72       |
| 1.15.1     | [@react-native-ohos/react-native-email-link Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-email-link/releases) | 0.72       |
| 1.16.2     | [@react-native-ohos/react-native-email-link Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-email-link/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-email-link
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-email-link
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import {
  SafeAreaView,
  View,
  StyleSheet,
  Text,
  StatusBar,
  Button,
} from "react-native";
import {
  getEmailClients,
  openInbox,
  openComposer,
} from "react-native-email-link";

export function EmailLinkExample() {
  const [emailClients, setEmailClients] = useState(
    "click button getEmailClients to get email information"
  );
  return (
    <SafeAreaView style={styles.container}>
      <View style={styles.wrapper}>
        <Text style={styles.text}>{emailClients}</Text>
        <Button
          title="getEmailClients"
          onPress={async () => {
            let clients = await getEmailClients();
            setEmailClients(JSON.stringify(clients));
          }}
        />

        <Button
          title="openInbox-without-app"
          onPress={() => {
            openInbox();
          }}
        />

        <Button
          title="openInbox-with-app"
          onPress={() => {
            openInbox({
              app: "mail",
            });
          }}
        />

        <Button
          title="openComposer-without-app"
          onPress={() => {
            openComposer({
              to: "support@example.com",
              cc: "cc@example.com",
              bcc: "bcc@example.com",
              subject: "I have a question",
              body: "Hi, can you help me with...",
            });
          }}
        />

        <Button
          title="openComposer-with-app"
          onPress={() => {
            openComposer({
              app: "mail",
              to: "support@example.com",
              cc: "cc@example.com",
              bcc: "bcc@example.com",
              subject: "I have a question",
              body: "Hi, can you help me with...",
            });
          }}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight,
  },
  item: {
    backgroundColor: "#f9c2ff",
    justifyContent: "center",
    marginVertical: 8,
    marginHorizontal: 16,
    padding: 20,
  },
  title: {
    fontSize: 24,
  },
  wrapper: {
    height: 200,
  },
  text: {
    marginBottom: 20,
    color: "white",
    textAlign: "center",
  },
});
```

## Use Codegen

Version >= @react-native-ohos/react-native-email-link@1.15.1，compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

**Note：** V1.16.1 does not require Codegen.

## Link

Version >= @react-native-ohos/react-native-email-lin@1.15.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

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
    "@react-native-ohos/react-native-email-link": "file:../../node_modules/@react-native-ohos/react-native-email-link/harmony/email_link.har"
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

### 3.Configuring CMakeLists and Introducing RNEmailLinkPackage Package

> V1.16.1 requires configuring CMakeLists and introducing RNEmailLinkPackage.

This library embeds the code generated by codegen in the library file.

Open entry/src/main/cpp/CMakeLists.txt，and add the following code：
```diff
{
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")

set(RNOH_CPP_DIR "${OH_MODULE_DIR}/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")

add_compile_definitions(WITH_HITRACE_SYSTRACE)
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-email-link/src/main/cpp" ./email_link)

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")
add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC rnoh_email_link)
}
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "EmailLinkGeneratedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+     std::make_shared<EmailLinkRNOHGeneratedPackage>(ctx)
    };
}
```

### 4. Introducing RNEmailLinkPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNEmailLinkPackage} from '@react-native-ohos/react-native-email-link/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNEmailLinkPackage(ctx)
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

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `openInbox`       | Directly open the inbox of the default mail client on your device.                                     | function | No       | All      | yes               |
| `openComposer`    | Used to open a new email authoring interface that allows users to create emails directly from the app. | function | No       | All      | yes               |
| `getEmailClients` | Get a list of all supported mail client applications installed on the device.                          | function | No       | All      | yes               |

**openInbox method parameters**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `title` | Text for the top of the ActionSheet or Intent | string | no | All | no |
| `message` | Subtext under the title on the ActionSheet | string | no | iOS | no |
| `cancelLabel` | Text for last button of the ActionSheet | string | no | iOS | no |
| `removeText` | If true, not text will be show above the ActionSheet or Intent. Default value is false | boolean | no | All | no |
| `defaultEmailLabel` | Text for first button of the ActionSheet | function | no | iOS | no |
| `newTask` | If true, the email Intent will be started in a new Android task. Else, the Intent will be launched in the current task | boolean | no | Android | no |

**openComposer method parameters**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `app` | App to open the composer with| string | no | All | yes |
| `title` | Text for the top of the ActionSheet or Intent | string | no | All | no |
| `message` | Subtext under the title on the ActionSheet | string | no | iOS | no |
| `cancelLabel` | Text for last button of the ActionSheet | string | no | iOS | no |
| `removeText` | If true, not text will be show above the ActionSheet or Intent. Default value is false | boolean | no | All | no |
| `defaultEmailLabel` | Text for first button of the ActionSheet | function | no | iOS | no |
| `to` | Recipient's email address | string | no | All | yes |
| `cc` | Email's cc | string | no | All | yes |
| `bcc` | Email's bcc | string | no | All | yes |
| `subject` | Email's subject | string | no | All | yes |
| `body` | Email's body | string | no | All | yes |
| `encodeBody` | Apply encodeURIComponent to the email's body | boolean | no | All | yes |

## Known Issues

- [ ] 目前只支持 harmonyOS 系统自带邮箱，本库支持邮箱均未适配 harmonyOS Next。[issues#5](https://github.com/react-native-oh-library/react-native-email-link/issues/5)

## Others

- title、message、cancelLabel、 removeText、defaultEmailLabel、newTaskProperties 暂不支持，与 iOS 表现一致。[issue#141](https://github.com/tschoffelen/react-native-email-link/issues/141)。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/tschoffelen/react-native-email-link/blob/master/LICENSE).

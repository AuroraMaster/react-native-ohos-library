> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-clipboard/clipboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-clipboard/clipboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-clipboard/clipboard/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/clipboard/tree/sig)

Please check the matching version information at the Releases page of the third-party library:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 1.13.2 | @react-native-oh-tpl/clipboard | [Github](https://github.com/react-native-oh-library/clipboard) | [Github Releases](https://github.com/react-native-oh-library/clipboard/releases) | 0.72 |
| 1.16.3                        | @react-native-ohos/clipboard       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_clipboard) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_clipboard/releases) | 0.77 |

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/clipboard

# 0.77
npm install @react-native-ohos/clipboard
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/clipboard

# 0.77
yarn add @react-native-ohos/clipboard
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

#### **For RN0.72**

```js
import Clipboard from "@react-native-clipboard/clipboard";

const [copiedText, setCopiedText] = useState("");

const copyToClipboard = () => {
  Clipboard.setString("hello world");
};

const fetchCopiedText = async () => {
  const text = await Clipboard.getString();
  setCopiedText(text);
};

const App = () => {
  return (
    <View style={styles.container}>
      <TouchableOpacity onPress={copyToClipboard}>
        <Text>Click here to copy to Clipboard</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={fetchCopiedText}>
        <Text>View copied text</Text>
      </TouchableOpacity>

      <Text style={styles.copiedText}>{copiedText}</Text>
    </View>
  );
};

export default App;
```

**For RN0.77**

```js
import React, { useState } from 'react';
import { StyleSheet, Text, TouchableOpacity, View } from 'react-native';
import Clipboard from "@react-native-clipboard/clipboard";

const App = () => {
  const [copiedText, setCopiedText] = useState("");

  const copyToClipboard = () => {
    Clipboard.setString("hello world");
  };

  const fetchCopiedText = async () => {
    const text = await Clipboard.getString();
    setCopiedText(text);
  };

  return (
    <View style={styles.container}>
      <TouchableOpacity onPress={copyToClipboard}>
        <Text>Click here to copy to Clipboard</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={fetchCopiedText}>
        <Text>View copied text</Text>
      </TouchableOpacity>

      <Text style={styles.copiedText}>{copiedText}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    padding: 20,
  },
  copiedText: {
    marginTop: 20,
    fontSize: 18,
  },
};

export default App;
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

1. Introduce via har package (this method will be deprecated after the IDE improves related functions, currently the preferred method);
2. Directly link to the source code.

Method 1: Introduce via har package

> [!TIP] The har package is located in the [harmony] folder in the third-party library installation path.

Open `entry/oh-package.json5` and add the following dependencies:

- 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/clipboard": "file:../../node_modules/@react-native-oh-tpl/clipboard/harmony/clipboard.har"
  }
```

- 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/clipboard": "file:../../node_modules/@react-native-ohos/clipboard/harmony/clipboard.har"
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

### 3. Configuring CMakeLists and Introducing ClipboardPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/clipboard/src/main/cpp" ./clipboard)

# 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/clipboard/src/main/cpp" ./clipboard)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_clipboard)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ClipboardPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ClipboardPackage>(ctx),
    };
}
```

### 4. Introducing ClipboardPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';

// 0.72
+ import {ClipboardPackage} from '@react-native-oh-tpl/clipboard/ts';

// 0.77
+ import {ClipboardPackage} from '@react-native-ohos/clipboard/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ClipboardPackage(ctx)
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

This document is verified based on the following versions:

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/clipboard Releases](https://github.com/react-native-oh-library/clipboard/releases)

### Permission Requirements

> [!TIP] The "ohos.permission.READ_PASTEBOARD" permission level is <B>system_basic</B>, and the authorization method is <B>user_grant</B>. [Configuration Guide for Using ACL Signature](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

#### Add permissions in the module.json5 file under the entry directory

Open `entry/src/main/module.json5` and add the following code:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.READ_PASTEBOARD",
+    "reason": "$string:Access_clipboard",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"always"
+    }
+  },
]
```

#### Add the reason for requesting clipboard permissions under the entry directory

Open `entry/src/main/resources/base/element/string.json` and add the following code:

```diff
...
{
  "string": [
+    {
+      "name": "Access_clipboard",
+      "value": "access clipboard"
+    }
  ]
}
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description                                                                                                                                                                                                               | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| getString   | Get content of string type, this method returns a Promise, so you can use following code to get clipboard content                                                                                                         | function | NO       | iOS,Android | yes               |
| setString   | Set content of string type. You can use following code to set clipboard content                                                                                                                                           | function | NO       | iOS,Android | yes               |
| hasString   | Returns whether the clipboard has content or is empty.                                                                                                                                                                    | function | NO       | iOS,Android | yes               |
| getImage    | Get content of image in base64 string type, this method returns a Promise, so you can use following code to get clipboard content (ANDROID only)                                                                          | function | NO       | Android     | no                |
| getStrings  | (iOS only) Get contents of string array type, this method returns a Promise, so you can use following code to get clipboard content                                                                                       | function | NO       | iOS        | yes                |
| setStrings  | (iOS only) Set content of string array type. You can use following code to set clipboard content                                                                                                                          | function | NO       | iOS        | yes                |
| hasNumber   | (iOS 14+ only) Returns whether the clipboard has a Number(UIPasteboardDetectionPatternNumber) content. Can check if there is a Number content in clipboard without triggering PasteBoard notification for iOS 14+         | function | NO       | iOS        | yes               |
| hasImage    | Returns whether the clipboard has a Image                                                                                                                                                                                 | function | NO       | iOS        | yes               |
| hasUrl      | (iOS only) Returns whether the clipboard has a URL content. Can check if there is a URL content in clipboard without triggering PasteBoard notification for iOS 14+                                                       | function | NO       | iOS        | yes                |
| hasWebUrl   | (iOS 14+ only) Returns whether the clipboard has a WebURL(UIPasteboardDetectionPatternProbableWebURL) content. Can check if there is a WebURL content in clipboard without triggering PasteBoard notification for iOS 14+ | function | NO       | iOS        | yes               |
| setImage    | Set content of Image type.（base64 string）                                                                                                                                                                               | function | NO       | iOS        | yes               |
| getImageJPG | get base64 string of JPG Image                                                                                                                                                                                            | function | NO       | iOS        | yes               |
| getImagePNG | get base64 string of PNG Image                                                                                                                                                                                            | function | NO       | iOS        | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-clipboard/clipboard/blob/master/LICENSE).

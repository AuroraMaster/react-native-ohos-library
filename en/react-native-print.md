> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-print</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/christopherdro/react-native-print">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20Windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/christopherdro/react-native-print/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-print)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 0.11.0-0.0.3@deprecated  | [@react-native-oh-tpl/react-native-print Releases(deprecated)](https://github.com/react-native-oh-library/react-native-print/releases) | 0.72       |
| 0.11.1             | [@react-native-ohos/react-native-print Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-print/releases)   | 0.72       |
| 0.12.0             | [@react-native-ohos/react-native-print Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-print/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-print
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-print
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] This example depends on the react-native-document-picker library. For details, see [@react-native-ohos/react-native-document-picker document](/en/react-native-document-picker.md).

```js
import React, {useState} from 'react';
import {
  ScrollView,
  Button,
} from 'react-native';
import {
  pick,
  DocumentPickerOptions,
  isCancel,
} from 'react-native-document-picker';
import RNPrint from 'react-native-print';

type DirType = 'documentDirectory' | 'cachesDirectory';

interface DirOpt {
  label: DirType;
  selected: boolean;
}

export default function RNPrint(): JSX.Element {
  const [pickResult, setPickResult] = useState('');
  const [allowMultiSelection, setAllowMultiSelection] = useState(true);
  const [fileTypes, setFileTypes] = useState<string[]>([]);
  const [dirUi, setDirui] = useState<Array<DirOpt>>([
    {label: 'documentDirectory', selected: false},
    {label: 'cachesDirectory', selected: false},
  ]);
  const copyTo = dirUi.find(d => d.selected)?.label;
  const pickOpt: DocumentPickerOptions<'harmony'> = {
    allowMultiSelection,
    presentationStyle: 'overFullScreen',
  };
  if (copyTo) {
    pickOpt.copyTo = copyTo;
  }
  if (fileTypes.length) {
    pickOpt.type = fileTypes;
  }
  const pickFile = async () => {
    try {
      const res = await pick(pickOpt);
      setPickResult(JSON.stringify(res));
      return res;
    } catch (err) {
      console.log(err);
      console.log('isCancel: ' + isCancel(err));
    }
  };

  return (
        <Button
         title="local url printing"
         onPress={async () => {
            const res = await pickFile();
            RNPrint.print({
                filePath: res[0].uri,
                jobName: 'huawei',
            });
            }}
        />
  );
}

```

## Use Codegen

Version >= @react-native-ohos/react-native-inappbrowser@0.11.1, The codegen-lib has been adapted to generate bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Version >= @react-native-ohos/react-native-print@0.11.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
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

```JSON
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-print": "file:../../node_modules/@react-native-ohos/react-native-print/harmony/print.har"
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

### 3.Configuring CMakeLists and Introducing PrintPackage

> If you are using version <= 0.11.0-0.0.3, please skip this chapter.

open `entry/src/main/cpp/CMakeLists.txt` and add:

``` cmake
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-print/src/main/cpp" ./print)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_print)
# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`and add:

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "PrintPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+        std::make_shared<PrintPackage>(ctx)
    };
}
```

### 4. Introducing RNPrintPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNPrintPackage} from '@react-native-ohos/react-native-print/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNPrintPackage(ctx)
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

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements

#### Include applicable permissions in the module.json5 file within the entry directory.

Open the `entry/src/main/module.json5` file and add the following code:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.PRINT",
+    "reason": "$string:print_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"always"
+    }
+  },
+  {
+    "name": "ohos.permission.INTERNET",
+    "reason": "$string:internet_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"always"
+    }
+  }
]
```

#### Apply the reasons for applicable permission in the entry directory.

Open the `entry/src/main/resources/base/element/string.json` file and add the following code:

```diff
...
{
  "string": [
+    {
+      "name": "print_reason",
+      "value": "Using a printer"
+    },
+    {
+      "name": "internet_reason",
+      "value": "Network request data"
+    },
  ]
}
```

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### print(options: Object)

| Name          | Description                                                   | Type    | Required | Platform     | HarmonyOS Support |
| ------------- | ------------------------------------------------------------- | ------- | -------- | ------------ | ----------------- |
| `html`        | HTML string to print(The value must be html or filepath.)     | string  | no       | Android, iOS| no                |
| `filePath`    | Local or remote file url(The value must be html or filepath.) | string  | no       | Android, iOS| yes               |
| `printerURL`  | **iOS Only:** URL returned from `selectPrinterMethod()`       | string  | no       | iOS          | no                |
| `isLandscape` | Landscape print; default value is false                       | boolean | no       | Android, iOS| no                |
| `jobName`     | Name of printing job; default value is "Document"             | string  | no       | Android, iOS| yes               |
| `baseUrl`     | Used to resolve relative links in the HTML                    | string  | no       | Android      | no                |

### selectPrinter(options: Object)

| Name | Description                        | Type   | Required | Platform | HarmonyOS Support |
| ---- | ---------------------------------- | ------ | -------- | -------- | ----------------- |
| `x`  | The x position of the popup dialog | number | yes      | iOS      | no                |
| `y`  | The y position of the popup dialog | number | yes      | iOS      | no                |

## Known Issues

- [ ] HarmonyOS NEXT does not support parameters such as **html**, **printerURL**, **isLandscape**, and **baseUrl**, and does not support printing of Word documents: [issue#1](https://github.com/react-native-oh-library/react-native-print/issues/1).
- [ ] HarmonyOS NEXT does not support **selectPrinter()**: [issue#2](https://github.com/react-native-oh-library/react-native-print/issues/4).

## Others

## License

This project is licensed under [MIT License](https://github.com/christopherdro/react-native-print/blob/master/LICENSE).

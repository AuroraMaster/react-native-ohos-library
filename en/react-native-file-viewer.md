> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-viewer
</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vinzscam/react-native-file-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-file-viewer)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 2.1.6@deprecated | [@react-native-oh-tpl/react-native-file-viewer Releases(deprecated)](https://github.com/react-native-oh-library/react-native-file-viewer/releases) | 0.72       |
| 2.1.7 | [@react-native-ohos/react-native-file-viewer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-viewer/releases)                        | 0.72       |
| 2.2.0 | [@react-native-ohos/react-native-file-viewer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-viewer/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-file-viewer
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-file-viewer
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { StyleSheet, ScrollView, Text, TouchableOpacity } from "react-native";
import DocumentPicker from "react-native-document-picker";
import FileViewer from "react-native-file-viewer";

export function FlieViewerExample() {
  const FileViewerTest = async (option?: any) => {
    try {
      const res: any = await DocumentPicker.pick({
        type: [DocumentPicker.types.allFiles],
      });
      await FileViewer?.open(res[0].uri, option);
    } catch (e) {
      // error
    }
  };

  const onDismissCb = () => {
    // do sth ...
  };

  return (
    <ScrollView style={{ backgroundColor: "skyblue" }}>
      <TouchableOpacity onPress={() => FileViewerTest()} style={styles.btn}>
        <Text style={styles.btnText}>Toogle Status Bar</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() => FileViewerTest("show_displayName string")}
        style={styles.btn}
      >
        <Text style={styles.btnText}>Toogle Status Bar (displayName str)</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() =>
          FileViewerTest({ displayName: "show_displayName option" })
        }
        style={styles.btn}
      >
        <Text style={styles.btnText}>Toogle Status Bar (displayName opt)</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() =>
          FileViewerTest({ showOpenWithDialog: true, onDismiss: onDismissCb })
        }
        style={styles.btn}
      >
        <Text style={styles.btnText}>Toogle Status Bar (onDismiss)</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() => FileViewerTest({ showOpenWithDialog: true })}
        style={styles.btn}
      >
        <Text style={styles.btnText}>
          Toogle Status Bar (showOpenWithDialog)
        </Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() => FileViewerTest({ showAppsSuggestions: true })}
        style={styles.btn}
      >
        <Text style={styles.btnText}>
          Toogle Status Bar (showAppsSuggestions)
        </Text>
      </TouchableOpacity>
    </ScrollView>
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
  btnText: {
    fontWeight: "bold",
    color: "#fff",
    fontSize: 20,
  },
  selectBtn: {
    padding: 8,
    margin: 3,
    fontSize: 18,
    borderWidth: 1,
    borderRadius: 8,
    borderColor: "#753c13",
  },
  selectBtnActive: {
    padding: 8,
    margin: 3,
    backgroundColor: "#e2803b",
    fontSize: 18,
    borderRadius: 8,
    borderWidth: 1,
  },
});
```

## Use Codegen


This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~2.2.0                               |  No                   |  0.77                |
| ~2.1.7                               |  Yes                  |  0.72                |
| <= 2.1.6@deprecated                  |  No                   |  0.72                |

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

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-file-viewer": "file:../../node_modules/@react-native-ohos/react-native-file-viewer/harmony/file_viewer.har"
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


### 3.configuring CMakeLists and introducing FileViewerPackage

> If you are using version <= 2.1.6, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt`，add：  

```cmake
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-file-viewer/src/main/cpp" ./file-viewer)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_file_viewer)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp`，add：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FileViewerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FileViewerPackage>(ctx)
    };
}
```


### 4. Introducing RNFileViewerTurboModule Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNFileViewerPackage } from '@react-native-ohos/react-native-file-viewer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFileViewerPackage(ctx)
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

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### `open(filepath: string, options?: Object): Promise<void>`

| Name                   | Description                                                                                                                                                                                                                                        | Type   | Required | Platform | HarmonyOS Support |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| **filepath**           | The absolute path where the file is stored. The file needs to have a valid extension to be successfully detected. Use [react-native-fs constants](https://github.com/itinance/react-native-fs#constants) to determine the absolute path correctly. | string | yes      | All      | yes               |
| **options** (optional) | Some options to customize the behaviour. See below.                                                                                                                                                                                                | Object | no       | All      | yes               |

#### Options

| Name                               | Description                                                                                       | Type     | Required | Platform | HarmonyOS Support |
| ---------------------------------- | ------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| **displayName** (optional)         | Customize the QuickLook title.                                                                    | string   | no       | iOS      | yes               |
| **onDismiss** (optional)           | Callback invoked when the viewer is being dismissed.                                              | function | no       | All      | partially         |
| **showOpenWithDialog** (optional)  | If there is more than one app that can open the file, show an _Open With_ dialogue box.           | boolean  | no       | Android  | yes               |
| **showAppsSuggestions** (optional) | If there is not an installed app that can open the file, open the Play Store with suggested apps. | boolean  | no       | Android  | partially         |

## Known Issues

- [x] HarmonyOS not support close preview window callback: [issue#1](https://github.com/react-native-oh-library/react-native-file-viewer/issues/4)
- [x] HarmonyOS not support jump to app market recommended apps page: [issue#2](https://github.com/react-native-oh-library/react-native-file-viewer/issues/5)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE).


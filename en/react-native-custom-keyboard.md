
> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-custom-keyboard</code> </h1>
</p>

This project is based on [react-native-custom-keyboard](https://github.com/reactnativecn/react-native-custom-keyboard) 。

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is：`@react-native-ohos/react-native-custom-keyboard` The version correspondence details are as follows：
| Name | Version | Release Information | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address     |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-custom-keyboard | ~1.1.0 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-custom-keyboard/releases) | 0.77.* | No | API23+ | 1.0.4 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-custom-keyboard) |
| @react-native-ohos/react-native-custom-keyboard | ~1.0.4 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-custom-keyboard/releases) | 0.72.* | Yes | API23+ | 1.0.4 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-custom-keyboard) |
| @react-native-oh-tpl/react-native-custom-keyboard | <= 1.0.3-0.0.2@deprecated | [Github Releases](https://github.com/react-native-oh-library/react-native-custom-keyboard/releases) | 0.72.* | No | API12+ | 1.0.3 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-custom-keyboard) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-ohos/react-native-custom-keyboard
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-custom-keyboard
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';  
import {  
  StyleSheet,  
  Text,  
  View,  
  TouchableOpacity,  
} from 'react-native';  

import {  
  CustomTextInput,  
  register,  
  insertText,  
  backSpace,  
} from 'react-native-custom-keyboard';  

/**  
 * Custom Keyboard Component  
 */  
const MyKeyboard = ({ tag }) => {  
  const onPress = (value) => {  
    insertText(tag, value);  
  };  

  return (  
    <View style={styles.keyboard}>  
      {[[1, 2, 3], [4, 5, 6], [7, 8, 9]].map((row, rowIndex) => (  
        <View style={styles.row} key={`row-${rowIndex}`}>  
          {row.map((num) => (  
            <View style={styles.button} key={num}>  
              <TouchableOpacity onPress={() => onPress(num.toString())}>  
                <Text style={styles.buttonLabel}>{num}</Text>  
              </TouchableOpacity>  
            </View>  
          ))}  
        </View>  
      ))}  
      <View style={styles.row}>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => onPress('0')}>  
            <Text style={styles.buttonLabel}>0</Text>  
          </TouchableOpacity>  
        </View>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => onPress('.')}>  
            <Text style={styles.buttonLabel}>.</Text>  
          </TouchableOpacity>  
        </View>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => backSpace(tag)}>  
            <Text style={styles.buttonLabel}>←</Text>  
          </TouchableOpacity>  
        </View>  
      </View>  
    </View>  
  );  
};  

register('price', () => MyKeyboard);  

/**  
 * Main Application Component  
 */  
const App = () => {  
  return (  
    <View style={styles.container}>  
      <CustomTextInput  
        customKeyboardType="price"  
        style={styles.input}  
      />  
    </View>  
  );  
};  

export default App;  

/**  
 * Style Definition  
 */  
const styles = StyleSheet.create({  
  container: {  
    flex: 1,  
    justifyContent: 'center',  
    alignItems: 'center',  
    backgroundColor: '#F5FCFF',  
  },  
  input: {  
    backgroundColor: '#ffffff',  
    borderWidth: 1,  
    borderColor: 'grey',  
    width: 270,  
    fontSize: 19,  
  },  
  keyboard: {  
    backgroundColor: 'white',  
  },  
  row: {  
    flexDirection: 'row',  
  },  
  button: {  
    width: '33.3333%',  
  },  
  buttonLabel: {  
    borderWidth: 0.5,  
    borderColor: '#d6d7da',  
    paddingVertical: 13,  
    textAlign: 'center',  
    fontSize: 20,  
  },  
});   
```

## 2. Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~1.1.0                               |  No                   |  0.77                |
| ~1.0.4                               |  Yes                  |  0.72                |
| <= 1.0.3-0.0.2@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.

  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.


### 2.1. Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2. Introducing Native Code

Currently, two methods are available:

1. Use the HAR file(recommended)；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-ohos/react-native-custom-keyboard": "file:../../node_modules/@react-native-ohos/react-native-custom-keyboard/harmony/custom_keyboard.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 2.3. Configuring CMakeLists and Introducing RNCustomKeyboardPackage Package

> If you are using version <= 1.0.3-0.0.2, please skip this chapter.

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-custom-keyboard/src/main/cpp" ./custom-keyboard)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_custom_keyboard_package)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CustomKeyboardPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<CustomKeyboardPackage>(ctx),
    };
}
```

### 2.4. Introducing RNCustomKeyboardPackage Package to ArkTS 

Open `entry/src/main/ets/RNPackagesFactory.ts` and add the following code:

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';

+import {RNCustomKeyboardPackage}  from '@react-native-ohos/react-native-custom-keyboard/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNCustomKeyboardPackage(ctx)
  ];
}
```


## 2.5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 3.2. API requirements

> [!TIP] All versions of the current third-party libraries have implemented version isolation, supporting compilation in `API12+` projects and execution on `API12+` ROMs.

> [!TIP] The following features depend on specific API versions. Compiling the project with an API version lower than specified or running the ROM with an API version lower than specified may result in limited functionality.

1. version >=1.0.4 for 0.72 introduced [setcustomkeyboardcontinuefeature](https://gitcode.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-arkui/arkts-apis-uicontext-uicontext.md#setcustomkeyboardcontinuefeature23), Implemented the custom keyboard continuation feature (resolved the issue of text hiding when switching custom keyboards).. This API requires compilation in a project that supports `API23+` and must run on a ROM that supports `API23+` to take effect.

2. version >=1.1.0 for 0.77 introduced [setcustomkeyboardcontinuefeature](https://gitcode.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-arkui/arkts-apis-uicontext-uicontext.md#setcustomkeyboardcontinuefeature23), Implemented the custom keyboard continuation feature (resolved the issue of text hiding when switching custom keyboards).. This API requires compilation in a project that supports `API23+` and must run on a ROM that supports `API23+` to take effect.


## 4. Properties (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                       | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | --------------------------------- | ------ | -------- | -------- | ----------------- |
| customKeyboardType | Use a registered custom keyboard. | string | no       | All      | yes               |

## 5. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                                                                                                                                                   | Type     | Required | Platform | HarmonyOS Support |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| register             | Register a custom keyboard type.                                                                                                                                                              | function | no       | All      | yes               |
| install              | Install custom keyboard to a TextInput.  Generally you can use CustomTextInput instead of this. But you can use this API to install/change custom keyboard dynamically.                       | function | no       | All      | yes               |
| uninstall            | Uninstall custom keyboard from a TextInput dynamically.                                                                                                                                       | function | no       | All      | yes               |
| insertText           | Use in a custom keyboard, insert text to TextInput.                                                                                                                                           | function | no       | All      | yes               |
| backSpace            | Use in a custom keyboard, delete selected text or the charactor before cursor.                                                                                                                | function | no       | All      | yes               |
| doDelete             | Use in a custom keyboard, delete selected text or the charactor after cursor.                                                                                                                 | function | no       | All      | yes               |
| moveLeft             | Use in a custom keyboard, move cursor to selection start or move cursor left.                                                                                                                 | function | no       | All      | yes               |
| moveRight            | Use in a custom keyboard, move cursor to selection end or move cursor right.                                                                                                                  | function | no       | All      | yes               |
| switchSystemKeyboard | Use in a custom keyboard. Switch to system keyboard.Next time user press or focus on the TextInput, custom keyboard will appear again. To keep using system keyboard, call uninstall instead. | function | no       | All      | yes               |

## 6. Others

## 7. Known Issues

## 8. License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org).
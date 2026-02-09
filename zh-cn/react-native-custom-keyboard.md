
> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-custom-keyboard</code> </h1>
</p>

本项目基于 [react-native-custom-keyboard](https://github.com/reactnativecn/react-native-custom-keyboard) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-custom-keyboard` 版本所属关系如下：
| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-custom-keyboard | ~1.1.0 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-custom-keyboard/releases) | 0.77.* | 否 | API23+ | 1.0.4 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-custom-keyboard) |
| @react-native-ohos/react-native-custom-keyboard | ~1.0.4 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-custom-keyboard/releases) | 0.72.* | 是 | API23+ | 1.0.4 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-custom-keyboard) |
| @react-native-oh-tpl/react-native-custom-keyboard | <= 1.0.3-0.0.2@deprecated | [Github Releases](https://github.com/react-native-oh-library/react-native-custom-keyboard/releases) | 0.72.* | 否 | API12+ | 1.0.3 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-custom-keyboard) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-ohos/react-native-custom-keyboard
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-custom-keyboard
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|------------------|-----------|
| ~1.1.0                               |  No              |  0.77     |
| ~1.0.4                               |  Yes             |  0.72     |
| <= 1.0.3-0.0.2@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK
为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2. 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-ohos/react-native-custom-keyboard": "file:../../node_modules/@react-native-ohos/react-native-custom-keyboard/harmony/custom_keyboard.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 RNCustomKeyboardPackage

> 若使用的是 <= 1.0.3-0.0.2 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 2.4. 在 ArkTs 侧引入 RNCustomKeyboardPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 3.2. 编译运行API要求
> [!TIP] 当前三方库所有版本均已实现版本隔离，支持在 `API12+` 工程编译，及 `API12+` ROM运行。

> [!TIP] 以下功能依赖特定版本的API，使用 `低于指定API版本的工程编译` 或 `低于指定API版本的ROM运行` 均可能导致部分功能受限。
1. 版本 >=1.0.4 for 0.72引入[setcustomkeyboardcontinuefeature](https://gitcode.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-arkui/arkts-apis-uicontext-uicontext.md#setcustomkeyboardcontinuefeature23)，实现了自定义键盘接续功能（解决自定义键盘切换text隐藏问题），此API需要在支持`API23+`的工程编译，并在支持`API23+`的ROM上运行，方可生效。
2. 版本 >=1.1.0 for 0.77引入[setcustomkeyboardcontinuefeature](https://gitcode.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-arkui/arkts-apis-uicontext-uicontext.md#setcustomkeyboardcontinuefeature23)，实现了自定义键盘接续功能（解决自定义键盘切换text隐藏问题），此API需要在支持`API23+`的工程编译，并在支持`API23+`的ROM上运行，方可生效。

## 4. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                       | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | --------------------------------- | ------ | -------- | -------- | ----------------- |
| customKeyboardType | Use a registered custom keyboard. | string | no       | All      | yes               |

## 5. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 6. 其他

## 7. 遗留问题

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。

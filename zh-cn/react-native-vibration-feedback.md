> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"><code>react-native-vibration-feedback</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nascimentorafael/react-native-vibration-feedback">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-vibration-feedback/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-vibration-feedback)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.0.1     | [@react-native-ohos/react-native-vibration-feedback Releases](https://github.com/react-native-oh-library/react-native-vibration-feedback/releases) | 0.72       |
| 1.1.0     | [@react-native-ohos/react-native-vibration-feedback Releases](https://github.com/react-native-oh-library/react-native-vibration-feedback/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-vibration-feedback
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-vibration-feedback
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Button} from "react-native";
import {TestCase, Tester, TestSuite} from "@rnoh/testerino"
import RNVibrationFeedback from 'react-native-vibration-feedback';

const App = (props) => {

  return (
    <Tester style={{flex: 1 , marginTop: 30}}>
      <TestSuite name='vibration-feedback'>
          <View style={{ margin: 50, flexDirection: "column", justifyContent: "space-between" }}>
            <View>
              <TestCase itShould={"Peek"}>
                <Button
                title="Peek"
                onPress={() => RNVibrationFeedback.vibrateWith(1519)}
                />
              </TestCase>
              <TestCase itShould={"Pop"}>
                <Button
                title="Pop"
                onPress={() => RNVibrationFeedback.vibrateWith(1520)}
                />
              </TestCase>
              <TestCase itShould={"Nope"}>
                <Button
                title="Nope"
                onPress={() => RNVibrationFeedback.vibrateWith(1521)}
                />
              </TestCase>
            </View>
          </View>
      </TestSuite>  
    </Tester>
  );
};

export default App
```

## 使用 Codegen


本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前暂不支持AutoLink，所以Link步骤需要手动配置。

首先需要使用DevEco Studio打开项目里的HarmonyOS工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```


### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-vibration-feedback": "file:../../node_modules/@react-native-ohos/react-native-vibration-feedback/harmony/vibration_feedback.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 ViewShotPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-vibration-feedback/src/main/cpp" ./vibration-feedback)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_vibration_feedback)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ReactNativeVibrationFeedbackPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReactNativeVibrationFeedbackPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 BlePlxPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+   import {RNVibrationFeedbackPackage} from '@react-native-ohos/react-native-vibration-feedback/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNVibrationFeedbackPackage(ctx)
  ];
}
```

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

1. RNOH：0.72.90; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.112;
2. RNOH：0.72.90; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：5.0.0.102;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.112;
4. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 6.0.0.858; ROM：5.0.0.102;

### 权限要求

- 由于此库涉及振动功能，使用对应接口时则需要配置对应的权限，权限需配置在entry/src/main目录下module.json5文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要normal权限：ohos.permission.VIBRATE。

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### RNVibrationFeedback
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| vibrateWith(id: number)  | 触发指定id的震动         | void | yes | iOS/Android      | yes |
## 遗留问题

## 其他
提供以下三种震动类型
|  ID  | Name |           Description           |
|:----:|:----:|:-------------------------------:|
| 1519 | Peek | 弱短震动
| 1520 | Pop  | 强烈的短震动        |
| 1521 | Nope | 短时间内三次震动  |
1521这个震动需要在API18以上才会生效，API18以下使用该震动，会自动变为1519的震动类型。

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/react-native-oh-library/react-native-vibration-feedback/blob/sig/LICENSE). ，请自由地享受和参与开源。

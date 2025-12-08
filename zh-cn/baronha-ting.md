> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@baronha/ting</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/<原库源码仓地址>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/baronha/ting/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/ting)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 1.2.2-0.0.3@deprecated  | [@react-native-oh-tpl/ting Releases(deprecated)](https://github.com/react-native-oh-library/ting/releases) | 0.72       |
| 1.2.3             | [@react-native-ohos/ting Releases](https://gitcode.com/openharmony-sig/rntpc_ting/releases)   | 0.72       |
| 1.3.0             | [@react-native-ohos/ting Releases](https://gitcode.com/openharmony-sig/rntpc_ting/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/ting
```

#### **yarn**

```bash
yarn add @react-native-ohos/ting
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, Button } from "react-native";
import {
    ToastOptions,
    toast
} from '@baronha/ting';

function handleToast(options: ToastOptions) {
    toast(options);
}

const App = () => {
  return (
    <View style={{ justifyContent: 'center', alignItems: 'center', flex: 1 }}>
      <Button
        title="defalut"
        onPress={() => {
          const options: ToastOptions = {
            title: 'title-Toast',
            message: 'message-Toast',
          };
          handleToast(options);
        }}
      />
    </View>
  );
};

export default App;
```

## 使用 Codegen

Version >= @react-native-ohos/ting@1.2.3，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/ting@1.2.3，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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
    "@react-native-ohos/ting": "file:../../node_modules/@react-native-ohos/ting/harmony/ting.har"
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

### 3. 配置 CMakeLists 和引入 RNTingPackage

> 若使用的是 <=1.2.2-0.0.3 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/Ting/src/main/cpp" ./ting)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_ting)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "TingPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<TingPackage>(ctx)
}
```

### 4.在 ArkTs 侧引入 RNTingPackage

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
  ...
+ import {RNTingPackage} from '@react-native-ohos/ting';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTingPackage(ctx)
  ];
}
```

### 5.运行

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

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### ToastOptions

| Name                 | Description                                             | Type | Required | Platform | HarmonyOS Support   |
|----------------------|---------------------------------------------------------|------|----------|----------|---------------------|
| title                | Toast 标题文本                                       | string   | no        | All      | yes  |
| message              | Toast 消息文本                                     | string   | no        | All      | yes  |
| titleColor           | 标题文本颜色（十六进制格式）      | string   | no        | All      | yes  |
| messageColor         | 消息文本颜色（十六进制格式）    | string   | no        | All      | yes  |
| preset               |  Toast 预设样式。选项包括：done（成功）、error（错误）、none（无样式）、spinner（加载指示器）  | string  | no        | All      | partially |
| duration             | Toast 显示时长（秒）                    | number  | no         | All      | yes  |
| haptic               | 触觉反馈类型。选项包括：success（成功）、warning（警告）、error（错误）、none（无触觉反馈） | string  | no         | iOS      | yes                 |
| shouldDismissByDrag  | 是否可以通过拖拽关闭 Toast  | boolean  | no        | All      | yes  |
| position             | Toast 显示位置（顶部或底部）                  | string   | no         | All      |yes                 |
| backgroundColor      | Toast 背景颜色（十六进制格式）| string   | no         | All      |yes       |
| icon                 | 自定义图标  | object  | no        | All      | yes  |
| progressColor        | spinner 预设样式的进度指示器颜色 | string  | no        | Android   | yes  |

### AlertOptions

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title                | Alert 标题文本                                       | string   | no        | All      | yes  |
| message              | Alert 消息文本                                     | string   | no        | All      | yes  |
| titleColor           | 标题文本颜色（十六进制格式）      | string   | no        | All      | yes  |
| messageColor         | 消息文本颜色（十六进制格式）    | string   | no        | All      | yes  |
| preset               |  Alert 预设样式。选项包括：done（成功）、error（错误）、none（无样式）、spinner（加载指示器）| string  | no        | All      | partially |
| duration             | Alert 显示时长（秒）     | number  | no         | All      | yes  |
| haptic               | 触觉反馈类型。选项包括：success（成功）、warning（警告）、error（错误）、none（无触觉反馈） | string  | no         | iOS      | yes                 |
| shouldDismissByTap  | 是否可以通过点击关闭 Alert      | boolean  | no        | All      | yes  |
| backgroundColor      | Alert 背景颜色（十六进制格式）| string   | no         | All      |yes       |
| borderRadius  | Alert 边框圆角半径，决定圆角程度   | number  | no | All      | yes |
| blurBackdrop  | Android 平台上背景模糊效果的强度    | number  | no | Android      | no |
| backdropOpacity  | 背景模糊效果的不透明度，范围从 0（完全透明）到 1（完全不透明）  | number  | no | All      | yes |
| icon                 | 自定义图标                                                     | object  | no        | All      | yes  |
| progressColor        | spinner 预设样式的进度指示器颜色                                                 | string  | no        | Android   | yes  |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| toast  | 显示 Toast 通知       | function  | yes | All      | yes |
| alert  | 显示 Alert 对话框         | function  | yes | All      | yes |
| dismissAlert  | 关闭当前显示的 Alert 对话框        | function  | yes | All      | yes |
| setup  | 配置 Toast 和 Alert 的全局设置         | function  | yes | All      | yes |

## 遗留问题

- [ ] AlertOptions和ToastOptions中的preset：done，动画效果未实现。[issue#3](https://github.com/react-native-oh-library/ting/issues/3)

## 其他

- AlertOptions中的blurBackdrop参数配置后，iOS不支持，Android无效果。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/baronha/ting/blob/main/LICENSE) ，请自由地享受和参与开源。
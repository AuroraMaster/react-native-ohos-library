> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>@react-native-picker/picker</code> </h1>
</p>

本项目基于 [@react-native-picker/picker](https://github.com/react-native-picker/picker) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/picker` 版本所属关系如下：

| 三方库名称                  | 三方库版本          | 发布信息                                                     | 支持RN版本 | Autolink | 编译API版本 | 社区基线版本 | npm地址                                                      |
| --------------------------- | ------------------- | ------------------------------------------------------------ | ---------- | -------- | ----------- | ------------ | ------------------------------------------------------------ |
| @react-native-ohos/picker   | ~ 2.12.0            | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_picker/releases) | 0.82.*     | 否       | API12+      | 2.11.4       | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/picker) |
| @react-native-ohos/picker   | ~2.11.2             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_picker/releases) | 0.77.*     | 否       | API12+      | 2.11.1       | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/picker) |
| @react-native-ohos/picker   | ~ 2.6.4             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_picker/releases) | 0.72.*     | 是       | API12+      | 2.6.1        | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/picker) |
| @react-native-oh-tpl/picker | <= 2.6.3@deprecated | [Github Releases(deprecated)](https://github.com/react-native-oh-library/picker) | 0.72.*     | 否       | API12+      | 2.6.1        | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/picker) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/picker
```

#### **yarn**

```bash
yarn add @react-native-ohos/picker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from "react";
import { Picker } from "picker";

import { View } from "react-native";

export const PickerExample = ()=>{
  const [selectedLanguage, setSelectedLanguage] = React.useState();

  return (
    <View style={{backgroundColor:"#fff",padding:40}}>
      <Picker
        selectedValue={selectedLanguage}
        onValueChange={(itemValue, itemIndex) => setSelectedLanguage(itemValue)}>
        <Picker.Item label="Java" value="java" />
        <Picker.Item label="JavaScript" value="js" />
      </Picker>
    </View>
  )
}
```

## 2. Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~2.12.0 | No | 0.82 |
| ~2.11.2                              |  No              |  0.77  |
| ~2.6.4                              |  Yes             |  0.72     |
| <= 2.6.3@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。

<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>


首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

此步骤为手动配置原生依赖项的指导。

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

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/picker": "file:../../node_modules/@react-native-ohos/picker/harmony/picker.har",
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 PickerPackage

> 若使用的是 <=  2.6.3 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/picker/src/main/cpp" ./picker)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_picker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "PickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<PickerPackage>(ctx)
    };
}
```


### 2.4. 在 ArkTs 侧引入 picker 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNCPicker, PICKER_TYPE } from "@react-native-ohos/picker"

 @Builder
 export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === PICKER_TYPE) {
+   RNCPicker({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
+ PICKER_TYPE
  ];
```

### 2.5. 在 ArkTs 侧引入 RNCPickerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNCPickerPackage } from '@react-native-ohos/picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNCPickerPackage(ctx)
  ];
}
```

</details>

### 2.6. 运行

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
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM: 6.0.0.120 SP7;

## 4.属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### PickerProps

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `onValueChange` | 选中某项时的回调函数。 | function | No | All | Yes |
| `selectedValue` | 与其中某项的值相匹配的值。可以是字符串或整数。 | any | No | All | Yes |
| `style` | 应用于 Picker 视图的样式。 | pickerStyleType | No | All | Yes |
| `testID` | 用于在端到端测试中定位此视图。 | string | No | All | Yes |
| `enabled` | 如果设置为 false，选择器将被禁用，即用户将无法进行选择。 | boolean | No | Android, Web, Windows | Yes |
| `mode` | 在 Android 上，指定用户点击选择器时如何显示选项。 | enum('dialog', 'dropdown') | No | Android | No |
| `dropdownIconColor` | 在 Android 上，指定下拉三角形的颜色。 | ColorValue | No | Android | No |
| `dropdownIconRippleColor` | 在 Android 上，指定下拉三角形的波纹颜色。 | ColorValue | No | Android | No |
| `prompt` | 此选择器的提示字符串，在 Android 的 dialog 模式下用作对话框标题。 | string | No | Android | No |
| `itemStyle` | 应用于每个选项标签的样式。 | [text styles](https://reactnative.dev/docs/text-style-props) | No | iOS, Windows | partially |
| `numberOfLines` | 在 Android 和 iOS 上，用于在计算文本布局后用省略号截断文本。 | number | No | Android, iOS | No |
| `onBlur` | 当选择器失去焦点时的回调函数。 | function | No | Android | No |
| `onFocus` | 当选择器获得焦点时的回调函数。 | function | No | Android | No |
| `selectionColor` | 应用于选中指示器的颜色。 | ColorValue | No | iOS | Yes |
| `themeVariant` | 指定 iOS 上的主题变体（例如 'light' 或 'dark'）。 | enum('light', 'dark') | No | iOS | No |

### PickerItemProps

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `label` | 显示在 Picker 选项上的文字。 | string | Yes | All | Yes |
| `value` | Picker 选项的实际值。 | number,string | Yes | All | Yes |
| `color` | Picker 选项显示的颜色。 | ColorValue | No | All | No |
| `fontFamily` | Picker 选项显示的字体。 | string | No | All | No |
| `style` | 应用于单个选项标签的样式。 | ViewStyleProp | No | Android | No |
| `enabled` | 如果设置为 false，该特定选项将被禁用，即用户无法选中它。 | boolean | No | Android | No |
| `contentDescription` | 设置 Picker 选项的内容描述。 | string | No | Android | No |

## 5. 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `blur` | 以编程方式关闭选择器。 | function | No | Android | No |
| `focus` | 以编程方式打开选择器。 | function | No | Android | No |

## 6. API

## 7. 遗留问题

- [ ] numberOfLines 属性不支持[issue#2](https://github.com/react-native-oh-library/picker/issues/2)
- [ ] PickerItemProps 的 color 和 fontFamily 不支持（OH 的 Picker 组件不支持单独设置 PickerItem 的样式） [issue#21](https://github.com/react-native-oh-library/picker/issues/21)
- [ ] themeVariant 属性不支持[issue#22](https://github.com/react-native-oh-library/picker/issues/22)
- [ ] itemStyle 不支持设置 textAlign（OH 的 Picker 不支持设置）[issue#23](https://github.com/react-native-oh-library/picker/issues/23)

## 8. 其他

## 9. 开源协议

本项目基于 [The MIT License (MIT)](https://gitcode.com/openharmony-sig/rntpc_picker/blob/master/LICENSE) ，请自由地享受和参与开源。


模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-date-picker</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/henninghall/react-native-date-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/henninghall/react-native-date-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-date-picker)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-date-picker`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 5.0.5      | [@react-native-oh-tpl/react-native-date-picker Releases](https://github.com/react-native-oh-library/react-native-date-picker/releases) | 0.72       |
| 5.1.0      | [@react-native-ohos/react-native-date-picker Releases]()     | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-date-picker

# 0.77
npm install @react-native-ohos/react-native-date-picker
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-date-picker

# 0.77
yarn add @react-native-ohos/react-native-date-picker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react'
import { Button, View } from 'react-native'
import DatePicker from 'react-native-date-picker'

export default () => {
  const [date, setDate] = useState(new Date())
  const [open, setOpen] = useState(false)

  return (
    <View style={{flex:1, flexDirection:'column', justifyContent:'center'}}>
      <Button title="Open" onPress={() => setOpen(true)} />
      <DatePicker
        mode='date'
        modal
        open={open}
        date={date}
        onConfirm={(date) => {
          setOpen(false)
          setDate(date)
        }}
        onCancel={() => {
          setOpen(false)
        }}
      />
    </View>
  )
}


```

## 使用 Codegen

> [!TIP] 0.77 不需要使用Codegen。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

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

-  0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-date-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-date-picker/harmony/date_picker.har"
  }
```

-  0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-date-picker": "file:../../node_modules/@react-native-ohos/react-native-date-picker/harmony/date_picker.har"
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

### 3.配置 CMakeLists 和引入 RNDatePickerPackage

> [!TIP] 仅 0.77需要配置CMakeLists 和引入 RNDatePickerPackage。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
txtproject(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULE "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

+ add_subdirectory("${OH_MODULE}/@react-native-ohos/react-native-date-picker/src/main/cpp" ./date_picker)

# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_date_picker)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "DatePickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<DatePickerPackage>(ctx), 
    };
}
```

### 4.在 ArkTs 侧引入 RNDatePicker 组件

找到 **function buildCustomRNComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
//  0.72
+ import { RNDatePicker } from "@react-native-oh-tpl/react-native-date-picker"

//  0.77
+ import { RNDatePicker } from "@react-native-ohos/react-native-date-picker"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNDatePicker.NAME) {
+   RNDatePicker({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+   })
+ }
 ...
}
...
```
> [!TIP] 本库使用了混合方案，需要添加组件名。

在entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets 找到常量 arkTsComponentNames 在其数组里添加组件名

```diff
  ...
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNDatePicker.NAME, 
  ];
```

### 5. 在 ArkTs 侧引入 RNDatePickerPackage

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
//  0.72
+ import {RNDatePickerPackage} from '@react-native-oh-tpl/react-native-date-picker/ts';

//  0.77
+ import {RNDatePickerPackage} from '@react-native-ohos/react-native-date-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNDatePickerPackage(ctx)
  ];
}
```
### 6.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

### 兼容性

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| props                   | Description                                                  | Type                                                        | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ----------------------------------------------------------- | -------- | -------- | ----------------- |
| date                    | 当前选中的日期                                               | Date                                                        | no       | all      | yes               |
| onDateChange            | 日期变化处理器（仅内联模式有效）                             | (date: Date) => void                                        | no       | all      | yes               |
| maximumDate             | 最大可选日期。示例：new Date ("2021-12-31")                  | Date                                                        | no       | all      | yes               |
| minimumDate             | 最小可选日期。示例：new Date ("2021-01-01")                  | Date                                                        | no       | all      | yes               |
| mode                    | 日期选择器模式。可选值："datetime"（日期时间）、"date"（仅日期）、"time"（仅时间） | “'date' \|'time' \| 'datetime'”                             | yes      | all      | yes               |
| onConfirm               | 仅模态框模式有效：用户点击确认按钮时的日期回调函数           | (date: Date) => void                                        | no       | all      | yes               |
| onCancel                | 仅模态框模式有效：用户点击取消按钮或点击模态框外部关闭时的回调函数 | () => void                                                  | no       | all      | yes               |
| is24hourSource          | 24 小时制（上午 / 下午）模式的判定来源，可选设备设置或区域设置。取值：{'locale'（区域设置）, 'device'（设备设置）}（仅 Android 支持，默认值：'device'） | “'locale' \| 'device'”                                      | no       | all      | no                |
| modal                   | 是否启用模态框模式的布尔值。默认值："false"。启用后，需配合其他模态框相关属性使用 | boolean                                                     | no       | all      | yes               |
| open                    | 仅模态框模式有效：控制模态框是否打开的布尔值                 | boolean                                                     | no       | all      | yes               |
| minuteInterval          | 分钟选择的间隔。可选值：1、2、3、4、5、6、10、12、15、20、30 | 1 \| 2 \| 3 \| 4 \| 5 \| 6 \|  10 \|  12 \| 15 \|  20 \| 30 | no       | all      | no                |
| title                   | 仅模态框模式有效：标题文本。设为 null 可隐藏文本             | string                                                      | no       | all      | no                |
| confirmText             | 仅模态框模式有效：确认按钮文本                               | string                                                      | no       | all      | no                |
| cancelText              | 仅模态框模式有效：取消按钮文本                               | string                                                      | no       | all      | no                |
| theme                   | 仅模态框模式有效：模态框主题。可选值："light"（浅色）、"dark"（深色）、"auto"（自动）。默认值："auto" | 'light' \| 'dark' \| 'auto'                                 | no       | all      | no                |
| buttonColor             | 确认和取消按钮的颜色（仅 Android 模态框支持）                | string                                                      | no       | Android  | no                |
| dividerColor            | 分隔线颜色（仅 Android 支持）                                | string                                                      | no       | Android  | no                |
| onStateChange           | 加载状态变化处理器。在 "idle"（空闲）和 "spinning"（加载中）状态切换时触发（仅 Android 内联模式支持） | (state: 'spinning' \| 'idle') => void                       | no       | Android  | no                |
| locale                  | 日期选择器的区域设置。影响语言、日期顺序和上午 / 下午偏好。值需为区域 ID（如 "zh-CN"、"en-US"） | string                                                      | no       | all      | no                |
| timeZoneOffsetInMinutes | 时区偏移量（单位：分钟，默认值：设备当前时区）               | number                                                      | no       | all      | no                |


## 遗留问题
 
- [ ]  不支持属性confirmText。[issue#11](https://github.com/react-native-oh-library/react-native-date-picker/issues/11)
- [ ]  不支持属性cancelText。[issue#12](https://github.com/react-native-oh-library/react-native-date-picker/issues/12)
- [ ]  不支持属性theme。[issue#13](https://github.com/react-native-oh-library/react-native-date-picker/issues/13)
- [ ]  不支持属性locale。[issue#17](https://github.com/react-native-oh-library/react-native-date-picker/issues/17)
- [ ]  不支持属性timeZoneOffsetInMinutes。[issue#18](https://github.com/react-native-oh-library/react-native-date-picker/issues/18)
- [ ]  当属性modal为false，mode属性为datetime时，harmonyOS不支持内联datetime组件。[issue#22](https://github.com/react-native-oh-library/react-native-date-picker/issues/22)
- [ ]  不支持is24hourSource属性。[issue#30](https://github.com/react-native-oh-library/react-native-date-picker/issues/30)
- [ ]  不支持minuteInterval属性。[issue#34](https://github.com/react-native-oh-library/react-native-date-picker/issues/34)
## 其他
- 该三方库封装了 ArkUI DatePicker 组件，存在某些异常情形，请参考查阅[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V13/ts-basic-components-datepicker-V13#datepickeroptions%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)，滑出设置范围的日期需要等会有拖尾动画属性结束才会回弹。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/henninghall/react-native-date-picker/blob/master/LICENSE) ，请自由地享受和参与开源。

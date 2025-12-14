> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/datetimepicker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-datetimepicker/datetimepicker">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
       <a href="https://github.com/react-native-datetimepicker/datetimepicker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/datetimepicker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 7.6.2-0.1.1@deprecated      | [@react-native-oh-tpl/datetimepicker Releases(deprecated)](https://github.com/react-native-oh-library/datetimepicker/releases) | 0.72       |
| 7.6.3      | [@react-native-ohos/datetimepicker Releases](https://gitcode.com/openharmony-sig/rntpc_datetimepicker/releases) | 0.72       |
| 8.4.3      | [@react-native-ohos/datetimepicker Releases](https://gitcode.com/openharmony-sig/rntpc_datetimepicker/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/datetimepicker
```

#### **yarn**

```bash
yarn add @react-native-ohos/datetimepicker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react'
import DateTimePicker from '@react-native-community/datetimepicker';
import { SafeAreaView, Button, Text } from 'react-native'

export const MDatetimepicker = () => {
  const [date, setDate] = useState(new Date(new Date()));
  const [mode, setMode] = useState('date');
  const [show, setShow] = useState(false);

  const onChange = (event: any, selectedDate: any) => {
    const currentDate = selectedDate;
    setShow(false);
    setDate(currentDate);
  };

  const showMode = (currentMode: React.SetStateAction<string>) => {
    setShow(true);
    setMode(currentMode);
  };

  const showDatepicker = () => {
    showMode('date');
  };

  const showTimepicker = () => {
    showMode('time');
  };

  return (
    <SafeAreaView>
      <Button onPress={showDatepicker} title="Show date picker!" />
      <Button onPress={showTimepicker} title="Show time picker!" />
      <Text>selected: {date.toLocaleString()}</Text>
      {show && (
        <DateTimePicker
          mode={mode}//partially (仅支持 date/time 模式)
          style={{ width: 180, height: 80, backgroundColor: '#FFFFDD' }}
          display='default' //partially (支持"default"，"spinner"，"compact"，"inline")
          onChange={onChange}//partially (仅支持 type 为 set 类型)
          value={date}
          is24Hour={true} 
          disabled={false} 
          textColor={'#FFFFFF'}
        />
      )}
    </SafeAreaView>
  );
};
```

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~8.4.3                               |  No              |  0.77     |
| ~7.6.3                               |  Yes             |  0.72     |
| <= 7.6.2-0.1.1@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md。

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/datetimepicker": "file:../../node_modules/@react-native-ohos/datetimepicker/harmony/datetimepicker.har"
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

### 3.配置 CMakeLists 和引入 datetimepicker

> 若使用的是 <= 7.6.2-0.1.1 版本，请跳过本章。

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/datetimepicker/src/main/cpp" ./datetimepicker)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_datetime_picker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "DateTimePickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<DateTimePickerPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 DateTimePicker 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNDateTimePicker, DATETIME_PICKER_VIEW_TYPE } from "@react-native-ohos/datetimepicker"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === DATETIME_PICKER_VIEW_TYPE) {
+   RNDateTimePicker({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
 ...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。（如使用混合方案）

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ DATETIME_PICKER_VIEW_TYPE
];
```
</details>

## 运行

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

详情请查看[datetimepicker 官方文档](https://github.com/react-native-datetimepicker/datetimepicker)

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `mode` | 定义选择器的类型 | string | 否 | All | partially (仅支持 date/time 模式) |
| `style` | 直接设置选择器组件的样式。 | object | 否 | IOS only | yes |
| `display` | 定义选择器的视觉显示方式。默认值为 "default"。 | string | 否 | All | partially (支持"default"，<br/>"spinner"，"compact"，"inline") |
| `design` | 定义选择器是否应使用 Material 3 组件或默认选择器。默认值为 "default"。 | string | 否 | Android only | No |
| `initialInputMode` | 仅当 design 为 "material" 时生效。允许设置选择器的初始输入模式。 | string | 否 | Android only | No |
| `title` | 仅当 design 为 "material" 时生效。允许设置选择器对话框的标题。 | string | 否 | Android only | No |
| `fullscreen` | 仅当 design 为 "material" 时生效。允许设置日期选择器对话框全屏显示。 | bool | 否 | Android only | No |
| `onChange` | 日期变更处理程序。 | function | 否 | All | partially (仅支持 type 为 set 类型) |
| `value` | 定义组件中使用的日期或时间值。 | Date | 是 | All | partially (仅 mode=date 且 <br/>display=spinner 时支持动态设置) |
| `is24Hour` | 允许将时间选择器更改为 24 小时制格式。 | bool | 否 | Windows and Android only | yes |
| `maximumDate` | 定义可选择的最大日期。 | Date | 否 | All | partially (仅支持在 mode=date 且 <br/>display=spinner 时设置) |
| `minimumDate` | 定义可选择的最小日期。 | Date | 否 | All | partially (仅支持在 mode=date 且 <br/>display=spinner 时设置) |
| `disabled` | 如果为 true，用户将无法与该视图交互。 | bool | 否 | IOS only | yes |
| `textColor` | 允许更改日期选择器的文本颜色。 | string | 否 | IOS only | partially (仅支持在 mode=date 且 <br/>display=compact 时设置) |
| `timeZoneName` | 允许更改日期选择器的时区。默认情况下，使用设备的时区。<br/>使用来自 https://en.wikipedia.org/wiki/List_of_tz_database_time_zones 的 IANA (TZDB) 数据库名称中的时区名称。 | string | 否 | iOS and Android only | No |
| `timeZoneOffsetInMinutes` | 允许更改日期选择器的时区。<br/>默认情况下，使用设备的时区。<br/>我们强烈建议改用 timeZoneName 属性；<br/>此属性在 Android 实现中存在已知问题（例如 #528）。 | number | 否 | iOS and Android only | No |
| `timeZoneOffsetInSeconds` | 允许更改日期选择器的时区。<br/>默认情况下，使用设备的时区。 | number | 否 | Windows only | No |
| `dayOfWeekFormat` | 设置星期标题的显示格式。<br/>参考：https://docs.microsoft.com/en-us/uwp/api/windows.<br/>ui.xaml.controls.calendarview.dayofweekformat?view=winrt-18362#remarks | string | 否 | Windows only | No |
| `dateFormat` | 设置选择器文本框中日期值的显示格式。<br/>参考：https://docs.microsoft.com/en-us/uwp/api/windows.globalization.datetimeformatting.datetimeformatter?view=winrt-18362#examples | string | 否 | Windows only | No |
| `firstDayOfWeek` | 指定哪一天显示为一周的第一天。 | number | 否 | Android and Windows only | No |
| `accentColor` | 允许更改日期选择器的强调色（tintColor）。<br/>当 display 为 "spinner" 时无效。 | string | 否 | iOS only | No |
| `themeVariant` | 允许覆盖日期选择器使用的系统主题变体（深色或浅色模式）。<br/>但是，我们建议您使用 react-native-theme-control 来控制整个应用程序的主题。 | string | 否 | iOS only | No |
| `locale` | 允许更改组件的区域设置（locale）。<br/>这会影响显示的文本和日期/时间格式。<br/>默认情况下，使用设备的区域设置。<br/>请注意，不建议使用此属性，因为它在所有选择器模式下工作均不可靠。建议按照“本地化说明”中的记录进行本地化。 | string | 否 | iOS only | No |
| `positiveButton` | 设置确认按钮（positive button）的标签和文本颜色。 | Object | 否 | Android only | No |
| `neutralButton` | 允许在选择器对话框上显示中性按钮。<br/>按下按钮可以在 onChange 处理程序中通过 event.type === 'neutralButtonPressed' 观察到。 | Object | 否 | Android only | No |
| `negativeButton` | 设置取消按钮（negative button）的标签和文本颜色。 | Object | 否 | Android only | No |
| `minuteInterval` | 可选分钟的时间间隔。<br/>可能的值为：1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30。<br/>在 Windows 上，这可以是 0-59 之间的任意数字。 | number | 否 | All | No |
| `testID` | 通常由应用自动化框架使用。<br/>在 iOS 上完全支持。<br/>在 Android 上，仅在 mode="date" 时支持。 | string | 否 | All | Yes |
| `ViewProps` | 在 iOS 上，您可以将任何 View 属性传递给组件。<br/>鉴于底层组件是原生视图，<br/>不能保证支持所有属性，<br/>但 testID 和 onLayout 是有效的。 | Object | 否 | iOS only | No |
| `onError` | 当日期选择器原生代码内部发生错误（如 activity 为空）时调用的回调。 | function | 否 | Android only | No |


## 遗留问题

- [x] 已解决：textColor 属性在 compact 和 inline 模式改变值后使用禁用操作，颜色会变白色[issue#17](https://github.com/react-native-oh-library/datetimepicker/issues/17)
- [ ] 部分接口，未适配: [issue#20](https://github.com/react-native-oh-library/datetimepicker/issues/20#issue-2390348970)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-datetimepicker/datetimepicker/blob/master/LICENSE.md) ，请自由地享受和参与开源。
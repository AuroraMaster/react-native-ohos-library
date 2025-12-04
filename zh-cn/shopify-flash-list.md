> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@shopify/flash-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Shopify/flash-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Shopify/flash-list/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" /> 
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/flash-list)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 1.6.3-0.2.9@deprecated  | [@react-native-oh-tpl/flash-list Releases(deprecated)](https://github.com/react-native-oh-library/flash-list/releases) | 0.72       |
| 1.6.4                      | [@react-native-ohos/flash-list Releases](https://gitcode.com/openharmony-sig/rntpc_flash-list/releases)   | 0.72       |
| 1.8.3                      | [@react-native-ohos/flash-list Releases](https://gitcode.com/openharmony-sig/rntpc_flash-list/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-ohos/flash-list
```

#### **yarn**

```bash
yarn add @react-native-ohos/flash-list
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Text } from "react-native";
import { FlashList } from "@shopify/flash-list";

const DATA = [
  {
    title: "First Item",
  },
  {
    title: "Second Item",
  },
];

const MyList = () => {
  return (
    <FlashList
      data={DATA}
      renderItem={({ item }) => <Text>{item.title}</Text>}
      estimatedItemSize={200}
    />
  );
};
```

## Link

Version >= @react-native-ohos/flash-list@1.6.4，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.77.86" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
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
    "@react-native-ohos/flash-list": "file:../../node_modules/@react-native-ohos/flash-list/harmony/flash_list.har"
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

### 3.配置 CMakeLists 和引入 FlashListPackage

> V1.6.4 需要配置 CMakeLists 和引入 FlashListPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/flash-list/src/main/cpp" ./flash-list)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_flash_list)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FlashListPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FlashListPackage>(ctx)
    };
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

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| contentContainerStyle                  | 可通过 contentContainerStyle 为整个内容区域设置内边距。                                                                                                                    | ContentStyle        | No       | All      | Yes                |
| estimatedListSize                      | 列表的预估可见高度和宽度（非滚动内容尺寸）。定义该属性可让列表立即渲染，否则列表需先测量自身尺寸，导致首次渲染稍有延迟。 | object              | No       | All      | Yes                |
| horizontal                             | 设置为 true 时，项目将水平并列排列而非垂直堆叠。默认为 false。                                                                                                                   | boolean             | No       | All      | Yes |
| keyExtractor                           | 用于为指定索引位置的项生成唯一键值。键值用于优化性能。                                                                                                                       | function            | No       | All      | Yes                |
| numColumns                             | Multiple columns can only be rendered with horizontal={false} and will zig-zag like a flexWrap layout. Items should all be the same height - masonry layouts are not supported.                                                                                | number              | No       | All      | Yes                |
| extraData                              | 用于指示列表重新渲染的标记属性（因列表实现为 PureComponent）。                                                                                                                                  | any                 | No       | All      | Yes                |
| drawDistance                           | 预渲染的绘制距离。                                                                                                                                                                                                   | number              | No       | All      | Yes                |
| estimatedItemSize                      | 用于在项目渲染前向 FlashList 提示项目近似尺寸的单个数值。                                                                                            | number              | No       | All      | Yes                |
| viewabilityConfig                      | 用于判定项目可见性的默认配置。                                                                                                                                                       | object              | No       | All      | Yes                |
| renderItem                             | 从 data 中获取项目并渲染至列表                                                                                                                                                                                        | function            | Yes      | All      | Yes                |
| data                                   | 数据源，为指定类型的简单项目数组。                                                                                                                                                                               | ItemT[]             | Yes      | All      | Yes                |
| CellRendererComponent                  | 每个单元格的渲染元素。可以是 React 类组件或渲染函数。                                                                                                                                   | JXS Element         | No       | All      | Yes                |
| ListFooterComponent                    | 在列表底部渲染的组件。                                                                                                                                                                                                           | JXS Element         | No       | All      | Yes                |
| ListHeaderComponent                    | 在列表顶部渲染的组件。                                                                                                                                                                                                | JXS Element         | No       | All      | Yes                |
| refreshControl                         | 自定义下拉刷新控件元素。                                                                                                                                                                                                                  | JXS Element         | No       | All      | Yes                |
| renderScrollComponent                  | 作为主滚动视图渲染的组件。                                                                                                                                                                                                                  | JXS Element         | No       | All      | Yes                |
| onEndReached                           | 当滚动位置接近渲染内容末尾（距离阈值为 onEndReachedThreshold）时触发一次 。                                                                                                              | callback            | No       | All      | Yes                |
| onEndReachedThreshold                  | 触发 onEndReached 回调时，列表底部边缘与内容末尾的距离阈值（以列表可见长度为单位。                                            | number              | No       | All      | Yes                |
| onViewableItemsChanged                 | 当项目的可见性发生变化时触发（可见性由 viewabilityConfig 属性定义）。                                                                                                                             | callback            | No       | All      | Yes                |
| getItemType                            | 允许开发者指定项目类型。                                                                                                                                                                                                           | function            | No       | All      | Yes                |
| overrideItemLayout                     | 用于显式指定项目尺寸估算值或更改项目列跨度。                                                                                                                                             | function            | No       | All      | Yes                |
| ItemSeparatorComponent                 | 在每项之间（不包括顶部和底部）渲染的分隔组件。                                                                                                                                                                            | JXS Element         | No       | All      | Yes                |
| ListEmptyComponent                     | 列表为空时渲染的组件。                                                                                                                                                                                                                     | JXS Element         | No       | All      |Yes               |
| ListFooterComponentStyle               | 列表底部组件内部容器的样式。                                                                                                                                                                                               | React.ComponentType | No       | All      | Yes                |
| ListHeaderComponentStyle               | 列表顶部组件内部容器的样式。                                                                                                                                                                                             | StyleProp           | No       | All      | Yes                |
| disableAutoLayout                      | FlashList 会对子项布局应用某些修复，这可能与自定义 CellRendererComponent 实现冲突。设置为 true 可禁用此行为。 | boolean             | No       | All      | Yes                |
| disableHorizontalListHeightMeasurement | 设置为 true 时，列表的渲染尺寸需确定（即高度和宽度大于0），FlashList 将跳过用于测量的额外项目渲染。默认值为 false。 | boolean             | No       | All      | Yes                |
| estimatedFirstItemOffset               | 指定列表窗口中首个项目的绘制偏移量（非列表头部偏移量）。      | number              | No       | All      | Yes               |
| initialScrollIndex                     | 不从首项开始显示，而是从 initialScrollIndex 指定位置开始。                                                                                                                                         | number              | No       | All      | Yes               |
| inverted                               | 反转滚动方向（使用 -1 缩放变换实现）。                                                                                                                                                                           | boolean             | No       | All      | Yes                |
| onBlankArea                            | 滚动或列表初始加载时，FlashList 会计算用户可见的空白区域。                                                                                                              | callback            | No       | All      | Yes                 |
| onLoad                                 | 当列表在屏幕上完成项目绘制后触发。                                                                                                                                                                             | callback            | No       | All      | Yes               |
| onRefresh                              | 提供此回调可添加标准 RefreshControl 实现"下拉刷新"功能。需确保同时正确设置 refreshing 属性。                                                    | callback            | No       | All      | Yes                |
| onScroll                               | 滚动期间每帧最多触发一次（继承自 ScrollView）。 | callback            | No       | All      | Yes                |
| overrideProps                          | 除调试外不建议使用此属性。列表的内部属性将被提供值覆盖。                                                                                       | object              | No       | All      | Yes               |
| progressViewOffset                     | 当加载指示器需要偏移量时才需设置此属性。                                                                                                                                                                | number              | No       | All      | Yes                |
| refreshing                             | 在等待刷新数据时设置为 true。                                                                                                                                                                                      | boolean             | No       | All      | Yes                 |
| viewabilityConfigCallbackPairs         | ViewabilityConfig/onViewableItemsChanged 配置对集合。当对应 ViewabilityConfig 的条件满足时，会触发特定的 onViewableItemsChanged 回调 。 | object              | No       | All      | Yes                 |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| prepareForLayoutAnimationRender | 在执行布局动画前调用此方法，例如删除元素时为其添加动画效果。                           | function | No       | All      | Yes               |
| recordInteraction               | 通知列表已发生交互行为，这将触发可见性计算（例如当waitForInteractions为true且用户未滚动时）。 | function | No       | All      | Yes              |
| scrollToEnd                     | 滚动至内容末尾。                                                                                                                    | function | No       | All      | Yes               |
| scrollToIndex                   | 滚动至指定索引位置。                                                                                                                            | function | No       | All      | Yes               |
| scrollToItem                    | 滚动至指定项目。                                                                                                                               | function | No       | All      | Yes              |
| scrollToOffset                  | 滚动至列表内特定的内容像素偏移量。                                                                                       | function | No       | All      | Yes              |
| recomputeViewableItems<sup>1.8.3</sup> | 重新触发可见性计算。适用于需要强制触发可见性计算的场景。 | function | No | All | Yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Shopify/flash-list/blob/main/LICENSE.md) ，请自由地享受和参与开源。
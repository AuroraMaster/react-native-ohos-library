> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/slider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-slider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-slider/blob/main/LICENSE.md">
        <img src="https://img.shields.io/npm/l/@react-native-community/slider.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-slider)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本                     | 发布信息                                                                                                                                            | 支持RN版本 |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 4.4.3-0.3.4@deprecated | [@react-native-oh-tpl/slider Releases(deprecated)](https://github.com/react-native-oh-library/react-native-slider/releases) | 0.72       |
| 4.4.4                     | [@react-native-ohos/slider Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-slider/releases)               | 0.72       |
| 5.0.1                     | [@react-native-ohos/slider Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-slider/releases)               | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/slider
```

#### **yarn**

```bash
yarn add @react-native-ohos/slider
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 使用thumbImage属性时请确保引入的图片路径地址正确，可检查harmony/entry/src/main/resources/rawfile/assets目录下是否被打包至静态资源目录，如若不存在则图片放置文件目录不对

```js
import Slider from "@react-native-community/slider"
import { View } from 'react-native'

export default function SliderExample() {
    return (
        <View style={{ backgroundColor: 'red', width: 200, height: 100 }}>
            <Slider
                style={{ width: 200, height: 40 }}
                minimumValue={0}
                maximumValue={1}
                minimumTrackTintColor="#FFFFFF"
                maximumTrackTintColor="#000000"
            />
        </View>
    );
};

```

## Link

Version >= @react-native-ohos/slider@4.4.4，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

## 在工程根目录的 oh-package.json5 添加 overrides 字段

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

    "@react-native-ohos/slider": "file:../../node_modules/@react-native-ohos/slider/harmony/slider.har"
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

### 3.配置 CMakeLists 和引入 SliderPackge

> 若使用的是 <= 4.4.3-0.3.4 版本，请跳过本章

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/slider/src/main/cpp" ./slider)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_slider)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SliderPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SliderPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 slider 组件

找到 function buildCustomRNComponent()，一般位于 entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets，添加：

```diff
  ...
+ import { RNCSlider, SLIDER_TYPE } from "@react-native-ohos/slider"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SLIDER_TYPE) {
+   RNCSlider({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
 ...
}
...
```
> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SLIDER_TYPE
  ];
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------ | -------------------------------------------- | ---- | ------------ | ----------------- |
| `style`         | 用于设置 `Slider` 的样式和布局。详见 `StyleSheet.js` 和 `ViewStylePropTypes.js`。    | View.style  | 否   | 所有平台 | 是       |
| `disabled`      | 如果为 true，用户将无法移动滑块。<br/>默认值为 false。 | bool    | 否   | 所有平台 | 是       |
| `maximumValue`      | 滑块的初始最大值。<br/>默认值为 1。                      | number      | 否   | 所有平台 | 是       |
| `minimumTrackTintColor` | 滑块按钮左侧轨道的颜色。<br/>在 iOS 上覆盖默认的蓝色渐变图像。  | [color](https://reactnative.dev/docs/colors) | 否   | 所有平台 | 是       |
| `minimumValue`      | 滑块的初始最小值。<br/>默认值为 0。       | number      | 否   | 所有平台 | 是       |
| `lowerLimit`        | 滑动下限。用户将无法滑到该限制以下。              | number      | 否   | Android, iOS | 是      |
| `upperLimit`        | 滑动上限。用户将无法滑到该限制以上。              | number      | 否   | Android, iOS | 是        |
| `onSlidingStart`    | 用户开始拖动滑块时调用的回调函数。<br/>初始值作为参数传递给回调处理函数。       | function    | 否   | 所有平台 | 是       |
| `onSlidingComplete`     | 用户释放滑块时调用的回调函数，无论值是否已更改。<br/>当前值作为参数传递给回调处理函数。    | function    | 否   | 所有平台 | 是       |
| `onValueChange`     | 用户拖动滑块时持续调用的回调函数。| function    | 否   | 所有平台 | 是       |
| `step`          | 滑块的步长值。该值应在 0 到 (maximumValue - minimumValue) 之间。默认值为 0。<br/>在 Windows 操作系统上，默认值为滑块范围（从 `minimumValue` 到 `maximumValue`）的 1%。       | number      | 否   | 所有平台 | 是       |
| `maximumTrackTintColor` | 滑块按钮右侧轨道的颜色。<br/>在 iOS 上覆盖默认的灰色渐变图像。        | [color](https://reactnative.dev/docs/colors) | 否   | 所有平台 | 是       |
| `value`         | 表示滑块值的只写属性。可用于以编程方式控制滑块拇指的位置。在开始时输入一次仍作为初始值。以编程方式更改值不会触发任何事件。<br/>该值应在 minimumValue 和 maximumValue 之间，默认值分别为 0 和 1。默认值为 0。<br/>_这不是受控组件_，您不需要在拖动过程中更新值。 | number      | 否   | 所有平台 | 是       |
| `tapToSeek`         | 允许点击滑块轨道来设置拇指位置。<br/>在 iOS 上默认为 false。在 Android 或 Windows 上无效。       | bool    | 否   | iOS      | 否        |
| `inverted`      | 反转滑块的方向。<br/>默认值为 false。  | bool    | 否   | 所有平台 | 是       |
| `vertical`      | 如果设置为 `true`，则将滑块方向更改为垂直。<br/>默认值为 false。   | bool    | 否   | Windows      | 是       |
| `thumbTintColor`    | 前景滑块手柄的颜色。<br/>**注意：** 此属性将覆盖设置的 `thumbImage` 属性，这意味着如果同时设置了 `thumbImage` 和 `thumbTintColor`，用于拇指的图像可能无法正确显示！| [color](https://reactnative.dev/docs/colors) | 否   | Android      | 是       |
| `maximumTrackImage`     | 分配最大轨道图像。仅支持静态图像。图像的最左侧像素将被拉伸以填充轨道。              | Image<br/>.propTypes<br/>.source         | 否   | iOS      | 否        |
| `minimumTrackImage`     | 分配最小轨道图像。仅支持静态图像。图像的最右侧像素将被拉伸以填充轨道。             | Image<br/>.propTypes<br/>.source         | 否   | iOS      | 否        |
| `thumbImage`        | 为拇指设置图像。仅支持静态图像。需要是本地或网络图像的 URI；不支持 base64 编码的 SVG。     | Image<br/>.propTypes<br/>.source         | 否   | 所有平台 | 是       |
| `trackImage`        | 为轨道分配单个图像。仅支持静态图像。图像的中心像素将被拉伸以填充轨道。         | Image<br/>.propTypes<br/>.source         | 否   | iOS      | 否        |
| `ref`           | 引用对象。 | MutableRefObject                     | 否   | web      | 否        |
| `View`          | [继承的 `View` 属性...](https://github.com/facebook/react-native-website/blob/master/docs/view.md#props)      |         |      |      |  |

## 遗留问题

- [x] upperLimit 和 lowerLimit 只对数值生效，滑动限制不生效: [issue#2](https://github.com/react-native-oh-library/react-native-slider/issues/2)
- [ ] 不支持滑轨设置图片: [issue#3](https://github.com/react-native-oh-library/react-native-slider/issues/3)
- [ ] 未适配无障碍: [issue#9](https://github.com/react-native-oh-library/react-native-slider/issues/9)
- [ ] 不支持点击滑块轨道来设置拇指位置，不支持指定最大轨迹图像，不支持分配最小轨道图像: [issue#10](https://github.com/react-native-oh-library/react-native-slider/issues/10)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。

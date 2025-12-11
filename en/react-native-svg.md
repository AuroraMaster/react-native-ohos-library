> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-svg(ArkTS)</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-svg">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-svg/blob/main/LICENSE">
        <img src="https://img.shields.io/npm/l/react-native-svg.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-harmony-svg)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information:

| Third-party Library Version | Release Information                                                     | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 15.0.1@deprecated      | [@react-native-oh-tpl/react-native-svg Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-svg/releases) | 0.72       |
| 15.0.2      | [@react-native-ohos/react-native-svg Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases)                        | 0.72       |
| 15.12.1    | [@react-native-ohos/react-native-svg Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->
#### **npm**

```bash
npm install @react-native-ohos/react-native-svg
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-svg
```
<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import Svg, { Path } from "react-native-svg";

<Svg width="100" height="100">
  <Path d="M90 0 L0 180 L180 180 Z" fill="red" />
</Svg>;
```

## Link

Version >= @react-native-ohos/react-native-svg@15.0.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

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

    "@react-native-ohos/svg": "file:../../node_modules/@react-native-ohos/react-native-svg/harmony/svg.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.Configuring CMakeLists and Introducing SVGPackage

> If you are using version <= 15.0.1, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-svg/src/main/cpp" ./svg)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_svg)
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SVGPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SVGPackage>(ctx),
    };
}
```

### 4. Introduce SVG component to ArkTs

Find `function buildCustomRNComponent()`, Generally located in `entry/src/main/ets/pages/index.ets ` or `entry/src/main/ets/rn/LoadBundle.ets`, add:

```diff
...
import { createRNPackages } from '../RNPackagesFactory'
+ import { SVG_VIEW_TYPE_NAME, SVGView } from "@react-native-ohos/svg"

@Builder
function buildCustomComponent(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnComponentContext,
      tag: ctx.tag,
      buildCustomComponent: buildCustomComponent
    })
  }
+ else if (ctx.componentName === SVG_VIEW_TYPE_NAME) {
+   SVGView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
 ...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  ...
+ SVG_VIEW_TYPE_NAME
  ];
```

### 5. Running

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

## 属性

详细请查看 [react-native-svg 的文档介绍](https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md)

以下为目前已支持的组件属性：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Svg**：绘制组件的父组件

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  width  |  组件宽度   | number\| string | Yes      | All      | Yes               |
| height  |  组件高度   | number\| string | Yes      | All      | Yes               |
| viewBox |  组件视区   |     string      | No       | All      | Yes               |
|  color  |    颜色     |     string      | No       | All      | Yes               |

**G**：该元素是用于对其他 SVG 元素进行分组的容器

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | -------- | -------- | ----------------- |

**Path**： 路径绘制组件，根据绘制路径生成封闭的自定义形状

| Name |     Description      |  Type  | Required | Platform | HarmonyOS Support |
| :--: | :------------------: | :----: | -------- | -------- | ----------------- |
|  d   | 路径绘制的命令字符串 | string | Yes      | All      | Yes               |

**Rect**： 矩形绘制组件，根据角位置和宽高生成矩形形状

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | Yes      | All      | Yes               |
| height |     元素高度      | number\| string | Yes      | All      | Yes               |
|   rx   | 定义 x 轴上的半径 | number\| string | No       | All      | Yes               |
|   ry   | 定义 y 轴上的半径 | number\| string | No       | All      | Yes               |

**Image**： 图像元素，支持 JPEG、PNG 格式

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | Yes      | All      | Yes               |
| height |     元素高度      | number\| string | Yes      | All      | Yes               |
|  href  |   图像资源引用    | source\| string | Yes      | All      | Yes               |

**Circle**： 园绘制组件，基于圆心和半径生成园形形状

| Name |      Description      |      Type       | Required | Platform | HarmonyOS Support |
| :--: | :-------------------: | :-------------: | -------- | -------- | ----------------- |
|  r   |        园半径         | number\| string | Yes      | All      | Yes               |
|  cx  | 圆心在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|  cy  | 圆心在 y 轴上平移距离 | number\| string | No       | All      | Yes               |

**Polygon**： 多边形制组件，用于创建至少包含三条边的图形

|  Name  |          Description           |      Type      | Required | Platform | HarmonyOS Support |
| :----: | :----------------------------: | :------------: | -------- | -------- | ----------------- |
| points | 定义多边形每个角的 x 和 y 坐标 | string\| array | Yes      | All      | Yes               |

**Defs**：该元素是用于对其他 SVG 元素进行分组的容器

**LinearGradient**：用于定义线性渐变

> [!TIP] 注： LinearGradient 目前仅支持 Path、Rect、Circle 组件，只支持在 fill 上使用，不支持 stroke

| Name |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :--: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|  x1  | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|  y1  | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
|  x2  | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|  y2  | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |

**Stop**：定义渐变上的颜色坡度

|    Name     |         Description          |      Type       | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------: | :-------------: | -------- | -------- | ----------------- |
|  stopColor  |        渐变停止的颜色        |     string      | No       | All      | Yes               |
| stopOpacity |      渐变停止的不透明度      | number\| string | No       | All      | Yes               |
|   offset    | 渐变停止沿渐变向量放置的位置 | number\| string | No       | All      | Yes               |

**Mask**：定义 alpha 蒙版，用于将当前对象合成到背景中

> [!TIP] 注： Mask 目前自有属性均不支持，仅支持 Path、Rect、Circle 组件的单一组件嵌套，不支持多组件嵌套

**Use**：该元素可以重复使用 SVG 元素

> [!TIP] 注： Use 目前仅支持 Path、Rect、Circle 组件

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | No       | All      | Yes               |
| height |     元素高度      | number\| string | No       | All      | Yes               |
|  href  |   图像资源引用    | source\| string | Yes      | All      | Yes               |


**公共属性**：Common props 组件属性 HarmonyOS 侧支持情况

|    Name     |             Description              |  Type  | Default | Required | Platform | G   | Path | Rect | Circle | Polygon |
| :---------: | :----------------------------------: | :----: | :-----: | :------: | -------- | --- | ---- | ---- | ------ | ------- |
|    fill     |           设置填充区域颜色           | string | '#000'  |    No    | All      |     | √    | √    | √      | √       |
|   stroke    | 设置边框颜色，不设置时，默认没有边框 | string | 'none'  |    No    | All      |     | √    | √    | √      | √       |
| strokeWidth |             设置边框宽度             | number |    1    |    No    | All      |     | √    | √    | √      | √       |

## 遗留问题

- [ ] svg 当前仅实现少部分属性（具体见上面已列出的属性），其余还未实现 HarmonyOS 化[issue#5](https://github.com/react-native-oh-library/react-native-svg/issues/5)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE) ，请自由地享受和参与开源。

> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-svg(CAPI)</code> </h1>
</p>


本项目基于 [react-native-svg](https://github.com/software-mansion/react-native-svg) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-svg` 版本所属关系如下：
| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-svg | ~ 15.13.0 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases) | 0.82.* | 否 | API15+ | 15.15.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-svg) |
| @react-native-ohos/react-native-svg | ~15.12.1 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases) | 0.77.* | 否 | API15+ | 15.12.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-svg) |
| @react-native-ohos/react-native-svg | ~ 15.0.2 | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-svg/releases) | 0.72.* | 是 | API15+ | 15.0.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-svg) |
| @react-native-oh-tpl/react-native-svg | <= 15.0.1@deprecated | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-harmony-svg/releases) | 0.72.* | 否 | API12+ | 15.0.0 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-svg) |


## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-svg@15.0.0
npm install @react-native-ohos/react-native-svg

# 0.77
npm install react-native-svg@15.12.0
npm install @react-native-ohos/react-native-svg

# 0.82
npm install react-native-svg@15.15.0
npm install @react-native-ohos/react-native-svg
```

#### **yarn**

```bash
# 0.72
yarn add react-native-svg@15.0.0
yarn add @react-native-ohos/react-native-svg

# 0.77
yarn add react-native-svg@15.12.0
yarn add @react-native-ohos/react-native-svg

# 0.82
yarn add react-native-svg@15.15.0
yarn add @react-native-ohos/react-native-svg
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { StyleSheet,SafeAreaView } from 'react-native';
import { Svg,Path } from 'react-native-svg';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <Svg width="100" height="100">
        <Path d="M90 0 L0 180 L180 180 Z" fill="red" />
      </Svg>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex:1,
    backgroundColor: 'grey',
  },
});
```

## 2. Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|------------------|-----------|
| ~15.13.0                      |  No              |  0.82     |
| ~15.12.1             |  No              |  0.77     |
| ~15.0.2                        |  Yes             |  0.72     |
| <= 15.0.1@deprecated |  No              |  0.72     |

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
    "@react-native-ohos/react-native-svg": "file:../../node_modules/@react-native-ohos/react-native-svg/harmony/svg.har"
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

### 2.3. 配置 CMakeLists 和引入 SVGPackage

>  [!TIP] 版本 v15.0.2 及以上需要

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-svg/src/main/cpp" ./svg)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_svg)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SVGPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<SVGPackage>(ctx),
    };
}
```

### 2.4. 在 ArkTs 侧引入 SvgPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { SvgPackage } from '@react-native-ohos/react-native-svg/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new SvgPackage(ctx),
  ];
}
```
</details>

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

### 在 ArkTs 侧引入和注册字体文件(非必选配置项，该模块始终需要手动配置)

> [!TIP] 本项非必配项，当使用 Text 组件的 fontFamily 属性指定字体时才需配置

步骤一：
    复制字体文件到  `entry/src/main/resources/rawfile/assets/fonts` 目录下(如使用了外部字体文件，需要将*.ttf文件复制过来)

步骤二：
    打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码


    const fonts: Record<string, Resource> = {
        "Noto Sans Pau Cin Hau": $rawfile("assets/fonts/Noto Sans Pau Cin Hau.ttf") ,
        "NotoSansVai-Regular": $rawfile("assets/fonts/NotoSansVai-Regular.ttf") ,
        "HarmonyOS_Sans_Condensed_Regular_Italic": $rawfile("assets/fonts/HarmonyOS_Sans_Condensed_Regular_Italic.ttf")
        "HarmonyOS_Sans_Digit_Medium": $rawfile("assets/fonts/HarmonyOS_Sans_Digit_Medium.ttf")
    }
    
    @Entry
    @Component
    struct Index {
        //...
        build() {
            Column(){
                //...
    
                //注册字体文件
                RNApp({
                rnInstanceConfig: {
                    //...
                    fontResourceByFontFamily: fonts
                },
                //...
            }
            
        }
        //...
    }

## 3. 约束与限制

### 3.1. 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM: 6.0.0.120 SP7;

### 3.2. 编译运行API要求

> [!TIP] 当前三方库所有版本均已实现版本隔离，支持在 `API12+` 工程编译，及 `API12+` ROM运行。

> [!TIP] 以下功能依赖特定版本的API，使用 `低于指定API版本的工程编译` 或 `低于指定API版本的ROM运行` 均可能导致部分功能受限。
1. 版本 >=15.0.2 for 0.72引入[OH_ArkUI_CreateSnapshotOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_createsnapshotoptions)，[OH_ArkUI_SnapshotOptions_SetScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_snapshotoptions_setscale)，[OH_ArkUI_GetNodeSnapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-node-h#oh_arkui_getnodesnapshot),实现了ForeignObject功能，此API需要在支持`API15+`的工程编译，并在支持`API15+`的ROM上运行，方可生效。
2. 版本 >=15.12.1 for 0.77引入[OH_ArkUI_CreateSnapshotOptions](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_createsnapshotoptions)，[OH_ArkUI_SnapshotOptions_SetScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-type-h#oh_arkui_snapshotoptions_setscale)，[OH_ArkUI_GetNodeSnapshot](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-native-node-h#oh_arkui_getnodesnapshot),实现了ForeignObject功能，此API需要在支持`API15+`的工程编译，并在支持`API15+`的ROM上运行，方可生效。

## 4. 属性

详细请查看 [react-native-svg 的文档介绍](https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Svg**：绘制组件的父组件

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|        width        |       组件宽度       | number\| string |   Yes    |   All    |        Yes        |
|       height        |       组件高度       | number\| string |   Yes    |   All    |        Yes        |
|       viewBox       |       组件视区       |     string      |    No    |   All    |        Yes        |
|        color        |         颜色         |     string      |    No    |   All    |        Yes        |
|        title        |      组件标题名      |     string      |    No    |   All    |        Yes        |
| preserveAspectRatio | 是否强制进行统一缩放 |     string      |    No    |   All    |        Yes        |
| style | 用于控制组件的视觉外观和布局 |object |    No    |   All    |        Yes        |

**G**：该元素是用于对其他 SVG 元素进行分组的容器

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
| opacity |   透明度    | number\| string | No       | All      | Yes               |

**Path**： 路径绘制组件，根据绘制路径生成封闭的自定义形状

|  Name   |     Description      |  Type  | Required | Platform | HarmonyOS Support |
| :-----: | :------------------: | :----: | -------- | -------- | ----------------- |
|    d    | 路径绘制的命令字符串 | string | Yes      | All      | Yes               |
| opacity |        透明度        | number | No       | All      | Yes               |

**Rect**： 矩形绘制组件，根据角位置和宽高生成矩形形状

|  Name   |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|    x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|    y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
|  width  |     元素宽度      | number\| string | Yes      | All      | Yes               |
| height  |     元素高度      | number\| string | Yes      | All      | Yes               |
|   rx    | 定义 x 轴上的半径 | number\| string | No       | All      | Yes               |
|   ry    | 定义 y 轴上的半径 | number\| string | No       | All      | Yes               |
| opacity |      透明度       | number\| string | No       | All      | Yes               |

**Image**： 图像元素，支持 JPEG、PNG 格式

> [!WARNING]
>
> 注： Image 依赖 Canary3 Sp2 以上版本的 SDK 和 ROM。

|        Name         |                Description                 |               Type               | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------: | :------------------------------: | -------- | -------- | ----------------- |
|          x          |             在 x 轴上平移距离              |         number\| string          | No       | All      | Yes               |
|          y          |             在 y 轴上平移距离              |         number\| string          | No       | All      | Yes               |
|        width        |                  元素宽度                  |         number\| string          | Yes      | All      | Yes               |
|       height        |                  元素高度                  |         number\| string          | Yes      | All      | Yes               |
|        href         |                图像资源引用                |         source\| string          | Yes      | All      | Yes               |
|      xlinkHref      |         用于指定要嵌入的图像的 URL         | RNImageProps['source'] \| string | No       | All      | Yes               |
| preserveAspectRatio | 控制在给定的容器尺寸内如何保持图像的宽高比 |              string              | No       | All      | Yes               |
|       opacity       |                   透明度                   |         source\| string          | No       | All      | Yes               |

**Circle**： 圆绘制组件，基于圆心和半径生成圆形形状

|  Name   |      Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :-------------------: | :-------------: | -------- | -------- | ----------------- |
|    r    |        圆半径         | number\| string | Yes      | All      | Yes               |
|   cx    | 圆心在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   cy    | 圆心在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| opacity |        透明度         |     number      | No       | All      | Yes               |

**Polygon**： 多边形绘制组件，用于创建至少包含三条边的图形

|  Name   |          Description           |      Type      | Required | Platform | HarmonyOS Support |
| :-----: | :----------------------------: | :------------: | -------- | -------- | ----------------- |
| points  | 定义多边形每个角的 x 和 y 坐标 | string\| array | Yes      | All      | Yes               |
| opacity |             透明度             |     number     | No       | All      | Yes               |

**Polyline**： 多段线组件，用于创建一条线段构成的轨迹

|  Name   |           Description            |      Type      | Required | Platform | HarmonyOS Support |
| :-----: | :------------------------------: | :------------: | -------- | -------- | ----------------- |
| points  | 定义多段线每个端点的 x 和 y 坐标 | string\| array | Yes      | All      | Yes               |
| opacity |              透明度              |     number     | No       | All      | Yes               |

**Defs**：该元素是用于对其他 SVG 元素进行分组的容器

> 注： 该组件无属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | -------- | -------- | ----------------- |
|  /   |      /      |  /   | /        | All      | Yes               |

**LinearGradient**：用于定义线性渐变

|       Name        |              Description               |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        x1         |           在 x 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        y1         |           在 y 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        x2         |           在 x 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        y2         |           在 y 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|   gradientUnits   |        指定元素属性使用的坐标系        | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | 指定从元素当前坐标系到目标坐标系的转换 |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**RadialGradient**：用于定义线性渐变

> [!WARNING]
>
> 注： RadialGradient 依赖 Canary3 Sp2 以上版本的 SDK 和 ROM。

|       Name        |              Description               |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        fx         |           起始圆的 x 轴坐标            |             number\| string             | No       | All      | Yes               |
|        fy         |           起始圆的 y 轴坐标            |             number\| string             | No       | All      | Yes               |
|        rx         |          终止椭圆的 x 轴半径           |             number\| string             | No       | All      | Yes               |
|        ry         |          终止椭圆的 y 轴半径           |             number\| string             | No       | All      | Yes               |
|        cx         |           终止圆的 x 轴坐标            |             number\| string             | No       | All      | Yes               |
|        cy         |           终止圆的 y 轴坐标            |             number\| string             | No       | All      | Yes               |
|         r         |              终止圆的半径              |             number\| string             | No       | All      | Yes               |
|   gradientUnits   |        指定元素属性使用的坐标系        | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | 指定从元素当前坐标系到目标坐标系的转换 |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**Stop**：定义渐变上的颜色坡度

|    Name     |  Description   |  Type  | Required | Platform | HarmonyOS Support |
| :---------: | :------------: | :----: | -------- | -------- | ----------------- |
|  stopColor  |     渐变色     | string | No       | All      | Yes               |
| stopOpacity |  渐变色透明度  | string | No       | All      | Yes               |
|   offset    | 渐变色相对位置 | string | No       | All      | Yes               |

**Mask**：定义 alpha 蒙版，用于将当前对象合成到背景中

|       Name       | Description                                                                                                | Type       | Required | Platform | HarmonyOS Support |
| :--------------: | ---------------------------------------------------------------------------------------------------------- | ---------- | -------- | -------- | :---------------: |
|        id        | 唯一标识                                                                                                   | string     | No       | All      |        Yes        |
|        x         | 左侧顶角横坐标                                                                                             | NumberProp | No       | All      |        Yes        |
|        y         | 左侧顶角纵坐标                                                                                             | NumberProp | No       | All      |        Yes        |
|      width       | 元素宽度                                                                                                   | NumberProp | No       | All      |        Yes        |
|      height      | 元素高度                                                                                                   | NumberProp | No       | All      |        Yes        |
|    maskUnits     | 定义 x,y,width,height 使用的坐标系，默认值为 objectBoundingBox，可以使用 objectBoundingBox\|userSpaceOnUse | TMaskUnits | No       | All      |        Yes        |
| maskContentUnits | 定义内容使用的坐标系，默认值为 userSpaceOnUse，可以使用 objectBoundingBox\|userSpaceOnUse                  | TMaskUnits | No       | All      |        Yes        |

**Use**：该元素可以重复使用 SVG 元素

|   Name    |                      Description                       |      Type       | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x     |                   在 x 轴上平移距离                    | number\| string | No       | All      | Yes               |
|     y     |                   在 y 轴上平移距离                    | number\| string | No       | All      | Yes               |
|   width   |                        元素宽度                        | number\| string | No       | All      | Yes               |
|  height   |                        元素高度                        | number\| string | No       | All      | Yes               |
|   href    |                      图像资源引用                      | source\| string | Yes      | All      | Yes               |
| xlinkHref | 指定了一个 URI，该 URI 指向了 SVG 文档中定义的一个元素 |     string      | No       | All      | Yes               |
|  opacity  |                         透明度                         | number\| string | No       | All      | Yes               |

**Ellipse**： 椭圆绘制组件，基于一个中心坐标以及它们的 x 半径和 y 半径

|  Name   |      Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :-------------------: | :-------------: | -------- | -------- | ----------------- |
|   cx    | 圆心在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   cy    | 圆心在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
|   rx    |   定义 x 轴上的半径   | number\| string | No       | All      | Yes               |
|   ry    |   定义 y 轴上的半径   | number\| string | No       | All      | Yes               |
| opacity |        透明度         | number\| string | No       | All      | Yes               |

**ClipPath**：该元素定义一条剪切路径，可作为其他元素的 clipPath 属性的值

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | -------- | -------- | ----------------- |
|  id    |      元素的唯一标识符。      |  string   | No       | All   | Yes   |

**Marker**：用于在绘制类组件上添加标记

|        Name         |                      Description                       |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                  为元素分配唯一的名称                  |     string      | Yes      | All      | Yes               |
|       viewBox       |              视窗在用户空间中的位置和尺寸              |     string      | No       | All      | Yes               |
|        refX         |                  标记参考点的 x 坐标                   | number\| string | No       | All      | Yes               |
|        refY         |                  标记参考点的 y 坐标                   | number\| string | No       | All      | Yes               |
|     markerUnits     | markerWidth 和 markerHeight 属性的坐标系以及标记的内容 |     string      | No       | All      | Yes               |
|       orient        |         将标记放置在形状上的相应位置时如何旋转         |     string      | No       | All      | Yes               |
|     markerWidth     |                表示标记进入的视窗的宽度                | number\| string | No       | All      | Yes               |
|    markerHeight     |                表示标记进入的视窗的高度                | number\| string | No       | All      | Yes               |

**Pattern**：用于定义一个图形对象，可以被引用以平铺重绘该图形对象以覆盖某个区域。

|        Name         |                                Description                                |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :-----------------------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                           为元素分配唯一的名称                            |     string      | Yes      | All      | Yes               |
|          x          |                            标记参考点的 x 坐标                            | number\| string | No       | All      | Yes               |
|          y          |                            标记参考点的 y 坐标                            | number\| string | No       | All      | Yes               |
|        width        |                         表示标记进入的视窗的宽度                          | number\| string | No       | All      | Yes               |
|       height        |                         表示标记进入的视窗的高度                          | number\| string | No       | All      | Yes               |
|    patternUnits     |              属性指示 pattern 元素的几何属性使用哪个坐标系。              |     string      | No       | All      | Yes               |
| patternContentUnit  |              属性指示 pattern 元素的几何属性使用哪个坐标系。              |     string      | No       | All      | Yes               |
|  patternTransform   |                   定义了应用于图案图块的变换定义的列表                    |     string      | No       | All      | Yes               |
|       viewBox       |                     定义视窗在用户空间中的位置和尺寸                      |     string      | No       | All      | Yes               |
| preserveAspectRatio | 指示具有提供给定宽高比的 viewBox 的元素必须如何适应具有不同宽高比的视口。 |     string      | No       | All      | Yes               |

**Symbol**：该元素用来定义一个图形模板对象，它可以用一个<use>元素实例化

|        Name         |                                Description                                |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :-----------------------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                           为元素分配唯一的名称                            |     string      | Yes      | All      | Yes               |
|       viewBox       |                     定义视窗在用户空间中的位置和尺寸                      |     string      | No       | All      | Yes               |
| preserveAspectRatio | 指示具有提供给定宽高比的 viewBox 的元素必须如何适应具有不同宽高比的视口。 |     string      | No       | All      | Yes               |

**Line**：SVG 基本形状，用于创建连接两点的线。

|  Name   |   Description    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :--------------: | :-------------: | -------- | -------- | ----------------- |
|   x1    | x 轴上线条的起点 | number\| string | No       | All      | Yes               |
|   y1    | y 轴上的线的起点 | number\| string | No       | All      | Yes               |
|   x2    | x 轴上的线的末端 | number\| string | No       | All      | Yes               |
|   y2    | y 轴上的线的末端 | number\| string | No       | All      | Yes               |
| opacity |      透明度      | number\| string | No       | All      | Yes               |

**Text**：绘制由文本组成的图形元素

|    Name    |           Description            |      Type       | Required | Platform | HarmonyOS Support |
| :--------: | :------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x      |      文本基线起点的 x 坐标       |  number\|string  | No       | All      | Yes               |
|     y      |      文本基线起点的 y 坐标       |  number\|string  | No       | All      | Yes               |
|     dx     | 从前一个文本元素水平移动文本位置 |  number\|string  | No       | All      | Yes               |
|     dy     | 从前一个文本元素垂直移动文本位置 | number\| string | No       | All      | Yes               |
|   rotate   |      旋转每个单独字形的方向      |      array      | No       | All      | Yes               |
|  opacity   |              透明度              |     number      | No       | All      | Yes               |
| inlineSize |          水平或垂直尺寸          |     number      | No       | All      | No               |
| alignmentBaseline | 指定文本的对齐基线        |      string      | NO       | ALL      | Yes               |
| baselineShift | 设置垂直位置调整              | number\| string  | No       | All      | Yes               |
| lengthAdjust | 调整文本以适应特定的布局约束    |      string      | No       | All      | Yes               |
| textLength | 指定文本应该被渲染的长度          |     number       | No       | All      | Yes               |

**TSpan**：绘制文本或 Text 内的子文本

|    Name    |           Description            |      Type       | Required | Platform | HarmonyOS Support |
| :--------: | :------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x      |      文本基线起点的 x 坐标       |  number\|string  | No       | All      | Yes               |
|     y      |      文本基线起点的 y 坐标       |  number\|string  | No       | All      | Yes               |
|     dx     | 从前一个文本元素水平移动文本位置 |  number\|string  | No       | All      | Yes               |
|     dy     | 从前一个文本元素垂直移动文本位置 | number\| string | No       | All      | Yes               |
|   rotate   |      旋转每个单独字形的方向      |      array      | No       | All      | Yes               |
|  opacity   |              透明度              |     number      | No       | All      | Yes               |
| inlineSize |          水平或垂直尺寸          |     number      | No       | All      | Yes               |

**TextPath**：若要沿路径形状呈现文本，将文本括在具有 href 属性的 TextPath 元素中，并引用 Path 元素。

|    Name     |            Description             |      Type       | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------------: | :-------------: | -------- | -------- | ----------------- |
|    href     | 用于呈现文本的路径或基本形状的 URL |     string      | No       | All      | No               |
|  xlinkHref  | 用于呈现文本的路径或基本形状的 URL |     string      | No       | All      | No               |
|   method    |      沿路径渲染各个字形的方法      |     string      | No       | All      | No               |
|   spacing   |         绘制字符之间的间距         |     string      | No       | All      | No               |
|    side     |      文本应呈现在路径的哪一侧      |     string      | No       | All      | No               |
|   midLine   |                中线                |     string      | No       | All      | No               |
| startOffset |  文本开始被沿着路径绘制时的偏移量  | number\| string | No       | All      | No               |

**SvgAst**：该组件通过传入 ast 来渲染出 svg

|   Name   |         Description          |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :--------------------------: | :------: | :------: | :------: | :---------------: |
|   ast    | 解析 svg 字符串得到的 ast 树 |  JsxAST  |   Yes    |   All    |        Yes        |
| override |    覆盖 svg 样式，如宽高     |  object  |    No    |   All    |        Yes        |

**SvgFromUri**：该组件通过传入 uri 地址来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   uri    |     svg 资源地址      |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |

**SvgFromXml**：该组件通过传入字符串来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   xml    |   svg 代码的字符串    |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |

**SvgXml**：该组件通过传入字符串来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   xml    |   svg 代码的字符串    |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |

**SvgUri**：该组件通过传入 uri 地址来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   uri    |     svg 资源地址      |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |
| onError  |      错误时触发       | function |    No    |   All    |        Yes        |
|  onLoad  |    加载成功后触发     | function |    No    |   All    |        Yes        |
| fallback |      加载中元素       | function |    No    |   All    |        Yes        |

**ForeignObject**：该元素可以嵌套非SVG内容到SVG中

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | No       | All      | Yes               |
| height |     元素高度      | number\| string | No       | All      | Yes               |
| SvgNodeCommonProps.opacity | 设置透明度      | number | No       | All      | Yes               |
| SvgNodeCommonProps.matrix |  设置transform动画 | Array<number> | No       | All      | Yes               |
| SvgNodeCommonProps.mask |   指定使用 Mask 元素实现遮罩效果  | string | No       | All      | Yes               |
| SvgNodeCommonProps.clipPath |  指定、关联一条裁剪路径  | string | No       | All      | Yes               |
| SvgNodeCommonProps.clipRule | 设置裁剪规则       | string | No       | All      | Yes               |
| SvgRenderableCommonProps |     Object      | object | No       | All      | No          |
| SvgGroupCommonProps |     Object      | object | No       | All      | No               |

**公共属性**：

Common props 组件属性 HarmonyOS 侧支持情况

|       Name       |                 Description                 |    Type     |  Default  | Required | Platform |
| :--------------: | :-----------------------------------------: | :---------: | :-------: | :------: | :------: |
|       fill       |              设置填充区域颜色               |   string    |  '#000'   |    No    |   All    |
|   fillOpacity    |             设置填充区域透明度              |   number    |     1     |    No    |   All    |
|     fillRule     |                设置填充规则                 |   number    |     1     |    No    |   All    |
|     clipRule     |                设置裁剪规则                 |   string    | 'evenodd' |    No    |   All    |
|     clipPath     |           指定、关联一条裁剪路径            |   string    |  'none'   |    No    |   All    |
|      stroke      |    设置边框颜色，不设置时，默认没有边框     |   string    |   none    |    No    |   All    |
|   strokeWidth    |                设置边框宽度                 |   number    |     1     |    No    |   All    |
|  strokeOpacity   |                 边框透明度                  |   number    |     1     |    No    |   All    |
| strokeDasharray  |         用来描边的点划线的图案范式          |   number    |   none    |    No    |   All    |
| strokeDashoffset |      指定了 dash 模式到路径开始的距离       |   number    |     1     |    No    |   All    |
|  strokeLinecap   |             设置路径两端的形状              |   string    |   butt    |    No    |   All    |
|  strokeLinejoin  |         指明路径的转角处使用的形状          |   string    |   miter   |    No    |   All    |
| strokeMiterlimit | 对斜接长度和 stroke-width 的比率设置极限 值 |   number    |     4     |    No    |   All    |
|   vectorEffect   |       指明绘制对象时要使用的矢量效果        |   string    |   none    |    No    |   All    |
|    translate     |                  设置位移                   | numberArray |    0,0    |    No    |   All    |
|    translateX    |                设置 x 轴位移                |   number    |     0     |    No    |   All    |
|    translateY    |                设置 y 轴位移                |   number    |     0     |    No    |   All    |
|      origin      |           更改一个元素变形的原点            | numberArray |    0,0    |    No    |   All    |
|     originX      |        更改一个元素变形的原点 x 坐标（单独使用无效，需配合其他属性如 rotation 使用）        |   number    |     0     |    No    |   All    |
|     originY      |        更改一个元素变形的原点 y 坐标（单独使用无效，需配合其他属性如 rotation 使用）       |   number    |     0     |    No    |   All    |
|      scale       |                定义缩放大小                 | numberArray |   1，1    |    No    |   All    |
|      scaleX      |              定义 x 轴缩放大小              |   number    |     1     |    No    |   All    |
|      scaleY      |              定义 y 轴缩放大小              |   number    |     1     |    No    |   All    |
|     rotation     |                设置旋转角度                 |   number    |   0，0    |    No    |   All    |
|        x         |              标识一个 x 轴坐标              |   number    |     0     |    No    |   All    |
|        y         |              标识一个 y 轴坐标              |   number    |     0     |    No    |   All    |
|    transform<sup>changed in 15.13.0</sup>     |   定义应用于元素及其子元素的变换规则列表, 小于15.13.0 版本，transform 属性类型仅支持string类型, 15.13.0 版本及以后版本，transform 属性同时支持string类型及Transform Object 数组    |   string\|TransformArray    |     -     |    No    |   All    |
|      marker      |         指定路径所有顶点的路标样式          |   string    |     -     |    No    |   All    |
|   markerStart    |        指定路径起点所采用的路标样式         |   string    |     -     |    No    |   All    |
|    markerMid     |      指定路径中间顶点所采用的路标样式       |   string    |     -     |    No    |   All    |
|    markerEnd     |        指定路径终点所采用的路标样式         |   string    |     -     |    No    |   All    |
|       mask       |    给元素指定使用 Mask 元素实现遮罩效果     |   string    |     -     |    No    |   All    |
|        id        |                 设置节点 id                 |   string    |     -     |    No    |   All    |
|     opacity      |                 设置透明度                  |   number    |     1     |    No    |   All    |
|     display      |             控制元素展示的方式              |   string    |   block   |    No    |   All    |
|  pointerEvents   |          设置元素如何响应点击事件           |   string    |           |    No    |   All    |

FontProps 组件属性 HarmonyOS 侧支持情况

|         Name          |                          Description                           |        Type        | Default | Required | Platform |
| :-------------------: | :------------------------------------------------------------: | :----------------: | :-----: | :------: | :------: |
|       fontSize        | 在多行布局环境中将多行文本设置为实线时，从基线到基线的字体大小 |       string       | medium  |    No    |   All    |
|      fontWeight       |   用于呈现文本的字形相对于同一字体族中的其他字体的粗度或亮度   |       string       | normal  |    No    |   All    |
|         font          |                   设置一个用于文字布局的字体                   | FontObject（对象） |  none   |    No    |   All    |
|       fontStyle       |                        指定文本渲染样式                        |       string       | normal  |    No    |   All    |
|      fontVariant      |                        设置文本字体变体                        |                    |         |    No    |   All    |
|      fontStretch      |                        控制字体拉伸程度                        |       string       | normal  |    No    |   All    |
|      fontFamily       |                          指定文本字体                          |       string       | normal  |    No    |   All    |
|      textAnchor       |               用于指定文本相对于其锚点的对齐方式               |       string       |  start  |    No    |   All    |
|    textDecoration     |                        设置文本装饰效果                        |       string       |    -    |    No    |   All    |
|     letterSpacing     |                     设置字符间距或字母间距                     |       number       |    1    |    No    |   All    |
|      wordSpacing      |                     设置英文单词之间的距离                     |       number       |    1    |    No    |   All    |
|        kerning        |                       设置字符之间的间距                       |       number       |    0    |    No    |   All    |
|  fontFeatureSettings  |                          字体特性控制                          |       string       | normal  |    No    |   All    |
| fontVariantLigatures  |                         控制文本中连字                         |       string       | normal  |    No    |   All    |
| fontVariationSettings |                 设置字体的宽度、高度、倾斜度等                 |       string       | normal  |    No    |   All    |

## 5. 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|         Name         |        Description         |   Type   | Required | Platform | HarmonyOS Support |
| :------------------: | :------------------------: | :------: | :------: | :------: | :---------------: |
|        parse         | 将 svg 字符串解析成 JsxAST | function |    No    |   All    |        Yes        |
| err<sup>15.0.x</sup> |          打印日志          | function |    No    |   All    |        Yes        |
|      camelCase       |    字符串首字母转成大写    | function |    No    |   All    |        Yes        |
|      fetchText       | 将 svg 字符串解析成 JsxAST | function |    No    |   All    |        Yes        |

## 6. 遗留问题

- [ ] isPointInFill 判断点位坐标是否在fill上 未实现
- [ ] isPointInStroke 判断点位坐标是否在stroke上 未实现
- [ ] getTotalLength 获取总path的长度 未实现
- [ ] getPointAtLength 获取点位坐标在path上的信息 未实现
- [ ] getBBox 获取组件的边界信息 未实现
- [ ] getCTM 获取相对于父组件的matrix矩阵信息 未实现
- [ ] getScreenCTM 获取组件的matrix矩阵信息 未实现
- [ ] getRawResource 获取android中的资源文件 未实现
- [X] foreignObject 该组件允许 svg 使用外部组件 已实现
- [ ] filter 该组件可以为 SVG 图形添加各种视觉效果 未实现
- [ ] TextPath 功能href,xlinkHref,startOffset,method,spacing,midLine,side未实现
- [ ] Text,TSpan组件的rotate,fontFamily,wordSpacing属性 未实现 
- [ ] Xml 组件中引入 'react-native-svg/src/ReactNativeSVG' 社区库的 err 属性, 社区库此属性对外暴露 未实现 [#2845](https://github.com/software-mansion/react-native-svg/pull/2845)  

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE) ，请自由地享受和参与开源。

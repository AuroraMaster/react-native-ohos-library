> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-image-sequence</code> </h1>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-sequence)

## 1. 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息，并下载适用版本的 tgz 包：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 0.9.1-0.0.3@deprecated     | [@react-native-oh-tpl/react-native-image-sequence-2 Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-sequence/releases) | 0.72       |
| 0.9.2                | [@react-native-ohos/react-native-image-sequence-2 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-sequence/releases) | 0.72       |
| 0.10.0                | [@react-native-ohos/react-native-image-sequence-2 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-sequence/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-sequence-2
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-sequence-2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { StyleSheet, View } from "react-native";
import ImageSequence from 'react-native-image-sequence-2'
const images = [
    { uri: "https://octodex.github.com/images/stormtroopocat.jpg" },
    { uri: 'https://octodex.github.com/images/saint_nictocat.jpg' },
    require("./assets/2.jpg"),
    require("./assets/3.jpg"),
    require("./assets/4.jpg"),
    require("./assets/5.jpg"),
    require("./assets/6.jpg"),
];
const centerIndex = Math.floor(Math.random() * images.length);
const TestDemo = () => {
    return (
        <View style={styles.container}>
            <ImageSequence
                images={images}
                startFrameIndex={centerIndex}
                style={{ width: 200, height: 300 }}
            />
        </View>
    )
}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
    },
})

export default TestDemo
```

## 2. 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## 3. Link

|                           | 是否支持autolink | RN框架版本 |
|---------------------------|-----------------|------------|
| ~0.10.0                   |  No              |  0.77     |
| ~0.9.2                    |  Yes             |  0.72     |
| <= 0.9.1-0.0.3@deprecated |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

### 3.1 Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `harmony/oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

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

### 3.2 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-image-sequence-2":"file:../../node_modules/@react-native-ohos/react-native-image-sequence-2/harmony/image_sequence.har"
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

### 3.3 配置 CMakeLists 和引入 ImageSequence2Package

> 若使用的是 <= 0.9.1-0.0.3 版本，请跳过本章。

 打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-sequence-2/src/main/cpp" ./image_sequence_2)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_sequence_2)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "ImageSequence2Package.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<ImageSequence2Package>(ctx)
    };
}
```

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNImageSequence } from "@react-native-ohos/react-native-image-sequence-2"

const arkTsComponentNames: Array<string> = ["SampleView", 
"Generated",
"PropsDisplayer",
+ RNImageSequence.NAME
]

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+  if (ctx.componentName === RNImageSequence.NAME) {
+     RNImageSequence({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag
+     })
+   }
...
}
...
```

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ImageSequencePackage } from "@react-native-ohos/react-native-image-sequence-2/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageSequencePackage(ctx) 
  ];
}
```

</details>

## 4. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 5. 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 6. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| images           | 源图像数组。数组的每个元素应该是调用require(imagePath)的结果 | any[]   | Yes      | All      | Yes               |
| startFrameIndex  | 序列应从图像数组的哪个索引开始。默认值: 0                    | number  | No       | All      | Yes               |
| framesPerSecond  | 图像序列的播放速度。默认值: 24                               | number  | No       | All      | Yes               |
| loop             | 序列是否循环播放。默认值: true                               | boolean | No       | All      | Yes               |
| downsampleWidth  | 用于可选降采样的宽度。必须将`downsampleWidth`和`downsampleHeight`都设置为正数才能启用降采样。默认值: -1 | number  | No       | All      | Yes               |
| downsampleHeight | 用于可选降采样的高度。必须将`downsampleWidth`和`downsampleHeight`都设置为正数才能启用降采样。默认值: -1 | number  | No       | All      | Yes               |

## 7. 遗留问题

## 8. 其他

## 9. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bwindsor/react-native-image-sequence/blob/aee3d372d7960234721e32d2b02432fb5d0fa98b/LICENSE) ，请自由地享受和参与开源。

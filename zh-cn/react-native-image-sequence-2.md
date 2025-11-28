> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-image-sequence</code> </h1>
</p>


本项目基于 [react-native-image-sequence@0.9.1](https://github.com/bwindsor/react-native-image-sequence/tree/aee3d372d7960234721e32d2b02432fb5d0fa98b) 开发。

## 1. 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息，并下载适用版本的 tgz 包：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.9.1@deprecated     | [@react-native-oh-tpl/react-native-mage-sequence-2 Releases(deprecated)](https://github.com/react-native-oh-library/react-native-mage-sequence-2/releases) | 0.72       |
| 0.9.2                | [@react-native-ohos/react-native-mage-sequence-2 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-mage-sequence-2/releases) | 0.72       |
| 0.10.0                | [@react-native-ohos/react-native-mage-sequence-2 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-mage-sequence-2/releases) | 0.77       |

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

TestDemo.tsx

```js
import React, { useState } from "react";
import { SafeAreaView, StyleSheet } from "react-native-harmony";
import { View, Text, Switch, TextInput, Button } from "react-native";
import TestDemo2 from "./TestDemo2";

const images = [
  { uri: "https://octodex.github.com/images/stormtroopocat.jpg" },
  { uri: 'https://octodex.github.com/images/saint_nictocat.jpg' },
  require("./assets/2.jpg"),
  require("./assets/3.jpg"),
  require("./assets/4.jpg"),
  require("./assets/5.jpg"),
  require("./assets/6.jpg"),
];

export interface sequenceType {
  images: NodeRequire[];
  loop: boolean;
  startFrameIndex: number;
  framesPerSecond: number;
  downsampleWidth: number;
  downsampleHeight: number;
}

const ImageSequenceDemo = (props: any) => {
  const [loopData, setLoopData] = useState(false);
  const [isShow, setIsShow] = useState(false);
  const [winWidth, setWinWidth] = useState(300);
  const [winHeight, setWinHeight] = useState(200);
  const [downsampleWidth, setDownSampleWidth] = useState(-1);
  const [downsampleHeight, setDownSampleHeight] = useState(-1);

  // 设置采样宽度
  const inputSampleWidth = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setDownSampleWidth(Number(value));
  };

  // 设置采样高度
  const inputSampleHeight = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setDownSampleHeight(Number(value));
  };

  // 设置起始位置
  const [startFrameIndex, setFrameIndex] = useState(0);
  const inputStartFrameIndex = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    let _value = Number(value);
    if (Number(value) > images.length) {
      _value = 0;
    }
    setFrameIndex(_value);
  };

  // 设置速率
  const [framesPerSecond, setFramesPerSecond] = useState(24);
  const inputFramesPerSecond = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    let _value = Number(value);
    if (Number(value) <= 0) {
      _value = 24;
    }
    setFramesPerSecond(_value);
  };

  const buttonIsShow = () => {
    setIsShow(!isShow);
  };

  const inputSetWinWidth = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setWinWidth(Number(value));
  };

  const inputSetWinHeight = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setWinHeight(Number(value));
  };

  return (
    <SafeAreaView>
      <View>
        <View>
          <Text>
            Current view size:width: {winWidth}, height:{winHeight}
          </Text>
          <Text>
            开启循环：<Switch onValueChange={(value) => setLoopData(value)}></Switch>
          </Text>
          <View>
            <Text>图片宽度/高度：</Text>
            <View style={styles.box}>
              <TextInput
                style={[styles.input, styles.input1]}
                onChangeText={(value) => inputSetWinWidth(value)}
                defaultValue="300"
                keyboardType="numeric"
              />
              <TextInput
                style={[styles.input, styles.input1]}
                onChangeText={(value) => inputSetWinHeight(value)}
                defaultValue="200"
                keyboardType="numeric"
              />
            </View>
          </View>
          <Text>开始位置：</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputStartFrameIndex(value)}
            defaultValue="0"
            keyboardType="numeric"
          />
          <Text>播放速度：</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputFramesPerSecond(value)}
            defaultValue="24"
            keyboardType="numeric"
          />
          <View>
             <Text>采样宽度/高度：</Text>
             <View style={styles.box}>
                <TextInput style={[styles.input, styles.input1]} onChangeText={value => inputSampleWidth(value)} defaultValue='-1' keyboardType='default' />
                 <TextInput style={[styles.input, styles.input1]} onChangeText={value => inputSampleHeight(value)} defaultValue='-1' keyboardType='default' />
              </View>
           </View>
        </View>
        {!isShow ? (
          <Button title="显示" onPress={() => buttonIsShow()} />
        ) : (
          <Button title="返回" onPress={() => buttonIsShow()} />
        )}
        {isShow ? (
          <TestDemo2
            loop={loopData}
            images={images}
            width={winWidth}
            height={winHeight}
            startFrameIndex={startFrameIndex}
            framesPerSecond={framesPerSecond}
            downsampleWidth={downsampleWidth}
            downsampleHeight={downsampleHeight}
          />
        ) : null}
      </View>
    </SafeAreaView>
  );
};
const styles = StyleSheet.create({
  continer: {
    flex: 1,
    justifyContent: "center",
    width: "100%",
    height: "100%",
  },
  title: {
    textAlign: "center",
    marginVertical: 8,
  },
  fixToText: {
    flexDirection: "row",
    justifyContent: "space-between",
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth,
  },
  input: {
    height: 40,
    margin: 12,
    borderWidth: 1,
    borderColor: "red",
    padding: 10,
    width: 200,
  },
  box: {
    flexDirection: "row",
    justifyContent: "flex-start",
  },
  input1: {
    width: 100,
  },
});

export default ImageSequenceDemo;
```

TestDemo2.tsx

```js
import { StyleSheet, View } from "react-native";
import ImageSequence from 'react-native-image-sequence-2'

const Separator = () => <View style={styles.separator}/>
const TestDemo2 = (props: any) => {
    return (
        <ImageSequence
        images={props.images}
        loop={props.loop}
        startFrameIndex={props.startFrameIndex}
        framesPerSecond={props.framesPerSecond}
        downsampleWidth={props.downsampleWidth}
        downsampleHeight={props.downsampleHeight}
        style={{width: props.width, height: props.height}}
        />
    )
}
const styles = StyleSheet.create({
    separator: {
        marginVertical: 8,
        borderBottomColor: '#737373',
        borderBottomWidth: StyleSheet.hairlineWidth
    }
})

export default TestDemo2
```

## 2. 使用 Codegen

Version >= @react-native-ohos/react-native-image-sequence-2@0.9.2，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## 3. Manual Link

Version >= @react-native-ohos/react-native-image-sequence-2@0.9.2，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

### 3.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 3.2. 引入原生端代码

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

### 3.3. 配置 CMakeLists 和引入 ImageSequence2Package

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

### 3.4. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 4. 约束与限制

### 4.1. 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 5. 属性

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

## 6. 遗留问题

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bwindsor/react-native-image-sequence/blob/aee3d372d7960234721e32d2b02432fb5d0fa98b/LICENSE) ，请自由地享受和参与开源。

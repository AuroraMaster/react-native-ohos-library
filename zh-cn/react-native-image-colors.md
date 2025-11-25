> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-colors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/osamaqarem/react-native-image-colors">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20|%20expo%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/osamaqarem/react-native-image-colors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-colors)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 2.4.0@deprecated      | [@react-native-oh-tpl/react-native-image-colors Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-colors/releases) | 0.72       |
| 2.4.1      | [@react-native-ohos/react-native-image-colors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-colors/releases)             | 0.72       |
| 2.5.1      | [@react-native-ohos/react-native-image-colors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-image-colors/releases)             | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-image-colors
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-image-colors
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect, useState } from 'react'
import {
  Platform,
  StyleSheet,
  Text,
  View,
  Image,
  SafeAreaView,
  Button,
} from 'react-native'
import { getColors } from 'react-native-image-colors'

const imgCat = require('./assets/images/cat.jpg')
const yunaUrl = 'https://img0.baidu.com/it/u=1934875822,4119553331&fm=253&fmt=auto&app=138&f=JPEG?w=720&h=480'
const base = 'data:image/jpeg;base64...'

const initialState = {
  colorOne: { value: '', name: '' },
  colorTwo: { value: '', name: '' },
  colorThree: { value: '', name: '' },
  colorFour: { value: '', name: '' },
  rawResult: '',
}

export default function demo() {
  const [colors, setColors] = useState(initialState)
  const fetchColors = async () => {
    const result = await getColors(imgCat, {
      fallback: '#000000',
    })

    switch (result.platform) {
      case 'android':
      case 'web':
        setColors({
          colorOne: { value: result.lightVibrant, name: 'lightVibrant' },
          colorTwo: { value: result.dominant, name: 'dominant' },
          colorThree: { value: result.vibrant, name: 'vibrant' },
          colorFour: { value: result.darkVibrant, name: 'darkVibrant' },
          rawResult: JSON.stringify(result),
        })
        break
      case 'ios':
        setColors({
          colorOne: { value: result.background, name: 'background' },
          colorTwo: { value: result.detail, name: 'detail' },
          colorThree: { value: result.primary, name: 'primary' },
          colorFour: { value: result.secondary, name: 'secondary' },
          rawResult: JSON.stringify(result),
        })
        break
      case 'harmony':
        setColors({
          colorOne: { value: result.mainColor, name: 'mainColor' },
          colorTwo: { value: result.largestProportionColor, name: 'largestProportionColor' },
          colorThree: { value: result.highestSaturationColor, name: 'highestSaturationColor' },
          colorFour: { value: result.averageColor, name: 'averageColor' },
          rawResult: JSON.stringify(result),
        })
        break
      default:
        throw new Error('Unexpected platform')
    }
  }

  return (
    <View style={styles.container}>
      <SafeAreaView style={styles.resultContainer}>
        <Text style={styles.loading}>Result:</Text>
        <Button title='按钮' onPress={() => fetchColors() }></Button>
        <Text style={styles.result}>{colors.rawResult}</Text>
      </SafeAreaView>
      <Image
        resizeMode="contain"
        style={styles.image}
        source={ imgCat }
      />
      <View style={styles.row}>

        <Box name={colors.colorOne.name} value={colors.colorOne.value} />
        <Box name={colors.colorTwo.name} value={colors.colorTwo.value} />
      </View>
      <View style={styles.row}>
        <Box name={colors.colorThree.name} value={colors.colorThree.value} />
        <Box name={colors.colorFour.name} value={colors.colorFour.value} />
      </View>
    </View>
  )
}

interface BoxProps {
  value: string
  name: string
}

const Box = ({ value, name }: BoxProps) => {
  return (
    <View
      style={[
        styles.box,
        {
          backgroundColor: value,
        },
      ]}
    >
      <Text style={styles.colorName}>{name}</Text>
    </View>
  )
}

const styles = StyleSheet.create({
  image: {
    width: '100%',
    height: 250,
  },
  colorName: {
    backgroundColor: 'white',
    padding: 4,
    fontSize: 18,
  },
  box: {
    flex: 1,
    backgroundColor: 'red',
    justifyContent: 'center',
    alignItems: 'center',
  },
  row: {
    flex: 1,
    flexDirection: 'row',
    width: '100%',
  },
  resultContainer: {
    flex: 1,
    padding: 20,
    width: '100%'
  },
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  loading: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  result: {
    textAlign: 'center',
    color: '#333333',
  },
})
```

## 使用 Codegen

> [!TIP] V2.4.1 不需要执行Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-image-colors@2.4.1，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

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
    "@react-native-ohos/react-native-image-colors": "file:../../node_modules/@react-native-ohos/react-native-image-colors/harmony/image_colors.har"
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


### 3.配置CMakeLists 和引入 ImageColorsPackage

> [!TIP] 若使用的是 2.4.0 版本，请跳过本章

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```cmake
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-image-colors/src/main/cpp" ./image-colors)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_colors)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ImageColorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ImageColorsPackage>(ctx)
    };
}
```


### 4.在 ArkTs 侧引入 RNImageColorsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNImageColorsPackage } from "@react-native-ohos/react-native-image-colors/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageColorsPackage(ctx)
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

在以下版本验证通过

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH：0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## API

### ImageColors.getColors(uri: string, config?: Config): Promise


> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                           | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | ----------------- |
| getColors | 从图像中获取主要颜色 | Function | yes      | all      | yes               |


### Uri

A string which can be:

| Name      | Description                           | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | ----------------- |
| uri |  1. URL: `https://i.imgur.com/O3XSdU7.jpg`<br>2. 本地文件: const catImg = require('./images/cat.jpg')<br>3. Base64: const catImgBase64 = 'data:image/jpeg;base64,/9j/4Ri...' | string | yes      | all | yes               |

  > The mime type prefix for base64 is required (e.g. data:image/png;base64).

### Config

The config object is optional.

| Name       | Description                                                                                                                                                                                    | Type                                                   | Required                                           | Default     | Supported | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ----------- | ------------------- | ----------------- | ----------------- |
| `fallback`     | 如果无法检索到颜色属性，将默认使用此十六进制颜色字符串                                                         | `string`                                               | no                                             | `"#000000"` | all              | yes |
| `cache`        | 启用结果的内存缓存 - 下次跳过下载相同图像 time.                                                                                                           | `boolean`                                              | no                                            | `false`     | all              | yes |
| `key`          | 用于缓存条目的唯一键。默认使用图像URI作为唯一键。如果启用缓存并使用base64字符串作为URI，应显式传递键 | `string`                                               | no                                             | `undefined` | all              | yes |
| `headers`      | 与下载图像的GET请求一起发送的HTTP头                                                                                                                       | `Record<string, string>`                               | no                             | `undefined` | iOS, Android        | yes |
| `pixelSpacing` | 迭代图像像素时要跳过的像素数。值越高性能越好（注意：值不能低于1）                                                            | `number`                                               | no                                             | `5`         | Android             | no |
| `quality`      | 最高意味着不降尺度且颜色非常好                                                                                                                                           | `'lowest'` <br> `'low'` <br> `'high'` <br> `'highest'` | no | `'low'`     | iOS, Web          | no |

### ImageColorsResult

Every result object contains a respective `platform` key to help narrow down the type.

HarmonyImageColors

| Name                     | Description                                         | Type        | Required | Platform  | HarmonyOS Support |
| ------------------------ | --------------------------------------------------- | ----------- | -------- | --------- | ----------------- |
| `mainColor`              | 图像的主要颜色                       | `string`    | no       | harmonyOS | yes               |
| `largestProportionColor` | 图像中比例最高的颜色 | `string`    | no       | harmonyOS | yes               |
| `highestSaturationColor` | 图像中饱和度最高的颜色 | `string`    | no       | harmonyOS | yes               |
| `averageColor`           | 图像的平均颜色                     | `string`    | no       | harmonyOS | yes               |
| `platform`               | 平台是HarmonyOS                | `string` | no       | all | yes               |

### ImageColors.cache

| Name      | Description                           | Type     | Required | Params | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | -------- | ----------------- |
| getItem | 读取缓存结果 | Function | no      | key: string      | all      | yes               |
| setItem | 设置缓存结果 | Function | no      | key: string, value: ImageColorsResult      | all      | yes               |
| removeItem | 删除缓存结果 | Function | no      | key: string      | all      | yes               |
| clear | 清除缓存 | Function | no      |                  | all      | yes               |


### Notes
- Since the implementation of each platform is different you can get **different color results for each**.
- This module is a wrapper around the [Palette](https://developer.android.com/reference/androidx/palette/graphics/Palette) class on Android, [UIImageColors](https://github.com/jathu/UIImageColors) on iOS and [node-vibrant](https://github.com/Vibrant-Colors/node-vibrant) for the web and [@ohos.effectKit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-effectkit-V5) on harmonyOS.


## 遗留问题

- [x] harmonyOS获取颜色值暂时只能得到固定的一种颜色，暂不支持通过传入`pixelSpacing`或`quality`参数来计算获取不同精确度的颜色值。[issue链接](https://github.com/react-native-oh-library/react-native-image-colors/issues/16) 

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/osamaqarem/react-native-image-colors/blob/master/LICENSE) ，请自由地享受和参与开源。

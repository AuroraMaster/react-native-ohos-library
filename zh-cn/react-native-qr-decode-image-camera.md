> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qr-decode-image-camera</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 1.1.4@deprecated     | [@react-native-oh-tpl/react-native-qr-decode-image-camera Releases(deprecated)](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases) | 0.72       |
| 1.1.5      | [@react-native-ohos/react-native-qr-decode-image-camera Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-qr-decode-image-camera/releases) | 0.72       |
| 1.2.0      | [@react-native-ohos/react-native-qr-decode-image-camera Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-qr-decode-image-camera/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-qr-decode-image-camera
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-qr-decode-image-camera
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> 示例中：launchImageLibrary 方法需引入 Harmony OS 的 react-native-image-picker 库，跳转 [react-native-image-picker](/zh-cn/react-native-image-picker.md)查看使用方法。

QRreader

```js
import React, {useState} from 'react';
import {Button, View, Text} from 'react-native';
import {QRreader} from 'react-native-qr-decode-image-camera';
import {launchImageLibrary} from 'react-native-image-picker';

export const qrExample = () => {
  const [reader, setReader] = useState<any>('');
  return (
    <View style={{flex: 1, justifyContent: 'center', alignItems: 'center'}}>
      <Button
        onPress={() => {
          launchImageLibrary({mediaType: 'photo', selectionLimit: 1}, data => {
            if (data.assets?.length) {
              const path = {
                uri: data.assets[0].originalPath,
              };
              QRreader(path)
                .then(res => {
                  setReader(res?.[0]?.originalValue);
                })
                .catch(error => {
                  console.log(error);
                });
            }
          });
        }}
        title="点击选择二维码照片 "
      />
      <Text style={{fontSize: 20}}>{reader}</Text>
    </View>
  );
};
```
QRscanner

```json
import React, {useState} from 'react';
import { View, Text, TouchableOpacity, StyleSheet} from 'react-native';
import { QRscanner} from 'react-native-qr-decode-image-camera';


export const qrExample = () => {

  const [flashMode, setflashMode] = useState(false);
  const onRead = res => {
    console.log(res);
  };
  return (
    <View style={styles.container}>
      <QRscanner
        onRead={onRead}
        renderBottomView={() => {
          return (
            <View
              style={{
                flex: 1,
                flexDirection: 'row',
                backgroundColor: '#0000004D',
              }}>
              <TouchableOpacity
                style={{
                  flex: 1,
                  alignItems: 'center',
                  justifyContent: 'center',
                }}
                onPress={() => {
                  if (flashMode) {
                    setflashMode(false);
                  } else {
                    setflashMode(true);
                  }
                }}>
                <Text style={{color: '#fff'}}>flashMode</Text>
              </TouchableOpacity>
            </View>
          );
        }}
        flashMode={flashMode}
        finderY={50}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000',
  },
});
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-qr-decode-image-camera@1.1.5，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-qr-decode-image-camera@1.1.5，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

本库鸿蒙侧实现依赖@react-native-ohos/react-native-vision-camera 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-ohos/react-native-vision-camera](/zh-cn/react-native-vision-camera.md)进行引入

此步骤为手动配置原生依赖项的指导。

## 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

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

- 0.72
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-qr-decode-image-camera": "file:../../node_modules/@react-native-ohos/react-native-qr-decode-image-camera/harmony/qr_decode_image_camera.har"
  }
```

- 0.77
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-qr-decode-image-camera": "file:../../node_modules/@react-native-ohos/react-native-qr-decode-image-camera/harmony/qr_decode_image_camera.har"
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

### 3.在 ArkTs 侧引入 RNQrDecodeImageCameraPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：


```diff
  ...
+ import {RNQrDecodeImageCameraPackage} from '@react-native-ohos/react-native-qr-decode-image-camera/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQrDecodeImageCameraPackage(ctx)
  ];
}
```

### 4.在 ArkTs 侧引入 Fabric 组件

找到 function buildCustomRNComponent()，一般位于 entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets，添加：

```diff
  ...
  // 0.72
+ import { NativeScan } from "@react-native-oh-tpl/react-native-qr-decode-image-camera"
  // 0.77
+ import { NativeScan } from "@react-native-ohos/react-native-qr-decode-image-camera"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === NativeScan.NAME) {
+   NativeScan({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

### 5.配置 CMakeLists 和引入 QrDecodeImageCameraPackage

> 若使用的是 <= 1.1.4 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-qr-decode-image-camera/src/main/cpp" ./qr-decode-image-camera)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_qr_decode_image_camera)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "QrDecodeImageCameraPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<QrDecodeImageCameraPackage>(ctx),
    };
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

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

 | Name | Description | Type | Required | Platform | HarmonyOS Support |
 | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
 | QRreader | Invoke this method to invoke the gallery, select the QR code image for image decoding, and asynchronously return the result. | funtion | no | iOS/Android | yes |

## 属性

### QRscanner

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| isRepeatScan | 是否允许重复扫描 | boolean | no | iOS/Android | yes |
| zoom | 相机焦距范围 0-1 | number | no | iOS/Android | no |
| flashMode | 开启闪光灯 | boolean | no | iOS/Android | yes |
| onRead | 扫描回调 | funtion | yes | iOS/Android | yes |
| maskColor | 遮罩层颜色 | string | no | iOS/Android | yes |
| borderColor | 边框颜色 | string | no | iOS/Android | yes |
| cornerColor | 扫描框边角颜色 | string | no | iOS/Android | yes |
| borderWidth | 扫描框边框宽度 | number | no | iOS/Android | yes |
| cornerBorderWidth | 扫描框边角宽度 | number | no | iOS/Android | yes |
| cornerBorderLength | 扫描框边角的宽高 | number | no | iOS/Android | yes |
| rectHeight | 扫描框高度 | number | no | iOS/Android | yes |
| rectWidth | 扫描框宽度 | number | no | iOS/Android | yes |
| finderX | 扫描框 X 轴偏移量 | number | no | iOS/Android | yes |
| finderY | 扫描框 Y 轴偏移量 | number | no | iOS/Android | yes |
| isCornerOffset | 边角是否有偏移 | boolean | no | iOS/Android | yes |
| cornerOffsetSize | 偏移量 | number | no | iOS/Android | yes |
| bottomHeight | 底部预留高度 | number | no | iOS/Android | yes |
| scanBarAnimateTime | 扫描线动画时间 | number | no | iOS/Android | yes |
| scanBarColor | 扫描线颜色 | string | no | iOS/Android | yes |
| scanBarImage | 扫描线图片 | any | no | iOS/Android | yes |
| scanBarHeight | 扫描线高度 | number | no | iOS/Android | yes |
| scanBarMargin | 扫描线左右边距 | number | no | IOS/Android | yes |
| hintText | 提示文本 | string | no | IOS/Android | yes |
| hintTextStyle | 提示文本样式 | object | no | iOS/Android | yes |
| hintTextPosition | 提示文本位置 | number | no | iOS/Android | yes |
| renderTopView | 渲染顶部视图 | funtion | no | iOS/Android | yes |
| renderBottomView | 渲染底部视图 | funtion | no | iOS/Android | yes |
| isShowScanBar | 是否显示扫描线 | boolean | no | iOS/Android | yes |
| topViewStyle | 顶部容器样式 | object | no | iOS/Android | yes |
| bottomViewStyle | 底部容器样式 | object | no | iOS/Android | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE) ，请自由地享受和参与开源。
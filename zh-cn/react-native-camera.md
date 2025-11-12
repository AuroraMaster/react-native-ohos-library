> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-camera</code> </h1>
</p>


本项目基于 [react-native-camera@v3.40.0](https://github.com/react-native-camera/react-native-camera/tree/v3.40.0) 开发。

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-ohos/react-native-camera Releases](https://github.com/react-native-oh-library/react-native-camera/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

| 三方库版本                 | 发布信息                                      |  支持RN版本                 |
| ------------------------- | ------------------------------------------------- |  -------------------------- |
| v3.40.0                 | [@react-native-ohos/react-native-camera Releases](https://github.com/react-native-oh-library/react-native-camera/releases)  | 0.72/0.77 |


## 1. 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-ohos/react-native-camera
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-camera
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Text, View } from 'react-native';
import { RNCamera } from 'react-native-camera';
import {
    StyleSheet,
} from 'react-native';

export function CameraExample() {
    return (
        <View>
            <View style={[styles.button, styles.margin20]}
                onTouchEnd={() => {
                    const options = {
                        quality: 0.5,
                        base64: true,
                        width: 300,
                        height: 300,
                    };
                    this.camera.takePictureAsync(options).then((photoResult) => {
                        console.log("takepicture result:" + photoResult?.path)
                    });

                }
                }>
                <Text style={styles.buttonText}>测试takepicture</Text>
            </View>
           

            <RNCamera
                ref={ref => {
                    this.camera = ref;
                }}
                style={styles.cameraPreview}
            >
            </RNCamera>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        paddingTop: 10,
        backgroundColor: '#000',
    },
    button: {
        width: 160,
        height: 36,
        backgroundColor: 'hsl(190, 50%, 70%)',
        paddingHorizontal: 16,
        paddingVertical: 8,
        borderRadius: 8,
    },
    margin20: {
        marginLeft: 20
    },
    buttonText: {
        width: '100%',
        height: '100%',
        fontWeight: 'bold',
    },
    cameraPreview: { width: '100%', aspectRatio: 56 / 100 }
});

export default CameraExample;
```

## 2. Manual Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)：

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

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/react-native-camera": "file:../../node_modules/@react-native-ohos/react-native-camera/harmony/reactNativeCamera.har"
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

### 2.3.配置 CMakeLists 和引入 NativeCameraPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-camera/src/main/cpp" ./reactNativeCamera)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_native_camera)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "NativeCameraPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+      std::make_shared<NativeCameraPackage>(ctx)
    };
}
```


###  2.4.在 ArkTs 侧引入 react-native-camera 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { ReactCameraView } from '@react-native-ohos/react-native-camera';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+    if (ctx.componentName === ReactCameraView.NAME) {
+      ReactCameraView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
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
+ ReactCameraView.NAME
  ];
```

###  2.5.在 ArkTs 侧引入 ReactNativeCameraPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：


```diff  
  ... 
+ import { ReactNativeCameraPackage, FaceDectorPackage } from '@react-native-ohos/react-native-camera/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReactNativeCameraPackage(ctx),
+   new FaceDectorPackage(ctx)
  ];
}
```

###  2.6.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3.  约束与限制

### 3.1. 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-camera Releases](https://github.com/react-native-oh-library/react-native-camera/releases) 

### 3.2. 权限要求

####  在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.CAMERA",
+    "reason": "$string:camera_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.MICROPHONE",
+    "reason": "$string:microphone_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
]
```

#### 在 entry 目录下添加申请以上权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "camera_reason",
+      "value": "使用相机"
+    },
+    {
+      "name": "microphone_reason",
+      "value": "使用麦克风"
+    },
  ]
}
```

## 4. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform  | HarmonyOS Support |
| ---- | ----------- | ---- | -------- |-----------|-------------------|
| children                 | 设置子组件               | View    | no       | iOS/Android | yes               |
| type                     | 选择摄像头               | string  | no       | iOS/Android | yes               |
| flashMode                | 设置闪光灯               | string  | no       | iOS/Android | yes               |
| exposure                 | 设置曝光                 | number  | no       | iOS/Android | yes               |
| autoFocus                | 设置自动对焦             | string  | no       | iOS/Android | yes               |
| whiteBalance             | 白平衡                   | string  | no       | iOS/Android | yes               |
| captureAudio             | 是否开启录音             | boolean | no       | iOS/Android | yes               |
| zoom                     | 设置缩放比例             | number  | no       | iOS/Android | yes               |
| focusDepth               | 非自动对焦时，设置对焦值 | number  | no       | iOS/Android | yes               |
| maxZoom                  | 设置最大缩放比例         | number  | no       | iOS/Android | yes               |
| pictureSize              | 设置默认图片分辨率       | striing | no       | iOS/Android | yes               |
| notAuthorizedView        | 未授权显示的ui           | View    | no       | Android     | no                |
| pendingAuthorizationView | 正在授权显示的ui         | View    | no       | Android     | no                |
| ratio                    | 相机比例                 | string  | no       | Android     | no                |
| defaultVideoQuality      | 默认视频分辨率           | string  | no       | iOS/Android | yes               |

### 
## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
### camera
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- |-------------------|
| onBarCodeRead        | 接收barcode扫描数据  | BarCodeReadEvent    | no       | iOS/Android | yes               |
| onFacesDetected      | 接收人脸识别数据 | Face | no | iOS/Android | no             |
| takePictureAsync     | 照相                 | TakePictureResponse | no       | iOS/Android | yes               |
| recordAsync          | 开始录像             | RecordResponse      | no       | iOS/Android | yes               |
| stopRecording        | 停止录像             | void                | no       | iOS/Android | yes               |
| getCameraIdAsync     | 获取可用摄像头id列表 | CameraType          | no       | iOS/Android | yes               |
| refreshAuthorization | 请求权限             | void                | no       | iOS/Android | yes               |


## 5.遗留问题
- [ ] onFacesDetected能力无法实现 [issue#1](https://github.com/react-native-oh-library/react-native-camera/issues/8) 

## 6.其他
- notAuthorizedView属性,pendingAuthorizationView属性是android独有的属性，申请授权时显示的UI，harmony已经提供授权时的弹窗。
- ratio是android独有的属性，在ios无效果 [源库readme位置](https://github.com/react-native-camera/react-native-camera/blob/v3.40.0/docs/RNCamera.md#android-ratio)

## 7.开源协议

本项目基于 [MIT License (MIT)](https://github.com/react-native-camera/react-native-camera/blob/master/LICENSE) ，请自由地享受和参与开源。

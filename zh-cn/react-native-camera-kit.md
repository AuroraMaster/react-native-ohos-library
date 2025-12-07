> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-camera-kit</code> </h1>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-camera-kit)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 14.0.1@deprecated      | [@react-native-oh-tpl/react-native-camera-kit Releases(deprecated)](https://github.com/react-native-oh-library/react-native-camera-kit/releases) | 0.72       |
| 14.0.2      | [@react-native-ohos/react-native-camera-kit Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-camera-kit/releases)                        | 0.72       |
| 15.1.1     | [@react-native-ohos/react-native-camera-kit Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-camera-kit/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-camera-kit
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-camera-kit
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
### camera example
``` js
import React, {useRef, useState} from 'react';
import {Text, StyleSheet, View, Button} from 'react-native';
import {CameraApi, CameraType,Camera} from 'react-native-camera-kit';

export const CameraDemo: React.FC = (): JSX.Element => {
  const nativeRef = useRef<CameraApi>(null);
  const [zoom, setZoom] = useState<number>(0);
  const [errorStr, setErrorStr] = useState<string>('');
  const [photo, setPhoto] = useState<string>('');

  const onError = (e: any) => {
    setErrorStr(e.nativeEvent.errorMessage);
  };

  const onZoom = (e: any) => {
    setZoom(e.nativeEvent.zoom);
  };

  const onPhoto = async () => {
    const result = await nativeRef.current?.capture();
    result && setPhoto(JSON.stringify(result));
  };

  return (
    <>
      <View>
        <Camera
          style={{width: '100%', height: 500}}
          ref={nativeRef}
          maxZoom={10}
          cameraType={CameraType.Back}
          flashMode={0}
          onError={onError}
          onZoom={onZoom}
        />
      </View>
      <View>
        <Button title="拍照" onPress={onPhoto} />
        <Text style={styles.text}>zoom:{zoom}</Text>
        <Text style={styles.text}>error:{errorStr}</Text>
        <Text style={styles.text}>photo:{photo}</Text>
      </View>
    </>
  );
};

const styles = StyleSheet.create({
  text: {
    fontSize: 20,
    textAlign: 'center',
    color: '#000',
    marginTop: 10,
  },
});

```
### scanCode example
``` js
import React, {useRef, useState} from 'react';
import {Text, StyleSheet, View} from 'react-native';
import {CameraApi, CameraType,Camera} from 'react-native-camera-kit';

export const ScanCodeDemo: React.FC = (): JSX.Element => {
  const nativeRef = useRef<CameraApi>(null);
  const [zoomStr, setZoomStr] = useState<number>(0);
  const [errorStr, setErrorStr] = useState<string>('');
  const [codeResult, setCodeResult] = useState<string>('');

  const onError = (e: any) => {
    setErrorStr(e.nativeEvent.errorMessage);
  };

  const onZoom = (e: any) => {
    setZoomStr(e.nativeEvent.zoom);
  };

  const onReadCode = (e: any) => {
    setCodeResult(JSON.stringify(e));
  };

  return (
    <>
      <View>
        <Camera
          style={{width: 300, height: 400}}
          ref={nativeRef}
          maxZoom={50}
          cameraType={CameraType.Back}
          onError={onError}
          onZoom={onZoom}
          scanBarcode
          onReadCode={onReadCode}
          ratioOverlay="4:3"
        />
      </View>
      <View>
        <Text style={styles.text}>zoom:{zoomStr}</Text>
        <Text style={styles.text}>code:{codeResult}</Text>
        <Text style={styles.text}>error:{errorStr}</Text>
      </View>
    </>
  );
};

const styles = StyleSheet.create({
  text: {
    fontSize: 20,
    textAlign: 'center',
    color: '#000',
    marginTop: 10,
  },
});


```
## 使用 Codegen

Version >= @react-native-ohos/react-native-camera-kit@14.0.2，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-camera-kit@14.0.2，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides字段

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

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-camera-kit": "file:../../node_modules/@react-native-ohos/react-native-camera-kit/harmony/camera_kit.har"
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

### 3.在 ArkTs 侧引入 RTNCameraKitView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RTNCameraKitView } from "@react-native-ohos/react-native-camera-kit";

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RTNCameraKitView.NAME) {
+   RTNCameraKitView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
...
}
...
```
在`entry/src/main/ets/pages/index.ets`中，如果当前文件中存在`arkTsComponentNames`数组(后续版本新增内容)，则需要在其中追加：`RTNCameraKitView.NAME`;

```ts
  ...
 const arkTsComponentNames: Array<string> = [..., RTNCameraKitView.NAME]; 
  ...
```

### 4.在 ArkTs 侧引入 RTNCameraKitPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RTNCameraKitPackage } from "@react-native-ohos/react-native-camera-kit/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RTNCameraKitPackage(ctx),
  ];
}
```

### 5.配置 CMakeLists 和引入 CameraKitPackage

> 若使用的是 <= 14.0.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-camera-kit/src/main/cpp" ./camera_kit)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_camera_kit)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "CameraKitPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<CameraKitPackage>(ctx)
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

### 权限要求

以下权限中有`system_basic` 权限，而默认的应用权限是 `normal` ，只能使用 `normal` 等级的权限，所以可能会在安装hap包时报错**9568289**，请参考 [文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/bm-tool-V5#ZH-CN_TOPIC_0000001884757326__%E5%AE%89%E8%A3%85hap%E6%97%B6%E6%8F%90%E7%A4%BAcode9568289-error-install-failed-due-to-grant-request-permissions-failed) 修改应用等级为 `system_basic`

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
+  {
+    "name": "ohos.permission.APPROXIMATELY_LOCATION",
+    "reason": "$string:location_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  }
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
+      "name": "location_reason",
+      "value": "获取当前位置"
+    },
+    {
+      "name": "microphone_reason",
+      "value": "使用麦克风"
+    },
  ]
}
```

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Camera**：相机组件

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| ref | 相机视图的引用     | Ref | no       | All | yes               |
| style | 应用在相机视图上的样式 | StyleProp\<ViewStyle> | no       | All | yes               |
| flashMode  | 相机闪光灯模式。默认值：FlashMode.FLASH_MODE_CLOSE | FlashMode.FLASH_MODE_CLOSE / FlashMode.FLASH_MODE_OPEN / FlashMode.FLASH_MODE_AUTO / FlashMode.FLASH_MODE_ALWAYS_OPEN | no       | All | yes               |
| focusMode  | 相机对焦模式。默认值：FOCUS_MODE_AUTO     | FOCUS_MODE_CONTINUOUS_AUTO / FOCUS_MODE_AUTO / FOCUS_MODE_LOCKED / FocusMode.FOCUS_MODE_MANUAL | no       | All | yes               |
| zoomMode  | 启用双指缩放手势。默认值：开启     | 'on'`/`'off' | no       | All | yes               |
| zoom  | 控制缩放。默认值：1.0     | Number | no       | All | yes               |
| maxZoom  | 允许的最大缩放倍数（但不超过相机允许的最大值）。默认值：undefined（相机默认最大值）     | Number | no       | All | yes               |
| onZoom  | 用户做出捏合手势时的回调，无论zoom属性被设置为什么值。返回的事件包含zoom。例如：onZoom={(e) => console.log(e.nativeEvent.zoom)}。     | Function | no       | All | yes               |
| torchMode  | 相机激活时切换闪光灯。默认值：关闭     | 'on'`/`'off' | no       | All | yes               |
| cameraType  | 选择使用的相机。默认值：`CameraType. | 'front'/'back' | no       | All | yes               |
| onOrientationChange  | 物理设备方向改变时的回调。返回的事件包含orientation。例如：onOrientationChange={(event) => console.log(event.nativeEvent.orientation)}。使用import { Orientation } from 'react-native-camera-kit'; if (event.nativeEvent.orientation === Orientation.PORTRAIT) { ... }来理解新值     | Function | no       | iOS | yes               |
| onError  | 仅Android。相机初始化失败时的回调。例如：onError={(e) => console.log(e.nativeEvent.errorMessage)}。     | Function | no       | Android | yes               |
| shutterPhotoSound  |仅Android。启用或禁用拍照时的快门声音。默认值：`true`     | Boolean | no       | Android | yes   
| ratioOverlay  | 在相机预览中显示选定比例的引导覆盖层。不会裁剪图像（截至v9.0）。例如：'16:9'     | String | no       | iOS | yes               |
| ratioOverlayColor  | 任何带透明度的颜色。默认值：'#ffffff77'     | String | no       | All | yes               |
| resetFocusTimeout  | 在这么多毫秒后取消点击对焦。默认值0（禁用）。例如：5000是5秒。     | Number | no       | All | yes               |
| resetFocusWhenMotionDetected	  | 当对焦区域内容发生变化时取消点击对焦。原生iOS功能，参见文档：https://developer.apple.com/documentation/avfoundation/avcapturedevice/1624644-subjectareachangemonitoringenabl?language=objc)。默认值true。     | Boolean | no       | iOS | no             |
| resizeMode  | 确定视图内内容的缩放和裁剪行为。cover（在iOS上为resizeAspectFill）将内容缩放到完全填充视图，如果其宽高比与视图不同，则可能裁剪内容。contain（在iOS上为resizeAspect）将内容缩放到视图边界内而不裁剪，确保所有内容可见但可能引入黑边。默认行为取决于具体使用情况。     | 'cover' / 'contain' | no       | iOS | no             |
| onCaptureButtonPressIn  | iPhone拍摄按钮按下时的回调。例如：onCaptureButtonPressIn={() => console.log("volume button pressed in")}    | Function | no       | iOS | yes          |
| onCaptureButtonPressOut  | iPhone拍摄按钮释放时的回调。例如：onCaptureButtonPressOut={() => console.log("volume button released")}     | Function | no       | iOS | no             |

**ScanCode**：扫码组件

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| ref | 相机视图的引用     | Ref | no       | All      | yes               |
| style | 应用在相机视图上的样式 | StyleProp\<ViewStyle> | no       | All | yes               |
| flashMode  | 获取秘密值     | FlashMode.FLASH_MODE_CLOSE / FlashMode.FLASH_MODE_ALWAYS_OPEN | no       | All | yes          |
| zoomMode  | 启用双指缩放手势。默认值：开启     | 'on'`/`'off' | no       | All | yes               |
| zoom  | 控制缩放。默认值：1.0     | Number | no       | All | yes               |
| maxZoom  | 允许的最大缩放倍数（但不超过相机允许的最大值）。默认值：undefined（相机默认最大值）     | Number | no       | All | yes               |
| onZoom  | 用户做出捏合手势时的回调，无论zoom属性被设置为什么值。返回的事件包含zoom。例如：onZoom={(e) => console.log(e.nativeEvent.zoom)}。     | Function | no       | All | yes               |
| torchMode  | 相机激活时切换闪光灯。默认值：关闭     | 'on'`/`'off' | no       | All | yes               |
| cameraType                   | 选择使用的相机。默认值：`CameraType.             | 'front'/'back'        | no       | All | no                |
| onOrientationChange  | 物理设备方向改变时的回调。返回的事件包含orientation。例如：onOrientationChange={(event) => console.log(event.nativeEvent.orientation)}。使用import { Orientation } from 'react-native-camera-kit'; if (event.nativeEvent.orientation === Orientation.PORTRAIT) { ... }来理解新值     | Function | no       | iOS | no             |
| onError  | 仅Android。相机初始化失败时的回调。例如：onError={(e) => console.log(e.nativeEvent.errorMessage)}。     | Function | no       | Android | yes               |
| resetFocusTimeout  | 在这么多毫秒后取消点击对焦。默认值0（禁用）。例如：5000是5秒。     | Number | no       | All | yes               |
| scanThrottleDelay  | 扫描检测之间的时间间隔（毫秒）。默认值2000（2秒），如果需要动态设置此值，需要添加key参数来强制刷新此组件     | Number | no       | All | yes              |
| scanBarcode  | 启用条形码扫描器。默认值：`false`     | boolean | no       | All | yes               |
| showFrame  | 在条形码扫描器中显示框架。默认值：`false`     | boolean | no       | All | yes               |
| laserColor  | 条形码扫描器激光可视化的颜色。默认值：`red`     | string | no       | All | yes               |
| frameColor  | 条形码扫描器框架可视化的颜色。默认值：`yellow`     | string | no       | All | yes               |
| onReadCode  | 扫描器成功读取条形码时的回调。返回的事件包含`codeStringValue`。默认值：`null`。例如：`onReadCode={(event) => console.log(event.nativeEvent.codeStringValue)}     | Function | no       | All | yes               |

## 静态方法

| Name  | Description         | Type       | Required | Platform | HarmonyOS Support |
| ----- | ------------------- | ---------- | -------- | -------- | ----------------- |
| capture  | 以JPEG格式捕获图像。  | Promise<CaptureData> | No       | All      | Yes               |
| requestDeviceCameraAuthorization  | `AVAuthorizationStatusAuthorized`返回`true`，否则返回`false` | Promise<boolean> | No       | All      | Yes               |
| checkDeviceCameraAuthorizationStatus  | `AVAuthorizationStatusAuthorized`返回`true`，否则返回`false` | Promise<boolean> | All      | Yes               |Yes|


## 遗留问题

- [ ] 不支持查询传感器旋转角度 [issue#1](https://github.com/react-native-oh-library/react-native-camera-kit/issues/1) 
- [ ] 不支持使用前置相机进行扫码 [issue#2](https://github.com/react-native-oh-library/react-native-camera-kit/issues/2) 
- [ ] 不能同时设置flashMode和torchMode属性 [issue#3](https://github.com/react-native-oh-library/react-native-camera-kit/issues/3)
- [ ] 暂不支持onCaptureButtonPressOut属性 [issue#4](https://github.com/react-native-oh-library/react-native-camera-kit/issues/4)
- [ ] 暂不支持resetFocusWhenMotionDetected属性 [issue#5](https://github.com/react-native-oh-library/react-native-camera-kit/issues/5)
- [ ] 暂不支持resizeMode属性 [issue#6](https://github.com/react-native-oh-library/react-native-camera-kit/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/teslamotors/react-native-camera-kit/blob/master/LICENSE) ，请自由地享受和参与开源。

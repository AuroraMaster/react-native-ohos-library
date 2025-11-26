> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-cameraroll</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-cameraroll/react-native-cameraroll">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/react-native-cameraroll/react-native-cameraroll/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-cameraroll)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/camera-roll`，具体版本所属关系如下：

| Version                   | Package Name                     | Repository                                                   | Release                                                      | Supported RN Version |
| ------------------------- | -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------- |
| <= 7.8.3-0.1.5@deprecated | @react-native-oh-tpl/camera-roll | [Github(deprecated)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-cameraroll) | [Github Releases(deprecated)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-cameraroll%2Freleases) | 0.72                 |
| 7.8.4                    | @react-native-oh-tpl/camera-roll | [Github](https://github.com/react-native-oh-library/react-native-cameraroll) | [GitHub Releases](https://github.com/react-native-oh-library/react-native-cameraroll/releases) | 0.72                 |
| 7.10.1                   | @react-native-ohos/camera-roll   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-cameraroll) | [GitCode Releases]()                                         | 0.77                 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/camera-roll
```

#### **yarn**

```bash
yarn add @react-native-ohos/camera-roll
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, Button } from "react-native";
import {
  CameraRoll
} from "@react-native-camera-roll/camera-roll";

export default function App() {
  return (
    <View>
      <Button
        title="savePhotos"
        onPress={() => {
          CameraRoll.saveAsset("https://res.vmallres.com/uomcdn/CN/cms/202408/5442d69d916d4bcf9ee740d595a164fb.jpg").then((res) => {
            console.log('res-----',res);
          });
        }}
      />
    </View>
  );
}
```

## 使用 Codegen

Version >= @react-native-ohos/camera-roll@7.8.4，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/camera-roll@7.8.4，已支持 Autolink，无需手动配置。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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
    "@react-native-ohos/camera-roll": "file:../../node_modules/@react-native-ohos/camera-roll/harmony/camera_roll.har"
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

### 3.配置 CMakeLists 和引入 CameraRollPackage

> [!TIP] 仅0.77需要配置 CMakeLists 和引入 CameraRollPackage。

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/camera-roll/src/main/cpp" ./camera-roll)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_camera_roll)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "CameraRollPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<CameraRollPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 CameraRollPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { CameraRollPackage } from '@react-native-ohos/camera-roll/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CameraRollPackage(ctx),
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

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] HarmonyOS受限权限官方说明：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/restricted-permissions-V5#section397164718158 

**CameraRoll**

| Name | Description | Type | Required | Platform | HarmonyOS Support | Remarks |
| ---- | ----------- | ---- | -------- | -------- | ------------------ | ---- |
| save | 保存图片/视频 | function | no | iOS/Android | partially | 由于原库版本升级，该方法已弃用，可用saveAsset接口代替。 |
| saveAsset | 保存图片/视频 | function | no | iOS/Android | partially |  |
| saveToCameraRoll | 保存图片/视频 | function | no | iOS/Android | partially | 由于原库版本升级，该方法已弃用，调用会弹出警告，可用saveAsset接口代替。 |
| getPhotos | 查找图片/视频 | function | no | iOS/Android | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| getAlbums | 查找相册 | function | no | iOS/Android | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| deletePhotos | 删除图片/视频 | function | no | iOS/Android | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| iosGetImageDataById | 获取图片数据 | function | no | iOS | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| getPhotoThumbnail | 获取缩略图 | function | no | iOS | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                       | Description  | Type     | Required | Platform | HarmonyOS Support | Remarks                                                      |
| :----------------------------------------- | :----------- | -------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| `iosReadGalleryPermission`                 | 权限验证     | function | no       | iOS      | no                |                                                              |
| `iosRequestReadWriteGalleryPermission`     | 读写权限申请 | function | no       | iOS      | no                |                                                              |
| `iosRequestAddOnlyGalleryPermission`       | 添加权限申请 | function | no       | iOS      | no                |                                                              |
| `iosRefreshGallerySelection`               | 图片列表刷新 | function | no       | iOS      | no                |                                                              |
| `harmonyReadGalleryPermission`             | 权限验证     | function | no       | harmony  | no                | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| `harmonyRequestReadWriteGalleryPermission` | 读写权限申请 | function | no       | harmony  | no                | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| `harmonyRequestAddOnlyGalleryPermission`   | 添加权限申请 | function | no       | harmony  | no                | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| `harmonyRefreshGallerySelection`           | 图片列表刷新 | function | no       | harmony  | no                |                                                              |

## 遗留问题

- [ ] deletePhotos删除图片/视频，未实现 HarmonyOS 化: [issue#5](https://github.com/react-native-oh-library/react-native-cameraroll/issues/5)
- [ ] harmonyRefreshGallerySelection，HarmonyOS 暂无对应图片列表刷新的接口：[issue#8](https://github.com/react-native-oh-library/react-native-cameraroll/issues/8)
- [ ] 部分接口由于Harmony OS安全策略调整无法使用: [issue#25](https://github.com/react-native-oh-library/react-native-cameraroll/issues/25)
- [ ] saveAsset接口未完全支持: [issue#26](https://github.com/react-native-oh-library/react-native-cameraroll/issues/26)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-cameraroll/react-native-cameraroll/blob/master/LICENCE) ，请自由地享受和参与开源。
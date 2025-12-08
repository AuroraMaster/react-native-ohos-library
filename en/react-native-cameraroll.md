> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-cameraroll)

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/camera-roll`, After introducing the new version of the third-party library, The version correspondence details are as follows:

| Version                   | Package Name                     | Repository                                                   | Release                                                      | Supported RN Version |
| ------------------------- | -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------- |
| <= 7.8.3-0.1.5@deprecated | @react-native-oh-tpl/camera-roll | [Github(deprecated)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-cameraroll) | [Github Releases(deprecated)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-cameraroll%2Freleases) | 0.72                 |
| 7.8.4                     | @react-native-oh-tpl/camera-roll | [Github](https://github.com/react-native-oh-library/react-native-cameraroll) | [GitHub Releases](https://github.com/react-native-oh-library/react-native-cameraroll/releases) | 0.72                 |
| 7.10.1                    | @react-native-ohos/camera-roll   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-cameraroll) | [GitCode Releases]()                                         | 0.77                 |

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

Version >= @react-native-ohos/camera-roll@7.8.4, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/camera-roll@7.8.4 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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
    "@react-native-ohos/camera-roll": "file:../../node_modules/@react-native-ohos/camera-roll/harmony/camera_roll.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.Configure CMakeLists and import CameraRollPackage

> [!TIP] Only version 0.77 requires configuring CMakeLists and importing CameraRollPackage

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4.Introducing CameraRollPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 5.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

Verified in the following version:

RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200;ROM: 3.0.0.18;

RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK;IDE: DevEco Studio  6.0.0.868;ROM:6.0.0.112;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!TIP] HarmonyOS受限权限官方说明：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/restricted-permissions-V5#section397164718158 

**CameraRoll**

| Name | Description | Type | Required | Platform | HarmonyOS Support | Remarks |
| ---- | ----------- | ---- | -------- | -------- | ------------------ | ---- |
| save | 保存图片/视频 | function | no | iOS/Android | partially | 由于原库版本升级，该方法已弃用，可用saveAsset接口代替。<br />Image support format: png/jpg/jpeg/heif/bmp/gif/webp/svg/heic<br />Video support formats：mp4/mov |
| saveAsset | 保存图片/视频 | function | no | iOS/Android | partially | Image support format: png/jpg/jpeg/heif/bmp/gif/webp/svg/heic<br />Video support formats：mp4/mov |
| saveToCameraRoll | 保存图片/视频 | function | no | iOS/Android | partially | 由于原库版本升级，该方法已弃用，调用会弹出警告，可用saveAsset接口代替。<br />Image support format: png/jpg/jpeg/heif/bmp/gif/webp/svg/heic<br />Video support formats：mp4/mov |
| getPhotos | 查找图片/视频 | function | no | iOS/Android | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| getAlbums | 查找相册 | function | no | iOS/Android | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| deletePhotos | 删除图片/视频 | function | no | iOS/Android | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| iosGetImageDataById | 获取图片数据 | function | no | iOS | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |
| getPhotoThumbnail | 获取缩略图 | function | no | iOS | no | 由于 HarmonyOS 安全策略要求，该接口需要使用 ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.WRITE_IMAGEVIDEO 权限，需应用方自行申请后，才可以正常使用 |

## APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] deletePhotos删除图片/视频，未实现 HarmonyOS 化: [issue#5](https://github.com/react-native-oh-library/react-native-cameraroll/issues/5)
- [ ] harmonyRefreshGallerySelection，HarmonyOS 暂无对应图片列表刷新的接口：[issue#8](https://github.com/react-native-oh-library/react-native-cameraroll/issues/8)
- [ ] 部分接口由于Harmony OS安全策略调整无法使用: [issue#25](https://github.com/react-native-oh-library/react-native-cameraroll/issues/25)
- [ ] saveAsset接口未完全支持: [issue#26](https://github.com/react-native-oh-library/react-native-cameraroll/issues/26)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-cameraroll/react-native-cameraroll/blob/master/LICENCE).

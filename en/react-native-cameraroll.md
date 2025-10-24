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

| Version                        | Package Name                                  | Repository                                                   | Release                                                      |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 7.8.3-0.1.5@deprecated | @react-native-oh-tpl/camera-roll | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-cameraroll) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-cameraroll/releases) |
| >= 7.8.4                        | @react-native-ohos/camera-roll       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-cameraroll) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-cameraroll/releases) |

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-ohos/react-native-cameraroll Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-cameraroll/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

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

Version >= @react-native-ohos/camera-roll@7.8.4 now supports Autolink without requiring manual configuration.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

Currently, Version <= @react-native-oh-tpl/camera-roll@7.8.3-0.1.5@deprecated does not support AutoLink. Therefore, you need to manually configure the linking.

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

### 3.Introducing CameraRollPackage to ArkTS

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

### 4.Running

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

Check the release version information in the release address of the third-party library: [@react-native-ohos/camera-roll Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-cameraroll/releases)

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

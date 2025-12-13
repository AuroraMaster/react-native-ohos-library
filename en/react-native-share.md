> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-share</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-share/react-native-share">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-share/react-native-share/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-share/react-native-share)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=10.2.1-0.0.6@deprecated | [@react-native-oh-tpl/react-native-share Releases(deprecated)](https://github.com/react-native-oh-library/react-native-share/releases) | 0.72       |
| 10.2.2            | [@react-native-ohos/react-native-share Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-share/releases)   | 0.72       |
| 12.1.1             | [@react-native-ohos/react-native-share Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-share/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and enter the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-share
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-share
```

<!-- tabs:end -->

进入项目的 HarmonyOS 工程 harmony，打开 `entry/src/main/module.json5`，在 module 中添加: querySchemes 字段，表示允许当前应用进行跳转查询的 URI schemes，只允许 entry 类型模块配置，最多 50 个。例如如需要查询是否可以跳转微博，可以添加

```diff

   "querySchemes": [
      "sinaweibo"  //三方APP的所支持的scheme，sinaweibo是测试hap的scheme
    ]

```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { Button } from "react-native";
import RNShare, { ShareSheet } from "react-native-share";

function App() {
  return (
    <ShareSheet style={{ padding: 20 }} visible onCancel={() => {}}>
      <Button
        title="share"
        onPress={() => {
          RNShare.open({
            title: "share title",
            subject: "Share Summary",
            url: "https://www.baidu.com/",
          })
            .then((res) => {})
            .catch((err) => {});
        }}
      ></Button>
    </ShareSheet>
  );
}

export default App;
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~12.1.1                               |  No                   |  0.77                |
| ~10.2.2                              |  Yes                  |  0.72                |
| <= 10.2.1-0.0.6@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

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
    "@react-native-ohos/react-native-share": "file:../../node_modules/@react-native-ohos/react-native-share/harmony/react_native_share.har"
  }

```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Introducing RNSharePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {RNSharePackage} from '@react-native-ohos/react-native-share/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSharePackage(ctx)
  ];
}
```

### 4. Configure CMakeLists and Import RNSharePackage

> If you are using version <=10.2.1-0.0.6, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-share/src/main/cpp" ./react_native_share)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_share)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
+ #include "RNSharePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<RNSharePackage>(ctx)
}
```
</details>

## Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified successfully in the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Overlay**:分享面板弹窗组件

| Name     | Description | Type            | Required | Platform    | HarmonyOS Support |
| -------- | ----------- | --------------- | -------- | ----------- | ----------------- |
| visible  | 是否显示    | boolean         | no       | iOS,Android | yes               |
| children | JSX element | React.ReactNode | no       | iOS,Android | yes               |

**Button**: 分享按钮

| Name        | Description | Type                                                                  | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | --------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| onPress     | 是否显示    | boolean                                                               | no       | iOS,Android | yes               |
| iconSrc     | icon 属性   | [ImageSourcePropType](https://reactnative.dev/docs/image#imagesource) | no       | iOS,Android | yes               |
| buttonStyle | button 属性 | [ ViewStyle ](https://reactnative.dev/docs/view#props)                | no       | iOS,Android | yes               |
| textStyle   | text 属性   | [TextStyle](https://reactnative.dev/docs/text#props)                  | no       | iOS,Android | yes               |
| children    | JSX element | React.ReactNode                                                       | no       | iOS,Android | yes               |

**ShareSheet**: 分享面板组件

| Name         | Description                  | Type                                                   | Required | Platform    | HarmonyOS Support |
| ------------ | ---------------------------- | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| visible      | 是否显示                     | boolean                                                | no       | iOS,Android | yes               |
| onCancel     | 关闭面板的回调函数           | function                                               | no       | iOS,Android | yes               |
| style        | 分享面板中 Sheet 的 CSS 属性 | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| overlayStyle | 分享面板 CSS 属性            | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children     | JSX element                  | React.ReactNode                                        | no       | iOS,Android | yes               |

**Sheet**: 分享面板组件的子组件，ShareSheet 包含 Sheet

| Name     | Description | Type            | Required | Platform    | HarmonyOS Support |
| -------- | ----------- | --------------- | -------- | ----------- | ----------------- |
| visible  | 是否显示    | boolean         | no       | iOS,Android | yes               |
| children | JSX element | React.ReactNode | no       | iOS,Android | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                                             | Description               | Type    | Required | Platform    | HarmonyOS Support |
| -------------------------------------------------------------------------------- | ------------------------- | ------- | -------- | ----------- | ----------------- |
| Social                                                                           | 支持分享的三方 APP 名称   | object  | yes      | iOS,Android | partially         |
| open: (options: ShareOptions) => Promise<ShareOpenResult\>                       | 系统分享                  | fuction | yes      | iOS,Android | yes               |
| shareSingle: (options: ShareSingleOptions) => Promise<ShareSingleResult\>        | 三方分 APP 分享           | fuction | yes      | iOS,Android | partially         |
| isPackageInstalled: (packagename: string) => Promise <IsPackageInstalledResult\> | 三方 APP 是否已在本机安装 | fuction | yes      | iOS,Android | no                |

**ShareOptions** : 系统分享参数

| Name                  | Description                                                                                                                                              | Type                       | Required | Platform    | HarmonyOS Support |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- | -------- | ----------- | ----------------- |
| type                  | 分享路径资源类型 Mime Type                                                                                                                                | string                     | no       | iOS,Android | yes               |
| urls                  | 分享多个路径                                                                                                                                             | string[]                   | no       | iOS,Android | yes               |
| url                   | 分享路径                                                                                                                                                 | string[]                   | no       | iOS,Android | yes               |
| filename              | 分享路径文件名                                                                                                                                           | string                     | no       | iOS,Android | yes               |
| filenames             | 分享多个路径的文件名（不带后缀，如 123，要与 urls 对应）                                                                                                 | Array<string>              | no       | iOS,Android | yes               |
| message               | 分享短信消息文本                                                                                                                                         | string                     | no       | iOS,Android | partially               |
| title                 | 分享标题                                                                                                                                                 | string                     | no       | iOS,Android | partially               |
| subject               | 分享内容摘要                                                                                                                                             | string                     | no       | iOS,Android | partially               |
| email                 | 收件人邮箱地址                                                                                                                                           | string                     | no       | iOS,Android | no                |
| recipient             | 接收短信消息的号码                                                                                                                                       | string                     | no       | iOS,Android | no               |
| excludedActivityTypes | 系统分享面板操作区不应显示的能力列表(harmonyOS 中传参例如['0','1']，对应解释为: 0:复制到剪切板,1:保存到媒体库,2:保存到文件管理器 ,3:打印,4:保存到中转站) | ActivityType[] \| string[] | no       | iOS,Android | partially         |
| failOnCancel          | 分享失败的是否抛出异                                                                                                                                     | boolean                    | no       | iOS,Android | yes               |
| showAppsToView        | 是否显示可以预览分享文件的 APP                                                                                                                           | boolean                    | no       | Android     | no                |
| saveToFiles           | 是否保存分享的路径文件到本地                                                                                                                             | boolean                    | no       | iOS,Android | yes               |
| activityItemSources   | 系统分享面板中自定义分享数据                                                                                                                             | ActivityItemSource[]       | no       | iOS         | no                |
| isNewTask             | 是否开启 Activity 的启动模式 FLAG_ACTIVITY_NEW_TASK                                                                                                      | boolean                    | no       | Android     | no                |

**ShareSingleOptions** : 三方 APP 分享参数

| Name                  | Description                                                                  | Type     | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------------------- | -------- | -------- | ----------- |-------------------|
| social                | 分享的三方 APP 名称                                                          | string   | yes      | iOS,Android | partially         |
| appId                 | 三方 APP 上架市场的 appid(social 为 instagramstories,facebookstories 时必传) | string   | no       | iOS,Android | no                |
| type                  | 分享路径资源类型 Mime Type                                                    | string   | no       | iOS,Android | no              |
| urls                  | 分享多个路径                                                                 | string[] | no       | iOS,Android | yes               |
| url                   | 分享路径                                                                     | string[] | no       | iOS,Android | yes               |
| filename              | 分享路径文件名（不带后缀，如 123）                                           | string   | no       | iOS,Android | no                |
| message               | 分享短信消息文本                                                             | string   | no       | iOS,Android | yes               |
| title                 | 分享标题                                                                     | string   | no       | iOS,Android | no                |
| subject               | 分享内容摘要                                                                 | string   | no       | iOS,Android | yes               |
| email                 | 收件人邮箱地址                                                               | string   | no       | iOS,Android | yes               |
| recipient             | 接收短信消息的号码                                                           | string   | no       | iOS,Android | yes               |
| forceDialog           | 是否开启三方分享对话框                                                       | boolean  | no       | Android     | no                |
| backgroundImage       | 背景图像（social 为 instagramstories,facebookstories 传参）                  | string   | no       | iOS,Android | no                |
| stickerImage          | 贴纸图像（social 为 instagramstories,facebookstories 传参）                  | string   | no       | iOS,Android | no                |
| backgroundBottomColor | 背景底部颜色（social 为 instagramstories,facebookstories 传参）              | string   | no       | iOS,Android | no                |
| attributionURL        | 属性路径（social 为 instagramstories,facebookstories 传参）                  | string   | no       | iOS,Android | no                |
| backgroundVideo       | 背景视频（social 为 instagramstories,facebookstories 传参）                  | string   | no       | iOS,Android | no                |

**Social**: 可支持的三方 APP 种类

| Name              | Description      | Type   | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------- | ------ | -------- | ----------- |-------------------|
| FACEBOOK          | facebook         | string | yes      | iOS,Android | no                |
| FACEBOOK_STORIES  | facebookstories  | string | yes      | iOS,Android | no                |
| PAGESMANAGER      | pagesmanager     | string | yes      | iOS,Android | no                |
| TWITTER           | twitter          | string | yes      | iOS,Android | no                |
| WHATSAPP          | whatsapp         | string | yes      | iOS,Android | no                |
| WHATSAPPBUSINESS  | whatsappbusiness | string | yes      | iOS,Android | no                |
| INSTAGRAM         | instagram        | string | yes      | iOS,Android | no                |
| INSTAGRAM_STORIES | instagramstories | string | yes      | iOS,Android | no                |
| GOOGLEPLUS        | googleplus       | string | yes      | iOS,Android | no                |
| EMAIL             | email            | string | yes      | iOS,Android | yes               |
| PINTEREST         | pinterest        | string | yes      | iOS,Android | no                |
| LINKEDIN          | linkedin         | string | yes      | iOS,Android | no                |
| SMS               | sms              | string | yes      | iOS,Android | yes               |
| TELEGRAM          | telegram         | string | yes      | iOS,Android | no                |
| SNAPCHAT          | snapchat         | string | yes      | iOS,Android | no                |
| MESSENGER         | messenger        | string | yes      | iOS,Android | no                |
| VIBER             | viber            | string | yes      | iOS,Android | no                |
| DISCORD           | discord          | string | yes      | iOS,Android | no                |

**ShareAsset** : 分享图片、视频数据枚举

| Name                      | Description                                                 | Type | Required | Platform    | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------- | ---- | -------- | ----------- | ----------------- |
| BackgroundImage           | social 为 instagramstories,facebookstories 时分享的图片     | enum | no       | no,Android  | no                |
| BackgroundVideo           | social 为 instagramstories,facebookstories 时分享的视频     | enum | no       | no,Android  | no                |
| StickerImage              | social 为 instagramstories,facebookstories 时分享的贴纸图   | enum | no       | no,Android  | no                |
| BackgroundAndStickerImage | social 为 instagramstories,facebookstories 时分享的背景贴纸 | enum | no       | iOS,Android | no                |

**ActivityType**: 系统分享面板上支持的分享操作

| Name         | Description                                                                                                                                                                                                                                                         | Type   | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| ActivityType | default \| addToReadingList \| airDrop \| assignToContact \| copyToPasteBoard \| mail \| message \| openInIBooks \| postToFacebook \| postToFlickr \| postToTencentWeibo \| postToTwitter \| postToVimeo \| postToWeibo \| print \| saveToCameraRoll \| markupAsPDF | string | no       | iOS,Android | no                |

**ShareSingleResult**: 调用三方分享接口返回的数据类型

| Name    | Description | Type    | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------- | -------- | ----------- | ----------------- |
| message | 返回的消息  | string  | yes      | iOS,Android | yes               |
| success | 是否成功    | boolean | yes      | iOS,Android | yes               |

**ShareOpenResult**: 调用系统分享接口返回的数据类型

| Name    | Description | Type    | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------- | -------- | ----------- | ----------------- |
| message | 返回的消息  | string  | yes      | iOS,Android | yes               |
| success | 是否成功    | boolean | yes      | iOS,Android | yes               |

**IsPackageInstalledResult**: 调用是否安装三方应用接口返回的数据类型

| Name        | Description         | Type    | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------- | ------- | -------- | ----------- |-------------------|
| message     | 返回的消息          | string  | yes      | iOS,Android | no                |
| isInstalled | 三方 APP 是否已安装 | boolean | yes      | iOS,Android | no                |

**ActivityItem**: 系统面板分享类型

| Name    | Description              | Type    | Required | Platform | HarmonyOS Support |
| ------- | ------------------------ | ------- | -------- | -------- | ----------------- |
| type    | 活动面板类型 text \| url | string  | yes      | iOS      | no                |
| content | 内容                     | boolean | yes      | iOS      | no                |

**LinkMetadata**: 系统分享中自定义分享操作的元数据

| Name           | Description                    | Type    | Required | Platform | HarmonyOS Support |
| -------------- | ------------------------------ | ------- | -------- | -------- | ----------------- |
| originalUrl    | 元数据请求的原始 URL           | string  | no       | iOS      | no                |
| url            | 元数据的 URL                   | boolean | no       | iOS      | no                |
| title          | URL 代表的标题                 | boolean | no       | iOS      | no                |
| icon           | URL 代表的 icon                | boolean | no       | iOS      | no                |
| image          | URL 的代表性图像数据           | boolean | no       | iOS      | no                |
| remoteVideoUrl | URL 的代表视频相对应的远程 URL | boolean | no       | iOS      | no                |
| video          | URL 的代表视频数据             | boolean | no       | iOS      | no                |

**ActivityItemSource**: 系统分享中自定义分享数据

| Name               | Description            | Type         | Required | Platform | HarmonyOS Support |
| ------------------ | ---------------------- | ------------ | -------- | -------- | ----------------- |
| placeholderItem    | 分享数据的占位显示数据 | ActivityItem | yes      | iOS      | no                |
| item               | 分享操作项             | ActivityItem | yes      | iOS      | no                |
| subject            | 分享内容               | string       | no       | iOS      | no                |
| dataTypeIdentifier | 数据类型标识符         | string       | no       | iOS      | no                |
| thumbnailImage     | 分享数据的缩略图       | string       | no       | iOS      | no                |
| linkMetadata       | 分享的数据             | LinkMetadata | no       | iOS      | no                |

## Known Issues

- [ ] 无法分享三方 APP 问题: [issue#1](https://github.com/react-native-oh-library/react-native-share/issues/1)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-share/react-native-share/blob/main/LICENSE).

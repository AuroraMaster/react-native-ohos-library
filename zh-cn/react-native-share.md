> 模板版本：v0.2.2

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

 [!TIP] [Github 地址](https://github.com/react-native-share/react-native-share)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <=10.2.1-0.0.6@deprecated | [@react-native-oh-tpl/react-native-share Releases(deprecated)](https://github.com/react-native-oh-library/react-native-share/releases) | 0.72       |
| 10.2.2            | [@react-native-ohos/react-native-share Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-share/releases)   | 0.72       |
| 12.1.1             | [@react-native-ohos/react-native-share Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-share/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

进入项目的 HarmonyOS 工程 harmony，打开 `entry/src/main/module.json5`，在module中添加：querySchemes字段，表示允许当前应用进行跳转查询的URI schemes，只允许entry类型模块配置，最多50个。例如如需要查询是否可以跳转微博，可以添加

```diff

   "querySchemes": [
      "sinaweibo"  //三方APP的所支持的scheme，sinaweibo是测试hap的scheme
    ]
 
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js

    import React from 'react';
    import { Button } from 'react-native';
    import RNShare,{ShareSheet} from 'react-native-share';

    function App() {
    return (
        <ShareSheet style={{padding:20}} visible onCancel={()=>{}}>
            <Button title='分享' onPress={()=>{
                RNShare.open({
                title:'分享标题',
                subject:'分享摘要',
                url:'https://www.baidu.com/'
                }).then((res) => {
                
                }).catch((err) => {
                })
            }}></Button>
        </ShareSheet>
    );
    }

    export default App;

```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~12.1.1                               |  No              |  0.77     |
| ~10.2.2                               |  Yes             |  0.72     |
| <= 10.2.1-0.0.6@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-ohos/react-native-share": "file:../../node_modules/@react-native-ohos/react-native-share/harmony/react_native_share.har"
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

### 3.配置CMakeLists和引入RNSharePackage

>[!TIP] V12.1.0及以上需要配置CMakeLists和引入RNSharePackage。

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

# (VM) Define a variable and assign it to the current module's cpp directory
set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

# Add the Header File directory, including cpp, cpp/include, and tell cmake to find the Header Files introduced by the code here
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-share/src/main/cpp" ./share)

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp") # this line is needed by codegen v1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC rnoh_share)

```

打开`entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "RNSharePackage.h"
using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx)
{
    return {
+        std::make_shared<RNSharePackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNSharePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import {RNSharePackage} from '@react-native-ohos/react-native-share/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSharePackage(ctx)
  ];
}
```
</details>

## 运行

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

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

 **Overlay**:分享面板弹窗组件

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  visible  | 是否显示    | boolean   | no | iOS,Android      | yes |
|  children  |  JSX element   | React.ReactNode   | no | iOS,Android      | yes |

**Button**：分享按钮

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  onPress  | 是否显示    | boolean   | no | iOS,Android      | yes |
|  iconSrc  | icon属性    | [ImageSourcePropType](https://reactnative.dev/docs/image#imagesource)   | no | iOS,Android      | yes |
|  buttonStyle  | button属性    | [ ViewStyle ](https://reactnative.dev/docs/view#props)   | no | iOS,Android      | yes |
|  textStyle  | text属性    | [TextStyle](https://reactnative.dev/docs/text#props)   | no | iOS,Android      | yes |
|  children  | JSX element   |  React.ReactNode   | no | iOS,Android      | yes |

**ShareSheet**：分享面板组件

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  visible  | 是否显示    | boolean   | no | iOS,Android      | yes |
|  onCancel  | 关闭面板的回调函数    | function   | no | iOS,Android      | yes |
|  style  | 分享面板中Sheet的CSS属性    | [ ViewStyle ](https://reactnative.dev/docs/view#props)    | no | iOS,Android      | yes |
|  overlayStyle  | 分享面板CSS属性    |  [ ViewStyle ](https://reactnative.dev/docs/view#props)     | no | iOS,Android      | yes |
|  children  | JSX element   | React.ReactNode   | no | iOS,Android      | yes |

**Sheet**：分享面板组件的子组件，ShareSheet包含Sheet

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  visible  | 是否显示    | boolean   | no | iOS,Android      | yes |
|  children  |  JSX element   | React.ReactNode   | no | iOS,Android      | yes |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  Social  | 支持分享的三方APP名称        | object  | yes | iOS,Android      | partially |
|  open: (options: ShareOptions) => Promise<ShareOpenResult\>  | 系统分享         | fuction  | yes | iOS,Android      | yes |
|  shareSingle: (options: ShareSingleOptions) => Promise<ShareSingleResult\>  | 三方分APP分享         | fuction  | yes | iOS,Android      | partially |
|  isPackageInstalled: (packagename: string) => Promise <IsPackageInstalledResult\>  | 三方APP是否已在本机安装        | fuction  | yes | iOS,Android      | no |

**ShareOptions** ：系统分享参数

| Name | Description                                                                                    | Type | Required | Platform | HarmonyOS Support |
| ---- |------------------------------------------------------------------------------------------------| ---- | -------- | -------- |-------------------|
|  type  | 分享路径资源类型Mime Type                                                                              | string   | no | iOS,Android      | yes               |
|  urls  | 分享多个路径                                                                                         | string[]  | no | iOS,Android      | yes               |
|  url  | 分享路径                                                                                           | string[]  | no | iOS,Android      | yes               |
|  filename  | 分享路径文件名                                                                                        | string | no | iOS,Android      | yes               |
|  filenames  | 分享多个路径的文件名（不带后缀，如123，要与urls对应）                                                                 | Array<string>  | no | iOS,Android      | yes               |
|  message  | 分享短信消息文本                                                                                       | string  | no | iOS,Android      | 	partially                |
|  title  | 分享标题                                                                                           | string  | no | iOS,Android      | 	partially               |
|  subject  | 分享内容摘要                                                                                         | string  | no | iOS,Android      | 	partially                |
|  email  | 收件人邮箱地址                                                                                        | string  | no | iOS,Android      | no                |
|  recipient  | 接收短信消息的号码                                                                                      | string  | no | iOS,Android      | no                |
|  excludedActivityTypes  | 系统分享面板操作区不应显示的能力列表(harmonyOS中传参例如['0','1']，对应解释为： 0:复制到剪切板,1:保存到媒体库,2:保存到文件管理器 ,3:打印,4:保存到中转站) | ActivityType[] \| string[]  | no | iOS,Android      | partially         |
|  failOnCancel  | 分享失败的是否抛出异                                                                                     | boolean  | no | iOS,Android      | yes               |
|  showAppsToView  | 是否显示可以预览分享文件的APP                                                                               | boolean  | no | Android      | no                |
|  saveToFiles  | 是否保存分享的路径文件到本地                                                                                 | boolean  | no | iOS,Android       | yes               |
|  activityItemSources  | 系统分享面板中自定义分享数据                                                                                 | ActivityItemSource[]  | no | iOS      | no                |
|  isNewTask  | 是否开启Activity的启动模式FLAG_ACTIVITY_NEW_TASK                                                        | boolean  | no | Android      | no                |

**ShareSingleOptions** ：三方APP分享参数

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- |-------------------|
|   social  |分享的三方APP名称       | string   | yes | iOS,Android      | partially         |
|   appId  |三方APP上架市场的appid(social为instagramstories,facebookstories时必传)       | string   | no | iOS,Android      | no                |
|   type  | 分享路径资源类型Mime Typ        | string   | no | iOS,Android      | no                |
|  urls  | 分享多个路径       | string[]  | no | iOS,Android      | yes               |
|  url  | 分享路径       | string[] | no | iOS,Android      | yes               |
|  filename  | 分享路径文件名（不带后缀，如 123）      | string | no | iOS,Android      | no                |
|  message  | 分享短信消息文本      | string  | no | iOS,Android      | yes               |
|  title  | 分享标题      | string  | no | iOS,Android      | no                |
|  subject  | 分享内容摘要      | string  | no | iOS,Android      | yes               |
|  email  | 收件人邮箱地址      | string  | no | iOS,Android      | yes               |
|  recipient  | 接收短信消息的号码     | string  | no | iOS,Android      | yes               |
|  forceDialog  | 是否开启三方分享对话框     | boolean  | no | Android      | no                |
|  backgroundImage  |  背景图像（social为instagramstories,facebookstories传参）   | string  | no | iOS,Android      | no                |
|  stickerImage  | 贴纸图像（social为instagramstories,facebookstories传参）   | string  | no | iOS,Android      | no                |
|  backgroundBottomColor  | 背景底部颜色（social为instagramstories,facebookstories传参）  | string  | no | iOS,Android       | no                |
|  attributionURL  | 属性路径（social为instagramstories,facebookstories传参）  | string  | no | iOS,Android     | no                |
|  backgroundVideo  | 背景视频（social为instagramstories,facebookstories传参）   | string  | no | iOS,Android     | no                |

**Social**：可支持的三方APP种类

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- |-------------------|
|  FACEBOOK  | facebook | string | yes | iOS,Android      | no                |
| FACEBOOK_STORIES | facebookstories | string | yes | iOS,Android      | no                |
| PAGESMANAGER | pagesmanager  | string  | yes | iOS,Android  | no                |
| TWITTER | twitter | string  | yes | iOS,Android      | no                |
| WHATSAPP | whatsapp | string  | yes | iOS,Android      | no                |
|  WHATSAPPBUSINESS  | whatsappbusiness | string   | yes | iOS,Android      | no                |
| INSTAGRAM | instagram | string    | yes | iOS,Android      | no                |
| INSTAGRAM_STORIES | instagramstories  | string  | yes | iOS,Android      | no                |
| GOOGLEPLUS | googleplus        | string  | yes | iOS,Android      | no                |
| EMAIL | email        | string  | yes | iOS,Android  | yes               |
|  PINTEREST  | pinterest | string   | yes | iOS,Android  | no                |
| LINKEDIN | linkedin | string    | yes | iOS,Android      | no                |
| SMS | sms | string  | yes | iOS,Android      | yes               |
| TELEGRAM | telegram | string  | yes | iOS,Android      | no                |
|  SNAPCHAT  | snapchat | string   | yes | iOS,Android      | no                |
| MESSENGER | messenger  | string  | yes | iOS,Android      | no                |
| VIBER | viber | string  | yes | iOS,Android      | no                |
| DISCORD | discord | string  | yes | iOS,Android   | no                |

**ShareAsset** ：分享图片、视频数据枚举

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  BackgroundImage  | social为instagramstories,facebookstories时分享的图片 | enum | no | no,Android      | no |
| BackgroundVideo | social为instagramstories,facebookstories时分享的视频 | enum | no | no,Android      | no |
| StickerImage | social为instagramstories,facebookstories时分享的贴纸图  | enum  | no | no,Android  | no |
| BackgroundAndStickerImage | social为instagramstories,facebookstories时分享的背景贴纸 | enum  | no | iOS,Android      | no |

**ActivityType**：系统分享面板上支持的分享操作

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  ActivityType  |  default \| addToReadingList \| airDrop \| assignToContact \| copyToPasteBoard \| mail \| message \|  openInIBooks \| postToFacebook \| postToFlickr \|  postToTencentWeibo \| postToTwitter \| postToVimeo \|  postToWeibo \|  print \| saveToCameraRoll \| markupAsPDF | string | no | iOS,Android      | no |


**ShareSingleResult**：调用三方分享接口返回的数据类型

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  message  | 返回的消息 | string | yes | iOS,Android      | yes |
| success | 是否成功 | boolean | yes | iOS,Android      | yes |

**ShareOpenResult**： 调用系统分享接口返回的数据类型

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  message  | 返回的消息 | string | yes | iOS,Android      | yes |
| success | 是否成功 | boolean | yes | iOS,Android      | yes |

**IsPackageInstalledResult**：调用是否安装三方应用接口返回的数据类型

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- |-------------------|
|  message  | 返回的消息 | string | yes | iOS,Android      | no                |
| isInstalled | 三方APP是否已安装 | boolean | yes | iOS,Android      | no                |

**ActivityItem**：系统面板分享类型

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  type  |活动面板类型 text \| url  | string | yes | iOS    | no |
| content | 内容 | boolean | yes | iOS  | no |

**LinkMetadata**：系统分享中自定义分享操作的元数据

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  originalUrl  | 元数据请求的原始URL | string | no | iOS      | no |
| url | 元数据的URL | boolean | no | iOS      | no |
| title | URL代表的标题 | boolean | no | iOS      | no |
| icon | URL代表的icon | boolean | no | iOS      | no |
| image | URL的代表性图像数据 | boolean | no | iOS      | no |
| remoteVideoUrl | URL的代表视频相对应的远程URL | boolean | no | iOS      | no |
| video | URL的代表视频数据 | boolean | no | iOS      | no |

**ActivityItemSource**：系统分享中自定义分享数据

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  placeholderItem  | 分享数据的占位显示数据 | ActivityItem | yes | iOS      | no |
| item | 分享操作项 | ActivityItem | yes | iOS      | no |
| subject | 分享内容 | string | no | iOS      | no |
| dataTypeIdentifier | 数据类型标识符 | string | no | iOS      | no |
| thumbnailImage | 分享数据的缩略图 | string | no | iOS      | no |
| linkMetadata | 分享的数据 | LinkMetadata | no | iOS      | no |


## 遗留问题

- [ ] 无法分享三方APP问题：[issue#1](https://github.com/react-native-oh-library/react-native-share/issues/1)


## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-share/react-native-share/blob/main/LICENSE) ，请自由地享受和参与开源。

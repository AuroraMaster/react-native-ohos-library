> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-create-thumbnail</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/souvik-ghosh/react-native-create-thumbnail">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-create-thumbnail)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| 2.0.0@deprecated | [@react-native-oh-tpl/react-native-create-thumbnail Releases(deprecated)](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases) | 0.72       |
| 2.0.1 | [@react-native-ohos/react-native-create-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/releases)                        | 0.72       |
| 2.1.0 | [@react-native-ohos/react-native-create-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-create-thumbnail
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-create-thumbnail
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, {useState } from 'react';
import {  StyleSheet, Text, Button ,ScrollView,View} from 'react-native';
import { createThumbnail } from 'react-native-create-thumbnail';

// 导出组件
export default function CreateThumbnailDemo() {

  const [text, setText] = useState('');

  const CreateThumbnail = async()=> {
    let obj = await createThumbnail({ 
      url:'https://media.w3.org/2010/05/sintel/trailer.mp4',
      timeStamp: 10000
    });
    setText(JSON.stringify(obj))
  }

  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style = {styles.title}>Math</Text>
      </View>
      <View style = {styles.inputArea}>
        <Text style={styles.baseText}>
          {text}
        </Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={ { flexDirection: 'column'}}>
          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>createThumbnail</Text>
             <Button title='运行' color='#841584' onPress={CreateThumbnail}></Button>
          </View>
    
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    flexDirection: 'column',
    alignItems: 'center',
    backgroundColor: '#F1F3F5',
  }, 
  baseText: {
    fontWeight: 'bold',
    textAlign:'center',
    fontSize:16
  },

  titleArea:{
    width:'90%',
    height:'8%',
    alignItems:'center',
    flexDirection:'row',
  },

  title: {
    width:'90%',
    color:'#000000',
    textAlign:'left',
    fontSize: 30,
  },

  scrollView: {
    width:'90%',
    marginHorizontal: 20,
  },

  inputArea: {
    width:'90%',
    height:'30%',
    borderWidth:2,
    borderColor:'#000000',
    marginTop:8,
    justifyContent:'center',
    alignItems:'center',
  },
  baseArea: {
    width:'100%',
    height:60,
    borderRadius:4,
    borderColor:'#000000',
    marginTop:8,
    backgroundColor:'#FFFFFF',
    flexDirection: 'row',
    alignItems:'center',
    paddingLeft:8,
    paddingRight:8
  }
});
```

## Link

Version >= @react-native-ohos/react-native-create-thumbnail@2.0.1，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

- V2.0.0

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-create-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-create-thumbnail/harmony/createThumbnail.har"
  }
```

- V2.0.2

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-create-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-create-thumbnail/harmony/createThumbnail.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

- V2.0.0

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-create-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-create-thumbnail/harmony/createThumbnail"
  }
```

- V2.0.2

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-create-thumbnail": "file:../../node_modules/@react-native-ohos/react-native-create-thumbnail/harmony/createThumbnail"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 3.配置 CMakeLists 和引入 CreateThumbnailPackage

> [!TIP] 若使用的是 2.0.0 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-create-thumbnail/src/main/cpp" ./create-thumbnail)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_create_thumbnail)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CreateThumbnailPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<CreateThumbnailPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 CreateThumbnailPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { CreateThumbnailPackage } from '@react-native-ohos/react-native-create-thumbnail/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CreateThumbnailPackage(ctx)
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| 2.0.0@deprecated | [@react-native-oh-tpl/react-native-create-thumbnail Releases(deprecated)](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases) | 0.72       |
| 2.0.1 | [@react-native-ohos/react-native-create-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/releases)                        | 0.72       |
| 2.1.0 | [@react-native-ohos/react-native-create-thumbnail Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/releases)                        | 0.77       |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **createThumbnail**
| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
|  createThumbnail    | thumbnail generator with storage/cache management and support for both local and remote videos  | function | NO | yes |

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  url | Path to video file (local or remote)   |    String    | yes  |   Android/ios    |    yes    |
|  timeStamp | Thumbnail timestamp (in milliseconds)   |    Number     | NO  |   Android/ios    |    yes    |
|  format | Thumbnail format, can be one of: jpeg, or png   |    String      | NO  |   Android/ios    |    yes    |
|  dirSize | Maximum size of the cache directory (in megabytes). When this directory is full, the previously generated thumbnails will be deleted to clear about half of it's size.   |    Number       | NO  |   Android/ios    |    yes    |
|  headers | Headers to load the video with. e.g. { Authorization: 'someAuthToken' }   |    Object      | NO  |   Android/ios    |    yes    |
|  cacheName | Cache name for this thumbnail to avoid duplicate generation. If specified, and a thumbnail already exists with the same cache name, it will be returned instead of generating a new one.   |    String     | NO  |   Android/ios    |    yes    |
| maxWidth<sup>2.0.2+</sup> | Max thumbnail width in px. | Number | NO | Android/ios | yes |
| maxHeight<sup>2.0.2+</sup> | Max thumbnail height in px. | Number | NO | Android/ios | yes |
| timeToleranceMs<sup>2.0.2+</sup> | Time tolerance in ms for the system to pick the best matching video frame. | Number | NO | ios | NO |
| onlySyncedFrames<sup>2.0.2+</sup> | Specify how Android target frames. Use true to retrieve a sync frame that has a timestamp closest to the specified one. Use false to retrieve a frame that may or may not be a sync frame but is closest to the specified timestamp. | Boolean | NO | Android | yes |
## 返回值

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  path | Path to generated thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  size | Size (in bytes) of thumbnail   |    Number     | NO  |   Android/ios    |    yes    |
|  mime | Mimetype of thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  width | Thumbnail width   |    Number     | NO  |   Android/ios    |    yes    |
|  height | Thumbnail height   |    Number     | NO  |   Android/ios    |    yes    |

## 遗留问题

- [ ] timeToleranceMs 属性不支持，因为在 HarmonyOS 中没有提供对应的属性 [issues#1](https://gitcode.com/openharmony-sig/rntpc_react-native-create-thumbnail/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE) ，请自由地享受和参与开源。

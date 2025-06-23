> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-blob-util</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/RonRadtke/react-native-blob-util">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/RonRadtke/react-native-blob-util/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-blob-util)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-blob-util Releases](https://github.com/react-native-oh-library/react-native-blob-util/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-blob-util@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-blob-util@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import {
  ScrollView,
  StyleSheet,
  Button,
  View,
  Text,
  NativeEventEmitter,
} from "react-native";
import ReactNativeBlobUtil from "react-native-blob-util";

export default function BlobUtilDemo() {
  const [result, setResult] = useState < string | null > (null);
  const [mkdirParam, setMkdirParam] = useState("");

  const createFile = async () => {
    await ReactNativeBlobUtil.fs.createFile(
      result + "/text.txt",
      "123456",
      "utf8"
    );
  };

  const ls = async () => {
    await ReactNativeBlobUtil.fs.ls(ReactNativeBlobUtil.fs.dirs.CacheDir);
  };

  const createFileASCII = async () => {
    await ReactNativeBlobUtil.fs.createFile(
      result + "/text.txt",
      [102, 111, 111],
      "ascii"
    );
  };

  const unlink = () => {
    ReactNativeBlobUtil.fs.unlink(result + "/text.txt");
  };

  const getConstants = () => {
    let obj = ReactNativeBlobUtil.fs.dirs.CacheDir;
    setResult(obj);
  };

  const writeFile = () => {
    ReactNativeBlobUtil.fs.writeFile(
      result + "/text.txt",
      "Try to write str",
      "utf8"
    );
  };

  const writeStream = () => {
    ReactNativeBlobUtil.fs.writeStream(result + "/text.txt", "utf8", false);
  };

  const writeArrayChunk = () => {
    ReactNativeBlobUtil.fs
      .writeStream(result + "/text.txt", "ascii", false)
      .then((reactNativeBlobUtilWriteStream:any) => {
        reactNativeBlobUtilWriteStream.write([101, 32, 97]);
        reactNativeBlobUtilWriteStream.close();
      });
  };

  const writeChunk = () => {
    ReactNativeBlobUtil.fs
      .writeStream(result + "/text.txt", "utf8", false)
      .then((reactNativeBlobUtilWriteStream:any) => {
        reactNativeBlobUtilWriteStream.write("Zm9vIChXcml0ZSBCYXNlNjQpMQ==");
        reactNativeBlobUtilWriteStream.close();
      });
  };

  const closeStream = () => {
    ReactNativeBlobUtil.fs
      .writeStream(result + "/text.txt", "utf8", false)
      .then((reactNativeBlobUtilWriteStream:any) => {
        setTimeout(() => {
          reactNativeBlobUtilWriteStream.close();
        }, 1000);
      });
  };
  const readStream = () => {
    ReactNativeBlobUtil.fs.readStream(result + "/text.txt", "utf8", 4000, 200);
  };

  const mkdir = () => {
    ReactNativeBlobUtil.fs.mkdir(
      ReactNativeBlobUtil.fs.dirs.DocumentDir + "/" + mkdirParam
    );
  };

  const stat = () => {
    ReactNativeBlobUtil.fs.stat(result + "/text.txt");
  };

  const copyFileToCache = () => {
    ReactNativeBlobUtil.fs.cp(result + "/text.txt", result + "/text1.txt");
  };

  const writeFileArray = () => {
    ReactNativeBlobUtil.fs.writeFile(
      result + "/text.txt",
      [102, 111, 111],
      "ascii"
    );
  };

  const exists = () => {
    ReactNativeBlobUtil.fs.exists(result + "/text.txt");
  };

  const lstat = () => {
    ReactNativeBlobUtil.fs.lstat(result + "/text.txt");
  };

  const mv = () => {
    ReactNativeBlobUtil.fs.mv(result + "/text.txt", result + "/text1.txt");
  };

  const hash = () => {
    ReactNativeBlobUtil.fs.hash(result + "/text.txt", "md5");
  };

  const readFile = () => {
    ReactNativeBlobUtil.fs.readFile(result + "/text.txt", "utf8", 4000);
  };

  const slice = () => {
    ReactNativeBlobUtil.fs.slice(
      result + "/text.txt",
      result + "/text1.txt",
      2,
      5
    );
  };

  const df = () => {
    ReactNativeBlobUtil.fs.df();
  };

  const addListener = () => {
    let obj = "addListener是空实现";
    setResult(obj);
  };

  const removeListeners = () => {
    let obj = "removeListeners是空实现";
    setResult(obj);
  };

  const emitExpiredEvent = () => {
    let obj = "emitExpiredEvent是空实现,三方库没有调用";
    setResult(obj);
  };

  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style={styles.title}>BlobUtil</Text>
      </View>
      <View style={styles.inputArea}>
        <Text style={styles.baseText} ellipsizeMode="tail" numberOfLines={2}>{result}</Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={{ flexDirection: "column" }}>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.getConstants()</Text>
            <Button
              title="运行"
              color="#841584"
              onPress={getConstants}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.createFile()</Text>
            <Button title="运行" color="#841584" onPress={createFile}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.unlink()</Text>
            <Button title="运行" color="#841584" onPress={unlink}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.copyFileToCache()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={copyFileToCache}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.writeFile()</Text>
            <Button title="运行" color="#841584" onPress={writeFile}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.stat()</Text>
            <Button title="运行" color="#841584" onPress={stat}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.mkdir()</Text>
            <Button title="运行" color="#841584" onPress={mkdir}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.writeStream()</Text>
            <Button title="运行" color="#841584" onPress={writeStream}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.ls()</Text>
            <Button title="运行" color="#841584" onPress={ls}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.createFileASCII()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={createFileASCII}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.writeFileArray()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={writeFileArray}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.exists()</Text>
            <Button title="运行" color="#841584" onPress={exists}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.lstat()</Text>
            <Button title="运行" color="#841584" onPress={lstat}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.hash()</Text>
            <Button title="运行" color="#841584" onPress={hash}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.readFile()</Text>
            <Button title="运行" color="#841584" onPress={readFile}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.slice()</Text>
            <Button title="运行" color="#841584" onPress={slice}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.df()</Text>
            <Button title="运行" color="#841584" onPress={df}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.closeStream()</Text>
            <Button title="运行" color="#841584" onPress={closeStream}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.writeArrayChunk()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={writeArrayChunk}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.writeChunk()</Text>
            <Button title="运行" color="#841584" onPress={writeChunk}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.readStream()</Text>
            <Button title="运行" color="#841584" onPress={readStream}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.mv()</Text>
            <Button title="运行" color="#841584" onPress={mv}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>addListener()</Text>
            <Button title="运行" color="#841584" onPress={addListener}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>removeListeners()</Text>
            <Button
              title="运行"
              color="#841584"
              onPress={removeListeners}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>emitExpiredEvent()</Text>
            <Button
              title="运行"
              color="#841584"
              onPress={emitExpiredEvent}
            ></Button>
          </View>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: "100%",
    height: "100%",
    flexDirection: "column",
    alignItems: "center",
    backgroundColor: "#F1F3F5",
  },
  baseText: {
    width: "100%",
    height: "100%",
    fontWeight: "bold",
    textAlign: "center",
    fontSize: 16,
  },
  titleArea: {
    width: "90%",
    height: "8%",
    alignItems: "center",
    flexDirection: "row",
  },
  title: {
    width: "90%",
    color: "#000000",
    textAlign: "left",
    fontSize: 30,
  },
  scrollView: {
    width: "90%",
    marginHorizontal: 10,
  },

  inputArea: {
    width: "90%",
    height: "10%",
    borderWidth: 2,
    borderColor: "#000000",
    marginTop: 8,
    justifyContent: "center",
    alignItems: "center",
  },
  baseArea: {
    width: "100%",
    height: 60,
    borderRadius: 4,
    borderColor: "#000000",
    marginTop: 6,
    backgroundColor: "#FFFFFF",
    flexDirection: "row",
    alignItems: "center",
    paddingLeft: 8,
    paddingRight: 8,
  },
});
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```
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

```json
"dependencies": {
     "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
     "@react-native-oh-tpl/react-native-blob-util": "file:../../node_modules/@react-native-oh-tpl/react-native-blob-util/harmony/blobUtil.har"
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


### 3.配置 CMakeLists 和引入 BlobUtilPackage

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

# RNOH_BEGIN: rnoh_blob_util
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-blob-util/src/main/cpp" ./blob-util)
# RNOH_END: rnoh_blob_util

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: rnoh_blob_util
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_blob_util)
# RNOH_END: rnoh_blob_util
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "BlobUtilPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<BlobUtilPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 BlobUtilPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {BlobUtilPackage} from '@react-native-oh-tpl/react-native-blob-util/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BlobUtilPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-blob-util Releases](https://github.com/react-native-oh-library/react-native-blob-util/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
#### Fetch API

##### ReactNativeBlobUtil.fetch

| Name    | Description|Type | Required | Platform    | HarmonyOS Support |
| ------- | --------|--- | -------- | ----------- | ----------------- |
| progress | 进度   | Function    | No       | iOS/Android | yes                |
| uploadProgress | 上传进度  | Function        | No       | iOS/Android | yes                |
| cancel | 取消   | Function       | No       | iOS/Android | yes                |



#### Android API

##### ReactNativeBlobUtil.android

|        Name         | Description| Type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :------|----: | :------: | :------: | :---------------: |
|  actionViewIntent   | 动作视图意图| Function  |    No    | Android  |        No         |
|  getContentIntent   | 获取内容意图| Function  |    No    | Android  |        No         |
| addCompleteDownload | 添加完整下载| Function  |    No    | Android  |        No         |

#### File System Access API

##### ReactNativeBlobUtil.fs

|    Name     |            Description  | Type             | Required |  Platform   | HarmonyOS Support |
| :---------: | :---------------------| -----------: | :------: | :---------: | :---------------: |
|    dirs     |                目录 | Function               |    NO    | iOS/Android |        yes        |
| createFile  |              创建文件 | Function             |    NO    | iOS/Android |        yes        |
|  writeFile  |               写文件   | Function            |    NO    | iOS/Android |        yes        |
| writeStream |                写流    | Function            |    NO    | iOS/Android |        yes        |
| appendFile  |              追加文件   | Function           |    NO    | iOS/Android |        yes        |
|  readFile   |              读取文件  | Function            |    NO    | iOS/Android |        yes        |
|    hash     |                哈希   | Function             |    NO    | iOS/Android |        yes        |
| readStream  |                读流    | Function            |    NO    | iOS/Android |        yes        |
|    mkdir    |              创建目录   | Function           |    NO    | iOS/Android |        yes        |
|     ls      |        查看当下的文件和目录| Function        |    NO    | iOS/Android |        yes        |
|     mv      |            移动文件位置  | Function          |    NO    | iOS/Android |        yes        |
|     cp      |              复制文件   | Function           |    NO    | iOS/Android |        yes        |
|   exists    |          检查文件是否存在 | Function         |    NO    | iOS/Android |        yes        |
|    isDir    |             是否是目录  | Function           |    NO    | iOS/Android |        yes        |
|   unlink    |              删除文件   | Function           |    NO    | iOS/Android |        yes        |
|    lstat    |      获取目录下文件的统计数据 | Function     |    NO    | iOS/Android |        yes        |
|    stat     |   类似地获取数据或目录的统计信息| Function   |    NO    | iOS/Android |        yes        |
|  scanFile   |              扫描文件    | Function          |    NO    |   Android   |        no         |
|    asset    |                资产      | Function          |    NO    | iOS/Android |        yes        |
|     df      | 获取设备的可用磁盘空间和总磁盘空间| Function |    NO    | iOS/Android |        yes        |

#### iOS API

#### ReactNativeBlobUtil.ios

| Name            | Description      | Type                      | Required | Platform | HarmonyOS Support |
| --------------- | ----------------------| ---------------- | -------- | -------- | ----------------- |
| previewDocument | 文档查看器--需要系统权限  | Function             | No       | iOS      | yes                |
| openDocument    | 显示与文件交互的选项菜单--需要系统权限| Function | No       | iOS      | yes                |

#### Network Utils

##### ReactNativeBlobUtil.net

| Name          | Description| Type | Required | Platform    | HarmonyOS Support |
| ------------- | ----------- | ---| ----- | ----------- | ----------------- |
| getCookies    | 获取 cookie| Function | No       | iOS/Android | no                |
| removeCookies | 删除 cookie| Function | No       | iOS/Android | no               |

#### Session API

##### ReactNativeBlobUtil.session

| Name    | Description| Type | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | --| ------ | ----------- | ----------------- |
| add | 向此会话添加文件路径   | Function     | No       | iOS/Android | yes                |
| remove | 从此会话中删除会话条目而不删除文件  | Function      | No       | iOS/Android | yes                |
| list | 返回包含此会话中的文件路径的数组   | Function     | No       | iOS/Android | yes                |
| dispose | 删除会话中的所有文件  | Function      | No       | iOS/Android | yes                |

#### MediaStore(Android Media Storage)

##### ReactNativeBlobUtil.MediaCollection

| Name             | Description | Type   | Required | Platform | HarmonyOS Support |
| ---------------- | --------| ------ | -------- | -------- | ----------------- |
| CopyToMediaStore | 复制到媒体存储| Function | No       | Android  | no                |
| createMediaFile  | 创建媒体文件| Function   | No       | Android  | no                |
| writeMediaFile   | 写媒体文件 | Function    | No       | Android  | no                |
| copyToInternal   | 复制到内部 | Function    | No       | Android  | no                |

#### Utils API

| Name   | Description| Type | Required | Platform    | HarmonyOS Support |
| ------ | ----------- | ---| ----- | ----------- | ----------------- |
| wrap   |  使文件路径可以被识别| Function           | No       | iOS/Android | yes                |
| base64 |   使用base64编码解码| Function          | No       | iOS/Android | yes                |
| session |  用于管理缓存文件 | Function          | No       | iOS/Android | yes                |

## 遗留问题
 - [ ] blob-util在使用getCookies、removeCookies	在Android、iOS、Harmony OS 上使用都会报错: [issue#381](https://github.com/RonRadtke/react-native-blob-util/issues/381)
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/RonRadtke/react-native-blob-util/blob/master/LICENSE) ，请自由地享受和参与开源。


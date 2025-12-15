> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-access</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alpha0010/react-native-file-access">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/alpha0010/react-native-file-access/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-file-access)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=3.1.1@deprecated | [@react-native-oh-tpl/react-native-file-access Releases(deprecated)](https://github.com/react-native-oh-library/react-native-file-access/releases) | 0.72       |
| 3.1.2              | [@react-native-ohos/react-native-file-access Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-access/releases)     | 0.72       |
| 3.2.0              | [@react-native-ohos/react-native-file-access Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-access/releases)     | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-file-access
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-file-access
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 以下 demo 中使用的是本地文件。

```js
import React, { useState } from 'react';
import { Button, ScrollView, StyleSheet, Text, View } from 'react-native';
import { Dirs, FileSystem } from 'react-native-file-access';

function FileAccessDemo() {
  const [fileContent, setFileContent] = useState('');
  const [mkdirParam, setMkdirParam] = useState('');
  const [statInfo, setStatInfo] = useState<any>([]);
  const [isExists, setExists] = useState<boolean | string>('');
  const [lsList, setLsList] = useState<any>([]);
  const [totalSize, setTotalSize] = useState<number>();
  const [freeSize, setFreeSize] = useState<number>();
  const [hashValue, setHashValue] = useState<string>();
  const [statDirInfo, setStatDirInfo] = useState<object[]>([]);
  const [readFileChunkInfo, setReadFileChunkInfo] = useState<string>();
  const [concatBeyts, setConcatBeyts] = useState<number>();
  const [dirOrNot, setDirOrNot] = useState<any>('');

  // 将内容写入文件
  const wirteFile = () => {
    FileSystem.writeFile(Dirs.DocumentDir + '/0801.txt', "DDDD", "utf8")
  };

  // 读取文件的内容
  const readFile = () => {
    FileSystem.readFile(Dirs.DocumentDir + "/0801.txt").then((res) => {
      setFileContent(res);
    })
  };

  // 删除文件
  const unlink = () => {
    FileSystem.unlink(Dirs.DocumentDir + '/0801.txt');
  };

  // 创建一个新目录，返回创建目录的路径
  const mkdir = () => {
    FileSystem.mkdir(Dirs.DocumentDir + "/wxwx").then((res) => {
      setMkdirParam(res);
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  // 移动文件
  const mv = () => {
    FileSystem.mv(Dirs.DocumentDir + "/0801.txt", Dirs.DocumentDir + "/text1.txt");
  };

  // 解压一个 zip 档案
  const unzip = () => {
    FileSystem.unzip(Dirs.DocumentDir + "/wxwx.zip", Dirs.DocumentDir);
  };

  // 读取文件元数据
  const stat = () => {
    FileSystem.stat(Dirs.DocumentDir + "/text1.txt").then((res) => {
      setStatInfo(JSON.stringify(res));
    }).catch(err => {
      console.log(err);
    })
  };

  // 检查路径是否存在
  const exists = () => {
    FileSystem.exists(Dirs.DocumentDir + "/text1.txt").then((res) => {
      setExists(res);
    }).catch((error) => {
      console.log(error, 'error');
    });
  };

  // 复制文件
  const cp = async () => {
    await FileSystem.cp(Dirs.DocumentDir + "/text1.txt", Dirs.DocumentDir + "/text4.txt")
  };

  // 对文件内容进行哈希处理
  const hash = () => {
    FileSystem.hash(Dirs.DocumentDir + "/text1.txt", 'SHA-256').then((res) => {
      setHashValue(res);
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  // 检查路径是否是目录
  const isDir = async () => {
    let res = await FileSystem.isDir(Dirs.DocumentDir + '/text1.txt');
    setDirOrNot(res);
  };

  // 列出目录中的文件
  const ls = async () => {
    await FileSystem.ls(Dirs.DocumentDir).then((res) => {
      setLsList(res.join('、'));
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  // 检查设备可用空间
  const df = async () => {
    await FileSystem.df().then(res => {
      setFreeSize(res?.internal_free);
      setTotalSize(res?.internal_total);
    })
  };

  // 读取目录中所有文件的元数据
  const statDir = () => {
    FileSystem.statDir(Dirs.DocumentDir).then(res => {
      setStatDirInfo(res);
    }).catch(err => {
      console.log(err);
    });
  };

  // 读取文件的一大块内容，从位于的字节开始offset，读取length字节
  const readFileChunk = () => {
    FileSystem.readFileChunk(Dirs.DocumentDir + "/text1.txt", 1, 1, 'utf8').then((res) => {
      setReadFileChunkInfo(res);
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  // 将内容附加到文件
  const appendFile = async () => {
    await FileSystem.appendFile(Dirs.DocumentDir + "/text3.txt", "AAAAAA", 'utf8');
  }

  // 将一个文件附加到另一个文件。返回写入的字节数
  const concatFiles = async () => {
    await FileSystem.concatFiles(Dirs.DocumentDir + "/text3.txt", Dirs.DocumentDir + "/text4.txt").then((res) => {
      setConcatBeyts(res)
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  return (
    <ScrollView>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.wirteFile()</Text>
        <Button title="运行" color="#841584" onPress={wirteFile}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.readFile()</Text>
          <Button title="运行" color="#841584" onPress={readFile}></Button>
        </View>
        <Text>读取的文件内容：{fileContent}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.unlink()</Text>
        <Button title="运行" color="#841584" onPress={unlink}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.mkdir()</Text>
          <Button title="运行" color="#841584" onPress={mkdir}></Button>
        </View>
        <Text>新目录路径：{mkdirParam}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.mv()</Text>
        <Button title="运行" color="#841584" onPress={mv}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.stat()</Text>
          <Button title="运行" color="#841584" onPress={stat}></Button>
        </View>
        <Text>文件信息：{statInfo}</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.exists()</Text>
          <Button title="运行" color="#841584" onPress={exists}></Button>
        </View>
        <Text>文件是否存在：{isExists === '' ? '' : isExists ? '存在' : '不存在'}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.cp()</Text>
        <Button title="运行" color="#841584" onPress={cp}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.isDir()</Text>
          <Button title="运行" color="#841584" onPress={isDir}></Button>
        </View>
        <Text>是否是目录：{dirOrNot === '' ? '' : dirOrNot ? '是' : '不是'}</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.ls()</Text>
          <Button title="运行" color="#841584" onPress={ls}></Button>
        </View>
        <Text>目录中的文件：{lsList}</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.df()</Text>
          <Button title="运行" color="#841584" onPress={df}></Button>
        </View>
        <Text>可用空间：{freeSize ? (freeSize / (1000 * 1000 * 1000)).toFixed(2) : ''}GB</Text>
        <Text>总空间：{totalSize ? (totalSize / (1000 * 1000 * 1000)).toFixed(2) : ''}GB</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.hash()</Text>
          <Button title="运行" color="#841584" onPress={hash}></Button>
        </View>
        <Text>哈希值：{hashValue}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.unzip()</Text>
        <Button title="运行" color="#841584" onPress={unzip}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.statDir()</Text>
          <Button title="运行" color="#841584" onPress={statDir}></Button>
        </View>
        <Text>以下为目录下的文件信息：</Text>
        {statDirInfo.map((item, index) => (<Text key={index}>{JSON.stringify(item)}</Text>))}
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.readFileChunk()</Text>
          <Button title="运行" color="#841584" onPress={readFileChunk}></Button>
        </View>
        <Text>读取的部分文件内容：{readFileChunkInfo}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.appendFile()</Text>
        <Button title="运行" color="#841584" onPress={appendFile}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.concatFiles()</Text>
          <Button title="运行" color="#841584" onPress={concatFiles}></Button>
        </View>
        <Text>写入的字节数：{concatBeyts}</Text>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  key: { flex: 1.5, padding: 2 },
  row: { flexDirection: 'row', paddingVertical: 2 },
  value: { flex: 4, padding: 2 },
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
export default FileAccessDemo
```

## 使用 Codegen 


本库已经适配了 Codegen ，在使用前需要主动执行生成三方库桥接代码，详细请参考 [Codegen 文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|------------------|-----------|
| ~3.2.0                               |  No              |  0.77     |
| ~3.1.2                               |  Yes             |  0.72     |
| <=3.1.1@deprecated                   |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

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
     "@react-native-ohos/react-native-file-access": "file:../../node_modules/@react-native-ohos/react-native-file-access/harmony/file_access.har"
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

### 3.配置 CMakeLists 和引入 RNFileAccessPackage

> 若使用的是 <=3.1.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

# (VM) Define a variable and assign it to the current module's cpp directory
set(NATIVERENDER_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})

# Add the Header File directory, including cpp, cpp/include, and tell cmake to find the Header Files introduced by the code here
include_directories(${NATIVERENDER_ROOT_PATH}
                    ${NATIVERENDER_ROOT_PATH}/include)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-file-access/src/main/cpp" ./file_access)
# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp") # this line is needed by codegen v1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC rnoh_file_access)

```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNFileAccessPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx)
{
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+ 		std::make_shared<RNFileAccessPackage>(ctx)
    };
}
```



### 4.在 ArkTs 侧引入 RNFileAccessPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNFileAccessPackage } from '@react-native-ohos/react-native-file-access/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFileAccessPackage(ctx)
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

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### File System Access API

| Name           | Description                                                  | Type     | Platform | Required    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| appendFile     | 向文件追加内容                                               | Function | No       | iOS/Android | Yes               |
| concatFiles    | 将一个文件追加到另一个文件，返回写入的字节数                 | Function | No       | iOS/Android | Yes               |
| cp             | 复制文件                                                     | Function | No       | iOS/Android | Yes               |
| cpAsset        | 复制捆绑的资源文件                                           | Function | No       | iOS/Android | Yes               |
| cpExternal     | 将文件复制到外部控制的位置                                   | Function | No       | iOS/Android | Yes               |
| df             | 检查设备可用空间                                             | Function | No       | iOS/Android | Yes               |
| exists         | 检查路径是否存在                                             | Function | No       | iOS/Android | Yes               |
| fetch          | 将网络请求保存到文件                                         | Function | No       | iOS/Android | Yes               |
| getAppGroupDir | 获取应用组目录（仅限 iOS 和 MacOS）                          | Function | No       | iOS         | No                |
| hash           | 对文件内容进行哈希计算                                       | Function | No       | iOS/Android | Yes               |
| isDir          | 检查路径是否为目录                                           | Function | No       | iOS/Android | Yes               |
| ls             | 列出目录中的文件                                             | Function | No       | iOS/Android | Yes               |
| mkdir          | 创建新目录                                                   | Function | No       | iOS/Android | Yes               |
| mv             | 移动文件                                                     | Function | No       | iOS/Android | Yes               |
| readFile       | 读取文件内容                                                 | Function | No       | iOS/Android | Yes               |
| readFileChunk  | 读取文件的一部分内容，从偏移量字节开始，读取指定长度的字节  | Function | No       | iOS/Android | Yes               |
| stat           | 读取文件元数据                                               | Function | No       | iOS/Android | Yes               |
| statDir        | 读取目录中所有文件的元数据                                   | Function | No       | iOS/Android | Yes               |
| unlink         | 删除文件                                                     | Function | No       | iOS/Android | Yes               |
| unzip          | 解压 ZIP 压缩包                                              | Function | No       | iOS/Android | Yes               |
| writeFile      | 将内容写入文件                                               | Function | No       | iOS/Android | Yes               |

## 遗留问题

- [ ] getAppGroupDir方法（获取应用程序目录权限,仅iOS、Mac iOS）依赖问题，目前Harmony侧未提供支持 [issue#4](https://github.com/react-native-oh-library/react-native-file-access/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/alpha0010/react-native-file-access/blob/master/LICENSE) ，请自由地享受和参与开源。
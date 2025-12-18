> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-turbo-log</code> </h1>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.6.1      | [@react-native-ohos/react-native-turbo-log Releases](https://github.com/react-native-oh-library/react-native-turbo-log/releases) | 0.72       |
| 0.7.0     | [@react-native-ohos/react-native-turbo-log Releases](https://github.com/react-native-oh-library/react-native-turbo-log/releases) | 0.77       |

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-turbo-log)

## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-turbo-log
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-turbo-log
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
### turbo_log example
``` js
import { StyleSheet, Text, View, Image, TouchableOpacity, Alert } from 'react-native';
import TurboLogger, { LogLevel } from "@react-native-ohos/react-native-turbo-log";
import { useState, useEffect } from "react"


export default function ReactNativeTurboLog() {
  useEffect(() => {
    try {
      TurboLogger.configure({
        dailyRolling: false,
        maximumFileSize: 1024 * 1024,
        maximumNumberOfFiles: 2,
      });
      Alert.alert('TurboLogger.configure初始化成功')
    } catch (error) {
      Alert.alert('TurboLogger.configure初始化失败', JSON.stringify(error))
    }
  }, [])

  const [result, setResult] = useState<string>();
  const [iswrite, setIswrite] = useState<boolean>(true);
  const isEmptyDataString = (data: string): boolean => {
    const trimmed = data.trim();
    return trimmed === '[]' || trimmed === '""' || trimmed === '{}';
  };

  return (
    <View style={styles.container}>
      <View><Text>LogToFile的值为{JSON.stringify(iswrite)}</Text></View>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          setIswrite(false)
          TurboLogger.setLogToFile(false)
        }}>
        <Text>setLogToFile属性值为false</Text>
      </TouchableOpacity>
      <View><Text>原库代码逻辑是所有的log方法最后都调用的是write方法，且setLogToFile属性值为true的时候会正常调用生效</Text></View>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          setIswrite(true)
          TurboLogger.setLogToFile(true)
        }}>
        <Text>setLogToFile属性值为true</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.debug(LogLevel.Debug, '写入debug日志成功')
        }}>
        <Text>写入debug日志</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.error(LogLevel.Error, '写入error日志成功')
        }}>
        <Text>写入error日志</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.warn(LogLevel.Warning, '写入warn日志成功')
        }}>
        <Text>写入Warning日志</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.info(LogLevel.Info, '写入info日志成功')
        }}>
        <Text>写入Info日志</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.log(LogLevel.Info, '写入log-info日志成功')
        }}>
        <Text>TurboLogger.log属性</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          const res = await TurboLogger.getLogPaths()
          if (!isEmptyDataString(JSON.stringify(res))) {
            setResult(JSON.stringify(res))
          } else {
            setResult('')
          }
        }}>
        <Text>日志路径获取</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          const res = await TurboLogger.deleteLogs()
          if (res) {
            setResult('')
          }
        }}>
        <Text>删除日志</Text>
      </TouchableOpacity>
      <View><Text>{result}</Text></View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    justifyContent: 'center',
    alignItems: 'center',
    padding: 10,
    margin: 25,
    borderRadius: 5,
    borderWidth: 3,
    marginTop: 50,
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: 'red',
    borderRadius: 5,
  },
});

```
## Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
  ...
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
    "@react-native-ohos/react-native-turbo-log": "file:../../node_modules/@react-native-ohos/react-native-turbo-log/harmony/turbo_log.har"
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


### 3.配置 CMakeLists 和引入 turbo_log

打开 entry/src/main/cpp/CMakeLists.txt，添加：

```diff
include(FetchContent)
# BOOST
set(BOOST_ENABLE_CMAKE On)
FetchContent_Declare(
 Boost
 URL /7277/boost-1.82.0.tar.xz
 OVERRIDE_FIND_PACKAGE)
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)


add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-gesture-handler/src/main/cpp" ./gesture-handler)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-turbo-log/src/main/cpp" ./rnoh-turbo-log)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp") # this line is needed by codegen v1
add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_gesture_handler)
+ target_link_libraries(rnoh_app PUBLIC rnoh_turbo_log)
# RNOH_END: manual_package_linking_2

```

### 4. 在ArkTS侧引入TurboLogPackage

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "TurboLogPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<TurboLogPackage>(ctx),
    };
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

本文档内容基于以下版本验证通过：
1. RNOH：0.72.90; SDK：HarmonyOS NEXT Developer DB3; IDE: DevEco Studio: 5.0.5.220; ROM：NEXT.0.0.105;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;



## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Turbo_log**：一个日志存储获取日志路径删除日志的功能

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| configure | 初始化配置     | function | no       | Android | yes               |
| deleteLogFiles | 删除所有日志     | function | no       | Android | yes               |
| getLogFilePaths | 返回所有日志路径     | function | no       | Android | yes               |
| setLogToFile | 启用或禁用讲日志打印到文件     | function | no       | Android | yes               |
| debug | 封装TurboLogger.debug     | function | no       | Android | yes               |
| error | 封装TurboLogger.error     | function | no       | Android | yes               |
| warn | 封装TurboLogger.warn     | function | no       | Android | yes               |
| info | 封装TurboLogger.info     | function | no       | Android | yes               |
| log | 打印判断的日志     | function | no       | Android | yes               |

## 静态方法

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mattermost/react-native-turbo-log/blob/master/LICENSE) ，请自由地享受和参与开源。

> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-turbo-log</code> </h1>
</p>

Please refer to the Releases page of the third-party library for the matching version information:

| Third-party library version | Release information | Supported RN version |
| --------------------------- | ------------------- | -------------------- |
| 0.6.0                       |                     | 0.72                 |
| 0.6.0                       |                     | 0.77                 |

> [!TIP] [Github 地址](https://github.com/mattermost/react-native-turbo-log)

####  npm

```bash
npm install @@react-native-ohos/react-native-turbo-log
```

#### yarn

```bash
yarn add @@react-native-ohos/react-native-turbo-log
```

<!-- tabs:end -->

The following code demonstrates the basic usage scenarios of this library:

> [!WARNING] The library name imported remains unchanged during usage.
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
## Using Codegen
Version >= @react-native-ohos/react-native-turbo-log@14.0.2, which has been adapted to codegen-lib to generate bridge code.

This library has been adapted to Codegen. Before using it, you need to actively execute the generation of third-party library bridge code. For details, please refer to the Codegen Usage Documentation.

## Link
Version >= @react-native-ohos/react-native-turbo-log@14.0.2, which supports Autolink and no manual configuration is required. Currently, only the 72 framework is supported. Autolink framework guide document: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/en/Autolinking.md
This step is a guide for manually configuring native dependencies.
First, you need to open the HarmonyOS project harmony in the project using DevEco Studio.

### Add overrides field to oh-package.json in the project root directory

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
  ...
}
```

There are currently two methods:

Import via har package (this method will be deprecated after the IDE improves related functions, and it is the preferred method currently);
Link source code directly.

Method 1: Import via har package (recommended)

> [!TIP] The HAR package can be found in the harmony subfolder of the third-party library's installation directory.

Open the entry/oh-package.json5 file and append the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-turbo-log": "file:../../node_modules/@@react-native-ohos/react-native-turbo-log/harmony/turbo_log.har"
  }
```

Click the sync button at the top right corner.

Or run this command in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link the source code directly

> [!TIP] For direct source code linking, refer to [Direct Source Code Linking Instructions](/zh-cn/link-source-code.md)


### 4.Configure CMakeLists and import turbo_log

open entry/src/main/cpp/CMakeLists.txt，add：

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
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
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

### 5.Run

Click the sync button in the upper right corner.

Alternatively, execute the following command in the terminal:


```bash
cd entry
ohpm install
```

Then compile and run the project.

## Constraints and Limitations

### Compatibility Support

The content of this document has been verified based on the following versions：
1. RNOH：0.72.90; SDK：HarmonyOS NEXT Developer DB3; IDE: DevEco Studio: 5.0.5.220; ROM：NEXT.0.0.105;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

```

## Properties

> [!TIP] "Platform"This column shows which platforms the property supports in the original third-party library。

> [!TIP] "HarmonyOS Support"A value of "yes" in this column means the HarmonyOS platform supports the property; "no" means it does not; "partially" means partial support. The usage method is consistent across platforms, and the effect is comparable to that on iOS or Android。

**Turbo_log**：A feature for log storage, retrieving log paths, and deleting logs

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| configure | Initialize Configuration     | function | no       | Android | yes               |
| deleteLogFiles | Delete All Logs     | function | no       | Android | yes               |
| getLogFilePaths | Return All Log Paths     | function | no       | Android | yes               |
| setLogToFile | Turn on/off logging to files     | function | no       | Android | yes               |
| debug | Encapsulate TurboLogger.debug     | function | no       | Android | yes               |
| error | Encapsulate TurboLogger.error     | function | no       | Android | yes               |
| warn | Encapsulate TurboLogger.warn     | function | no       | Android | yes               |
| info | EncapsulateTurboLogger.info     | function | no       | Android | yes               |
| log | Print logs for judgment/condition checks     | function | no       | Android | yes               |

## Static Method

## Pending Issues

## Others

## Open Source License

This project is based on [The MIT License (MIT)](https://github.com/@react-native-ohos/react-native-turbo-log/blob/master/LICENSE) ，Feel free to enjoy and contribute to the open source project。

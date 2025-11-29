> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-sensors</code> </h1>
</p>

本项目基于 [react-native-sensors@7.2.1-rc.2](https://github.com/react-native-sensors/react-native-sensors/tree/v7.2.1-rc.2) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-sensors`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 7.2.1@deprecated     | [@react-native-oh-library/react-native-sensors Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sensors/releases) | 0.72       |
| 7.2.3      | [@react-native-ohos/react-native-sensors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensors/releases) | 0.72       |
| 7.3.7      | [@react-native-ohos/react-native-sensors Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sensors/releases) | 0.77       |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-sensors
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-sensors
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { Alert } from "react-native";
import { Subscription } from "rxjs";
import { Button, View, Text, TextInput, StyleSheet } from 'react-native';
import { accelerometer, gyroscope, magnetometer, barometer, orientation, gravity, setUpdateIntervalForType, setLogLevelForType } from 'react-native-sensors';
export const App = () => {
    const [value, setValue] = React.useState('15');
    const [sensors, setSensorsValue] = React.useState('');
    const [IsProintLog, setIsProintLog] = React.useState(true);
    const setInterVal = () => {
        if(!sensors) return
        if (IsProintLog) {
            setUpdateIntervalForType(sensors, value);
            setIsProintLog(false)
            let sensorsSubscription: Subscription;
            switch (sensors) {
                case 'accelerometer':
                    sensorsSubscription = accelerometer.subscribe();
                    break;
                case 'gyroscope':
                    sensorsSubscription = gyroscope.subscribe();
                    break;
                case 'magnetometer':
                    sensorsSubscription = magnetometer.subscribe();
                    break;
                case 'barometer':
                    sensorsSubscription = barometer.subscribe();
                    break;
                case 'orientation':
                    sensorsSubscription = orientation.subscribe();
                    break;
                case 'gravity':
                    sensorsSubscription = gravity.subscribe();
                    break;
                default:
            }
            const timer = setTimeout(() => {
                sensorsSubscription.unsubscribe();
                clearTimeout(timer)
                setIsProintLog(true)
            }, 5000);
        }
    }
    const setLogLevel0 = () => {
        setLogLevelForType(sensors, 0)
    }
    const setLogLevel1 = () => {
        setLogLevelForType(sensors, 1)
    }
    const setLogLevel2 = () => {
        setLogLevelForType(sensors, 2)
    }
    const handleChangeText = (text:string) => {
        if (!text) {
            Alert.alert('请输入间隔时间，且不能为空！');
            return
        }
        const numericValue = text.replace(/[^0-9]/g, "");
        setValue(numericValue);
    }
    const styles = StyleSheet.create({
        divider: {
            height: 1,
            backgroundColor: '#CCCCCC',
            marginVertical: 5,
        }
    })
    return (
        <View>
            <Text>操作流程：1、输入间隔时间。2、选择传感器类型。3、选择输出日志级别。4、点击日志打印按钮。请保证设备支持</Text>
            <View style={styles.divider}></View>
            <Text>setUpdateIntervalForType设置数据采集频率</Text>
            <TextInput style={{ height: 40, borderColor: 'gray', borderWidth: 1 }} keyboardType="numeric" onChangeText={handleChangeText} value={value} placeholder="单位为ms"></TextInput>
            <Button onPress={() => { setSensorsValue('accelerometer') }} title="accelerometer"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('gyroscope') }} title="gyroscope"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('magnetometer') }} title="magnetometer"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('barometer') }} title="barometer"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('orientation') }} title="orientation"></Button>
            <View style={styles.divider}></View>
            <Button onPress={() => { setSensorsValue('gravity') }} title="gravity"></Button>
            <View style={styles.divider}></View>
            <View style={{ display: 'flex', justifyContent: 'space-around', flexDirection: 'row' }}>
                <View style={{ width: '25%', flex: 1 }}><Button onPress={setLogLevel0} title="设置LogLevel等级为0"></Button></View>
                <View style={{ width: '25%', flex: 1 }}><Button onPress={setLogLevel1} title="设置LogLevel等级为1"></Button></View>
                <View style={{ width: '25%', flex: 1 }}><Button onPress={setLogLevel2} title="设置LogLevel等级为2"></Button></View>
            </View>
            <Button disabled={!IsProintLog} onPress={setInterVal} title="setUpdateIntervalForType 日志打印"></Button>
        </View>
    )
}
export default App;
```

## 2. Manual Link

Version >= @react-native-ohos/react-native-sensors@7.2.3，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1 Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `harmony/oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-sensors": "file:../../node_modules/react-native-ohos/react-native-sensors/harmony/sensors.har"
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

### 2.3 配置 CMakeLists 和引入 SensorsPackage

 > **[!TIP] 版本 7.2.2 及以上需要.**

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-sensors/src/main/cpp" ./sensors)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_sensors)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SensorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<SensorsPackage>(ctx)
    };
}
```

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {SensorsPackage} from '@react-native-ohos/react-native-sensors/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SensorsPackage(ctx)
  ];
}
```

### 2.4 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

### 3.2 权限要求

在 module.json5 中配置所需要的权限

accelerometer 需要的权限：ohos.permission.ACCELEROMETER

gyroscope 需要的权限：ohos.permission.GYROSCOPE

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                     | Description  | Type       | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------ | ---------- | -------- | ----------- | ----------------- |
| accelerometer            | accelerometer     | Observable | no       | ios/Android | yes               |
| gyroscope                | gyroscope       | Observable | no       | ios/Android | yes               |
| magnetometer             | magnetometer       | Observable | no       | ios/Android | yes               |
| barometer                | barometer       | Observable | no       | ios/Android | yes               |
| orientation              | orientation         | Observable | no       | ios/Android | yes               |
| gravity                  | gravity         | Observable | no       | ios/Android | yes               |
| setUpdateIntervalForType | setUpdateIntervalForType     | function   | no       | ios/Android | yes               |
| setLogLevelForType       | setLogLevelForType | function   | no       | ios/Android | yes               |

## 5. 遗留问题

## 6. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-sensors/react-native-sensors/blob/master/LICENSE) ，请自由地享受和参与开源。
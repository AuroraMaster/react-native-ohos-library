> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-network-info</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/pusherman/react-native-network-info">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/pusherman/react-native-network-info/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-network-info)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 5.2.1      | [@react-native-oh-tpl/react-native-network-info  Releases](https://github.com/react-native-oh-library/react-native-network-info/releases) | 0.72       |
| 5.3.0      | @react-native-ohos/react-native-network-info  Releases       | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72 
npm install @react-native-oh-tpl/react-native-network-info
# 0.77
npm install @react-native-ohos/react-native-network-info
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-network-info
# 0.77
yarn add @react-native-ohos/react-native-network-info
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, {useState} from 'react';
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  TouchableOpacity,
} from 'react-native';
import {NetworkInfo} from 'react-native-network-info';

interface NetworkInfoState {
  ipAddress: string | null;
  ipv4Address: string | null;
  broadcast: string | null;
  ssid: string | null;
  bssid: string | null;
  subnet: string | null;
  defaultGateway: string | null;
  frequency: number | null;
}

export default NetworkInfoDemo(): JSX.Element {
  const [info, setInfo] = useState<NetworkInfoState>({
    ipAddress: '',
    ipv4Address: '',
    broadcast: '',
    ssid: '',
    bssid: '',
    subnet: '',
    defaultGateway: '',
    frequency: 0,
  });

  return (
    <ScrollView style={styles.container}>
      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getIPAddress();
            setInfo({...info, ipAddress: value});
          }}>
          <Text style={styles.button}>ipAddress</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.ipAddress}`}</Text>
      </View>

      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getIPV4Address();
            setInfo({...info, ipv4Address: value});
          }}>
          <Text style={styles.button}>ipv4Address</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.ipv4Address}`}</Text>
      </View>

      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getBroadcast();
            setInfo({...info, broadcast: value});
          }}>
          <Text style={styles.button}>broadcast</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.broadcast}`}</Text>
      </View>

      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getSSID();
            setInfo({...info, ssid: value});
          }}>
          <Text style={styles.button}>ssid</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.ssid}`}</Text>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  infoContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginBottom: 10,
  },
  infoText: {
    fontSize: 16,
  },
  button: {
    paddingVertical: 6,
    paddingHorizontal: 12,
    backgroundColor: 'hsl(193, 95%, 68%)',
    borderWidth: 2,
    borderColor: 'hsl(193, 95%, 30%)',
    borderRadius: 4,
  },
});

```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

* 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-network-info": "file:../../node_modules/@react-native-oh-tpl/react-native-network-info/harmony/rn_network_info.har"
  }
```

* 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-network-info": "file:../../node_modules/@react-native-ohos/react-native-network-info/harmony/rn_network_info.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 RNOrientationPackage

> [!TIP] 版本 `5.3.0` 及以上需要

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-network-info/src/main/cpp" ./rn_network_info)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_network_info)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "NetworkInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<NetworkInfoPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNNetworkInfoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
  # 0.72
+  import { RNNetworkInfoPackage } from '@react-native-oh-tpl/react-native-network-info/ts';
  # 0.77
+  import { RNNetworkInfoPackage } from '@react-native-ohos/react-native-network-info/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNNetworkInfoPackage(ctx)
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

本文档内容基于以下版本验证通过：

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK; IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112;

### 权限要求

在 entry 目录下的 module.json5 中添加wifi和网络信息权限

打开entry/src/main/module.json5，添加：

```json
...
"requestPermissions": [
    {
    "name" : "ohos.permission.GET_WIFI_INFO"
    },
    {
    "name": "ohos.permission.GET_NETWORK_INFO"
    }
]
```

## 静态方法

> [!TIP]"平台"列表示该属性在原三方库上支持的平台。

> [!TIP]"HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| -- | -- | -- | -- | -- | -- |
getSSID | 获取 SSID | function | no | All | yes |
getBSSID | 获取 BSSID | function | no | All | yes |
getBroadcast | 获取广播地址 | function | no | All | yes |
getIPAddress | 获取本地 IP 地址 | function | no | All | yes |
getIPV4Address | 获取 IPv4 IP 地址（优先 WiFi，其次蜂窝网络） | function | no | All | yes |
getSubnet | 获取子网掩码 | function | no | All | yes |
getGatewayIPAddress | 获取默认网关 IP 地址 | function | no | All | yes |
getFrequency | 获取频率 | function | no | Android | yes | 
getSignalStrength | 获取信号强度 | function | no | Android | yes |  

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/pusherman/react-native-network-info/blob/master/LICENSE) ，请自由地享受和参与开源。
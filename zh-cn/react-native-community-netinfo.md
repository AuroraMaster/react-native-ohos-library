> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/netinfo</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-netinfo/react-native-netinfo">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20windows%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-netinfo/react-native-netinfo/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-netinfo)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/netinfo`，具体版本所属关系如下：

| Version                    | Package Name                 | Repository                                                   | Release                                                      | Supported RN Version |
| -------------------------- | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------- |
| <= 11.1.0-0.0.8@deprecated | @react-native-oh-tpl/netinfo | [Github(deprecated)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-netinfo) | [Github Releases(deprecated)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-netinfo%2Freleases) | 0.72                 |
| 11.1.0                     | @react-native-ohos/netinfo   | [Github](https://github.com/react-native-oh-library/react-native-netinfo) | [Github Releases](https://github.com/react-native-oh-library/react-native-netinfo/releases) | 0.72                 |
| 11.4.2                     | @react-native-ohos/netinfo   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-netinfo) | [GitCode Releases]()                                         | 0.77                 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/netinfo
```

#### **yarn**

```bash
yarn add @react-native-ohos/netinfo
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Text } from "react-native";
import NetInfo, { useNetInfo } from "@react-native-community/netinfo";

const App = () => {
  const [fetchInfo, setFetchInfo] = React.useState("");
  const [refreshInfo, setRefreshInfo] = React.useState("");
  const netInfo = useNetInfo();

  NetInfo.fetch().then((state) => {
    setFetchInfo(JSON.stringify(state));
  });
  NetInfo.refresh().then((state) => {
    setRefreshInfo(JSON.stringify(state));
  });

  return (
    <View>
      <Text>Type: {netInfo.type}</Text>
      <Text>Is Connected? {netInfo.isConnected?.toString()}</Text>
      <Text style={{ fontSize: 16, fontWeight: "600" }}>fetch():</Text>
      <Text>{fetchInfo}</Text>
      <Text style={{ fontSize: 16, fontWeight: "600" }}>refresh():</Text>
      <Text>{refreshInfo}</Text>
    </View>
  );
};
export default App;
```

## Link

Version >= @react-native-ohos/netinfo@11.1.1，已支持 Autolink，无需手动配置。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/netinfo": "file:../../node_modules/@react-native-ohos/netinfo/harmony/netinfo.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明]( https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md )

### 3.配置 CMakeLists 和引入 RNCNetInfoPackage

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

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/netinfo/src/main/cpp" ./netinfo)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_netinfo)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNCNetInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNCNetInfoPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 NetInfoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {NetInfoPackage} from '@react-native-ohos/netinfo/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new NetInfoPackage(ctx)
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

## 兼容性

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### NetInfoStateType

| Name        | Description                | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | -------------------------- | ------ | -------- | ----------- | ----------------- |
| `none`      | 无有效网络连接             | String | no       | iOS Android | yes               |
| `unknown`   | 网络状态无法确定或尚未确定 | String | no       | iOS Android | yes               |
| `cellular`  | 蜂窝数据网络               | String | no       | iOS Android | yes               |
| `wifi`      | 无线网络Wi-Fi              | String | no       | iOS Android | yes               |
| `bluetooth` | 通过蓝牙的活动网络         | String | no       | Android     | no                |
| `ethernet`  | 有线以太网                 | String | no       | iOS Android | yes               |
| `wimax`     | 全球微波互联接入（WiMax）  | String | no       | Android     | no                |
| `vpn`       | 虚拟专用网络（VPN）        | String | no       | Android     | yes               |
| `other`     | 其他网络                   | String | no       | iOS Android | yes               |

#### NetInfoCellularGeneration

| Name   | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| `null` | 未连接至蜂窝网络或无法确定类型                               | String | no       | iOS Android | yes               |
| `2g`   | 连接到2G蜂窝网络。支持CDMA、EDGE、GPRS及IDEN类型的连接       | String | no       | iOS Android | yes               |
| `3g`   | 连接到3G蜂窝网络。包括EHRPD、EVDO、HSPA、HSUPA、HSDPA和UTMS类型的连接 | String | no       | iOS Android | yes               |
| `4g`   | 连接到4G蜂窝网络。包括HSPAP和LTE类型的连接                   | String | no       | iOS Android | yes               |
| `5g`   | 连接到5G蜂窝网络。包括NRNSA（仅限iOS）和NR类型的连接         | String | no       | iOS Android | yes               |

#### NetInfoState

| Name                                    | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------------------------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| `type`                                  | 当前连接的类型                                               | NetInfoStateType | yes      | iOS Android | yes               |
| `isConnected`<sup>11.4.2+</sup>         | 如果存在活动的网络连接。<br/>对于未知网络，在大多数平台上默认为null。<br/>注意：Web浏览器报告许多其他有效网络的网络类型未知 (https://caniuse.com/netinfo),<br/>因此，isConnected可能为真或假，在某些情况下，即使对于未知的网络类型，也表示真实的连接状态。  <br/>> 11.1.0 :连接时:isConnected:true;断开时:isConnected:false                                             <br/>11.4.2 : 不论连接还是断开：isConnected:boolean | boolean, null    | yes      | iOS Android | yes               |
| `isInternetReachable`<sup>11.4.2+</sup> | 如果当前活动的网络连接可以访问互联网。<br/>如果未知默认为null<br/>> 11.1.0 :连接时:isConnected:true;断开时:isInternetReachable:false                                             <br/>11.4.2 : 不论连接还是断开：isInternetReachable:boolean | boolean, null    | yes      | iOS Android | yes               |
| `isWifiEnabled`                         | (仅限Android) 设备的WiFi是打开还是关闭。                     | boolean          | yes      | iOS Android | yes               |
| `details`                               | 该值取决于类型值。见下文。                                   | object           | yes      | iOS Android | yes               |

### Details

#### Type is wifi

| Name                    | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| `isConnectionExpensive` | 网络连接是否被视为 “高成本”。<br/>这可能涉及能耗或费用层面。 | boolean | yes      | iOS Android | yes               |
| `ssid`                  | 网络的服务集标识（SSID）。<br/>若无法确定，该参数可能不存在、为 null 或为空字符串。<br/>在 iOS 上，应用需至少满足以下要求之一，且必须设置 shouldFetchWiFiSSID 配置选项，否则不会尝试获取 SSID。<br/>在 Android 上，需在 AndroidManifest.xml 中配置 ACCESS_FINE_LOCATION 权限，<br/>并获得用户同意。 | string  | yes      | iOS Android | yes               |
| `bssid`                 | 网络的基本服务集标识（BSSID）。 <br/>若无法确定，该参数可能不存在、为 null 或为空字符串。 <br/>在 iOS 上，需确保应用至少满足以下要求之一。 <br/>在 Android 上，需在 AndroidManifest.xml 中配置 ACCESS_FINE_LOCATION 权限。<br/>并获得用户同意。 | string  | yes      | iOS Android | yes               |
| `strength`              | 信号强度的整数值，范围为 0 至 100。 <br/>若无法确定信号强度，该参数可能不存在。 | number  | yes      | Android     | yes               |
| `ipAddress`             | 外部 IP 地址，支持 IPv4 或 IPv6 格式。 <br/>若无法确定，该参数可能不存在。 | string  | yes      | iOS Android | yes               |
| `subnet`                | IPv4 格式的子网掩码。 <br/>若无法确定，该参数可能不存在。    | string  | yes      | iOS Android | yes               |
| `frequency`             | 网络频率。例如：2.4GHz 网络会返回 2457。<br/>若无法确定，该参数可能不存在。 | number  | yes      | Android     | yes               |
| `linkSpeed`             | 链路速度，单位为兆比特每秒（Mbps）。                         | number  | yes      | Android     | yes               |
| `rxLinkSpeed`           | 当前接收链路速度，单位为兆比特每秒（Mbps）。                 | number  | yes      | Android     | yes               |
| `txLinkSpeed`           | 当前发送链路速度，单位为兆比特每秒（Mbps）。                 | number  | yes      | Android     | yes               |

#### Type is cellular

| Name                    | Description                                                  |           Type            | Required |  Platform   | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | :-----------------------: | :------: | :---------: | :---------------: |
| `isConnectionExpensive` | 网络连接是否被视为 “高成本”。这可能涉及能耗或费用层面。      |          boolean          |   yes    | iOS Android |        yes        |
| `cellularGeneration`    | 用户所连接的蜂窝网络代际。这可用于指示网络速度，但不提供任何保证 | NetInfoCellularGeneration |   yes    | iOS Android |        yes        |
| `carrier`               | 网络运营商名称。若无法确定，该参数可能不存在或为空字符串。   |          string           |   yes    | iOS Android |        yes        |

#### Type is bluetooth, ethernet, wimax, vpn, or other

| Name                    | Description                                                  |  Type   | Required |  Platform   | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | :-----: | :------: | :---------: | :---------------: |
| `isConnectionExpensive` | 网络连接是否被视为 “高成本”。<br/>这可能涉及能耗或费用层面。 | boolean |   yes    | iOS Android |        yes        |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                  |   Type   | Required |  Platform   | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | :------: | :------: | :---------: | :---------------: |
| `fetch()`              | 返回一个 Promise，该 Promise 会解析为 NetInfoState 对象。    | function |   yes    | iOS Android |        yes        |
| `refresh()`            | 更新 NetInfo 的内部状态，然后返回一个 Promise，该 Promise 会解析为 NetInfoState 对象。 <br/>此方法与 fetch () 类似，但仅在不原生提供网络可达性检测的平台上有用。 <br/>例如，若网络请求意外失败，你可使用此方法立即重新执行网络可达性测试。 | function |   yes    | iOS Android |        yes        |
| `addEventListener()`   | 订阅网络连接信息。 <br/>每当连接状态发生变化时，回调函数会接收一个 NetInfoState 类型的参数。 <br/>订阅后不久，监听器会收到最新信息，后续状态变化时也会收到通知。<br/>请勿假设监听器在不同设备或平台上的调用方式一致。 | function |   yes    | iOS Android |        yes        |
| `useNetInfo()`         | 一个 React Hook，可用于从全局实例获取最新状态。<br/>它会返回一个 NetInfoState 类型的 Hook。 | function |   yes    | iOS Android |        yes        |
| `useNetInfoInstance()` | 一个 React Hook，可用于创建和管理网络管理器类的独立实例。 <br/>它会返回一个刷新函数和当前的 NetInfoState 对象。 | function |   yes    | iOS Android |        yes        |

## 遗留问题

- [ ] bluetooth接口属性未适配: [issue#14](https://github.com/react-native-oh-library/react-native-netinfo/issues/14)
- [ ] wimax接口属性未适配: [issue#15](https://github.com/react-native-oh-library/react-native-netinfo/issues/15)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-netinfo/react-native-netinfo/blob/master/LICENSE) ，请自由地享受和参与开源。

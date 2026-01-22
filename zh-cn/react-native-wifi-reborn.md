> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-wifi-reborn</code> </h1>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.6.1      | [@react-native-ohos/react-native-wifi-reborn Releases](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-wifi-reborn) | 0.72       |
| 0.7.0     | [@react-native-ohos/react-native-wifi-reborn Releases](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-wifi-reborn) | 0.77       |

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-wifi-reborn)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-wifi-reborn
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-wifi-reborn
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] # demo使用了权限三方库[react-native-permissions](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-permissions.md)

### wifi-reborn example

```js
import React, { useState } from 'react';
import { ScrollView, StyleSheet, Text, TouchableOpacity, View, TextInput, Alert } from 'react-native';
import { Tester, TestSuite, TestCase } from '@rnoh/testerino';
import WifiManager from 'react-native-wifi-reborn';
import RTNPermissions, { Permission } from "react-native-permissions";

const permissionNormal: Permission[] = [
    'ohos.permission.GET_WIFI_INFO',
    'ohos.permission.SET_WIFI_INFO',
    'ohos.permission.LOCATION',
    'ohos.permission.APPROXIMATELY_LOCATION',
];

const COLORS = {
    primary: '#007AFF',
    secondary: '#5856D6',
    success: '#4CD964',
    background: '#F2F2F7',
    card: '#FFFFFF',
    text: '#000000',
    subText: '#8E8E93',
    border: '#C7C7CC',
    error: '#FF3B30',
};

const CustomButton = ({ title, onPress, color = COLORS.primary }: { title: string, onPress: () => void, color?: string }) => (
    <TouchableOpacity style={[styles.button, { backgroundColor: color }]} onPress={onPress}>
        <Text style={styles.buttonText}>{title}</Text>
    </TouchableOpacity>
);

const ResultArea = ({ text }: { text: string }) => {
    if (!text) return null;
    return (
        <View style={styles.resultContainer}>
            <Text style={styles.resultLabel}>Result:</Text>
            <Text style={styles.resultText}>{text}</Text>
        </View>
    );
};

const Description = ({ text }: { text: string }) => (
    <Text style={styles.descriptionText}>{text}</Text>
);

export const TurboLogDemoTest = () => {
    const [wifiList, setWifiList] = useState<any[]>([]);
    const [ssid, setSsid] = useState('');
    const [password, setPassword] = useState('');
    const [log, setLog] = useState('');
    const [results, setResults] = useState<{ [key: string]: string }>({});

    const addLog = (msg: string) => {
        console.info(msg);
        setLog(prev => msg + '\n' + prev);
    };

    const updateResult = (key: string, value: string) => {
        setResults(prev => ({ ...prev, [key]: value }));
        addLog(`${key}: ${value}`);
    };

    const safeStringify = (val: any) => {
        if (typeof val === 'string') return val;
        try {
            return JSON.stringify(val, null, 2);
        } catch (e) {
            return String(val);
        }
    };

      return (
        <Tester style={{ paddingBottom: 80, backgroundColor: COLORS.background }}>
            <ScrollView stickyHeaderIndices={[0]}>
                <View style={styles.headerContainer}>
                    <Text style={styles.headerTitle}>Wifi Manager Demo</Text>
                    <View style={styles.inputCard}>
                        <TextInput
                            style={styles.input}
                            placeholder="Enter SSID"
                            placeholderTextColor={COLORS.subText}
                            value={ssid}
                            onChangeText={setSsid}
                        />
                        <TextInput
                            style={styles.input}
                            placeholder="Enter Password"
                            placeholderTextColor={COLORS.subText}
                            value={password}
                            onChangeText={setPassword}
                            secureTextEntry
                        />
                    </View>
                </View>

                <TestSuite name="Permissions">
                    <TestCase title="Request Permissions">
                        <View style={styles.testCaseContent}>
                            <Description text="请求应用运行所需的权限（位置、WiFi）。" />
                            <CustomButton
                                title="Request Permissions"
                                onPress={async () => {
                                    try {
                                        let requestMultiple = await RTNPermissions.requestMultiple(permissionNormal);
                                        updateResult("Permissions", safeStringify(requestMultiple));
                                    } catch (e) {
                                        updateResult("Permissions", "Error: " + safeStringify(e));
                                    }
                                }}
                            />
                            <ResultArea text={results["Permissions"]} />
                        </View>
                    </TestCase>
                </TestSuite>

                <TestSuite name="loadWifiList">
                    <TestCase title="loadWifiList">
                        <View style={styles.testCaseContent}>
                            <Description text="返回附近WiFi网络的列表。" />
                            <CustomButton
                                title="loadWifiList"
                                onPress={() => {
                                    WifiManager.loadWifiList().then((list: any) => {
                                        updateResult("loadWifiList", "Loaded " + list.length + " networks");
                                        setWifiList(list);
                                    }).catch((err: any) => updateResult("loadWifiList", "Error: " + safeStringify(err)));
                                }}
                            />
                            <ResultArea text={results["loadWifiList"]} />
                        </View>
                    </TestCase>
                    {wifiList.length > 0 && (
                        <View style={styles.wifiListContainer}>
                            <Text style={styles.sectionTitle}>Available Networks</Text>
                            {wifiList.map((item, index) => (
                                <TouchableOpacity
                                    key={index}
                                    style={styles.wifiItem}
                                    onPress={() => {
                                        setSsid(item.SSID);
                                        addLog("Selected SSID: " + item.SSID);
                                    }}
                                >
                                    <View style={styles.wifiItemHeader}>
                                        <Text style={styles.wifiSSID}>{item.SSID || '<Hidden>'}</Text>
                                        <Text style={styles.wifiLevel}>{item.level} dBm</Text>
                                    </View>
                                    <Text style={styles.wifiBSSID}>{item.BSSID}</Text>
                                    <Text style={styles.wifiDetails}>{item.capabilities}</Text>
                                </TouchableOpacity>
                            ))}
                        </View>
                    )}
                </TestSuite>

                <TestSuite name="Connection">
                    <TestCase title="connectToProtectedSSID">
                        <View style={styles.testCaseContent}>
                            <Description text="连接到受保护的SSID" />
                            <CustomButton
                                title="connectToProtectedSSID"
                                onPress={() => {
                                    addLog(`Connecting to ${ssid}...`);
                                    if (password.length < 8) {
                                        Alert.alert('密码需大于8位字符')
                                        return
                                    } else {
                                        WifiManager.connectToProtectedSSID(ssid, password, false, false)
                                            .then(() => updateResult("connectToProtectedSSID", "Connected to " + ssid))
                                            .catch((err: any) => updateResult("connectToProtectedSSID", "Error: " + safeStringify(err)));
                                    }

                                }}
                            />
                            <ResultArea text={results["connectToProtectedSSID"]} />
                        </View>
                    </TestCase>
                </TestSuite>

                <TestSuite name="Disconnect">
                    <TestCase title="disconnect">
                        <View style={styles.testCaseContent}>
                            <Description text="断开当前连接的WiFi网络。" />
                            <CustomButton
                                title="Disconnect"
                                color={COLORS.error}
                                onPress={() => {
                                    WifiManager.disconnect()
                                        .then((res: any) => updateResult("disconnect", "Disconnect: " + safeStringify(res)))
                                        .catch((err: any) => updateResult("disconnect", "Error: " + safeStringify(err)));
                                }}
                            />
                            <ResultArea text={results["disconnect"]} />
                        </View>
                    </TestCase>
                </TestSuite>

            </ScrollView>
        </Tester>
    );
};

const styles = StyleSheet.create({
    headerContainer: {
        backgroundColor: COLORS.background,
        padding: 10,
        borderBottomWidth: 1,
        borderBottomColor: COLORS.border,
        elevation: 2,
        zIndex: 100,
    },
    headerTitle: {
        fontSize: 20,
        fontWeight: 'bold',
        color: COLORS.text,
        marginBottom: 10,
        textAlign: 'center',
    },
    inputCard: {
        backgroundColor: COLORS.card,
        borderRadius: 10,
        padding: 10,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.1,
        shadowRadius: 4,
        elevation: 3,
    },
    input: {
        height: 44,
        borderColor: COLORS.border,
        borderWidth: 1,
        borderRadius: 8,
        marginBottom: 10,
        paddingHorizontal: 12,
        backgroundColor: '#FAFAFA',
        fontSize: 16,
        color: COLORS.text,
    },
    testCaseContent: {
        padding: 10,
    },
    button: {
        paddingVertical: 12,
        paddingHorizontal: 20,
        borderRadius: 8,
        alignItems: 'center',
        justifyContent: 'center',
        elevation: 2,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 1 },
        shadowOpacity: 0.2,
        shadowRadius: 2,
    },
    buttonText: {
        color: 'white',
        fontSize: 16,
        fontWeight: '600',
    },
    resultContainer: {
        marginTop: 10,
        padding: 10,
        backgroundColor: '#F8F9FA',
        borderRadius: 6,
        borderLeftWidth: 4,
        borderLeftColor: COLORS.secondary,
    },
    resultLabel: {
        fontSize: 12,
        color: COLORS.subText,
        marginBottom: 4,
        fontWeight: '600',
    },
    resultText: {
        fontSize: 14,
        color: COLORS.text,
        fontFamily: 'monospace',
    },
    descriptionText: {
        fontSize: 13,
        color: '#666',
        marginBottom: 10,
        lineHeight: 18,
        fontStyle: 'italic',
    },
    wifiListContainer: {
        padding: 10,
        backgroundColor: COLORS.background,
    },
    sectionTitle: {
        fontSize: 18,
        fontWeight: 'bold',
        color: COLORS.text,
        marginBottom: 10,
        marginLeft: 5,
    },
    wifiItem: {
        padding: 15,
        backgroundColor: COLORS.card,
        borderRadius: 10,
        marginBottom: 8,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 1 },
        shadowOpacity: 0.1,
        shadowRadius: 2,
        elevation: 2,
    },
    wifiItemHeader: {
        flexDirection: 'row',
        justifyContent: 'space-between',
        alignItems: 'center',
        marginBottom: 4,
    },
    wifiSSID: {
        fontSize: 16,
        fontWeight: 'bold',
        color: COLORS.text,
    },
    wifiLevel: {
        fontSize: 14,
        color: COLORS.success,
        fontWeight: '600',
    },
    wifiBSSID: {
        fontSize: 12,
        color: COLORS.subText,
        marginBottom: 2,
    },
    wifiDetails: {
        fontSize: 11,
        color: COLORS.subText,
        fontStyle: 'italic',
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
    "@react-native-ohos/react-native-wifi-reborn": "file:../../node_modules/@react-native-ohos/react-native-wifi-reborn/harmony/wifi_reborn.har"
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

### 3.配置 CMakeLists 和引入 wifi_reborn

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-wifi-reborn/src/main/cpp" ./wifi_reborn)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp") # this line is needed by codegen v1
add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_wifi_reborn)
# RNOH_END: manual_package_linking_2
```

Import the TurboLogPackage on the ArkTS side

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "WifiRebornPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<WifiRebornPackage>(ctx),
    };
}
```

### 4. 在 ArkTs 侧引入 WifiRebornPackage 组件

找到 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+ import { WifiRebornPackage } from '@react-native-ohos/react-native-wifi-reborn';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
return [
+    new WifiRebornPackage (ctx)
  ];
 }
...
...
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

### 权限要求

以下权限中有`system_basic` 权限，而默认的应用权限是 `normal` ，只能使用 `normal` 等级的权限，所以可能会在安装hap包时报错**9568289**，请参考 [文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/bm-tool-V5#ZH-CN_TOPIC_0000001884757326__%E5%AE%89%E8%A3%85hap%E6%97%B6%E6%8F%90%E7%A4%BAcode9568289-error-install-failed-due-to-grant-request-permissions-failed) 修改应用等级为 `system_basic`

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
			{
				"name": "ohos.permission.GET_WIFI_INFO",
				"reason": "$string:wifi_info_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			},
			{
				"name": "ohos.permission.SET_WIFI_INFO",
				"reason": "$string:wifi_set_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			},
			{
				"name": "ohos.permission.LOCATION",
				"reason": "$string:location_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			},
			{
				"name": "ohos.permission.APPROXIMATELY_LOCATION",
				"reason": "$string:location_approx_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			}
		],
```

#### 在 entry 目录下添加申请以上权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
    {
      "name": "wifi_info_reason",
      "value": "需要获取WiFi信息以显示当前连接的网络状态"
    },
    {
      "name": "wifi_set_reason",
      "value": "需要配置WiFi网络以连接到指定的无线网络"
    },
    {
      "name": "location_reason",
      "value": "需要位置权限以扫描附近的WiFi网络（系统要求）"
    },
    {
      "name": "location_approx_reason",
      "value": "需要大致位置权限以扫描WiFi网络"
    }
  ]
}
```

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] &quot;HarmonyOS Support&quot;列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。droid 的效果。

**wifi-reborn**：适用于 React Native的 WiFi 管理第三方库，主要用于在应用中实现与设备 WiFi 功能相关的各种操作。

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| connectToProtectSSID | 连接到受保护的SSID     | function | no       | Android/IOS | yes               |
| suggestWifiNetwork | 向移动设备系统推荐/提示指定可见的 WIFI 网络    | function | no       | Android/IOS | yes               |
| connectToProtectedWifiSSID | 连接到名为SSID的受保护的 WIFI     | function | no       | Android/IOS | yes               |
| getCurrentWifiSSID | 返回当前WIFI网络的SSID     | function | no       | Android/IOS | yes               |
| connectToSSID | 连接到SSID     | function | no       | IOS | yes               |
| connectToSSIDPrefix | 连接到特定前缀的SSID     | function | no       | IOS | yes               |
| disconnectFromSSID | 断开与SSID的连接     | function | no       | IOS | yes               |
| connectToProtectedSSIDOnce | 连接到受保护的SSID一次     | function | no       |  IOS | no               |
| connectToProtectedSSIDPrefix | 连接到受保护的特定前缀的SSID     | function | no       | IOS | yes               |
| connectToProtectedSSIDPrefixOnce | 连接到受保护的特定前缀的SSID一次     | function | no       | IOS | no               |
| loadWifiList | 返回附近WIFI网络列表     | function | no       | Android | yes               |
| reScanAndLoadWifiList | 重新扫描周边可见 WiFi 网络，并加载返回完整的 WiFi 列表数据     | function | no       | Android | yes               |
| isEnabled | 检查 WIFI 是否已开启     | function | no       | Android | yes               |
| setEnabled | 在设备上设置 WIFI 开启或关闭     | function | no       | Android | yes               |
| connectionStatus | 当前设备连接 WIFI 的状态，已连接返回true     | function | no       | Android | yes               |
| disconnect | 断开当前连接的 WIFI     | function | no       | Android | yes               |
| getBSSID | 返回当前连接 WIFI 的BSSID     | function | no       | Android | yes               |
| getCurrentSignalStrength | 返回当前连接 WIFI 的RSSI(信号强度)     | function | no       | Android | yes               |
| getFrequency | 返回当前连接的 WIFI 的信号频率     | function | no       | Android | yes               |
| getIP | 返回当前连接 WIFI 的IP地址     | function | no       | Android | yes               |
| isRemoveWifiNetwork | 移除设备中已保存配置的指定 WiFi 网络     | function | no       | Android | yes               |
| forceWifiUsage | 强制当前应用的网络请求走设备已连接的WIFI通道，忽略移动数据     | function | no       | Android | yes               |
| forceWifiUsageWithOptions | 强制当前应用的网络请求走设备已连接的WIFI通道，忽略移动数据(可传入配置对象)     | function | no       | Android | yes               |

## 静态方法

## 遗留问题

## 其他

•connectToProtectedSSIDOnce和connectToProtectedSSIDPrefixOnce方法无法实现，这两个方法是专门为ios平台设计的，在ios系统中使用了NEHotspotConfigurationManager传递joinOnce参数来实现一次连接功能，鸿蒙侧不支持此功能。<br>
•setEnabled鸿蒙只支持跳转到wifi设置页<br>
•connectToProtectSSID,connectToProtectedWifiSSID,connectToProtectedSSIDPrefix,参数isWEP值为true的时候会有提示不支持的信息返回<br>

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/JuanSeBestia/react-native-wifi-reborn/blob/master/LICENSE) ，请自由地享受和参与开源。


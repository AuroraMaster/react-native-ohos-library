> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-ping</code> </h1>
</p>

本项目基于 [react-native-ping](https://github.com/RoJoHub/react-native-ping) 开发。

该第三方库支持直接从 npm 下载，包名为：`@react-native-ohos/react-native-ping` 版本所属关系如下：
| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-ping | ~ 1.3.0    | [Github Releases](https://github.com/react-native-oh-library/react-native-ping/releases) | 0.72.*/0.77.*/0.82.* | 是 | API20+ | 1.2.8 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-ping) |  

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-ping
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-ping
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
/**
 * react-native-ping 示例
 * 展示 React Native 中的 ICMP Ping 功能
 */

import React, { useState, useEffect } from 'react';
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  TouchableOpacity,
  ActivityIndicator,
  Alert,
} from 'react-native';
import Ping from '@react-native-ohos/react-native-ping';

const TestCase = ({
  title,
  description,
  onPress,
  isLoading,
  result,
}) => (
  <View style={styles.testCaseContainer}>
    <Text style={styles.testCaseTitle}>{title}</Text>
    {description && <Text style={styles.testCaseDescription}>{description}</Text>}
    <TouchableOpacity
      style={[styles.testButton, isLoading && styles.disabledButton]}
      onPress={onPress}
      disabled={isLoading}
    >
      {isLoading ? (
        <ActivityIndicator size="small" color="#FFFFFF" />
      ) : (
        <Text style={styles.testButtonText}>开始测试</Text>
      )}
    </TouchableOpacity>
    {result !== null && <Text style={styles.testResult}>{result}</Text>}
  </View>
);

interface TrafficStats {
  receivedNetworkSpeed: number;
  sendNetworkSpeed: number;
  receivedNetworkTotal: number;
  sendNetworkTotal: number;
}

interface TestResults {
  [key: string]: string | null;
}

interface LoadingTests {
  [key: string]: boolean;
}

const ReactNativePingDemo = () => {
  const [loadingTests, setLoadingTests] = useState<LoadingTests>({});
  const [testResults, setTestResults] = useState<TestResults>({});
  const [trafficStats, setTrafficStats] = useState<TrafficStats | null>(null);
  const [isLoadingTraffic, setIsLoadingTraffic] = useState(false);

  const runTest = async (testId: string, testFunction: () => Promise<string>) => {
    setLoadingTests(prev => ({ ...prev, [testId]: true }));
    setTestResults(prev => ({ ...prev, [testId]: null }));

    try {
      const result = await testFunction();
      setTestResults(prev => ({
        ...prev,
        [testId]: `测试结果: ${result}`,
      }));
    } catch (error) {
      const errorMessage = error.code
        ? `测试失败 (${error.code}): ${error.message}`
        : `测试失败: ${error.message || '未知错误'}`;
      setTestResults(prev => ({
        ...prev,
        [testId]: errorMessage,
      }));
    } finally {
      setLoadingTests(prev => ({ ...prev, [testId]: false }));
    }
  };

  const runAllTests = async () => {
    const testIds = [
      'testGoogleDNS',
      'test114DNS',
      'testInvalidHost',
      'testNoHost'
    ];

    for (const testId of testIds) {
      if (!loadingTests[testId]) {
        await runTest(testId, () => runSingleTest(testId));
      }
    }

    Alert.alert('测试完成', '所有测试已执行完毕');
  };

  const runSingleTest = async (testId) => {
    switch (testId) {
      case 'testGoogleDNS':
        return testPing('8.8.8.8', 'Google DNS');
      case 'test114DNS':
        return testPing('114.114.114.114', '114 DNS', { timeout: 5000 });
      case 'testInvalidHost':
        return testPing('invalid-host.example.com', '无效主机', { timeout: 5000 });
      case 'testNoHost':
        return testPing('', '未设置 host', { timeout: 5000 });  
      default:
        throw new Error('未知测试');
    }
  };

    const testPing = async (ipAddress: string, name: string, options: { timeout?: number } = {}) => {
        try {
            const start = Date.now();
            const rtt = await Ping.start(ipAddress, options);
            console.log("chy rrt:", rtt)
            return `${name} - RTT: ${rtt}ms`;
        } catch (e) {
            return JSON.stringify(e.message)
        }
    };

  const loadTrafficStats = async () => {
    setIsLoadingTraffic(true);
    try {
      const stats = await Ping.getTrafficStats();
      console.log("chy stats:", stats)
      setTrafficStats(stats);
    } catch (error) {
      Alert.alert('获取流量统计失败', error.message);
    } finally {
      setIsLoadingTraffic(false);
    }
  };

  useEffect(() => {
    loadTrafficStats();
  }, []);

  return (
    <ScrollView style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.title}>react-native-ping 演示</Text>
        <Text style={styles.subtitle}>
          高性能 ICMP Ping 控制器
        </Text>
      </View>

      <View style={styles.sectionContainer}>
        <Text style={styles.sectionTitle}>流量统计</Text>
        {isLoadingTraffic ? (
          <ActivityIndicator size="small" color="#007AFF" />
        ) : trafficStats ? (
          <View style={styles.statsContainer}>
            <Text style={styles.statItem}>
              接收速度: <Text style={styles.statValue}>{trafficStats.receivedNetworkSpeed}</Text>
            </Text>
            <Text style={styles.statItem}>
              发送速度: <Text style={styles.statValue}>{trafficStats.sendNetworkSpeed}</Text>
            </Text>
            <Text style={styles.statItem}>
              接收总量: <Text style={styles.statValue}>{trafficStats.receivedNetworkTotal}</Text>
            </Text>
            <Text style={styles.statItem}>
              发送总量: <Text style={styles.statValue}>{trafficStats.sendNetworkTotal}</Text>
            </Text>
          </View>
        ) : null}
        <TouchableOpacity
          style={styles.refreshButton}
          onPress={loadTrafficStats}
          disabled={isLoadingTraffic}
        >
          <Text style={styles.refreshButtonText}>刷新统计</Text>
        </TouchableOpacity>
      </View>

      <View style={styles.sectionContainer}>
        <Text style={styles.sectionTitle}>Ping 测试</Text>
        <TestCase
          title="Google DNS (8.8.8.8)"
          description="测试 Google Public DNS 响应"
          onPress={() => runTest('testGoogleDNS', () => runSingleTest('testGoogleDNS'))}
          isLoading={loadingTests['testGoogleDNS']}
          result={testResults['testGoogleDNS']}
        />
        <TestCase
          title="114 DNS (114.114.114.114)"
          description="测试 114 DNS 响应"
          onPress={() => runTest('test114DNS', () => runSingleTest('test114DNS'))}
          isLoading={loadingTests['test114DNS']}
          result={testResults['test114DNS']}
        />
        <TestCase
          title="无效主机"
          description="测试无效主机地址"
          onPress={() => runTest('testInvalidHost', () => runSingleTest('testInvalidHost'))}
          isLoading={loadingTests['testInvalidHost']}
          result={testResults['testInvalidHost']}
        />

        <TestCase
          title="未设置 host"
          description="未设置 host"
          onPress={() => runTest('testNoHost', () => runSingleTest('testNoHost'))}
          isLoading={loadingTests['testNoHost']}
          result={testResults['testNoHost']}
        />
      </View>

      <View style={styles.sectionContainer}>
        <TouchableOpacity
          style={[styles.runAllButton, Object.values(loadingTests).some(v => v) && styles.disabledButton]}
          onPress={runAllTests}
          disabled={Object.values(loadingTests).some(v => v)}
        >
          {Object.values(loadingTests).some(v => v) ? (
            <ActivityIndicator size="small" color="#FFFFFF" />
          ) : (
            <Text style={styles.runAllButtonText}>运行所有测试</Text>
          )}
        </TouchableOpacity>
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5F5F5',
  },
  header: {
    backgroundColor: '#007AFF',
    paddingVertical: 24,
    paddingHorizontal: 16,
    alignItems: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#FFFFFF',
    textAlign: 'center',
    marginBottom: 8,
  },
  subtitle: {
    fontSize: 14,
    color: 'rgba(255, 255, 255, 0.8)',
    textAlign: 'center',
  },
  sectionContainer: {
    backgroundColor: '#FFFFFF',
    marginVertical: 8,
    paddingHorizontal: 16,
    paddingVertical: 16,
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 16,
    color: '#333333',
  },
  testCaseContainer: {
    backgroundColor: '#F8F8F8',
    padding: 12,
    borderRadius: 8,
    marginBottom: 16,
  },
  testCaseTitle: {
    fontSize: 16,
    fontWeight: '600',
    marginBottom: 8,
    color: '#333333',
  },
  testCaseDescription: {
    fontSize: 12,
    color: '#666666',
    marginBottom: 12,
    lineHeight: 16,
  },
  testButton: {
    backgroundColor: '#007AFF',
    paddingVertical: 8,
    paddingHorizontal: 16,
    borderRadius: 6,
    alignItems: 'center',
  },
  disabledButton: {
    backgroundColor: '#CCCCCC',
  },
  testButtonText: {
    color: '#FFFFFF',
    fontSize: 14,
    fontWeight: '500',
  },
  testResult: {
    marginTop: 12,
    fontSize: 14,
    lineHeight: 20,
    color: '#333333',
  },
  statsContainer: {
    backgroundColor: '#F8F8F8',
    padding: 12,
    borderRadius: 8,
    marginBottom: 12,
  },
  statItem: {
    fontSize: 14,
    color: '#333333',
    marginBottom: 8,
  },
  statValue: {
    fontWeight: '600',
    color: '#007AFF',
  },
  refreshButton: {
    backgroundColor: '#007AFF',
    paddingVertical: 8,
    paddingHorizontal: 16,
    borderRadius: 6,
    alignItems: 'center',
  },
  refreshButtonText: {
    color: '#FFFFFF',
    fontSize: 14,
    fontWeight: '500',
  },
  runAllButton: {
    backgroundColor: '#34C759',
    paddingVertical: 12,
    paddingHorizontal: 16,
    borderRadius: 8,
    alignItems: 'center',
    justifyContent: 'center',
  },
  runAllButtonText: {
    color: '#FFFFFF',
    fontSize: 16,
    fontWeight: '600',
  },
});

export default ReactNativePingDemo;
```

## 2. Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|------------------|-----------|
| ~1.3.0                               |  Yes             |  0.72/0.77/0.82     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

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

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/react-native-ping": "file:../../node_modules/@react-native-ohos/react-native-ping/harmony/RNPing.har"
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 RNCPingPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-ping/src/main/cpp" ./ping)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_ping)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNCPingPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<RNCPingPackage>(ctx),
    };
}
```

### 2.5. 在 ArkTs 侧引入 react-native-ping Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNReactNativePingPackage} from '@react-native-ohos/react-native-ping/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNReactNativePingPackage(ctx),
  ];
}
```
</details>

### 2.6. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<@react-native-ohos/react-native-ping> Releases](https://github.com/react-native-oh-library/react-native-ping/releases)

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.59/0.77.18-1/0.82.7; SDK: HarmonyOS-6.0.0(API20); IDE: DevEco Studio 6.0.1.260; ROM: NEXT.0.0.71。

### 3.2. 权限要求（如有）

（填入相关权限配置）
打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "ohos.permission.INTERNET",
+    },
  ]
}
```

### 3.3. 编译运行API要求

> [!TIP] 当前三方库支持在 `API20+` 工程编译，及 `API20+` ROM运行。

> [!TIP] 以下功能依赖特定版本的API，使用 `低于指定API版本的工程编译` 或 `低于指定API版本的ROM运行` 均可能导致部分功能受限。
1. 1.3.0版本引入[NetConn_ProbeResultInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-netconnection-netconn-proberesultinfo)，来定义ping功能中返回的探测结果信息，NetConn_ProbeResultInfo需要在支持`API20+`的工程编译，并在支持`API20+`的ROM上运行，低版本上运行将会导致start方法中的ping功能不可用。

## 6. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### start
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ipAddress  | ping的Ip    | string  | yes | ALL  | yes                |
| options    | 超时时间配置 | object  | no  | ALL  | no                 |

### getTrafficStats
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| receivedNetworkSpeed  | 接收速度 | string  | yes | ALL | yes          |
| sendNetworkSpeed      | 发送速度 | string  | yes | ALL | yes          |
| receivedNetworkTotal  | 接收总量 | string  | yes | ALL | yes          |
| sendNetworkTotal      | 发送总量 | string  | yes | ALL | yes          |

## 7. 错误码

| Name     | Description  |   Type   |   default   | platform | HarmonyOS Support |
| :------- | :----------- | :------: | :---------: | -------- | ----------------- |
| PingUtil_Message_Timeout                    | 超时                | `string` | `0` | iOS,Android | NO |
| PingUtil_Message_PreviousPingIsStillRunning | 正在运行            | `string` | `1` | /           | NO |
| PingUtil_Message_HostErrorNotSetHost        | 未设置ip            | `string` | `2` | iOS,Android | YES |
| PingUtil_Message_HostErrorUnknown           | host未知错误        | `string` | `3` | iOS,Android | YES |
| PingUtil_Message_HostErrorHostNotFound      | host错误、host找不到| `string` | `4` | Only iOS    | NO |
| PingUtil_Message_Unknown                    | 未知错误            | `string` | `5` | Only iOS    | NO |

## 7. 遗留问题

- [ ]  start方法的options配置不生效
- [ ]  错误码只支持PingUtil_Message_HostErrorNotSetHost和PingUtil_Message_HostErrorUnknown，其他不支持

## 8. 其他


## 9. 开源协议

本项目基于 [MIT License (MIT)]() ，请自由地享受和参与开源。

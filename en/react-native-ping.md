> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-ping</code> </h1>
</p>

This project is based on [react-native-ping](https://github.com/RoJoHub/react-native-ping).

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-ping`, The version correspondence details are as follows:

| Name | Version | Release Information | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address     |
| --------------| -------------- | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-ping | ~ 1.3.0    | [Github Releases](https://github.com/react-native-oh-library/react-native-ping/releases) | 0.72.*/0.77.*/0.82.* | yes | API20+ | 1.2.8 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-ping) | 

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
// react-native-ping is used as an example.
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

## 2. Manual Link

|                                      | Supported Autolink | Supported RN Version |
|--------------------------------------|------------------|-----------|
| ~1.3.0                               |  Yes             |  0.72/0.77/0.82     |

Projects using AutoLink need to be configured according to this document, AutoLink framework guide.：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you are using supports Autolink and the project has integrated Autolink, you can skip the ManualLink configuration.

<details>
  <summary>ManualLink: This step provides guidance for manually configuring native dependencies.</summary>

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-ping": "file:../../node_modules/@react-native-ohos/react-native-ping/harmony/RNPing.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 2.3 Configuring CMakeLists and Introducing xxx Package

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-ping/src/main/cpp" ./ping)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_ping)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 2.4 Introducing react-native-ping Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 2.5 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

Check the release version information in the release address of the third-party library: [\<@react-native-ohos/react-native-ping> Releases](https://github.com/react-native-oh-library/react-native-ping/releases)

This document is verified based on the following versions:

1. RNOH: 0.72.59/0.77.18-1/0.82.7; SDK: HarmonyOS-6.0.0(API20); IDE: DevEco Studio 6.0.1.260; ROM: NEXT.0.0.71.

### 3.2 Permission Requirements

(Enter the related permission configuration.)
open `entry/src/main/resources/base/element/string.json` and add：

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

### 3.3. API requirements

> [!TIP] All versions of the current third-party libraries supporting compilation in `API20+` projects and execution on `API20+` ROMs.

> [!TIP] The following features depend on specific API versions. Compiling the project with an API version lower than specified or running the ROM with an API version lower than specified may result in limited functionality.
1. Version 1.3.0 introduced [NetConn_ProbeResultInfo](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-netconnection-netconn-proberesultinfo) to define the detection result information returned in the `ping` function. `NetConn_ProbeResultInfo` needs to be compiled in a project that supports `API20+` and run on a ROM that supports `API20+`. Running it on lower versions will result in the ping function in the `start` method being unavailable.

## 4. APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### start
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ipAddress  | Ip                    | string  | yes | ALL  | yes      |
| options    | Timeout Configuration | object  | no  | ALL  | no       |

### getTrafficStats
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| receivedNetworkSpeed  | Download Speed per second | string  | yes | ALL | yes          |
| sendNetworkSpeed      | Upload Speed per second | string  | yes | ALL | yes          |
| receivedNetworkTotal  | Download Total | string  | yes | ALL | yes          |
| sendNetworkTotal      | Upload Total | string  | yes | ALL | yes          |

## 5. Known Issues

- [ ]  The options configuration for the start method is not taking effect
- [ ]  The error code only supports PingUtil_Message_HostErrorNotSetHost and PingUtil_Message_HostErrorUnknown; others are not supported

## 6. Others

## 7. License

This project is licensed under [MIT License (MIT)]().

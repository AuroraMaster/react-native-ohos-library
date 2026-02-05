> 模板版本：v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-device-info</code> </h1>
</p>

本项目基于 [react-native-device-info](https://github.com/react-native-oh-library/react-native-device-info) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-device-info` 版本所属关系如下：
| 三方库名称    | 三方库版本    | 发布信息     | 支持RN版本    | Autolink     | 编译API版本     | 社区基线版本    | npm地址                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-device-info |   ~ 14.1.2    | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-device-info/releases) | 0.82.* | 否 | API12+ | 14.1.1 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-device-info) |
| @react-native-ohos/react-native-device-info |   ~ 14.0.5    | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-device-info/releases) | 0.77.* | 否 | API12+ | 14.0.4 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-device-info) |
| @react-native-ohos/react-native-device-info | ~ 11.1.1   | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-device-info/releases) | 0.72.* | 是 | API12+ | 11.1.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-device-info) | 
| @react-native-oh-tpl/react-native-device-info | <= 11.1.0-0.0.8@deprecated    | [Github Releases](https://github.com/react-native-oh-library/react-native-device-info/releases) | 0.72.* | 否 | API12+ | 11.1.0 | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/react-native-device-info) | 

    
## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-device-info
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-device-info
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx

import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
} from 'react-native';
import React, { useState, useEffect } from 'react';
import DeviceInfo from 'react-native-device-info';
import { Colors } from 'react-native/Libraries/NewAppScreen';

function App() {
  const isDarkMode = useColorScheme() === 'dark';
  const [deviceInfo, setDeviceInfo] = useState({
    BundleId: '',
    Version: '',
    ReadableVersion: '',
    BuildNumber: '',
    Tablet: false,
    ApplicationName: '',
    Brand: '',
    Model: '',
    DeviceType: '',
    DeviceName: '',
  });

  useEffect(() => {
    const fetchDeviceInfo = async () => {
      const BundleId = await DeviceInfo.getBundleId();
      const Version = await DeviceInfo.getVersion();
      const ReadableVersion = await DeviceInfo.getReadableVersion();
      const BuildNumber = await DeviceInfo.getBuildNumber();
      const Tablet = await DeviceInfo.isTablet();
      const ApplicationName = await DeviceInfo.getApplicationName();
      const Brand = await DeviceInfo.getBrand();
      const Model = await DeviceInfo.getModel();
      const DeviceType = await DeviceInfo.getDeviceType();
      const DeviceName = await DeviceInfo.getDeviceName();

      setDeviceInfo({
        BundleId,
        Version,
        ReadableVersion,
        BuildNumber,
        Tablet,
        ApplicationName,
        Brand,
        Model,
        DeviceType,
        DeviceName,
      });
    };

    fetchDeviceInfo();
  }, []);

  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };

  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={isDarkMode ? 'light-content' : 'dark-content'}
        backgroundColor={backgroundStyle.backgroundColor}
      />
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}>
        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
            padding: 16,
          }}>
          <Text style={styles.sectionTitle}>Device Information</Text>
          <Text style={styles.infoText}>BundleId: {deviceInfo.BundleId}</Text>
          <Text style={styles.infoText}>Version: {deviceInfo.Version}</Text>
          <Text style={styles.infoText}>ReadableVersion: {deviceInfo.ReadableVersion}</Text>
          <Text style={styles.infoText}>BuildNumber: {deviceInfo.BuildNumber}</Text>
          <Text style={styles.infoText}>Tablet: {deviceInfo.Tablet ? 'Yes' : 'No'}</Text>
          <Text style={styles.infoText}>ApplicationName: {deviceInfo.ApplicationName}</Text>
          <Text style={styles.infoText}>Brand: {deviceInfo.Brand}</Text>
          <Text style={styles.infoText}>Model: {deviceInfo.Model}</Text>
          <Text style={styles.infoText}>DeviceType: {deviceInfo.DeviceType}</Text>
          <Text style={styles.infoText}>DeviceName: {deviceInfo.DeviceName}</Text>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionTitle: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
  infoText: {
    fontSize: 16,
    marginBottom: 8,
  },
});

export default App;
```

> [!注意事项] 如果调用 getFontScale接口，需要进行以下配置。
```
1. harmony/AppScope/resources/base/profile文件夹下面新增configuration.json文件，内容如下：

{
  "configuration": {
    "fontSizeScale": "followSystem",
    "fontSizeMaxScale": "3.2"
  }
}

2.在harmony/AppScope/app.json5 文件中配置 "configuration": "$profile:configuration" 如下：
{
  "app": {
    "bundleName": "com.example.test",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:app_icon",
    "label": "$string:app_name",
    "distributedNotificationEnabled": true,
  + "configuration": "$profile:configuration"
  }
}
```

## 2. Link

|                            | 是否支持autolink | RN框架版本 |
|----------------------------|--------------|--------|
| ~14.1.2                    | No           | 0.82   |
| ~14.0.5                    | No           | 0.77   |
| ~11.1.1                     | Yes          | 0.72   |
| <= 11.1.0-0.0.8@deprecated | No           | 0.72   |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony"
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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-device-info": "file:../../node_modules/@react-native-ohos/react-native-device-info/harmony/device_info.har"
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

### 2.3. 配置 CMakeLists 和引入 RNDeviceInfoPackage

> 若使用的是  <= 11.1.0-0.0.8 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(REACT_NATIVE_DEVICE_INFO_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@react-native-ohos/react-native-device-info/src/main/cpp")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${REACT_NATIVE_DEVICE_INFO_CPP_DIR}" ./device_info)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC device_info)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNDeviceInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<RNDeviceInfoPackage>(ctx),
    };
}
```

### 2.4. 在 ArkTs 侧引入 RNDeviceInfoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNDeviceInfoPackage} from '@react-native-ohos/react-native-device-info/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNDeviceInfoPackage(ctx)
  ];
}
```
</details>

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 3.2. 权限要求

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
  {
    "name": "ohos.permission.GET_NETWORK_INFO"
  },
  {
    "name": "ohos.permission.GET_WIFI_INFO"
  },
  {
    "name": "ohos.permission.DISTRIBUTED_DATASYNC",
    "reason": "$string:DATA_SYNC",
    "usedScene": {
      "abilities": [
        "EntryAbility"
      ],
      "when": "always"
    }
  }
]
```

### 3.3. 编译运行API要求

> [!TIP] 当前三方库所有版本均已实现版本隔离，支持在 `API12+` 工程编译，及 `API12+` ROM运行。

> [!TIP] 以下功能依赖特定版本的API，使用 `低于指定API版本的工程编译` 或 `低于指定API版本的ROM运行` 均可能导致部分功能受限。
1. 14.0.5-rc.4 版本引入[getFontScale](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-configuration#configuration)，实现了获取当前系统的字体缩放比例功能，此API需要在支持`API18+`的工程编译，并在支持`API18+`的ROM上运行，方可生效。

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                 | Description                                                                                                                         | Type | Required | Platform | HarmonyOS Support  |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------| ---- | -------- | -------- | ------------------ |
| getAndroidId                         | 获取 ANDROID_ID。请参阅 API 文档了解正确使用方法。                                                                                                   | Promise<string>| No | Android      | no |
| getApiLevel                          | 获取 API 级别。                                                                                                                          | Promise<number>| No | Android      | yes |
| getApplicationName                   | 获取应用程序名称。                                                                                                                           | string | No | IOS/Android/Windows/visionOS      | yes |
| getAvailableLocationProviders        | 返回特定平台位置提供者/服务的对象，包含当前是否可用的布尔值。                                                                                                     | Promise<object>  | No | IOS/Android/visionOS      | yes |
| getBaseOs                            | 产品所基于的基础操作系统构建版本。                                                                                                                   | Promise<string>  | No | Android/Windows/Web      | yes |
| getBuildId                           | 获取操作系统的构建编号。                                                                                                                        | Promise<string>  | No | IOS/Android/Windows/visionOS      | yes |
| getBatteryLevel                      | 获取设备电池电量，返回 0 到 1 之间的浮点数。                                                                                                           | Promise<number>  | No | IOS/Android /Windows/Web/visionOS     | yes |
| getBootloader                        | 系统引导程序版本号。                                                                                                                          | Promise<string>  | No | Android      | yes |
| getBrand                             | 获取设备品牌。                                                                                                                             | string  | No | IOS/Android/Windows/visionOS      | yes |
| getBuildNumber                       | 获取应用程序构建编号。                                                                                                                         | string  | No | IOS/Android/Windows/visionOS      | yes |
| getBundleId                          | 获取应用程序包标识符。                                                                                                                         | string  | No | IOS/Android/Windows/visionOS      | yes |
| isCameraPresent                      | 判断设备当前是否有摄像头。                                                                                                                       | Promise<boolean>  | No | Android/Windows/Web      | yes |
| getCarrier                           | 获取运营商名称（网络运营商）。                                                                                                                     | Promise<string>  | No | IOS/Android      | yes |
| getCodename                          | 当前开发代号，如果是发布版本则为字符串"REL"。                                                                                                           | Promise<string>  | No | Android      | yes |
| getDevice                            | 工业设计名称。                                                                                                                             | Promise<string>  | No | Android      | yes |
| getDeviceId                          | 获取设备 ID。                                                                                                                            | string  | No | IOS/Android/Windows/visionOS     | no |
| getDeviceType                        | 返回设备类型的字符串。                                                                                                                         | string  | No | IOS/Android/visionOS      | yes |
| getDisplay                           | 用于向用户显示的构建 ID 字符串。                                                                                                                  | Promise<string>  | No | Android      | yes |
| getDeviceName                        | 获取设备名称。                                                                                                                             | Promise<string>  | No | IOS/Android/Windows/visionOS      | yes |
| getDeviceNameSync                    | 获取设备名称。                                                                                                                             | string  | No | No      | No |
| getDeviceToken                       | 获取设备令牌（参见 DeviceCheck）。仅适用于 iOS 11.0+ 的真实设备。当不支持 getDeviceToken 时会拒绝 Promise，请注意异常处理。                                               | Promise<string>  | No | IOS/visionOS      | no |
| getFirstInstallTime                  | 获取应用首次安装的时间（毫秒）。                                                                                                                    | Promise<number>  | No | IOS/Android/Windows/visionOS      | yes |
| getFingerprint                       | 唯一标识此构建的字符串。                                                                                                                        | Promise<string>  | No | Windows      | no |
| getFontScale                         | 获取设备字体缩放比例。字体缩放比例是当前系统字体与"正常"字体大小的比率。如果正常文本为 10pt 而系统字体当前为 15pt，则字体缩放比例为 1.5。这可用于确定设备的无障碍设置是否已更改；如果字体缩放比例明显较大（> 2.0），您可能需要重新布局某些视图。 | Promise<number>  | No | IOS/Android/Windows      | yes |
| getFreeDiskStorage                   | 获取可用存储空间大小的方法（字节），考虑根文件系统和数据文件系统的计算。                                                                                                | Promise<number>  | No | IOS/Android/Windows/Web/visionOS      | no |
| getFreeDiskStorageOld                | 获取可用存储空间大小的旧实现方法（字节）。                                                                                                               | Promise<number>  | No | IOS/Android/Windows/Web/visionOS      | no |
| getHardware                          | 硬件名称（来自内核命令行或 /proc）。                                                                                                               | Promise<string>  | No | Android      | yes |
| getHost                              | 主机名。                                                                                                                                | Promise<string>  | No | Android/Windows      | yes|
| getHostNames                         | 主机名列表。                                                                                                                              | Promise<string[]> | No | Windows      | no |
| getIpAddress                         | 已弃用。获取设备当前 IP 地址（仅 WiFi）。请切换到 react-native-netinfo/netinfo 或 react-native-network-info。                                             | Promise<string>  | No |  IOS/Android/Windows/visionOS      | yes |
| getIncremental                       | 底层源代码控制用于表示此构建的内部值。                                                                                                                 | Promise<string>  | No | Android      | yes |
| getInstallerPackageName              | 底层源代码控制用于表示此构建的内部值。                                                                                                                 | Promise<string>  | No | IOS/Android/Windows/visoinOS      | yes |
| getInstallReferrer                   | 获取应用安装时的来源引用字符串。                                                                                                                    | Promise<string>  | No | Android/Windows/Web      | no |
| getInstanceId                        | 获取应用程序实例 ID。                                                                                                                        | Promise<string>  | No | Android      | yes|
| getLastUpdateTime                    | 获取应用最后更新时间（毫秒）。                                                                                                                     | Promise<number>  | No | Android      | yes |
| getMacAddress                        | 获取网络适配器 MAC 地址。                                                                                                                     | Promise<string>  | No | IOS/Android/visionOS      | no |
| getManufacturer                      | 获取设备制造商。                                                                                                                            | Promise<string>  | No | IOS/Android/visoinOS      | yes |
| getManufacturerSync                  | 获取设备制造商。                                                                                                                            | string  | No | IOS/Android/visoinOS      | yes |
| getMaxMemory                         | 返回虚拟机将尝试使用的最大内存量（字节）。                                                                                                               | Promise<number>  | No | Android/Windows/Web      | no |
| getModel                             | 获取设备型号。                                                                                                                             | string  | No | IOS/Android      | yes |
| getPowerState                        | 获取设备电源状态，包括电池电量、是否正在充电以及系统是否处于低功耗模式。                                                                                                | Promise<object>  | No | IOS/Android/Windows/Web/visionOS      | yes |
| getProduct                           | 整体产品名称。                                                                                                                             | Promise<string>  | No | Android      | yes |
| getPreviewSdkInt                     | 预发布 SDK 的开发人员预览修订版。                                                                                                                 | Promise<number>  | No | Android      | no |
| getReadableVersion                   | 获取应用程序人类可读版本（等同于 getVersion() + '.' + getBuildNumber()）。                                                                            | string  | No | IOS/Android/Windows/visionOS      | yes |
| getSerialNumber                      | 获取设备序列号。在绝大多数情况下会是 'unknown'，除非您拥有特权应用并且知道自己在做什么。                                                                                   | Promise<string>  | No | Android/Windows      | no |
| getSecurityPatch                     | 用户可见的安全补丁级别。                                                                                                                        | Promise<string>  | No | Android      | yes |
| getSystemAvailableFeatures           | 返回 Android 上可用的系统功能列表。                                                                                                              | Promise<string[]>  | No | Android      | no |
| getSystemName                        | 获取设备操作系统名称。                                                                                                                         | string  | No | IOS/Android/Windows/visoinOS      | yes |
| getSystemVersion                     | 获取设备操作系统版本。                                                                                                                         | string  | No | IOS/Android/Windows/visoinOS      | yes |
| getTags                              | 描述构建的逗号分隔标签。                                                                                                                        | Promise<string>  | No | Android      | no |
| getType                              | 构建类型。                                                                                                                               | Promise<string>  | No | Android      | yes |
| getTotalDiskCapacity                 | 获取完整磁盘存储空间大小的方法（字节），考虑根文件系统和数据文件系统的计算。                                                                                              | Promise<number>  | No | Android      | no |
| getTotalDiskCapacityOld              | 获取完整磁盘存储空间大小的旧实现方法（字节）。                                                                                                             | Promise<number>  | No | Android      | no |
| getTotalMemory                       | 获取设备总内存（字节）。                                                                                                                        | Promise<number>  | No | IOS/Android/Web/visionOS      | no |
| getUniqueId                          | 获取设备唯一 ID。在 Android 上，当前与此模块中的相同。                                                                                                   | Promise<string>  | No | IOS/Android/Windows/visionOS      | no |
| getUsedMemory                        | 获取应用程序内存使用量（字节）。                                                                                                                    | Promise<string>  | No | IOS/Android/Windows/Web/visionOs      | yes |
| getUserAgent                         | 获取设备用户代理。                                                                                                                           | Promise<string>  | No | IOS/Android/Web/visionOs      | no |
| getUserAgentSync                     | 获取设备用户代理。                                                                                                                           | string  | No | Android/Web     | no |
| getVersion                           | 获取应用程序版本。请注意版本字符串是设备/操作系统格式的，可能包含任何额外数据（如构建编号等）。如果您想确定版本格式，可以使用正则表达式从返回的版本字符串中获取所需部分。                                               | string  | No | IOS/Android/Windows/visionOS      | yes |
| getBrightness                        | 获取设备主屏幕的当前亮度级别。目前仅限 iOS。返回 0.0 到 1.0 之间的数字（包含）。                                                                                     | Promise<number>  | No | IOS     | no |
| hasGms                               | 判断设备是否支持 Google 移动服务。                                                                                                               | Promise<boolean>  | No | Android      | yes |
| hasHms                               | 判断设备是否支持华为移动服务。                                                                                                                     | Promise<boolean>  | No | Android      | yes |
| hasNotch                             | 判断设备是否有刘海屏。                                                                                                                         | boolean  | No | IOS/Android/Windows/visionOS      | no |
| hasDynamicIsland                     | 判断设备是否有动态岛。                                                                                                                         | boolean  | No | IOS/Android/Windows/visionOS      | no |
| hasSystemFeature                     | 判断设备是否有特定的系统功能。                                                                                                                     | Promise<boolean>  | No | Android      | no |
| isAirplaneMode                       | 判断设备是否处于飞行模式。                                                                                                                       | Promise<boolean>  | No | Android/ Web     | no |
| isBatteryCharging                    | 判断电池是否正在充电。                                                                                                                         | Promise<boolean>  | No | IOS/Android/Windows/Web/visionOS      | yes |
| isEmulator                           | 判断应用程序是否在模拟器中运行。                                                                                                                    | Promise<boolean>  | No | IOS/Android/Windows/visionOS      | no |
| isKeyboardConnected                  | 判断设备是否连接了键盘。                                                                                                                        | Promise<boolean>  | No | Windows      | partially(Only supports asynchronous retrieval) |
| isLandscape                          | 判断设备是否当前处于横屏模式。                                                                                                                     | Promise<boolean>  | No | IOS/Android/Windows/visionOs      | yes |
| isLocationEnabled                    | 允许访问用户的位置信息。                                                                                                                        | Promise<boolean>  | No | IOS/Android/Web/visionOS      | yes |
| isMouseConnected                     | 判断设备是否连接了鼠标。                                                                                                                        | Promise<boolean>  | No | Windows   | partially(Only supports asynchronous retrieval) |
| isHeadphonesConnected                | 判断设备是否连接了耳机。                                                                                                                        | Promise<boolean>  | No | IOS/Android/visionOS      | yes |
| isWiredHeadphonesConnected           | 判断设备是否连接了有线耳机。                                                                                                                      | Promise<boolean>  | No | IOS/Android/visionOS      | yes |
| isBluetoothHeadphonesConnected       | 判断设备是否连接了蓝牙耳机。                                                                                                                      | Promise<boolean>  | No | IOS/Android/visionOS      | yes |
| isPinOrFingerprintSet                | 判断是否为设备设置了 PIN 码或指纹。                                                                                                                | Promise<boolean>  | No | IOS/Android/Windows/visoinOs      | yes |
| isTablet                             | 判断设备是否为平板电脑。                                                                                                                        | boolean  | No | IOS/Android/Windows/visoinOs      | yes |
| isLowRamDevice                       | 判断设备是否内存不足。                                                                                                                         | boolean  | No | Android      | yes |
| isDisplayZoomed                      | 判断用户是否将显示缩放更改为放大模式。                                                                                                                 | boolean  | No | IOS     | no |
| isTabletMode                         | 判断设备是否处于平板模式。                                                                                                                       | Promise<boolean>  | No | Windows     | no |
| supported32BitAbis                   | 设备支持 32 位 ABI。                                                                                                                      | Promise<string[]>  | No | Windows     | yes |
| supported64BitAbis                   | 设备支持 64 位 ABI。                                                                                                                      | Promise<string[]>  | No | Windows     | yes |
| supportedAbis                        | 设备支持的 ABI。                                                                                                                          | Promise<string[]>  | No | IOS/Android/Windows/visoinOS     | yes|
| syncUniqueId                         | 此方法专为 iOS 设计，它将 uniqueId 与 IDFV 同步或设置新的随机字符串。在 iOS 上使用 DeviceUID uid 标识符。在其他平台上，仅调用此模块中的 getUniqueId()。                             | Promise<string>  | No | IOS/visionOS     | no |
| getSupportedMediaTypeList            | 此方法获取支持的媒体编解码器列表。                                                                                                                   | Promise<string[]>  | No | IOS/Android      | yes |
| getStartupTime<sup>14.0.4+</sup>     | 获取当前应用程序进程启动的时间，单位为毫秒。                                                                                                              | Promise\<number\> | Yes | iOS/Android/visionOS | yes |



## 5. 遗留问题

- [ ] getDeviceId()接口harmony暂不支持[issue#8](https://github.com/react-native-oh-library/react-native-device-info/issues/8)
- [ ] getDeviceToken()接口harmony暂不支持[issue#9](https://github.com/react-native-oh-library/react-native-device-info/issues/9)
- [ ] getFingerprint()接口harmony暂不支持 [issue#10](https://github.com/react-native-oh-library/react-native-device-info/issues/10)
- [ ] getFreeDiskStorage()接口harmony暂不支持 [issue#11](https://github.com/react-native-oh-library/react-native-device-info/issues/11)
- [ ] getFreeDiskStorageOld()接口harmony暂不支持 [issue#12](https://github.com/react-native-oh-library/react-native-device-info/issues/12)
- [ ] getInstallReferrer()接口harmony暂不支持 [issue#13](https://github.com/react-native-oh-library/react-native-device-info/issues/13)
- [ ] getMacAddress()接口harmony暂不支持 [issue#14](https://github.com/react-native-oh-library/react-native-device-info/issues/14)
- [ ] getMaxMemory()接口harmony暂不支持 [issue#15](https://github.com/react-native-oh-library/react-native-device-info/issues/15)
- [ ] getSerialNumber()接口harmony暂不支持 [issue#16](https://github.com/react-native-oh-library/react-native-device-info/issues/16)
- [ ] getTags()接口harmony暂不支持 [issue#17](https://github.com/react-native-oh-library/react-native-device-info/issues/17)
- [ ] getTotalDiskCapacity()接口harmony暂不支持 [issue#18](https://github.com/react-native-oh-library/react-native-device-info/issues/18)
- [ ] getTotalDiskCapacityOld()接口harmony暂不支持 [issue#19](https://github.com/react-native-oh-library/react-native-device-info/issues/19)
- [ ] getTotalMemory()接口harmony暂不支持 [issue#20](https://github.com/react-native-oh-library/react-native-device-info/issues/20)
- [ ] getUniqueId()接口harmony暂不支持 [issue#21](https://github.com/react-native-oh-library/react-native-device-info/issues/21)
- [ ] syncUniqueId()接口harmony暂不支持 [issue#22](https://github.com/react-native-oh-library/react-native-device-info/issues/22)
- [ ] getUserAgent()接口harmony暂不支持 [issue#23](https://github.com/react-native-oh-library/react-native-device-info/issues/23)
- [ ] getUserAgentSync()接口harmony暂不支持 [issue#24](https://github.com/react-native-oh-library/react-native-device-info/issues/24)
- [ ] hasNotch()接口harmony暂不支持 [issue#25](https://github.com/react-native-oh-library/react-native-device-info/issues/25)
- [ ] hasDynamicIsland()接口harmony暂不支持 [issue#26](https://github.com/react-native-oh-library/react-native-device-info/issues/26)
- [ ] hasSystemFeature()接口harmony暂不支持 [issue#27](https://github.com/react-native-oh-library/react-native-device-info/issues/27)
- [ ] isEmulator()接口harmony暂不支持 [issue#28](https://github.com/react-native-oh-library/react-native-device-info/issues/28)
- [ ] isDisplayZoomed()接口harmony暂不支持 [issue#29](https://github.com/react-native-oh-library/react-native-device-info/issues/29)
- [ ] getBrightness()接口harmony暂不支持 [issue#30](https://github.com/react-native-oh-library/react-native-device-info/issues/30)
- [ ] isAirplaneMode()接口harmony暂不支持 [issue#69](https://github.com/react-native-oh-library/react-native-device-info/issues/69)

## 6. 其他

## 7. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-device-info/react-native-device-info/blob/master/LICENSE) ，请自由地享受和参与开源。

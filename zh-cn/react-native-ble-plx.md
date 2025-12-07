> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"><code>react-native-ble-plx</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dotintent/react-native-ble-plx">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dotintent/react-native-ble-plx/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-ble-plx)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 3.2.0-0.0.4@deprecated | [@react-native-oh-tpl/react-native-ble-plx Releases(deprecated)](https://github.com/react-native-oh-library/react-native-ble-plx/releases) | 0.72         |
| 3.2.1      | [@react-native-ohos/react-native-ble-plx Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-ble-plx/releases) | 0.72       |
| 3.5.1      | [@react-native-ohos/react-native-ble-plx Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-ble-plx/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-ble-plx
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-ble-plx
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Button, Alert } from 'react-native';
import {
  BleErrorCode,
  BleManager,
  Device,
  Service,
  Descriptor,
  type DeviceId,
  type UUID,
  type Characteristic,
} from 'react-native-ble-plx';
import Toast from 'react-native-simple-toast';

class BLEServiceInstance {
  manager: BleManager
  device: Device | null

  constructor() {
    this.device = null
    this.manager = new BleManager()
  }

  scanDevices = async (onDeviceFound: (device: Device) => void, UUIDs: UUID[] | null = null) => {
    this.manager.startDeviceScan(UUIDs, null, (error: any, device: any) => {
      if (error) {
        console.error(error.message)
        this.manager.stopDeviceScan()
        return
      }
      if (device) {
        onDeviceFound(device)
      }
    })
  }

  connectToDevice = (deviceId: DeviceId) =>
    new Promise<Device>((resolve, reject) => {
      this.manager.stopDeviceScan()
      this.manager
        .connectToDevice(deviceId)
        .then((device: any) => {
          this.device = device
          resolve(device)
        })
        .catch((error: any) => {
          if (error.errorCode === BleErrorCode.DeviceAlreadyConnected && this.device) {
            resolve(this.device)
          } else {
            console.error(error.message)
            reject(error)
          }
        })
    })
}

class App extends React.Component {
  deviceName: string = 'time'
  serviceUuid: string = '00001820-0000-1000-8000-00805F9B34FB'
  characteristicUuid: string = '00001820-0000-1000-8000-00805F9B34FB'
  descriptorUuid: string = '00002903-0000-1000-8000-00805F9B34FB'

  device?: Device;

  service?: Service;

  characteristic?: Characteristic;

  descriptor?: Descriptor;

  showLog(text: string) {
    Toast.show(text, Toast.SHORT);
    console.log('bleplx showLog:' + text);
  };

  ble = new BLEServiceInstance((text: string) => {
    this.showLog(text);
  });

  enable = () => {
    this.ble.manager.enable();
    Toast.show('enable', Toast.SHORT)
  }

  disable = () => {
    this.ble.manager.disable();
    Toast.show('disable', Toast.SHORT)
  }

  startScan = () => {
    console.log('startScan');
    Toast.show('开始扫描外设', Toast.LONG)
    this.ble.manager.startDeviceScan(null, null, (error: any, device: any) => {
      if (device?.name) {
        console.log('bleplx: startScan result:' + device?.name);
      }
      if (device?.name?.toLocaleLowerCase() == this.deviceName) {
        if (this.device != null) {
          return
        }
        this.device = device;
        this.stopDeviceScan();
        Alert.alert(
          '发现外设:' + device.name,
          '是否连连接？',
          [
            {
              text: '取消',
              style: 'cancel'
            },
            {
              text: '连接',
              onPress: () => {
                this.connectToDevice();
              },
              style: 'destructive'
            }
          ]
        )
      }
    })
  }

  stopDeviceScan = () => {
    this.ble.manager.stopDeviceScan();
    Toast.show('stopDeviceScan', Toast.SHORT)
  }

  connectToDevice = () => {
    if (this.device == null) {
      console.log('bleplx: 没有找到指定的连接设备');
      return;
    }

    console.log('bleplx: 开始连接：' + this.device.id);
    Toast.show('开始连接外设', Toast.LONG)
    this.ble.manager.connectToDevice(this.device.id).then((device: any) => {
      Toast.show('连接成功', Toast.SHORT);
      console.log('bleplx:连接成功:' + JSON.stringify(device));
    }).catch((error: any) => {
      Toast.show('连接失败', Toast.SHORT);
      console.log('bleplx:连接失败：' + error.message);
    });
  }

  render() {
    return (
      <View>
        <Button title='enable' onPress={this.enable}>enable</Button>
        <Button title='disable' onPress={this.disable}>disable</Button>
        <Button title='startScan' onPress={this.startScan}>startScan</Button>
        <Button title='stopDeviceScan' onPress={this.stopDeviceScan}>stopDeviceScan</Button>
      </View>
    )
  }
}

export default App;
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-ble-plx@3.2.1，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-ble-plx@3.2.1，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

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

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-ble-plx": "file:../../node_modules/@react-native-ohos/react-native-ble-plx/harmony/rn_bleplx.har"
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

### 3.配置 CMakeLists 和引入 BlePlxPackage

> 若使用的是 <= 3.2.0-0.0.4 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-ble-plx/src/main/cpp" ./rn_bleplx)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_ble_plx)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "BlePlxPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<BlePlxPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 BlePlxPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {BlePlxPackage} from '@react-native-ohos/react-native-ble-plx/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BlePlxPackage(ctx)
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 权限要求

- 由于此库涉及蓝牙系统控制功能，使用对应接口时则需要配置对应的权限，权限需配置在entry/src/main目录下module.json5文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要normal权限：ohos.permission.ACCESS_BLUETOOTH。

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| createClient(restoreStateIdentifier?: string)  | creat client         | void | No | iOS/Android      | yes |
| destroyClient()  | remove client         | Promise<void> | No | iOS/Android      | yes |
| cancelTransaction(transactionId: string)  | cancel transcation         | Promise<void> | No | iOS/Android      | no |
| setLogLevel(logLevel: string)  | set log level         | Promise<Object> | No | iOS/Android      | no |
| logLevel()  | show log level         | Promise<Object> | No | iOS/Android      | no |
| enable(transactionId: string)  | can get transaction Id       | Promise<void> | No | iOS/Android      | yes |
| disable(transactionId: string)  | cannot get transaction Id        | Promise<void> | No | iOS/Android      | yes |
| state()  | bluetooth state         | Promise<Object> | No | iOS/Android      | yes |
| startDeviceScan(filteredUUIDs: string[], options: Object)  | start scan device         | Promise<void>| No | iOS/Android      | yes |
| stopDeviceScan()  | stop scan device         | Promise<void> | No | iOS/Android      | yes |
| requestConnectionPriorityForDevice(deviceId: string, connectionPriority: number,transactionId: string) | request connect priority device         | Promise<Object> | No | iOS/Android      | no |                                     
| readRSSIForDevice(deviceId: string, transactionId: string)  | read RSSI device        | Promise<Object> | No | iOS/Android      | yes |
| requestMTUForDevice(deviceId: string, mtu: number, transactionId: string)  | request MTU device         | Promise<Object> | No | iOS/Android      | yes |
| devices(deviceIdentifiers: string[])  | identify devices         | Promise<Object[]> | No | iOS/Android      | yes |
| connectedDevices(serviceUUIDs: string[])  | connect devices         | Promise<Object[]> | No | iOS/Android      | yes |
| connectToDevice(deviceId: string, options?: Object)  | option to connect device         | Promise<Object> | No | iOS/Android      | yes |
| cancelDeviceConnection(deviceId: string)  | cancel device connection        | Promise<Object> | No | iOS/Android      | yes |
| isDeviceConnected(deviceId: string)  | connected device         | Promise<boolean> | No | iOS/Android      | yes |
| discoverAllServicesAndCharacteristicsForDevice(deviceId: string, transactionId: string)  | discover all device service and characteristics         | Promise<Object> | No | iOS/Android      | yes |
| servicesForDevice(deviceId: string)  | device service         | Promise<Object[]> | No | iOS/Android      | yes |
| characteristicsForDevice(deviceId: string, serviceUUID: string)  | device characteristics         | Promise<Object[]> | No | iOS/Android      | yes |
| characteristicsForService(serviceIdentifier: number)  | service characteristics         | Promise<Object[]> | No | iOS/Android      | yes |
| descriptorsForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string): Promise<Object[]>  | device descriptors         | Promise<Object[]> | No | iOS/Android      | yes |
| descriptorsForService(serviceIdentifier: number, characteristicUUID: string)  | service descriptors       | Promise<Object[]> | No | iOS/Android        | yes |
| descriptorsForCharacteristic(characteristicIdentifier: number)   |descriptors identifier device characteristic         | Promise<Object[]> | No | iOS/Android      | yes |
| readCharacteristicForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, transactionId: string)  | read device characteristic         | Promise<Object> | No | iOS/Android      | yes |
| readCharacteristicForService(serviceIdentifier: number, characteristicUUID: string,transactionId: string)  | read  service charcteristic        | Promise<Object> | No | iOS/Android      | yes |
| readCharacteristic(characteristicIdentifier: number, transactionId: string)  | read identifier characteristic      | Promise<Object> | No | iOS/Android      | yes |
| writeCharacteristicForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, valueBase64: string,response: boolean, transactionId: string)  | write device  characteristic      | Promise<Object> | No | iOS/Android      | yes |
| writeCharacteristicForService(serviceIdentifier: number, characteristicUUID: string, valueBase64: string,response: boolean, transactionId: string)  | write service characteristic       | Promise<Object> | No | iOS/Android      | yes |
| writeCharacteristic(characteristicIdentifier: number, valueBase64: string, response: boolean,transactionId: string)  |  write  identifier characteristic         | Promise<Object> | No | iOS/Android      | yes |
| monitorCharacteristicForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string,transactionId: string)  | monitor device  characteristic        | Promise<void> | No | iOS/Android      | yes |
| monitorCharacteristicForService(serviceIdentifier: number, characteristicUUID: string,transactionId: string)  | monitor service  characteristic         | Promise<void> | No | iOS/Android      | yes |
| monitorCharacteristic(characteristicIdentifier: number, transactionId: string)  | monitor identifier characteristic        | Promise<void> | No | iOS/Android      | yes |
| readDescriptorForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, descriptorUUID: string,transactionId: string)  | read device descriptor      | Promise<Object> | No | iOS/Android      | yes |
| readDescriptorForService(serviceIdentifier: number, characteristicUUID: string, descriptorUUID: string,transactionId: string)  | read service descriptor         | Promise<Object> | No | iOS/Android      | yes |
| readDescriptorForCharacteristic(characteristicIdentifier: number, descriptorUUID: string,transactionId: string)  | read identifier characteristic descriptor          | Promise<Object> | No | iOS/Android      | yes |
| readDescriptor(descriptorIdentifier: number, transactionId: string)  | read identifier descriptor         | Promise<Object> | No | iOS/Android      | yes |
| writeDescriptorForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, descriptorUUID: string,valueBase64: string, transactionId: string)  | write device descriptor        | Promise<Object> | No | iOS/Android      | yes |
| writeDescriptorForService(serviceIdentifier: number, characteristicUUID: string, descriptorUUID: string,valueBase64: string, transactionId: string)  | write service descriptor         | Promise<Object> | No | iOS/Android      | yes |
| writeDescriptorForCharacteristic(characteristicIdentifier: number, descriptorUUID: string, valueBase64: string,transactionId: string)  | write identifier characteristic descriptor          | Promise<Object> | No | iOS/Android      | yes |
| writeDescriptor(descriptorIdentifier: number, valueBase64: string, transactionId: string)  | write identifier descriptor        | Promise<Object> | No | iOS/Android      | yes |

## 遗留问题

- [ ] cancelTransaction(transactionId: string)接口harmony暂不支持: [issue#2](https://github.com/react-native-oh-library/react-native-ble-plx/issues/2)
- [ ] setLogLevel(logLevel: string)接口harmony暂不支持: [issue#3](https://github.com/react-native-oh-library/react-native-ble-plx/issues/3)
- [ ] logLevel()接口harmony暂不支持: [issue#4](https://github.com/react-native-oh-library/react-native-ble-plx/issues/4)
- [ ] requestConnectionPriorityForDevice(deviceId: string, connectionPriority: number,transactionId: string)接口harmony暂不支持: [issue#5](https://github.com/react-native-oh-library/react-native-ble-plx/issues/5)

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/dotintent/react-native-ble-plx/blob/master/LICENSE) ，请自由地享受和参与开源。

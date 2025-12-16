> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>mixpanel-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mixpanel/mixpanel-react-native/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mixpanel/mixpanel-react-native/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/mixpanel-react-native)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本           | 发布信息                                                     | 支持RN版本 |
|-----------------| ------------------------------------------------------------ | ---------- |
| <= 3.0.5-0.1.1@deprecated  | [@react-native-oh-tpl/mixpanel-react-native Releases(deprecated)](https://github.com/react-native-oh-library/mixpanel-react-native/releases) | 0.72       |
| 3.0.6           | [@react-native-ohos/mixpanel-react-native Releases](https://github.com/react-native-oh-library/mixpanel-react-native/releases)                | 0.72       |
| 3.2.0           |  [@react-native-ohos/mixpanel-react-native Releases](https://github.com/react-native-oh-library/mixpanel-react-native/releases)               | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/mixpanel-react-native
```


#### **yarn**

```bash
yarn add @react-native-ohos/mixpanel-react-native
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
> [!WARNING] 代码使用的 token值 需要在[ mixpanel 官网](https://mixpanel.com)上的项目设置中获取，事件发送后需要在[ mixpanel 官网](https://mixpanel.com)的项目分析中查看相应的数据

```js
import React from 'react';
import {Button, SafeAreaView} from 'react-native';
import {Mixpanel} from 'mixpanel-react-native';

const trackAutomaticEvents = false;
const token = 'Your Project Token';
const mixpanel = new Mixpanel(token, trackAutomaticEvents);
mixpanel.init();

export default function MixpanelDemo() {
    return (
    <SafeAreaView>
        <Button
    title="Select Premium Plan"
    onPress={() => mixpanel.track('Plan Selected', {Plan: 'Premium'})}
/>
    </SafeAreaView>
);
}
```


## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~3.2.0                               |  No              |  0.77     |
| ~3.0.6                              |  Yes             |  0.72     |
| <= 3.0.5-0.1.1@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

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
"@react-native-ohos/mixpanel-react-native": "file:../../node_modules/@react-native-ohos/mixpanel-react-native/harmony/mixpanel.har"
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

### 3.配置 CMakeLists 和引入 MixpanelPackage

> 若使用的是 <= 3.0.5-0.1.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/mixpanel-react-native/src/main/cpp" ./mixpanel)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_mixpanel)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "MixpanelPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<MixpanelPackage>(ctx)
}
```

### 4.在 ArkTs 侧引入 MixpanelPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { MixpanelPackage } from '@react-native-ohos/mixpanel-react-native/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new MixpanelPackage(ctx)
  ];
}
```
</details>

## 运行

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


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### Mixpanel

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- |----------| -------- |-------------------|
| init(): void; | 初始化Mixpanel实例<br /><br />3.0.5：参数为(<br/>    optOutTrackingDefault = DEFAULT_OPT_OUT,<br/>    superProperties = {},<br/>    serverURL = "https://api.mixpanel.com"<br/>  )<br />3.1.3：参数为(<br/>    optOutTrackingDefault = DEFAULT_OPT_OUT,<br/>    superProperties = {},<br/>    serverURL = "https://api.mixpanel.com",<br/>    useGzipCompression = false<br/>  )<br />新增参数useGzipCompression，HarmonyOS 暂未支持该参数 | function | yes      | iOS,Android | yes            |
| setServerURL(serverURL: string): void; | 设置Mixpanel API请求使用的基本URL | function | no       | iOS,Android | yes               |
| setLoggingEnabled(loggingEnabled: boolean): void; | 是否开启日志记录 | function | no       | iOS,Android | yes               |
| setFlushOnBackground(flushOnBackground: boolean): void; | 当应用程序在iOS上进入后台时,允许启用或禁用Mixpanel是否刷新事件 | function | no       | iOS | no                |
| setUseIpAddressForGeolocation(useIpAddressForGeolocation: boolean): void; | 是否发送ip作为地理定位的依据 | function | no       | iOS,Android | yes               |
| setFlushBatchSize(flushBatchSize: number): void; | 设置单个网络请求发送到mixpanel的事件数量 | function | no       | iOS,Android | yes               |
| hasOptedOutTracking(): Promise<boolean>; | 获取用户是否选择退出追踪 | function | no       | iOS,Android | yes               |
| optInTracking(): void; | 用户已选择跟踪 | function | no       | iOS,Android | yes               |
| optOutTracking(): void; | 用户已选择退出跟踪 | function | no       | iOS,Android | yes               |
| identify(distinctId: string): Promise<void>; | 将来的track调用都由以下的用户标识关联 | function | no       | iOS,Android | yes               |
| alias(alias: string, distinctId: string): void; | 创建一个映射，将新的标识与用户的原始distinct_id关联起来 | function | no       | iOS,Android | yes               |
| track(eventName: string, properties?: MixpanelProperties): void; | 发送事件 | function | yes      | iOS,Android | yes               |
| getPeople(): People; | 获取People实例 | function | no       | iOS,Android | yes               |
| trackWithGroups(eventName: string, properties?: MixpanelProperties, groups?: MixpanelProperties): void; | 追踪特定群体事件 | function | no       | iOS,Android | no                |
| setGroup(groupKey: string, groupID: MixpanelType): void; | 设置用户所属的组 | function | no       | iOS,Android | no                |
| getGroup(groupKey: string, groupID: MixpanelType): MixpanelGroup; | 获取Group实例 | function | no       | iOS,Android | yes               |
| addGroup(groupKey: string, groupID: MixpanelType): void; | 添加组 | function | no       | iOS,Android | no                |
| removeGroup(groupKey: string, groupID: MixpanelType): void; | 移除组 | function | no       | iOS,Android | no                |
| deleteGroup(groupKey: string, groupID: MixpanelType): void; | 删除组 | function | no       | iOS,Android | no                |
| registerSuperProperties(properties: MixpanelProperties): void; | 注册全局属性，这些属性通用于所有用户 | function | no       | iOS,Android | yes               |
| registerSuperPropertiesOnce(properties: MixpanelProperties): void; | 注册全局属性，这些属性通用于所有用户，但不会覆盖已有的属性 | function | no       | iOS,Android | yes               |
| unregisterSuperProperty(propertyName: string): void; | 删除指定的注册的全局属性 | function | no       | iOS,Android | yes               |
| getSuperProperties(): Promise<MixpanelProperties>; | 获取注册的全局属性 | function | no       | iOS,Android | yes               |
| clearSuperProperties(): void; | 删除所有注册的全局属性 | function | no       | iOS,Android | yes               |
| timeEvent(eventName: string): void; | 发送计时事件 | function | no       | iOS,Android | yes               |
| eventElapsedTime(eventName: string): Promise<number>; | 获取指定事件的当前计时 | function | no       | iOS,Android | yes               |
| reset(): void; | 重置用户的相关信息 | function | no       | iOS,Android | yes               |
| getDistinctId(): Promise<string>; | 获取唯一标识 | function | no       | iOS,Android | yes               |
| getDeviceId(): Promise<string>; | 获取设备标识 | function | no       | iOS,Android | yes               |
| flush(): void; | 推送所有事件及用户信息到服务器 | function | no       | iOS,Android | yes               |


#### People

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set(prop: string, to: MixpanelType): void; | 设置用户的属性 | function | no | iOS,Android | yes |
| set(properties: MixpanelProperties): void; | 设置用户的属性 | function | no | iOS,Android | yes |
| setOnce(prop: string, to: MixpanelType): void; | 设置用户的属性，但不会覆盖已有的属性 | function | no | iOS,Android | yes |
| setOnce(properties: MixpanelProperties): void; | 设置用户的属性，但不会覆盖已有的属性 | function | no | iOS,Android | yes |
| increment(prop: string, by: number): void; | 增加用户的某个数值属性的值，通常用于计数或累计某个行为的发生次数。 | function | no | iOS,Android | yes |
| increment(properties: MixpanelProperties): void; | 增加用户的某个数值属性的值，通常用于计数或累计某个行为的发生次数。 | function | no | iOS,Android | yes |
| append(name: string, value: MixpanelType): void; | 添加用户的某个属性的值，将值追加到用户属性中 | function | no | iOS,Android | yes |
| union(name: string, value: Array<MixpanelType>): void; | 添加用户的某个属性的值，如果属性已经存在值，则新添加的数据会与现有值合并 | function | no | iOS,Android | yes |
| remove(name: string, value: MixpanelType): void; | 删除用户的某个属性的指定值 | function | no | iOS,Android | yes |
| unset(name: string): void; | 删除用户的某个属性及属性的值 | function | no | iOS,Android | yes |
| trackCharge(charge: number, properties: MixpanelProperties): void; | 追踪用户的交易 | function | no | iOS,Android | yes |
| clearCharges(): void; | 永久清除用户的历史交易记录 | function | no | iOS,Android | yes |
| deleteUser(): void; | 从人员分析中永久删除用户 | function | no | iOS,Android | yes |


#### MixpanelGroup

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set(prop: string, to: MixpanelType): void; | 设置组的属性 | function | no | iOS,Android | no |
| setOnce(prop: string, to: MixpanelType): void; | 设置组的属性，但不会覆盖已有的属性 | function | no | iOS,Android | no |
| unset(prop: string): void; | 删除组的属性 | function | no | iOS,Android | no |
| remove(name: string, value: MixpanelType): void; | 删除组的属性的值，删除指定值 | function | no | iOS,Android | no |
| union(name: string, value: MixpanelType): void; | 添加组的属性的值，将值合并到组属性中 | function | no | iOS,Android | no |


## 遗留问题
- [ ] 部分接口暂未开发：[issue#5](https://github.com/react-native-oh-library/mixpanel-react-native/issues/5)
- [ ] init接口中useGzipCompression参数暂未支持：[issue#14](https://github.com/react-native-oh-library/mixpanel-react-native/issues/14)

## 其他

## 开源协议

本项目基于 [Apache License2.0](https://github.com/mixpanel/mixpanel-react-native/blob/master/LICENSE.md) ，请自由地享受和参与开源。


> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-safe-module</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lelandrichardson/react-native-safe-module">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lelandrichardson/react-native-safe-module/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-safe-module)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| version | Package Name                                       |Repository | Release               |  RN version |
| ---------- | ------------------------------------------------------------ | -------|--------|---------- |
| 1.2.0     | @react-native-oh-tpl/react-native-safe-module | [Github](https://github.com/react-native-oh-library/react-native-safe-module)  | [Github Releases](https://github.com/react-native-oh-library/react-native-safe-module/releases)|0.72       |
| 1.3.0    | @react-native-ohos/react-native-safe-module  | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-module)  | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-safe-module/releases)| 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

#### **npm**

```bash
#0.72
npm install @react-native-oh-tpl/react-native-safe-module

#0.77
npm install @react-native-ohos/react-native-safe-module
```

#### **yarn**

```bash
#0.72
yarn add @react-native-oh-tpl/react-native-safe-module

#0.77
yarn add @react-native-ohos/react-native-safe-module
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View } from 'react-native';
import SafeModule from 'react-native-safe-module';

const App = () => {
  const NativeLottieView = SafeModule.component({
    viewName: 'LottieAnimationView',
    mockComponent: View,
  });
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <NativeLottieView
        style={{backgroundColor: 'red', width: 100, height: 100}}
      />
    </View>
  );
};

export default App;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.2.0      | [@react-native-oh-tpl/react-native-safe-module Releases](https://github.com/react-native-oh-library/react-native-safe-module/releases) | 0.72       |
| 1.2.1      | [@react-native-ohos/react-native-safe-module Releases]()     | 0.77       |

在以下版本验证通过

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


Name | Description | Type | Required | Platform | HarmonyOS   Support
-- | -- | -- | -- | -- | --
SafeModule.create(options) | 创建Module | Object | Yes | iOS/Android | Yes |  


**options**：SafeModule.create(options) 方法的参数

| Name                                                      | Description                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| options.moduleName                                             |  需在 NativeModules 命名空间中查找的模块名称或名称数组。                                                                                      | string/Array<string> | Yes       | iOS/Android      | Yes               |
| options.mock                                              | 该原生模块的模拟实现                                        | mixed | Yes       | iOS/Android      | Yes               |
| options.getVersion                                | 用于获取原生模块版本的函数。仅在指定了覆盖配置且未在原生模块中导出 VERSION 属性时需要设置。默认值为 x => x.VERSION。VERSION.                                                                                                  | (module) => string/number | No       | iOS/Android      | Yes                |
| options.overrides                                 | 版本号与对应属性/方法覆写实现的映射表。若被覆写的属性或方法为函数类型，该函数将在 SafeModule.create(...) 执行期间被调用，并接收两个参数：原始模块中该属性的初始值及原始模块本身。此函数的返回值将被设置为 SafeModule.create(...) 的返回结果。                                                                                                  | [version: string]: mixed   | No       | iOS/Android      | Yes               |
| options.isEventEmitter                              | 标识原生模块是否为 EventEmitter 的标记。若启用，会将 EventEmitter 实例挂载至生成模块的 emitter 属性。默认值为 false。                                                                                                  | bool   | No       | iOS/Android      | Yes                |


## 遗留问题


## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/lelandrichardson/react-native-safe-module/blob/master/LICENSE) ，请自由地享受和参与开源。
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-overflow</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/entria/react-native-view-overflow">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/entria/react-native-view-overflow/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-view-overflow)

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                     | 支持RN版本 |
| ----------- | ------------------------------------------------------------ | ---------- |
| 0.0.5 | [@react-native-oh-tpl/react-native-view-overflow Releases](https://github.com/react-native-oh-library/react-native-view-overflow/releases) | 0.72       |
| 0.1.0   | [@react-native-ohos/react-native-view-overflow Releases]()   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-view-overflow

# 0.77
npm install @react-native-ohos/react-native-view-overflow
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-view-overflow

# 0.77
yarn add @react-native-ohos/react-native-view-overflow
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {View} from 'react-native';

import ViewOverflow from 'react-native-view-overflow';

export function ViewOverflowDemo() {
  return (
  <View style={{height: '100%', backgroundColor: 'white', padding: 10}}>

    <View style={{width: 200, height: 100, backgroundColor: 'red'}}>
      <ViewOverflow style={{width: 100, height: 50, backgroundColor: 'blue'}}>
          <ViewOverflow style={{width: 50, height: 25, backgroundColor: 'skyblue', left: 60, top: 30}}>
            <View style={{backgroundColor: 'yellow', height: '100%', left: 20, top: 10}} />
          </ViewOverflow>
      </ViewOverflow>
    </View>

  </View>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## 属性
[!TIP] 该库作为容器组件使用同View组件，可以让子控件溢出到父布局之外展示的效果；使用公共属性即可，不涉及私有属性及api方法。

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/entria/react-native-view-overflow/blob/master/LICENSE) ，请自由地享受和参与开源。

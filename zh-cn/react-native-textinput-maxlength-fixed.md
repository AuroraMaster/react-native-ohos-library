<p align="center">
  <h1 align="center"> <code>react-native-textinput-maxlength-fixed</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/2017398956/react-native-textinput-maxlength-fixed">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/2017398956/react-native-textinput-maxlength-fixed/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed)

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：
| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.1.2     | [@react-native-oh-tpl/react-native-textinput-maxlength-fixed Releases](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed/releases) | 0.72       |
| 0.2.0     | [@react-native-ohos/react-native-textinput-maxlength-fixed Releases]()     | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-textinput-maxlength-fixed
# 0.77
npm install @react-native-ohos/react-native-textinput-maxlength-fixed
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-textinput-maxlength-fixed
# 0.77
yarn add @react-native-ohos/react-native-textinput-maxlength-fixed
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import * as React from 'react';

import { StyleSheet, View, Text, TextInput } from 'react-native';
import { multiply } from 'react-native-textinput-maxlength-fixed';

export default function App() {
  const [result, setResult] = React.useState<number | undefined>();

  React.useEffect(() => {
    multiply(3, 7).then(setResult);
  }, []);

  return (
    <View style={styles.container}>
      <Text>Result: {result}</Text>
      <TextInput maxLength={6} style={styles.textInput} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
  textInput: {
    borderColor: 'gray',
    borderWidth: 1,
    padding: 16,
    width: 300,
  },
});
```

## 使用 Codegen

> [!TIP] V0.2.0 for RN0.77 不需要执行 Codegen。

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
> [!TIP] 引入原生代码之前请确认IDE版本，5.0.3.810及其之后的版本需要在harmony工程中的hvigor-config.json5文件中新增如下配置以解决路径过长导致的编译报错问题
> "properties":{
          "ohos.nativeResolver":false
}
目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

- V0.1.2

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-textinput-maxlength-fixed": "file:../../node_modules/@react-native-oh-tpl/react-native-textinput-maxlength-fixed/harmony/textinput_maxlength_fixed.har"
  }
```

- V0.2.0

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-textinput-maxlength-fixed": "file:../../node_modules/@react-native-ohos/react-native-textinput-maxlength-fixed/harmony/textinput_maxlength_fixed.har"
  }
```

点击右上角的 `sync` 按钮

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.在 ArkTs 侧引入 RNTextinputMaxlengthFixedPackage

打开 `entry/src/main/ets/rn/RNPackagesFactory.ts`，添加：

```diff
import { RNPackageContext, RNPackage } from '@rnoh/react-native-openharmony';
import { SampleTurboModulePackage } from '../TurboModule/SampleTurboModulePackage';
import { ViewPagerPackage } from '@react-native-oh-tpl/react-native-pager-view/ts';
// V0.1.2
+import { RNTextinputMaxlengthFixedPackage } from "@react-native-oh-tpl/react-native-textinput-maxlength-fixed/ts";
// V0.2.0
+import { RNTextinputMaxlengthFixedPackage } from "@react-native-ohos/react-native-textinput-maxlength-fixed/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SampleTurboModulePackage(ctx),
    new ViewPagerPackage(ctx),
+    new RNTextinputMaxlengthFixedPackage(ctx),
  ];
}
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH：0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| multiply  | 计算两个数字的乘积 | number  | no | All      | yes |

## 遗留问题
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-textinput-maxlength-fixed/blob/main/LICENSE) ，请自由地享受和参与开源。

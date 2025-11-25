> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localization-settings</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jakex7/react-native-localization-settings">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jakex7/react-native-localization-settings/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

本项目基于 [react-native-localization-settings](https://github.com/jakex7/react-native-localization-settings) 开发。

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-localization-settings`，具体版本所属关系如下：

| Version     | Package Name                                      | Repository         | Release                    |Support RN version|
|-------------| ------------------------------------------------- | ------------------ | -------------------------- |-------------------|
| 1.0.2-0.0.1 | @react-native-oh-tpl/react-native-localization-settings | [Github](https://github.com/react-native-oh-library/react-native-localization-settings) | [Github Releases](https://github.com/react-native-oh-library/react-native-localization-settings/releases) |0.72       |
| 1.2.1       | @react-native-ohos/react-native-localization-settings   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localization-settings) | [GitCode Releases]() |0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash

# 0.72
npm install @react-native-oh-tpl/react-native-localization-settings

# 0.77
npm install @react-native-ohos/react-native-localization-settings
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-localization-settings

# 0.77
yarn add @react-native-ohos/react-native-localization-settings
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 本示例依赖i18next react-i18next库，参照[react-i18next文档](https://react.i18next.com/guides/quick-start)进行引入

```js
import * as React from "react";
import { StyleSheet, View, Text, Button } from "react-native";
import { ReactNativeLanguageDetector } from "react-native-localization-settings";
import i18next from "i18next";
import { initReactI18next, useTranslation } from "react-i18next";

i18next
  .use(ReactNativeLanguageDetector)
  .use(initReactI18next)
  .init({
    resources: {
      en: {
        translation: {
          key: "hello world in english",
        },
      },
      pl: {
        translation: {
          key: "hello world in polish",
        },
      },
      fr: {
        translation: {
          key: "hello world in french",
        },
      },
    },
    fallbackLng: "en",
    interpolation: {
      escapeValue: false,
    },
    compatibilityJSON: "v3",
  });

export default function App() {
  const { t } = useTranslation();

  return (
    <View style={styles.container}>
      <Text>{t("key")}</Text>
      <Button
        title={"change to pl"}
        onPress={() => i18next.changeLanguage("pl-PL")}
      />
      <Button
        title={"change to en"}
        onPress={() => i18next.changeLanguage("en-US")}
      />
      <Button
        title={"change to fr"}
        onPress={() => i18next.changeLanguage("fr-FR")}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
});
```


## 使用 Codegen

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

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

- 0.72

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-localization-settings": "file:../../node_modules/@react-native-oh-tpl/react-native-localization-settings/harmony/localization_settings.har"
  }
```

- 0.77

```json
"dependencies": {
"@rnoh/react-native-openharmony": "file:../react_native_openharmony",
"@react-native-ohos/react-native-localization-settings": "file:../../node_modules/@react-native-ohos/react-native-localization-settings/harmony/localization_settings.har"
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

### 3.在 ArkTs 侧引入 RNLocalizationSettingsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNLocalizationSettingsPackage} from '@react-native-oh-tpl/react-native-localization-settings/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNLocalizationSettingsPackage(ctx)
  ];
}
```

### 4.运行

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

1. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] 在设置改变语言之前，确保手机系统添加相应语言

| Name                       | Description | Type     | Required | Platform    | HarmonyOS Support |
| -------------------------- |-------------| -------- | -------- | ----------- | ----------------- |
| I18nLanguageDetectorModule | i18next语言检测器 | function | no       | iOS/Android | yes               |
| getLanguage()              | 获取当前语言      | function | no       | iOS/Android | yes               |
| setLanguage()              | 设置当前语言      | function | no       | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jakex7/react-native-localization-settings/blob/main/LICENSE) ，请自由地享受和参与开源。

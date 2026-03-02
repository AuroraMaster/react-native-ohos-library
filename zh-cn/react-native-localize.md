> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localize</code></h1>
</p>
<p align="center">
    <a href="https://github.com/zoontek/react-native-localize">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-localize/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-localize)


请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------- |
| <= 3.1.0-0.0.1@deprecated | @react-native-oh-tpl/react-native-localize | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-localize) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-localize/releases) | 0.72 |
| 3.1.0 | @react-native-ohos/react-native-localize | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localize) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/releases) | 0.72 |
| 3.4.2                        | @react-native-ohos/react-native-localize       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localize) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/releases) | 0.77 |
| 3.6.2                        | @react-native-ohos/react-native-localize       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localize) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/releases) | 0.82 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-localize
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-localize
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```jsx
import * as React from "react";
import {
  I18nManager,
  Platform,
  SafeAreaView,
  ScrollView,
  StyleSheet,
  Text,
  View,
} from "react-native";
import * as RNLocalize from "react-native-localize";

const styles = StyleSheet.create({
  safeArea: {
    backgroundColor: "white",
    flex: 1,
  },
  container: {
    padding: 16,
    alignItems: "flex-start",
  },
  block: {
    marginBottom: 16,
    alignItems: "flex-start",
  },
  name: {
    textDecorationLine: "underline",
    fontWeight: "500",
    marginBottom: 8,
    color: "black",
  },
  value: {
    textAlign: "left",
    color: "black",
  },
});

const Line = ({ name, value }: { name: string; value: unknown }) => (
  <View style={styles.block}>
    <Text style={styles.name}>{name}</Text>
    <Text style={styles.value}>{JSON.stringify(value, null, 2)}</Text>
  </View>
);
function LocalizeDemo() {
  return (
    <SafeAreaView style={styles.safeArea}>
      <ScrollView contentContainerStyle={styles.container}>
        <Line name="RNLocalize.getLocales()" value={RNLocalize.getLocales()} />

        <Line name="RNLocalize.getCurrencies()" value={RNLocalize.getCurrencies()} />

        <Line name="RNLocalize.getCountry()" value={RNLocalize.getCountry()} />

        <Line name="RNLocalize.getCalendar()" value={RNLocalize.getCalendar()} />

        <Line name="RNLocalize.getTimeZone()" value={RNLocalize.getTimeZone()} />

        <Line name="RNLocalize.uses24HourClock()" value={RNLocalize.uses24HourClock()} />

        <Line
          name="RNLocalize.findBestLanguageTag(['en-US', 'en', 'fr', 'zh'])"
          value={RNLocalize.findBestLanguageTag(["en-US", "en", "fr", 'zh'])}
        />
      </ScrollView>
    </SafeAreaView>
  );
}
export default LocalizeDemo;
```

## 使用 Codegen
Version > @react-native-ohos/react-native-localize@3.1.0，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

**注意：** 0.77 不需要执行 Codegen。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~3.6.2                               |  No              |  0.82     |
| ~3.4.2                               |  No              |  0.77     |
| ~3.1.0                              |  Yes             |  0.72     |
| <= 3.1.0-0.0.1@deprecated            |  No              |  0.72     |

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
    "@react-native-ohos/react-native-localize": "file:../../node_modules/@react-native-ohos/react-native-localize/harmony/rn_localize.har"
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

### 3. 配置 CMakeLists 和引入 RNLocalizePackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-localize/src/main/cpp" ./rn_localize)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_localize)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "RNLocalizePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<RNLocalizePackage>(ctx)
}
```

### 4.在 ArkTs 侧引入 RNLocalizePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNLocalizePackage } from '@react-native-ohos/react-native-localize/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNLocalizePackage(ctx)
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

在以下版本验证通过：

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;
3. RNOH: 0.82.1; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0 Release; ROM:6.0.0.858;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name                                     | Description                                                  | Required | Platform | HarmonyOS Support |
| ---------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| getLocales()                             | 返回用户首选的语言环境，按顺序排列。                | No       | All      | yes               |
| getNumberFormatSettings()                | 返回数字格式设置。                          | No       | All      | yes               |
| getCurrencies()                          | 返回用户首选的货币代码，按顺序排列。         | No       | All      | yes               |
| getCountry()                             | 返回用户当前的国家代码（基于设备语言环境，而不是位置）。 | No       | All      | yes               |
| getCalendar()                            | 返回用户首选的日历格式。                  | No       | All      | yes               |
| getTemperatureUnit()                     | 返回用户首选的温度单位。                 | No       | All      | No                |
| getTimeZone()                            | 返回用户首选的时区（基于设备设置，而不是位置）。 | No       | All      | yes               |
| uses24HourClock()                        | 如果用户喜欢24小时制则返回true，否则返回false。 | No       | All      | yes               |
| usesMetricSystem()                       | 如果用户喜欢公制单位则返回true，否则返回false。 | No       | All      | No                |
| usesAutoDateAndTime()                    | 告诉手机是否启用了自动日期和时间设置。仅限Android | No       | Android  | No                |
| usesAutoTimeZone()                       | 告诉手机是否启用了自动时区设置。仅限Android | No       | Android  | No                |
| findBestLanguageTag()                    | 返回最佳的语言标签及其阅读方向 | No       | All      | yes               |
| openAppLanguageSettings<sup>3.4.2+</sup> | 打开应用语言设置              | No       | Android  | No                |
| ServerLanguagesProvider() | 服务端语言配置提供者组件，用于在服务端渲染场景下注入语言列表              | No       | Web  | No                |
| useLocalize() | 返回本地化相关的 API 集合              | No       | All  | yes                |

## 遗留问题
- [ ]  HarmonyOS 侧无法获取温度及长度单位[issue#2](https://github.com/react-native-oh-library/react-native-localize/issues/2)
- [ ]  SSR（Web 端专属）相关特性（`ServerLanguagesProvider`/`useLocalize` 的 SSR 逻辑）暂不支持鸿蒙系统[issue#13](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/issues/13)
- [ ]  react-native-localize 的 Expo 配置插件暂不支持鸿蒙系统，鸿蒙系统未集成 Expo 的构建/配置体系[issue#14](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/issues/14)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/zoontek/react-native-localize/blob/master/LICENSE) ，请自由地享受和参与开源。
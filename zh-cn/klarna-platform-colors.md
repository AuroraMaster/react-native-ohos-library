> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@klarna/platform-colors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/klarna-incubator/platform-colors">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/klarna-incubator/platform-colors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/platform-colors)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                     | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 0.4.0-0.0.1@deprecated  | [@react-native-oh-tpl/platform-colors Releases(deprecated)](https://github.com/react-native-oh-library/platform-colors/releases) | 0.72       |
| 0.4.1             | [@react-native-ohos/platform-colors Releases](https://gitcode.com/openharmony-sig/rntpc_platform-colors/releases)   | 0.72       |
| 0.5.0             | [@react-native-ohos/platform-colors Releases](https://gitcode.com/openharmony-sig/rntpc_platform-colors/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/platform-colors
```

#### **yarn**

```bash
yarn add @react-native-ohos/platform-colors
```

生成资源文件：

```bash
npx @react-native-ohos/platform-colors
```

> [!TIP] 第一次运行该命令时，它将提示您要为哪些平台生成文件，确定后将在工程根目录创建具有以下格式的文件：

```js
// platform-colors.config.js
module.exports = {
  prefix: "rnpc_",
  colors: {
    background: {
      light: "#000000",
      dark: "#ffffff",
    },
    text: "#696969",
    accent: "pink",
    contrasted: "#FFF0F5",
  },
  javascript: {
    typescript: true,
    outputDirectory: "src/colors/",
  },
  ios: {
    outputDirectory: "ios/app_name/Images.xcassets/",
  },
  android: {
    outputDirectory: "android/app/src/main/res/",
  },
  harmony: {
    outputDirectory: "harmony/AppScope/resources/",
  },
};
```

现在检查你的 android, ios 和 harmony 文件夹。您应该在每个平台上都有您的颜色定义。

当您需要修改颜色资源时，只需更改`colors`配置，然后再次执行以下命令即可生成最新的颜色资源。

资源文件生成后需要将harmony/AppScope/resources/内的生成的2个color文件复制到harmony工程的对应目录下。

```bash
npx @react-native-ohos/platform-colors
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React from "react";
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  Image,
  ColorValue,
} from "react-native";
import { resolveColor, resolveColorSync } from "@klarna/platform-colors";
import { PlatformColor } from "react-native";

const accent = PlatformColor("rnpc_accent");

export const PlatformColorsTest = () => {
  const [asyncColor, setAsyncColor] = React.useState<ColorValue | undefined>(
    undefined
  );
  const syncColor = resolveColorSync(accent);
  React.useEffect(() => {
    resolveColor(accent).then((color) => setAsyncColor(color));
  }, []);

  return (
    <View style={{ top: 48, flex: 1 }}>
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={styles.scrollView}
      >
        <ColorRow
          label="show color of id: rnpc_background"
          color={PlatformColor("rnpc_background")}
        />
        <ColorRow
          label="get 'ohos_id_color_warning' color by resolveColor api"
          color={asyncColor}
        />
        <ColorRow
          label="get 'ohos_id_color_warning' color by resolveColorSync api"
          color={syncColor}
        />
      </ScrollView>
    </View>
  );
};
const ColorRow = ({ label, color }: { label: string; color?: ColorValue }) => (
  <View style={styles.colorRow}>
    <View
      style={[
        styles.colorSample,
        {
          backgroundColor: color,
        },
      ]}
    />
    <Text style={styles.colorLabel}>{label}</Text>
  </View>
);
const styles = StyleSheet.create({
  scrollView: {
    flex: 1,
    paddingHorizontal: 10,
  },
  colorRow: {
    paddingHorizontal: 10,
    marginVertical: 10,
    flexDirection: "row",
    alignItems: "center",
  },
  colorSample: {
    width: 50,
    height: 50,
    borderRadius: 25,
    marginRight: 10,
    shadowOpacity: 0.2,
    shadowColor: "#999",
    shadowRadius: 1,
    shadowOffset: { width: 0, height: 0 },
  },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink       | RN框架版本           |
|--------------------------------------|-----------------------|----------------------|
| ~0.5.0                               |  No                   |  0.77                |
| ~0.4.1                               |  Yes                  |  0.72                |
| <= 0.4.0-0.0.1@deprecated            |  No                   |  0.72                |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

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
    "@react-native-ohos/platform-colors": "file:../../node_modules/@react-native-ohos/platform-colors/harmony/platform_colors.har"
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

### 3.在 ArkTs 侧引入 RNPlatformColorsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNPlatformColorsPackage } from '@react-native-ohos/platform-colors/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNPlatformColorsPackage(ctx)
  ];
}
```

### 4.配置 CMakeLists 和引入 RNPlatformColorsPackage

> 若使用的是 <= 0.4.0-0.0.1 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/platform-colors/src/main/cpp" ./platform_colors)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_platform_colors)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNPlatformColorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNPlatformColorsPackage>(ctx)
    };
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

## 属性

### platform-colors.config.js 配置文件属性

> 详情见 [@klarna/platform-colors 文档](https://github.com/klarna-incubator/platform-colors)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name       | Description                                                                                                                                                                           | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| prefix     | We prefix all colors with rnpc\_ by default, you can override that with this option.                                                                                                  | String | No       | iOS/Android | Yes               |
| colors     | An object where the key is the color name, and the value is either a string or an object containing light and optionally highContrastLight, dark & highContrastDark properties.       | Object | Yes      | iOS/Android | Yes               |
| ios        | An object containing outputDirectory which should be an .xcassets directory.                                                                                                          | Object | No       | iOS/Android | Yes               |
| android    | An object containing outputDirectory which should be an Android res directory.                                                                                                        | Object | No       | iOS/Android | Yes               |
| harmony    | An object containing outputDirectory which should be an Harmony res directory.                                                                                                        | Object | No       | --          | Yes               |
| css        | An object containing outputDirectory and filename which should be a directory where you store CSS files and if you want to change the default filename from colors.css.               | Object | No       | iOS/Android | Yes               |
| javascript | An object containing outputDirectory which should be a directory where you store your Type/JavaScript files and typescript which is set to true if you want the output in TypeScript. | Object | No       | iOS/Android | Yes               |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                          | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------ | -------- | -------- | ----------- | ----------------- |
| resolveColorSync | Getting hex value from dynamic color | Function | No       | iOS/Android | Yes               |
| resolveColor     | Getting hex value from dynamic color | Function | No       | iOS/Android | Yes               |

### resolveColorSync

```js
resolveColorSync(color: ColorValue): string;
```

| Name  | Description                                                                                                        | Type             | Required | Platform    | HarmonyOS Support |
| ----- | ------------------------------------------------------------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| color | Color value obtained through the PlatformColor interface.<br>Example: resolveColorSync(PlatformColor('coloeName')) | React.ColorValue | Yes      | iOS/Android | Yes               |

### resolveColor

```js
resolveColor(color: ColorValue): Promise<string>;
```

| Name  | Description                                                                                                    | Type             | Required | Platform    | HarmonyOS Support |
| ----- | -------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| color | Color value obtained through the PlatformColor interface.<br>Example: resolveColor(PlatformColor('coloeName')) | React.ColorValue | Yes      | iOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/klarna-incubator/platform-colors/blob/master/LICENSE) ，请自由地享受和参与开源。

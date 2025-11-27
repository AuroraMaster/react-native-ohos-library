模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localization</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/stefalda/ReactNativeLocalization">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/stefalda/ReactNativeLocalization/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/ReactNativeLocalization)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-localization`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| 2.3.2@deprecated | [@react-native-oh-tpl/react-native-localization Releases(deprecated)](https://github.com/react-native-oh-library/react-native-localization/releases) | 0.72       |
| 2.3.2            | [@react-native-oh-tpl/react-native-localization Releases](https://github.com/react-native-oh-library/ReactNativeLocalization/releases) | 0.72       |
| 2.4.0            | [@react-native-ohos/react-native-localization Releases]()    | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-localization
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-localization
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import Localize from 'react-native-localization';

// 定义本地化内容
const strings = new Localize({
  en: {//英语
    welcome: 'Welcome',
    question: 'I\'d like some {0} and {1}, or just {0}',
    bread: 'bread',
    butter: 'butter',
    greeting: 'Hello, {0}!   ',
    currentlanguage: 'Current Language',
    availableLanguages: 'Available Languages',
    interfaceLanguage: 'The System Language'
  },
  fr: {//法语
    welcome: 'Bienvenue',
    question: 'Je voudrais un peu de {0} et {1}, ou juste {0}',
    bread: 'pain',
    butter: 'beurre',
    greeting: 'Bonjour, {0}!',
    currentlanguage: 'Langue actuelle',
    availableLanguages: 'Langues disponibles',
    interfaceLanguage: 'Langue du système'
  },
  bo: {//藏语
    welcome: 'བསྐུལ་མཁན།',
    question: 'ང་ལུས་འདི་ལས། {0} དང། {1} ཡང་ཡིན། གང་ཡིན་ནི། {0}',
    bread: 'བཀྲུངས',
    butter: 'བརྡེན',
    greeting: 'བཀའ་བདག་ {0}!',
    currentlanguage: 'ད་དུས་ལག་འཁྱེར།',
    availableLanguages: 'ད་དུས་ལག་འཁྱེར་སྒྲིགས།',
    interfaceLanguage: 'རྩམ་གཞི་སྒྲིག་ལེན་དེ་རྒྱལ་སྤོད་'
  },
  zh: {//中文
    welcome: '欢迎',
    question: '我想要一些{0}和{1}，或者只要{0}',
    bread: '面包',
    butter: '黄油',
    greeting: '你好, {0}!',
    currentlanguage: '当前语言',
    availableLanguages: '当前可用语言列表',
    interfaceLanguage: '当前系统语言'
  },
});

export function LocalizationDemo() {
  // getLanguage API
  const [language, setLanguage] = useState(strings.getLanguage());
  const changeLanguage = (lang: string) => {
    // setLanguage API
    strings.setLanguage(lang);
    setLanguage(strings.getLanguage());
  };

  return (
    <View style={styles.screen}>
      <View style={{ height: 180, justifyContent: 'space-between', marginBottom: 30 }}>
        <Button
          color="#144400"
          title="切换成中文"
          onPress={() => changeLanguage('zh')}
        />
        <Button
          color="#841584"
          title="切换成法语"
          onPress={() => changeLanguage('fr')}
        />
        <Button
          color="#645555"
          title="切换成英语"
          onPress={() => changeLanguage('en')}
        />
        <Button
          color="#241595"
          title="切换成藏语"
          onPress={() => changeLanguage('bo')}
        />
      </View>

      <Text style={styles.text}>
        {strings.welcome}
      </Text>
      <Text style={styles.text}>
        {/* formatString API */}
        {strings.formatString(strings.question, strings.bread, strings.butter)}
      </Text>
      <Text style={styles.text}>
        {strings.currentlanguage}: {language}
      </Text>
      {/* getAvailableLanguages API */}
      <Text style={styles.text}>
        {strings.availableLanguages}: {strings.getAvailableLanguages().join(', ')}
      </Text>
      {/* getInterfaceLanguage API */}
      <Text style={styles.text}>
        {strings.interfaceLanguage}: {strings.getInterfaceLanguage()}
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: 'white'
  },

  screen: {
    flex: 1,
    padding: 4,
    paddingTop: 10,
    backgroundColor: 'black',
    marginHorizontal: 4,
    marginVertical: 8,
    paddingHorizontal: 8,
  },
});
```
## 使用 Codegen

Version >= @react-native-ohos/react-native-localization@2.3.3，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-localization@2.3.3，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@react-native-ohos/react-native-localization": "file:../../node_modules/@react-native-ohos/react-native-localization/harmony/react_localization.har"
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


### 3.在 ArkTs 侧引入 RNReactLocalizationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNReactLocalizationPackage } from '@react-native-ohos/react-native-localization/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNReactLocalizationPackage(ctx),
  ];
}
```

### 4.配置 CMakeLists 和引入 LocalizationPackage

> [!TIP] 0.77 需要执行 

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-localization/src/main/cpp" ./localization)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_localization)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "LocalizationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<LocalizationPackage>(ctx),
    };
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

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                      | Description                                                  | Type     | Required |  Platform   | HarmonyOS Support |
| ----------------------------------------- | :----------------------------------------------------------- | -------- | :------: | :---------: | :---------------: |
| setLanguage(languageCode)                 | 手动强制设置为特定语言                                       | void     |   yes    | iOS/Android |        yes        |
| getLanguage()                             | 获取当前显示的语言                                           | string   |   yes    | iOS/Android |        yes        |
| getInterfaceLanguage()                    | 获取当前设备的系统界面语言                                   | string   |   yes    | iOS/Android |        yes        |
| formatString()                            | 格式化传入的字符串，用其他参数替换字符串中的占位符。         | string   |   yes    | iOS/Android |        yes        |
| getAvailableLanguages()                   | 获取在构造函数中传入的语言数组                               | string[] |   yes    | iOS/Android |        yes        |
| getString(key: string, language?: string) | 根据键（key）获取对应的字符信息。如果指定了 `language`，则获取特定语言的字符信息。 | string   |   yes    | iOS/Android |        yes        |
| setContent(props: any)                    | 替换 `NamedLocalization` 对象的内容，而无需重新实例化该对象。 | void     |   yes    | iOS/Android |        yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/stefalda/ReactNativeLocalization/blob/master/LICENSE) ，请自由地享受和参与开源。
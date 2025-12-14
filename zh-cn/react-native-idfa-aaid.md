> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-idfa-aaid</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-idfa-aaid)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=1.2.0-0.0.1@deprecated | [@react-native-oh-tpl/react-native-idfa-aaid Releases(deprecated)](https://github.com/react-native-oh-library/react-native-idfa-aaid/releases) | 0.72       |
| 1.2.1      | [@react-native-ohos/react-native-idfa-aaid Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-idfa-aaid/releases)                        | 0.72       |
| 1.3.0      | [@react-native-ohos/react-native-idfa-aaid Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-idfa-aaid/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-idfa-aaid
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-idfa-aaid
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```
import React, { useEffect } from 'react';
import type { PropsWithChildren } from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
} from 'react-native';

import {
  Colors,
  DebugInstructions,
  Header,
  LearnMoreLinks,
  ReloadInstructions,
} from 'react-native/Libraries/NewAppScreen';

import ReactNativeIdfaAaid, {
  AdvertisingInfoResponse,
} from 'react-native-idfa-aaid';

type SectionProps = PropsWithChildren<{
  title: string;
}>;

function Section({ children, title }: SectionProps): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

  useEffect(() => {
    ReactNativeIdfaAaid.getAdvertisingInfo()
      .then((res: AdvertisingInfoResponse) =>
        console.log('Advertising info', res)
      )
      .catch(err => {
        console.log(err);
      });
  }, []);

  return (
    <View style={styles.sectionContainer}>
      <Text
        style={[
          styles.sectionTitle,
          {
            color: isDarkMode ? Colors.white : Colors.black,
          },
        ]}>
        {title}
      </Text>
      <Text
        style={[
          styles.sectionDescription,
          {
            color: isDarkMode ? Colors.light : Colors.dark,
          },
        ]}>
        {children}
      </Text>
    </View>
  );
}

function App(): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

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
        <Header />
        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
          }}>
          <Section title="Step One">
            Edit <Text style={styles.highlight}>App.tsx</Text> to change this
            screen and then come back to see your edits.
          </Section>
          <Section title="See Your Changes">
            <ReloadInstructions />
          </Section>
          <Section title="Debug">
            <DebugInstructions />
          </Section>
          <Section title="Learn More">
            Read the docs to discover what to do next:
          </Section>
          <LearnMoreLinks />
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: '600',
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: '400',
  },
  highlight: {
    fontWeight: '700',
  },
});

export default App;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                           | 是否支持autolink | RN框架版本 |
|---------------------------|-----------------|------------|
| ~1.3.0                    |  No              |  0.77     |
| ~1.2.1                    |  Yes             |  0.72     |
| <= 1.2.0-0.0.1@deprecated |  No              |  0.72     |

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
    "@react-native-ohos/react-native-idfa-aaid": "file:../../node_modules/@react-native-ohos/react-native-idfa-aaid/harmony/getOaid.har"
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


### 3.在 ArkTs 侧引入 GetOaidPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
  
+  import { GetOaidPackage } from "@react-native-ohos/react-native-idfa-aaid/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GetOaidPackage(ctx),
  ];
}
```
### 4.配置 CMakeLists 和引入 IdfaAaidPackage

> 若使用的是 <=1.2.0-0.0.1 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-idfa-aaid/src/main/cpp" ./getOaid)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_getOaid)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "IdfaAaidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<IdfaAaidPackage>(ctx)
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

### 权限要求

[!TIP] "ohos.permission.APP_TRACKING_CONSENT"，"ohos.permission.APP_TRACKING_CONSENT"权限等级为<B>normal</B>，授权方式为<B>user_grant</B>[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

#### 在 entry 目录下的module.json5中添加权限
在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

+    "requestPermissions":[
+      {
+        "name" : "ohos.permission.APP_TRACKING_CONSENT",
+        "reason": "$string:page_show",
+        "usedScene": {
+          "abilities": [
+            "FormAbility"
+          ],
+          "when":"always"
+        }
+     }
+    ]
  }
}
```
#### 在 entry 目录下添加申请权限的原因

在 `YourProject/entry/src/main/resources/base/element/string.json`补上配置

```diff
...
{
  "string": [
+    {
+      "name": "page_show",
+      "value": "page from npm package"
+    }
  ]
}
```
当前的 HarmonyOS 版本中，当用户请求 APP_TRACKING_CONSENT 权限时，系统并不会弹出授权提示框，而是默认禁止该应用获取 OAID 的权限.为了引导用户手动开启此权限，应用端可以自主设计并展示弹窗，指引用户前往设置界面进行相应的操作。此外，应用应严格按照 user_grant 权限的申请流程来提交请求，具体申请细节请参考：
[user_grant （用户授权）权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/permissions-for-all-V5#user_grant%E7%94%A8%E6%88%B7%E6%8E%88%E6%9D%83%E6%9D%83%E9%99%90%E5%88%97%E8%A1%A8)

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getAdvertisingInfo  |检查权限，申请权限，获取OAID。        | Function  | yes | iOS/Android      | yes |
| getAdvertisingInfoAndCheckAuthorization  | 该功能与上述相同，用于保持移植的一致性。        | Function  | no | iOS/Android      | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE) ，请自由地享受和参与开源。
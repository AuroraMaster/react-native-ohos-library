> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-email-link</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tschoffelen/react-native-email-link">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/tschoffelen/react-native-email-link/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-email-link)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=1.15.0-0.0.2@deprecated | [@react-native-oh-tpl/react-native-email-link Releases(deprecated)](https://github.com/react-native-oh-library/react-native-email-link/releases) | 0.72       |
| 1.15.1     | [@react-native-ohos/react-native-email-link Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-email-link/releases) | 0.72       |
| 1.16.2     | [@react-native-ohos/react-native-email-link Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-email-link/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-email-link
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-email-link
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import {
  SafeAreaView,
  View,
  StyleSheet,
  Text,
  StatusBar,
  Button,
} from "react-native";
import {
  getEmailClients,
  openInbox,
  openComposer,
} from "react-native-email-link";

export function EmailLinkExample() {
  const [emailClients, setEmailClients] = useState(
    "点击getEmailClients按钮获取邮箱信息"
  );
  return (
    <SafeAreaView style={styles.container}>
      <View style={styles.wrapper}>
        <Text style={styles.text}>{emailClients}</Text>
        <Button
          title="getEmailClients"
          onPress={async () => {
            let clients = await getEmailClients();
            setEmailClients(JSON.stringify(clients));
          }}
        />

        <Button
          title="openInbox-without-app"
          onPress={() => {
            openInbox();
          }}
        />

        <Button
          title="openInbox-with-app"
          onPress={() => {
            openInbox({
              app: "mail",
            });
          }}
        />

        <Button
          title="openComposer-without-app"
          onPress={() => {
            openComposer({
              to: "support@example.com",
              cc: "cc@example.com",
              bcc: "bcc@example.com",
              subject: "I have a question",
              body: "Hi, can you help me with...",
            });
          }}
        />

        <Button
          title="openComposer-with-app"
          onPress={() => {
            openComposer({
              app: "mail",
              to: "support@example.com",
              cc: "cc@example.com",
              bcc: "bcc@example.com",
              subject: "I have a question",
              body: "Hi, can you help me with...",
            });
          }}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight,
  },
  item: {
    backgroundColor: "#f9c2ff",
    justifyContent: "center",
    marginVertical: 8,
    marginHorizontal: 16,
    padding: 20,
  },
  title: {
    fontSize: 24,
  },
  wrapper: {
    height: 200,
  },
  text: {
    marginBottom: 20,
    color: "white",
    textAlign: "center",
  },
});
```
## 使用 Codegen


本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|------------------|-----------|
| ~1.16.2                              |  No              |  0.77     |
| ~1.15.1                              |  Yes             |  0.72     |
| <=1.15.0-0.0.2@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-ohos/react-native-email-link": "file:../../node_modules/@react-native-ohos/react-native-email-link/harmony/email_link.har"
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


### 3.配置 CMakeLists和引入 RNOHGeneratedPackage

> 若使用的是 <= 1.15.0-0.0.2 版本，请跳过本章。

本库将codegen生成的代码内置在库文件中。

打开 entry/src/main/cpp/CMakeLists.txt，添加：
```diff
{
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")

set(RNOH_CPP_DIR "${OH_MODULE_DIR}/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")

add_compile_definitions(WITH_HITRACE_SYSTRACE)
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-email-link/src/main/cpp" ./email_link)

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")
add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC rnoh_email_link)
}
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "EmailLinkGeneratedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+     std::make_shared<EmailLinkRNOHGeneratedPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNEmailLinkPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNEmailLinkPackage} from '@react-native-ohos/react-native-email-link/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNEmailLinkPackage(ctx)
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

| Name              | Description                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `openInbox`       | 直接打开设备上默认邮件客户端的收件箱                                     | function | No       | All      | yes               |
| `openComposer`    | 用于打开一个新的电子邮件创作界面，允许用户直接从应用程序创建电子邮件 | function | No       | All      | yes               |
| `getEmailClients` | 获取设备上安装的所有受支持的邮件客户端应用程序的列表。                          | function | No       | All      | yes               |

**openInbox 方法参数**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `title` | 操作表或意图顶部的文本 | string | no | All | no |
| `message` | 行动表标题下的子文本 | string | no | iOS | no |
| `cancelLabel` | 操作表最后一个按钮的文本| string | no | iOS | no |
| `removeText` | 如果为真，则不会在操作表或意图上方显示文本。默认值为false | boolean | no | All | no |
| `defaultEmailLabel` | 操作表第一个按钮的文本 | function | no | iOS | no |
| `newTask` | 如果为真，电子邮件Intent将在新的Android任务中启动。否则，Intent将在当前任务中启动 | boolean | no | Android | no |

**openComposer 方法参数**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `app` | 打开的应用程序| string | no | All | yes |
| `title` | 操作表或意图顶部的文本 | string | no | All | no |
| `message` | 行动表标题下的子文本 | string | no | iOS | no |
| `cancelLabel` | 操作表最后一个按钮的文本 | string | no | iOS | no |
| `removeText` | 如果为真，则不会在操作表或意图上方显示文本。默认值为false | boolean | no | All | no |
| `defaultEmailLabel` | 操作表第一个按钮的文本 | function | no | iOS | no |
| `to` | 收件人的电子邮件地址 | string | no | All | yes |
| `cc` | 电子邮件抄送 | string | no | All | yes |
| `bcc` | 电子邮件密送 | string | no | All | yes |
| `subject` | 电子邮件主题| string | no | All | yes |
| `body` | 电子邮件正文 | string | no | All | yes |
| `encodeBody` | 将encodeURIComponent应用于电子邮件正文 | boolean | no | All | yes |

## 遗留问题

- [ ] 目前只支持 harmonyOS 系统自带邮箱，本库支持邮箱均未适配harmonyOS Next。[issues#5](https://github.com/react-native-oh-library/react-native-email-link/issues/5)

## 其他

- title、message、cancelLabel、 removeText、defaultEmailLabel、newTask属性暂不支持，与iOS表现一致。[issue#141](https://github.com/tschoffelen/react-native-email-link/issues/141)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/tschoffelen/react-native-email-link/blob/master/LICENSE) ，请自由地享受和参与开源。

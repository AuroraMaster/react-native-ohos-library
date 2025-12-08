> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-quick-base64</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/craftzdog/react-native-quick-base64">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/craftzdog/react-native-quick-base64/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-quick-base64)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <=2.1.2-1.0.1@deprecated | [@react-native-oh-tpl/react-native-quick-base64 Releases(deprecated)](https://github.com/react-native-oh-library/react-native-quick-base64/releases) | 0.72       |
| 2.1.3             | [@react-native-ohos/react-native-quick-base64 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-quick-base64/releases)   | 0.72       |
| 2.2.0             | [@react-native-ohos/react-native-quick-base64 Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-quick-base64/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-quick-base64
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-quick-base64
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { Text, View, TextInput, ScrollView, StyleSheet, Button } from 'react-native';

import { byteLength, btoa, atob, toByteArray, fromByteArray, getNative, trimBase64Padding, shim } from '@react-native-ohos/react-native-quick-base64';
type FuncBase64ToArrayBuffer = (
  data: string,
  removeLinebreaks?: boolean
) => ArrayBuffer
type FuncBase64FromArrayBuffer = (
  data: string | ArrayBuffer,
  urlSafe?: boolean
) => string


interface NativeModule {
  base64FromArrayBuffer: FuncBase64FromArrayBuffer | undefined;
  base64ToArrayBuffer: FuncBase64ToArrayBuffer | undefined;
}

const PALETTE = {
  REACT_CYAN_LIGHT: 'hsl(193, 95%, 68%)',
  REACT_CYAN_DARK: 'hsl(193, 95%, 30%)',
};

export function QuickBase64Test() {
  // Test string to base64 conversion
  const [textTobase64, onChangeTextToBase64] = useState('');

  const [base64ToTextLength, onChangeBase64TextLength] = useState(0);

  const [base64ToText, onChangeBase64Text] = useState('');

  const [byteArray, onChangeByteArray] = useState(new Uint8Array(0));

  const [byteArrayRemove, onChangeByteArrayRemove] = useState(new Uint8Array(0));

  const [fbArrayBase64Str, onChangeFbArrayBase64Str] = useState('');

  const [fbArrayBase64StrUrlSafe, onChangeFbArrayBase64StrUrlSafe] = useState('');

  const [testShimBtoA, onChangeTestShimBtoA] = useState(''); // String to base64

  const [testShimAtoB, onChangeTestShimAtoB] = useState(''); // Base64 to string

  const [nativeModule, onChangeNativeModule] = useState<NativeModule>({
    base64FromArrayBuffer: undefined,
    base64ToArrayBuffer: undefined
  });

  const [nativeBFABText, onChangeNBFABText] = useState('');

  const [nativeBFABTextUrlSafe, onChangeNBFABTextUrlSafe] = useState('');

  const [nativeBTABText, onChangeNBTABText] = useState(new Uint8Array(0));

  const [nativeBTABTextRemoveLinebreaks, onChangeNBTABTextRemoveLinebreaks] = useState(new Uint8Array(0));

  const [trimBase64PaddingText, onChangeTrimBase64PaddingText] = useState('');

  const byArray = new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]);
  // Click event: string to base64
  const onPressBtoA = (text: string) => {
    let b64 = btoa(text);
    console.log(`String to base64 ${b64}`);
    onChangeTextToBase64(b64)
  }

  const [testText, onChangeTestText] = React.useState('');

  // Click event: base64 to string
  const onPressAtoB = (text: string) => {
    let textA = atob(text);
    console.log(`Base64 to string ${textA}`);
    onChangeBase64Text(textA)
  }

  // Print the length of base64 converted to Unit8Array byte array
  const onPressBase64Length = (text: string) => {
    console.log(`Print base64 length ${text}`);
    onChangeBase64TextLength(byteLength(text))
  }

  /* toByteArray: Decodes base64 string to Uint8Array */
  const onPressToByteArray = (text: string) => {
    let btArray = toByteArray(text);
    console.log(`toByteArray ${btArray}`);
    onChangeByteArray(btArray)
  }

  /* toByteArray: Decodes base64 string to Uint8Array with removeLinebreaks */
  const onPressToByteArrayRemove = (text: string, removeLinebreaks: boolean = false) => {
    let btArray = toByteArray(text, removeLinebreaks);
    console.log(`toByteArray ${btArray}`);
    onChangeByteArrayRemove(btArray)
  }

  /* fromByteArray: Encodes Uint8Array to Base64 string */
  const onPressFromByteArray = (
    uint8: Uint8Array,
    urlSafe: boolean = false) => {
    let b64 = fromByteArray(uint8);
    console.log(`fromByteArray ${b64}`);
    onChangeFbArrayBase64Str(b64)
  }

  /* fromByteArray: Encodes Uint8Array to Base64 string with URL safe option */
  const onPressFromByteArrayUrlSafe = (
    uint8: Uint8Array,
    urlSafe: boolean = false) => {
    let b64 = fromByteArray(uint8, urlSafe);
    console.log(`fromByteArray ${b64}`);
    onChangeFbArrayBase64StrUrlSafe(b64)
  }

  /* shim: Add btoa and atob function shim implementations to global object */
  const handleAddShimToGlobal = () => {
    shim();
    console.log(typeof global.btoa); // Should output "function"
    console.log(typeof global.atob); // Should also output "function"
  }

  const onPressTestShimBtoA = (text: string) => {
    const encodeBase64 = global.btoa(text);
    console.log(`shim global btoa ${encodeBase64}`);
    onChangeTestShimBtoA(encodeBase64)
  }

  const onPressTestShimAtoB = (text: string) => {
    const decodeBase64 = global.atob(text);
    console.log(`shim global atob ${decodeBase64}`);
    onChangeTestShimAtoB(decodeBase64)
  }

  /* trimBase64Padding: Remove padding characters from Base64 string */
  const onPressTrimBase64Padding = (text: string) => {
    let trimBase64 = trimBase64Padding(text);
    console.log(`trimBase64Padding ${trimBase64}`);
    onChangeTrimBase64PaddingText(trimBase64)
  }

  /* getNative: Returns object containing base64FromArrayBuffer and base64ToArrayBuffer functions */
  const onPressGetNative = () => {
    const native = getNative() as NativeModule;
    onChangeNativeModule(native)
  }

  /**
   * @param text 
   * base64FromArrayBuffer method accepts a Base64 encoded string or ArrayBuffer,
   * and an optional boolean parameter that determines whether the generated Base64 string is URL-safe.
   * This method converts ArrayBuffer object to Base64 encoded string.
   */
  const onPressNBFAB = (text: string | ArrayBuffer) => {
    if (nativeModule?.base64FromArrayBuffer) {
      let base64FromArrayBuffer = nativeModule.base64FromArrayBuffer(text);
      onChangeNBFABText(base64FromArrayBuffer)
    }
  }

  /** 
  * @description Convert base64 to Unit8Array, remove line breaks
  * @param text
  * @param removeLinebreaks true
  * 
  */
  const onPressNBFABUrlSafe = (text: string | ArrayBuffer, urlSafe: boolean = false) => {
    if (nativeModule?.base64FromArrayBuffer) {
      let base64FromArrayBuffer = nativeModule.base64FromArrayBuffer(text, urlSafe);
      onChangeNBFABTextUrlSafe(base64FromArrayBuffer)
    }
  }

  /** 
   * @description Convert base64 to Unit8Array
   * base64ToArrayBuffer method accepts a Base64 encoded string and an optional boolean parameter,
   * which determines whether to remove line breaks during conversion. This method converts Base64 encoded string to ArrayBuffer object.
   * @param text
   * @param removeLinebreaks default value false
   * 
   */
  const onPressNBTAB = (text: string) => {
    if (nativeModule?.base64ToArrayBuffer) {
      let base64ToArrayBuffer = new Uint8Array(nativeModule.base64ToArrayBuffer(text));
      onChangeNBTABText(base64ToArrayBuffer)
    }
  }

  /** 
   * @description Convert base64 to Unit8Array, remove line breaks
   * @param text
   * @param removeLinebreaks true
   * 
   */
  const onPressNBTABRemoveLinebreaks = (text: string, removeLinebreaks: boolean = false) => {
    if (nativeModule?.base64ToArrayBuffer) {
      let base64ToArrayBuffer = new Uint8Array(nativeModule.base64ToArrayBuffer(text, removeLinebreaks));
      onChangeNBTABTextRemoveLinebreaks(base64ToArrayBuffer)
    }
  }

  return (
    <ScrollView>
      <View style={styles.mainContainer}>
        <View>
          <TextInput
            style={{ height: 40, borderColor: '#978081', borderWidth: 1, width: 300, marginBottom: 20, backgroundColor: '#f5f5f5' }}
            onChangeText={(text) => onChangeTestText(text)}
            placeholder="please input test text"
            placeholderTextColor={'#674651'}
            value={testText}
          />
        </View>

        <View>BtoA Encodes a character string into a Base64 character string.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test string transform base64, testing the text: {testText}</Text>
          <Button
            title="BtoA"
            onPress={() => { onPressBtoA(testText) }}
          />
          <Text style={{ color: 'green' }}>{(textTobase64)}</Text>
        </View>

        <View>AtoB Convert base64 to character string.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test base64 transform string, testing the text: {textTobase64}</Text>
          <Button
            title="AtoB"
            onPress={() => { onPressAtoB(textTobase64) }}
          />
          <Text style={{ color: 'green' }}>{(base64ToText)}</Text>
        </View>

        <View>Decodes a base64 string into a Uint8Array.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test base64 transform Unit8Array, testing the text: {textTobase64}</Text>
          <Button
            title="onPressToByteArray"
            onPress={() => { onPressToByteArray(textTobase64) }}
          />
          <Text style={{ color: 'green' }}>{(byteArray.toString())}</Text>
        </View>

        <View>Decodes a base64 string into a Uint8Array. Whether to cancel line breaks.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test base64 transform Unit8Array add removeLinebreaks is true, testing the text: {textTobase64}</Text>
          <Button
            title="onPressToByteArrayRemove"
            onPress={() => { onPressToByteArrayRemove(textTobase64, true) }}
          />
          <Text style={{ color: 'green' }}>{(byteArrayRemove.toString())}</Text>
        </View>

        <View>Takes a base64 string and returns the length of the byte array.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>get Unit8Array length form base64 transform, testing the text: {textTobase64}</Text>
          <Button
            title="base64ToTextLength"
            onPress={() => { onPressBase64Length(textTobase64) }}
          />
          <Text style={{ color: 'green' }}>{(base64ToTextLength)}</Text>
        </View>

        <View>Encodes a Uint8Array into a Base64 character string.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test Uint8Array transform base64 string, testing the text: {byteArray.toString()}</Text>
          <Button
            title="onPressFromByteArray"
            onPress={() => { onPressFromByteArray(byteArray) }}
          />
          <Text style={{ color: 'green' }}>{(fbArrayBase64Str)}</Text>
        </View>

        <View>Encodes a Uint8Array into a Base64 character string. The urlSafe parameter determines whether Base64 encoding uses the URL-safe variant.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test Uint8Array transform base64 string add urlSafe params, testing the text: {byteArray.toString()}</Text>
          <Button
            title="onPressFromByteArrayUrlSafe"
            onPress={() => { onPressFromByteArrayUrlSafe(byteArray) }}
          />
          <Text style={{ color: 'green' }}>{(fbArrayBase64StrUrlSafe)}</Text>
        </View>

        <View
          style={{ display: 'flex', flexDirection: 'column', backgroundColor: '#ffffff' }}>
          <Text>Add btoa and atob functions for global objects</Text>
          <Button title="shim set global" onPress={() => handleAddShimToGlobal()} />
        </View>

        {/* Test whether shim sets btoa and atob functions successfully */}
        <View>Test whether the shim sets the btoa function successfully.</View>

        <View style={{ marginTop: 20, display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test shim BtoA, testing the text: {testText}</Text>
          <Button title="test shim BtoA" onPress={() => { onPressTestShimBtoA(testText) }} />
          <Text style={{ color: 'green' }}>{testShimBtoA}</Text>
        </View>

        {/* Test whether shim sets btoa and atob functions successfully */}
        <View>Test whether the shim sets the atob function successfully.</View>

        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test shim AtoB, testing the text: {textTobase64}</Text>
          <Button title="test shim AtoB" onPress={() => { onPressTestShimAtoB(textTobase64) }} />
          <Text style={{ color: 'green' }}>{testShimAtoB}</Text>
        </View>

        {/* trimBase64Padding: Remove padding characters from Base64 string */}
        <View>trimBase64Padding.</View>

        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>trimBase64Padding clears the padding characters of a Base64 string, testing the text: {textTobase64}</Text>
          <Button title="test trimBase64Padding" onPress={() => { onPressTrimBase64Padding(textTobase64) }} />
          <Text style={{ color: 'green' }}>{trimBase64PaddingText}</Text>
        </View>

        <View style={{ backgroundColor: "#ffffff" }}>
          <Text>Click the button below to get native function for base64FromArrayBuffer and base64ToArrayBuffer</Text>
          <Button title="Get getNative function" onPress={() => { onPressGetNative() }} />
        </View>

        <View>Click the button below to get base64FromArrayBuffer transform text.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>base64 transform string text: {testText}</Text>
          <Button title="onPressNBFAB" onPress={() => { onPressNBFAB(testText) }} />
          <Text style={{ color: 'green' }}>{nativeBFABText}</Text>
        </View>

        <View>Click the button below to get base64FromArrayBuffer transform text, The urlSafe parameter determines whether Base64 encoding uses the URL-safe variant.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>ArrayBuffer transform string text: {[72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]}</Text>
          <Button title="onPressNBFABUrlSafe" onPress={() => { onPressNBFABUrlSafe(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]).buffer) }} />
          <Text style={{ color: 'green' }}>{nativeBFABTextUrlSafe}</Text>
        </View>

        <View>Click the button below to get base64ToArrayBuffer transform text.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>base64 transform ArrayBuffer text: {textTobase64}</Text>
          <Button title="onPressNBTAB" onPress={() => { onPressNBTAB(textTobase64) }} />
          <Text style={{ color: 'green' }}>{nativeBTABText.toString()}</Text>
        </View>

        <View>Click the button below to get base64ToArrayBuffer transform text, Remove Line Breaks.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>base64 transform ArrayBuffer text: {textTobase64}</Text>
          <Button title="onPressNBTABRemoveLinebreaks" onPress={() => { onPressNBTABRemoveLinebreaks(textTobase64) }} />
          <Text style={{ color: 'green' }}>{nativeBTABTextRemoveLinebreaks}</Text>
        </View>

      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  mainContainer: {
    flex: 1,
    paddingTop: 20,
    paddingLeft: 20,
    paddingRight: 20,
    paddingBottom: 20,
    backgroundColor: '#f5f5f5',
    color: '#674651',
  },
});
```

## Link

Version >= @react-native-ohos/react-native-quick-base64@2.1.3，已支持 Autolink，无需手动配置，目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

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

    "@react-native-ohos/react-native-quick-base64": "file:../../node_modules/@react-native-ohos/react-native-quick-base64/harmony/rn_quick_base64.har"
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

### 3.配置 CMakeLists 和引入 RNQuickBase64Package

> 若使用的是 <=2.1.2-1.0.1 版本，请跳过本章。

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
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-ohos/react-native-quick-base64/src/main/cpp" ./rn_quick_base64)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_quick_base64)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNQuickBase64Package.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNQuickBase64Package>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNQuickBase64Package Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import { RNQuickBase64Package } from '@react-native-ohos/react-native-quick-base64/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQuickBase64Package(ctx),
  ];
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

> [!TIP] [官方文档](https://github.com/craftzdog/react-native-quick-base64)

## 静态方法

以下是提供的静态方法数据:
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME         | Description                                                             | TYPE | Required | Platform | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------- | ------ | ------ | -------- | -------- |
| btoa | 将字符串编码为 base64 格式。 | Function | no | All | yes |
| atob | 解码一个 base64 编码的字符串。 | Function | no | All | yes |
| toByteArray | 接收一个 base64 字符串并返回一个字节数组。可选参数 `removeLinebreaks` 用于移除所有 `\n` 字符。 | Function | no | All | yes |
| byteLength | 接收一个 base64 字符串并返回其字节数组的长度。 | Function | no | All | yes |
| fromByteArray | 接收一个字节数组并返回一个 base64 字符串。可选参数 `urlSafe` 设为 `true` 时，将使用 [URL 安全的字符集](https://github.com/craftzdog/react-native-quick-base64/blob/9d02dfd02599ca104d2ed6c1e2d938ddd9d6cd15/cpp/base64.h#L75)。 | Function | no | All | yes |
| shim | 将 `btoa` 和 `atob` 函数添加到 `global` 全局对象中。 | Function | no | All | yes |
| trimBase64Padding | 去除 base64 编码字符串末尾的 `=` 填充字符。同时，对于 base64url 编码的字符串，它也会去除末尾的 `.` 字符。 | Function | no | All | yes |
| getNative | 获取原生的 base64ToArrayBuffer 和 base64FromArrayBuffer 函数。 | Function | no | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-quick-base64/blob/sig/LICENSE) ，请自由地享受和参与开源。

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-viewer
</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vinzscam/react-native-file-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-file-viewer)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| <= 2.1.6@deprecated | [@react-native-oh-tpl/react-native-file-viewer Releases(deprecated)](https://github.com/react-native-oh-library/react-native-file-viewer/releases) | 0.72       |
| 2.1.7 | [@react-native-ohos/react-native-file-viewer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-viewer/releases)                        | 0.72       |
| 2.2.0 | [@react-native-ohos/react-native-file-viewer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-file-viewer/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-file-viewer
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-file-viewer
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { StyleSheet, ScrollView, Text, TouchableOpacity } from "react-native";
import DocumentPicker from "react-native-document-picker";
import FileViewer from "react-native-file-viewer";

export function FlieViewerExample() {
	const FileViewerTest = async (option?: any) => {
		try {
			// 使用react-native-document-picker来选择本地文件进行打开
			const res: any = await DocumentPicker.pick({
				type: [DocumentPicker.types.allFiles]
			});
			// uri 为本地文件绝对路径
			await FileViewer?.open(res[0].uri, option);
		} catch (e) {
			// error
		}
	};

	const onDismissCb = () => {
		// do sth ...
	};

	return (
		<ScrollView style={{ backgroundColor: "skyblue" }}>
			<TouchableOpacity onPress={() => FileViewerTest()} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest("show_displayName string")} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (displayName str)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ displayName: "show_displayName option" })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (displayName opt)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ showOpenWithDialog: true, onDismiss: onDismissCb })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (onDismiss)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ showOpenWithDialog: true })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (showOpenWithDialog)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ showAppsSuggestions: true })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (showAppsSuggestions)</Text>
			</TouchableOpacity>
		</ScrollView>
	);
}

const styles = StyleSheet.create({
	TextInput: {
		height: 40,
		borderColor: "#ccc",
		borderWidth: 1,
		borderRadius: 4,
		width: "90%"
	},
	btn: {
		borderRadius: 10,
		display: "flex",
		justifyContent: "center",
		alignItems: "center",
		padding: 10,
		margin: 10,
		backgroundColor: "blue"
	},
	btnText: {
		fontWeight: "bold",
		color: "#fff",
		fontSize: 20
	},
	selectBtn: {
		padding: 8,
		margin: 3,
		fontSize: 18,
		borderWidth: 1,
		borderRadius: 8,
		borderColor: "#753c13"
	},
	selectBtnActive: {
		padding: 8,
		margin: 3,
		backgroundColor: "#e2803b",
		fontSize: 18,
		borderRadius: 8,
		borderWidth: 1
	}
});
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-file-viewer@2.1.7，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-file-viewer@2.1.7，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

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
    "@react-native-ohos/react-native-file-viewer": "file:../../node_modules/@react-native-ohos/react-native-file-viewer/harmony/file_viewer.har"
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


### 3.配置CMakeLists 和引入 FileViewerPackage

> 若使用的是 <= 2.1.6 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```cmake
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-file-viewer/src/main/cpp" ./file-viewer)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_file_viewer)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FileViewerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FileViewerPackage>(ctx)
    };
}
```


### 4.在 ArkTs 侧引入 RNFileViewerTurboModule Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNFileViewerPackage } from '@react-native-ohos/react-native-file-viewer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFileViewerPackage(ctx)
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

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### `open(filepath: string, options?: Object): Promise<void>`

| Name | Description | Type | Required  | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- |
| **filepath** | 文件存储的绝对路径。文件需要有有效的扩展名才能被成功检测。使用 [react-native-fs constants](https://github.com/itinance/react-native-fs#constants) 来正确确定绝对路径。 | string | yes | All | yes |
| **options** (optional) | 用于自定义行为的一些选项。详见下文。 | Object | no | All | yes |

#### 属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- |
| **displayName** (optional) | 自定义QuickLook标题。 | string | no | iOS | yes |
| **onDismiss** (optional) | 当查看器被关闭时调用的回调函数。 | function | no | All | partially |
| **showOpenWithDialog** (optional) | 如果有多个应用可以打开文件，显示“打开方式”对话框。 | boolean | no | Android | yes |
| **showAppsSuggestions** (optional) | 如果没有安装可以打开文件的应用，打开应用商店并显示推荐应用。 | boolean | no | Android | partially |

## 遗留问题

- [x] HarmonyOS端暂不支持关闭预览窗口的回调函数调用: [issue#1](https://github.com/react-native-oh-library/react-native-file-viewer/issues/4)
- [x] HarmonyOS端无法直接跳转到应用市场的推荐应用页，目前只能跳转到应用市场首页: [issue#2](https://github.com/react-native-oh-library/react-native-file-viewer/issues/5)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE) ，请自由地享受和参与开源。


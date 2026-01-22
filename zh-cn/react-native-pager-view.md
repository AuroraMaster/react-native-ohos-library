> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-pager-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-pager-view">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
       <a href="https://github.com/callstack/react-native-pager-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-pager-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本               | 发布信息                                                                                                                                            | 支持RN版本 |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| 7.0.3                       | [@react-native-ohos/react-native-pager-view Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pager-view/releases)       | 0.82       |
| 6.7.2               | [@react-native-ohos/react-native-pager-view Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pager-view/releases)               | 0.77       |
| 6.2.5               | [@react-native-ohos/react-native-pager-view Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pager-view/releases)               | 0.72       |
| <= 6.2.4@deprecated | [@react-native-oh-tpl/react-native-pager-view Releases(deprecated)](https://github.com/react-native-oh-library/react-native-pager-view/releases) | 0.72       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-pager-view
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-pager-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { StyleSheet, View, Text } from "react-native";
import PagerView from "react-native-pager-view";

const MyPager = () => {
  return (
    <PagerView style={styles.pagerView} initialPage={0}>
      <View key="1" style={styles.page}>
        <Text>First page</Text>
      </View>
      <View key="2" style={styles.page}>
        <Text>Second page</Text>
      </View>
    </PagerView>
  );
};

const styles = StyleSheet.create({
	  pagerView: {
	    flex: 1,
	  },
	  page: {
	    justifyContent: 'center',
	    alignItems: 'center',
	    flex: 1,
	  },
	});
	
export default MyPager;
```

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~7.0.3                               |  No              |  0.82     |
| ~6.7.2                               |  No              |  0.77     |
| ~6.2.5                               |  Yes             |  0.72     |
| <= 6.2.4@deprecated                  |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。

<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 在工程根目录的 `oh-package.json5` 添加 overrides字段
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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/react-native-pager-view": "file:../../node_modules/@react-native-ohos/react-native-pager-view/harmony/pager_view.har"
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

### 3.配置 CMakeLists 和引入 ViewPagerPackage

> 若使用的是 <= 6.2.4 版本，请跳过本章

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

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-pager-view/src/main/cpp" ./pager_view)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_pager_view )
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ViewPagerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ViewPagerPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 ViewPagerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ViewPagerPackage } from '@react-native-ohos/react-native-pager-view/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ViewPagerPackage(ctx)
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

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.12;

## 属性

> [!TIP] " HarmonyOS 支持"列为 yes 的 API 表示支持 HarmonyOS 平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                     | Description                                                                                                                                                                                                                                                         | Type                           | Required | Platform     | HarmonyOS Support          |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ | -------- | ------------ | -------------------------- |
| initialPage                              | 被选中的初始页面索引                                                                                                                                                                                                                       | number                         | 是       | ios，android | yes                        |
| scrollEnabled                            | 当滚动启用时，页面视图是否应该滚动                                                                                                                                                                                                                       | bool                           | 是       | ios，android | yes                        |
| onPageScroll                             | 在页面之间转换时执行（无论是因为请求页面的动画已更改还是当用户在页面之间滑动/拖动时）                                                                                                       | function                       | 否       | ios，android | yes                        |
| onPageScrollStateChanged                 | 页面滚动状态发生变化时调用的函数                                                                                                                                                                                                           | function                       | 否       | ios，android | yes                        |
| onPageSelected                           | 一旦ViewPager完成导航到选定页面，将调用此回调                                                                                                                                                                            | function                       | 否       | ios，android | yes                        |
| pageMargin                               | 要显示在页面之间的空白空间                                                                                                                                                                                                                               | number （取值范围:0~屏幕宽度） | 否       | ios，android | 仅支持取 0-368（屏幕宽度） |
| keyboardDismissMode                      | 确定键盘是否会因拖拽而消失                                                                                                                                                                                                | one of 'none' ,'on-drag'       | 否       | ios,android  | yes                        |
| orientation                              | 设置水平或垂直滚动方向（不能动态工作）                                                                                                                                                                                     | one of horizontal vertical     | 否       | ios，android | yes                        |
| overScrollMode                           | 用于覆盖过度滚动模式的默认值。可以是auto、always或never。默认为auto                                                                                                                                                                   | one of auto, always ,never     | 否       | android      | yes                        |
| offscreenPageLimit                       | 设置应保留在当前可见页面两侧的页数。超出此限制的页面将在需要时从适配器重新创建。默认为RecyclerView的缓存策略。给定值必须大于0 | number                         | 否       | android      | no                         |
| overdrag                                 | 允许在到达页面末尾或开头后继续过度滚动。默认为false                                                                                                                                                                       | bool                           | 否       | ios          | yes                        |
| layoutDirection                          | 指定布局方向。使用ltr或rtl显式设置，或使用locale从区域设置的默认语言脚本推断。默认为locale                                                                                                                   | string                         | 否       | android,ios  | yes                        |
| setPage(index: number)                   | 滚动到PagerView中特定页面的函数。无效索引将被忽略                                                                                                                                                                                   | function                       | 否       | android,ios  | yes                        |
| setPageWithoutAnimation(index: number)   | 滚动到PagerView中特定页面的函数。无效索引将被忽略                                                                                                                                                                                   | function                       | 否       | android,ios  | yes                        |
| setScrollEnabled(scrollEnabled: boolean) | FA辅助函数，用于命令式地启用/禁用滚动。推荐的方式是使用scrollEnabled属性，但在某些情况下，命令式解决方案可能更有用（例如，不阻止动画）                                       | function                       | 否       | android,ios  | yes                        |

## 遗留问题

- [ ] offscreenPageLimit 未实现 HarmonyOS 化[issue#7](https://github.com/react-native-oh-library/react-native-pager-view/issues/7)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-pager-view/blob/harmony/LICENSE) ，请自由地享受和参与开源。

模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-ui-lib</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wix/react-native-ui-lib">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wix/react-native-ui-lib/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-ui-lib)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 7.29.1     | [@react-native-oh-tpl/react-native-ui-lib Releases](https://github.com/react-native-oh-library/react-native-ui-lib/releases) | 0.72       |
| 7.43.1     | [@react-native-ohos/react-native-ui-lib Releases](https://github.com/react-native-oh-library/react-native-ui-lib/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated和 @react-native-oh-tpl/react-native-gesture-handler的原生端代码，如已在 HarmonyOS 工程中引入过这些库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参考[@react-native-oh-tpl/react-native-reanimated文档](/zh-cn/react-native-reanimated.md)和[@react-native-oh-tpl/react-native-gesture-handler文档](/zh-cn/react-native-gesture-handler.md)进行引入。

下面是根据使用组件情况按需引入依赖项:

- [@react-native-community/blur](/zh-cn/react-native-community-blur.md) （Card 组件）

- [@react-native-community/datetimepicker](/zh-cn/react-native-community-datetimepicker.md) （DateTimePicker 组件）
- [@react-native-community/netinfo](/zh-cn/react-native-community-netinfo.md) （ConnectionStatusBar 组件）

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-ui-lib

# 0.77
npm install @react-native-ohos/react-native-ui-lib
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-ui-lib

# 0.77
yarn add @react-native-ohos/react-native-ui-lib
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, {Component} from 'react';
import {Colors, Typography, Spacings, ThemeManager, View, Text, Card, Button} from 'react-native-ui-lib';

Colors.loadColors({
  primaryColor: '#2364AA',
  secondaryColor: '#81C3D7',
  textColor: '##221D23',
  errorColor: '#E63B2E',
  successColor: '#ADC76F',
  warnColor: '##FF963C'
});

Typography.loadTypographies({
  heading: {fontSize: 36, fontWeight: '600'},
  subheading: {fontSize: 28, fontWeight: '500'},
  body: {fontSize: 18, fontWeight: '400'}
});

Spacings.loadSpacings({
  page: 20,
  card: 12,
  gridGutter: 16
});

// with plain object
ThemeManager.setComponentTheme('Card', {
  borderRadius: 8
});

// with a dynamic function
ThemeManager.setComponentTheme('Button', (props, context) => {
  // 'square' is not an original Button prop, but a custom prop that can
  // be used to create different variations of buttons in your app
  if (props.square) {
    return {
      borderRadius: 0
    };
  }
});

class MyScreen extends Component {
  render() {
    return (
      <View flex padding-page>
        <Text heading marginB-s4>
          My Screen
        </Text>
        <Card height={100} center padding-card marginB-s4>
          <Text body>This is an example card </Text>
        </Card>

        <Button label="Button" body bg-primaryColor square></Button>
      </View>
    );
  }
}
```

## 使用 Codegen

> [!TIP] V7.43.1 不需要执行 Codegen。

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
    "@react-native-oh-tpl/react-native-ui-lib": "file:../../node_modules/@react-native-oh-tpl/react-native-ui-lib/harmony/ui_lib.har"
  }
```

- 0.77

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-ui-lib": "file:../../node_modules/@react-native-ohos/react-native-ui-lib/harmony/ui_lib.har"
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

### 3.配置 CMakeLists 和引入 UiLibPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
+ set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)

# 0.72
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-ui-lib/src/main/cpp" ./ui-lib)

# 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-ui-lib/src/main/cpp" ./ui-lib)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_ui_lib)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "UiLibPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<UiLibPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 HighlighterView组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
// 0.72
+ import { HighlighterView } from "@react-native-oh-tpl/react-native-ui-lib";

// 0.77
+ import { HighlighterView } from "@react-native-ohos/react-native-ui-lib";

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === HighlighterView.NAME) {
+   HighlighterView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。（如使用混合方案）

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ HighlighterView.NAME
  ];
```

### 5.在 ArkTs 侧引入 UiLibPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
// 0.72
+ import { UiLibPackage } from '@react-native-oh-tpl/react-native-ui-lib/ts';

// 0.77
+ import { UiLibPackage } from '@react-native-ohos/react-native-ui-lib/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new UiLibPackage(ctx)
  ];
}
```

### 6.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.33; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 组件

详细请查看 [react-native-ui-lib的文档介绍](https://wix.github.io/react-native-ui-lib/docs/getting-started/setup)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Text**：文本组件，该组件扩展了[Text](https://reactnative.dev/docs/text)属性。

| Name            | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| animated        | 将 Animated.Text 用作容器                             | boolean                             | no       | iOS/Android | yes               |
| center          | 是否将文本居中（使用 textAlign）                 | boolean                             | no       | iOS/Android | yes               |
| color           | 文字颜色                                            | string                              | no       | iOS/Android | yes               |
| highlightString | 要高亮显示的子字符串。可以是简单的字符串或 HighlightStringProps 对象，或者上述类型的数组 | HighlightString \|HighlightString[] | no       | iOS/Android | yes               |
| highlightStyle  | 自定义强调字符串的高亮样式                  | TextStyle                           | no       | iOS/Android | yes               |
| recorderTag     | 记录器标签                                                | 'mask' \|'unmask'                   | no       | iOS/Android | yes               |
| underline       | 是否添加下划线                                  | boolean                             | no       | iOS/Android | yes               |
| uppercase       | 是否将文本改为大写                      | boolean                             | no       | iOS/Android | yes               |

**TouchableOpacity**：触摸反馈透明度组件，该组件扩展了[TouchableOpacity](https://reactnative.dev/docs/touchableopacity)属性。

| Name                  | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| activeBackgroundColor | 当 TouchableOpacity 处于激活状态（按下时）时应用背景颜色 | string                                                       | no       | iOS/Android | yes               |
| backgroundColor       | TouchableOpacity 的背景颜色                        | string                                                       | no       | iOS/Android | yes               |
| customValue           | 可传递给 TouchableOpacity 的任意类型自定义值，并在 onPress 回调中接收 | any                                                          | no       | iOS/Android | yes               |
| onPress               | 按下回调                                            | (props?: TouchableOpacityProps & {event: GestureResponderEvent} \|any) => void | no       | iOS/Android | yes               |
| recorderTag           | 记录器标签                                                | 'mask'\|'unmask'                                             | no       | iOS/Android | yes               |
| style                 | 自定义样式                                               | ViewStyle                                                    | no       | iOS/Android | yes               |
| throttleOptions       | 节流选项                                             | ThrottleOptions                                              | no       | iOS/Android | yes               |
| throttleTime          | 按下回调的节流时间（毫秒）                    | number                                                       | no       | iOS/Android | yes               |
| useNative             | 应使用具有额外功能的增强本地实现 | boolean                                                      | no       | iOS/Android | yes               |
| activeScale           | 将应用缩放按压反馈。这将强制使用 useNative 属性  | number                                                       | no       | iOS/Android | yes               |

**View**：容器组件，该组件扩展了[View](https://reactnative.dev/docs/view)属性。

| Name            | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| animated        | 将 Animate.View 用作容器                              | boolean          | no       | iOS/Android | yes               |
| backgroundColor | 设置背景颜色                                        | string           | no       | iOS/Android | yes               |
| inaccessible    | 关闭此视图及其子视图的辅助功能 | boolean          | no       | iOS/Android | yes               |
| reanimated      | 使用 Animate.View（来自 react-native-reanimated）作为容器 | boolean          | no       | iOS/Android | yes               |
| recorderTag     | 记录器标签                                                 | 'mask'\|'unmask' | no       | iOS/Android | yes               |
| renderDelay     | 实验性：以毫秒为单位传递时间以延迟渲染                | number           | no       | iOS/Android | yes               |
| style           | 自定义样式                                                | ViewStyle        | no       | iOS/Android | yes               |
| useSafeArea     | 如果为true，将呈现为 SafeAreaView                         | boolean          | no       | iOS/Android | yes               |

**ActionBar**：快速操作栏，每个操作都支持按钮组件道具，该组件扩展了[View](https://wix.github.io/react-native-ui-lib/docs/components/basic/View)属性。

| Name            | Description                                                  | Type          | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------- | -------- | ----------- | ----------------- |
| actions         | 操作栏的操作                               | ButtonProps[] | no       | iOS/Android | yes               |
| backgroundColor | 设置背景颜色                                             | string        | no       | iOS/Android | yes               |
| centered        | 行动是否应同样居中                            | boolean       | no       | iOS/Android | yes               |
| height          | 高度                                                      | number        | no       | iOS/Android | yes               |
| keepRelative    | 保持操作栏位置为相对，而不是绝对位置 | boolean       | no       | iOS/Android | yes               |
| style           | 组件的样式                                            | ViewStyle     | no       | iOS/Android | yes               |
| useSafeArea     | 在 iOS 中，使用安全区域，以防组件附着到底部 | boolean       | no       | iOS/Android | yes               |

**Button**：按钮组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)属性。

| Name                     | Description                                                  | Type                                            | Required | Platform    | HarmonyOS Support |
| :----------------------- | ------------------------------------------------------------ | ----------------------------------------------- | -------- | ----------- | ----------------- |
| animateLayout            | 应该为布局变化添加动画。注意：对于 Android，必须通过 RN 的 'UIManager' 设置 'setLayoutAnimationEnabledExperimental(true)' | boolean                                         | no       | iOS/Android | yes               |
| animateTo                | 动画的方向（“左”和“右”会影响按钮自身的对齐方式） | ButtonAnimationDirection                        | no       | iOS/Android | yes               |
| avoidInnerPadding        | 避免内部按钮间距                                   | boolean                                         | no       | iOS/Android | yes               |
| avoidMinWidth            | 避免最小宽度限制                              | boolean                                         | no       | iOS/Android | yes               |
| backgroundColor          | 按钮背景颜色                               | string                                          | no       | iOS/Android | yes               |
| borderRadius             | 自定义边角半径。                                        | number                                          | no       | iOS/Android | yes               |
| color                    | 按钮文本颜色（继承自文本组件）        | string                                          | no       | iOS/Android | yes               |
| disabled                 | 禁用组件的交互                      | boolean                                         | no       | iOS/Android | yes               |
| disabledBackgroundColor  | 禁用按钮背景颜色                      | string                                          | no       | iOS/Android | yes               |
| enableShadow             | 控制阴影可见性（仅限 iOS）                        | boolean                                         | no       | iOS         | no                |
| fullWidth                | 按钮是否应作为跨屏按钮（无边角圆弧） | boolean                                         | no       | iOS/Android | yes               |
| getActiveBackgroundColor | 用于获取 activeBackgroundColor 的回调（例如 (calculatedBackgroundColor, prop) => {...}）。最好通过 ThemeManager 设置 | (backgroundColor: string, props: any) => string | no       | iOS/Android | yes               |
| hyperlink                | 按钮看起来像一个超链接                           | boolean                                         | no       | iOS/Android | yes               |
| iconOnRight              | 图标应该在标签的右边吗                       | boolean                                         | no       | iOS/Android | yes               |
| iconProps                | 图标图片属性                                            | Partial<ImageProps>                             | no       | iOS/Android | yes               |
| iconSource               | 图标图像来源或返回来源的回调函数 | ImageProps['source']|Function                  | no       | iOS/Android | yes               |
| iconStyle                |图标图片样式                                             | ImageStyle                                      | no       | iOS/Android | yes               |
| label                    | 按钮内显示的文本                               | string                                          | no       | iOS/Android | yes               |
| labelProps               | 将传递给按钮文本标签的属性。        | TextProps                                       | no       | iOS/Android | yes               |
| labelStyle               | 标签文本的附加样式                             | TextStyle                                       | no       | iOS/Android | yes               |
| link                     | 按钮看起来像一个链接                                | boolean                                         | no       | iOS/Android | yes               |
| linkColor                | 标签颜色（当显示为链接或超链接时）     | string                                          | no       | iOS/Android | yes               |
| onPress                  | 动作处理器                                              | (props: any) => void                            | no       | iOS/Android | yes               |
| outline                  | 按钮将采用轮廓样式                               | boolean                                         | no       | iOS/Android | yes               |
| outlineColor             | 轮廓颜色                                            | string                                          | no       | iOS/Android | yes               |
| outlineWidth             | 轮廓宽度                                            | number                                          | no       | iOS/Android | yes               |
| round                    | 按钮是否是圆形按钮                          | boolean                                         | no       | iOS/Android | yes               |
| size                     | 按钮的大小 [large, medium, small, xSmall]            | ButtonSize                                      | no       | iOS/Android | yes               |
| supportRTL               | 图标在 RTL 语言环境下是否应水平翻转      | boolean                                         | no       | iOS/Android | yes               |

**Checkbox**：复选框组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)属性。

| Name             | Description                                                  | Type                       | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------------------------- | -------- | ----------- | ----------------- |
| borderRadius     | 复选框边框圆角                                   | number                     | no       | iOS/Android | yes               |
| color            | 复选框颜色                                          | string                     | no       | iOS/Android | yes               |
| containerStyle   | 复选框和标签容器的自定义样式          | ViewStyle                  | no       | iOS/Android | yes               |
| disabled         | 复选框是否应被禁用                      | boolean                    | no       | iOS/Android | yes               |
| iconColor        | 所选图标颜色                                      | string                     | no       | iOS/Android | yes               |
| label            | 为复选框添加标签                                 | string                     | no       | iOS/Android | yes               |
| labelProps       | 传递给标签组件的属性                      | TextProps                  | no       | iOS/Android | yes               |
| labelStyle       | 传递以设置标签样式                                      | TextStyle                  | no       | iOS/Android | yes               |
| onChangeValidity | 字段有效性更改时的回调                 | (isValid: boolean) => void | no       | iOS/Android | yes               |
| onValueChange    | 值变化事件的回调函数                     | (value) => void            | no       | iOS/Android | yes               |
| outline          | 替代复选框轮廓样式                           | boolean                    | no       | iOS/Android | yes               |
| required         | 是否需要复选框                             | boolean                    | no       | iOS/Android | yes               |
| selectedIcon     | 用于所选指示的图标资源            | ImageRequireSource         | no       | iOS/Android | yes               |
| size             | 复选框的大小会影响宽度和高度              | number                     | no       | iOS/Android | yes               |
| style            | 复选框的自定义样式                            | ViewStyle                  | no       | iOS/Android | yes               |
| value            | 复选框的值。如果为真，开关将被打开。默认值为假 | boolean                    | no       | iOS/Android | yes               |

**Chip**：芯片组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)，[View](https://wix.github.io/react-native-ui-lib/docs/components/basic/View)属性。

| Name                  | Description                                                  | Type                                      | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------------------------------------- | -------- | ----------- | ----------------- |
| avatarProps           | Avatar 属性                                          | AvatarProps                               | no       | iOS/Android | yes               |
| backgroundColor       | 背景色                                            | string                                    | no       | iOS/Android | yes               |
| badgeProps            | Badge 属性                                           | BadgeProps                                | no       | iOS/Android | yes               |
| borderRadius          | Border半径                                                | number                                    | no       | iOS/Android | yes               |
| containerStyle        | Component's container 风格                                  | ViewStyle                                 | no       | iOS/Android | yes               |
| dismissColor          | Dismiss 颜色                                            | string                                    | no       | iOS/Android | yes               |
| dismissContainerStyle | Dismiss container 风格                                      | ImageStyle                                | no       | iOS/Android | yes               |
| dismissIcon           | Dismiss 资源                                                | ImageSourcePropType                       | no       | iOS/Android | yes               |
| dismissIconStyle      | Dismiss 风格                                                | ImageStyle                                | no       | iOS/Android | yes               |
| iconProps             | Additional icon 属性                                        | Omit<ImageProps, 'source'>                | no       | iOS/Android | yes               |
| iconSource            | Left icon's 资源                                          | ImageSourcePropType                       | no       | iOS/Android | yes               |
| iconStyle             | Icon 风格                                                   | ImageStyle                                | no       | iOS/Android | yes               |
| label                 | 显式的文本                                            | string                                    | no       | iOS/Android | yes               |
| labelStyle            | Label的风格                                                | TextStyle                                 | no       | iOS/Android | yes               |
| leftElement           | 左边自定义元素                                          | JSX.Element                               | no       | iOS/Android | yes               |
| onDismiss             | 添加一个关闭按钮并作为其回调             | (props: any) => void                      | no       | iOS/Android | yes               |
| onPress               | 芯片按下回调                                       | (props: any) => void                      | no       | iOS/Android | yes               |
| resetSpacings         | 禁用所有内部元素的默认间距，有助于实现自定义设计 | boolean                                   | no       | iOS/Android | yes               |
| rightElement          | 右边自定义元素                                       | JSX.Element                               | no       | iOS/Android | yes               |
| rightIconSource       | 右边图标地址                                         | ImageSourcePropType                       | no       | iOS/Android | yes               |
| size                  | 芯片的尺寸。数字或宽度和高度对象             | number\|{{width: number, height: number}} | no       | iOS/Android | yes               |
| testID                | 端到端测试的测试 ID                                   | string                                    | no       | iOS/Android | yes               |
| useCounter            | 以计数器显示徽章（无背景）                    | boolean                                   | no       | iOS/Android | yes               |
| useSizeAsMinimum      | 使用大小作为最小宽度和最小高度                         | boolean                                   | no       | iOS/Android | yes               |

**RadioButton**：单选按钮组件。

| Name           | Description                                                  | Type                        | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------- | ----------------- |
| borderRadius   | 单选按钮边框半径                               | number                      | no       | iOS/Android | yes               |
| color          | 单选按钮的颜色                                | string                      | no       | iOS/Android | yes               |
| containerStyle | 容器的附加样式                         | ViewStyle                   | no       | iOS/Android | yes               |
| contentOnLeft  | 内容应该左对齐到按钮吗            | boolean                     | no       | iOS/Android | yes               |
| disabled       | 是否应禁用单选按钮                  | boolean                     | no       | iOS/Android | yes               |
| iconOnRight    | 图标应该放在标签的右侧吗            | boolean                     | no       | iOS/Android | yes               |
| iconSource     | 图标图片来源                                            | ImageSource                 | no       | iOS/Android | yes               |
| iconStyle      | 图标图片样式                                             | ImageStyle                  | no       | iOS/Android | yes               |
| label          | 单选按钮描述的标签                     | string                      | no       | iOS/Android | yes               |
| labelStyle     | 标签样式                                                  | TextStyle                   | no       | iOS/Android | yes               |
| onPress        | 在按下按钮时调用                             | (selected: boolean) => void | no       | iOS/Android | yes               |
| selected       | 在不使用 RadioGroup 的情况下使用 RadioButton 时，使用此属性来切换选中状态 | boolean                     | no       | iOS/Android | yes               |
| size           | 单选按钮的大小影响宽度和高度     | number                      | no       | iOS/Android | yes               |
| value          | 单选按钮的标识值。必须与同一组中的其他单选按钮不同 | string \| number \| boolean | no       | iOS/Android | yes               |

**RadioGroup**：包裹单选按钮组件，和RadioButton配合使用。

| Name          | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| initialValue  | 所选单选按钮的初始值               | string \| number \| boolean                                  | no       | iOS/Android | yes               |
| onValueChange | 当值改变时调用一次，通过选择组中的一个单选按钮 | ((value?: string) => void)\|((value?: number) => void)\|((value?: boolean) => void)\|((value?: any) => void) | no       | iOS/Android | yes               |

**Slider**：滑块组件。

| Name                  | Description                                                  | Type                                 | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------------------ | -------- | ----------- | ----------------- |
| accessible            | 如果为真，该组件将启用辅助功能 | boolean                              | no       | iOS/Android | yes               |
| activeThumbStyle      | 按压时的样式                       | ViewStyle                            | no       | iOS/Android | yes               |
| containerStyle        | 容器样式                                          | ViewStyle                            | no       | iOS/Android | yes               |
| disableActiveStyling  | 如果为真，滑块在按下时不会改变其样式       | boolean                              | no       | iOS/Android | yes               |
| disableRTL            | 如果为true，即使应用程序处于从右到左模式，滑块仍将保持从左到右模式 | boolean                              | no       | iOS/Android | yes               |
| disabled              | 如果为true，滑块将被禁用，并显示为禁用颜色 | boolean                              | no       | iOS/Android | yes               |
| initialMaximumValue   | 只有当 `useRange` 为 true 时，初始最大值          | number                               | no       | iOS/Android | yes               |
| initialMinimumValue   | 只有当 `useRange` 为 true 时，初始最小值          | number                               | no       | iOS/Android | yes               |
| maximumTrackTintColor | 轨道颜色                                            | string                               | no       | iOS/Android | yes               |
| maximumValue          | 追踪最大值                                          | number                               | no       | iOS/Android | yes               |
| migrate               | 迁移到滑块的新实现所需的临时属性 | boolean                              | no       | iOS/Android | yes               |
| minimumTrackTintColor | 用于从最小值到当前值的轨道颜色 | string                               | no       | iOS/Android | yes               |
| minimumValue          | 追踪最小值                                         | number                               | no       | iOS/Android | yes               |
| onRangeChange         | onRangeChange 的回调。返回包含最小值和最大值的值对象 | SliderOnRangeChange                  | no       | iOS/Android | yes               |
| onReset               | 当重置功能被调用时的回调通知   | () => void                           | no       | iOS/Android | yes               |
| onSeekEnd             | 回调，用于通知滑块拖动已完成      | () => void                           | no       | iOS/Android | yes               |
| onSeekStart           | 回调，用于通知滑块开始拖动       | () => void                           | no       | iOS/Android | yes               |
| onValueChange         | onValueChange 的回调                                   | SliderOnValueChange                  | no       | iOS/Android | yes               |
| renderTrack           | 自定义渲染而不是渲染轨道                 | () => ReactElement \| ReactElement[] | no       | iOS/Android | yes               |
| step                  | 滑块的步长值。该值应介于 0 与（最大值 - 最小值）之间 | number                               | no       | iOS/Android | yes               |
| testID                | 组件测试 ID                                      | string                               | no       | iOS/Android | yes               |
| thumbStyle            | thumb 样式                                            | ViewStyle                            | no       | iOS/Android | yes               |
| thumbTintColor        | Thumb 颜色                                                 | string                               | no       | iOS/Android | yes               |
| trackStyle            |  track 样式                                              | ViewStyle                            | no       | iOS/Android | yes               |
| useGap                | 如果为true，最小值和最大值的滑块将不会重叠              | boolean                              | no       | iOS/Android | yes               |
| useRange              | 如果为true，滑块将显示用于最小值的第二个滑块按钮 | boolean                              | no       | iOS/Android | yes               |
| value                 | 初始值                                                | number                               | no       | iOS/Android | yes               |

**Switch**：开关切换组件。

| Name          | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| disabled      | 是否应禁用开关                       | boolean                  | no       | iOS/Android | yes               |
| disabledColor | 开关禁用时的背景颜色               | string                   | no       | iOS/Android | yes               |
| height        | 开关高度                                           | number                   | no       | iOS/Android | yes               |
| id            | 组件 id                                                 | string                   | no       | iOS/Android | yes               |
| offColor      | 开关关闭时的背景颜色             | string                   | no       | iOS/Android | yes               |
| onColor       | 开关开启时的背景颜色              | string                   | no       | iOS/Android | yes               |
| onValueChange | 当值发生变化时，使用新值调用            | (value: boolean) => void | no       | iOS/Android | yes               |
| style         | 自定义样式                                                 | ViewStyle                | no       | iOS/Android | yes               |
| testID        | 组件测试 id                                            | string                   | no       | iOS/Android | yes               |
| thumbColor    | Switch的摇杆颜色                                     | string                   | no       | iOS/Android | yes               |
| thumbSize     | Switch 拇指大小（宽度和高度）                    | number                   | no       | iOS/Android | yes               |
| thumbStyle    | Switch的拇指风格                                    | ViewStyle                | no       | iOS/Android | yes               |
| value         | 开关的值。如果为true，开关将被打开。默认值为false | boolean                  | no       | iOS/Android | yes               |
| width         | 开关宽度                                             | number                   | no       | iOS/Android | yes               |

**ChipsInput**：芯片输入组件，该组件扩展了[TextField](https://wix.github.io/react-native-ui-lib/docs/components/form/TextField)属性。

| Name             | Description                                          | Type                                          | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| chips            | 要渲染的芯片列表                              | ChipProps[]                                   | no       | iOS/Android | yes               |
| defaultChipProps | 默认要传递给所有芯片的属性集合 | ChipProps                                     | no       | iOS/Android | yes               |
| maxChips         | 允许添加的最大筹码数                    | number                                        | no       | iOS/Android | yes               |
| onChange         | item变更回调（添加或移除item）  | (newChips, changeReason, updatedChip) => void | no       | iOS/Android | yes               |

**ColorPalette**：调色板组件。

| Name            | Description                                                  | Type                                          | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | --------------------------------------------- | -------- | ----------- | ----------------- |
| animatedIndex   | 默认值为最后一项，首次渲染时要动画的项目索引 | number                                        | no       | iOS/Android | yes               |
| backgroundColor | ColorPalette 的背景颜色                          | string                                        | no       | iOS/Android | yes               |
| colors          | 调色板中要显示的颜色数组                     | string[]                                      | no       | iOS/Android | yes               |
| containerStyle  | 组件的容器样式                                  | ViewStyle                                     | no       | iOS/Android | yes               |
| containerWidth  | 容器边距                                        | number                                        | no       | iOS/Android | yes               |
| loop            | 颜色分页是否循环滚动              | boolean                                       | no       | iOS/Android | yes               |
| numberOfRows    | 颜色行数从2到5                         | number                                        | no       | iOS/Android | yes               |
| onValueChange   | 当通过选择调色板中的一个色块而更改值时调用一次 | (value: string, colorInfo: ColorInfo) => void | no       | iOS/Android | yes               |
| style           | 组件样式                                            | ViewStyle                                     | no       | iOS/Android | yes               |
| swatchStyle     | 风格以通过调色板中的所有颜色样本           | ViewStyle                                     | no       | iOS/Android | yes               |
| testID          | 端到端测试的测试 ID                                    | string                                        | no       | iOS/Android | yes               |
| usePagination   | 当颜色数量超过行数时是否使用分页 | boolean                                       | no       | iOS/Android | yes               |
| value           | 所选色样的数值                             | string                                        | no       | iOS/Android | yes               |

**ColorPicker**：选色器组件。

| Name                | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| accessibilityLabels | 作为字符串对象的无障碍标签                 | { addButton: string, dismissButton: string, doneButton: string, input: string} | no       | iOS/Android | yes               |
| animatedIndex       | 默认为最后一项，首次渲染时要动画的项目索引 | number                                                       | no       | iOS/Android | yes               |
| backgroundColor     | ColorPicker 的背景颜色                           | string                                                       | no       | iOS/Android | yes               |
| colors              | 用于选择器调色板的颜色数组（十六进制值）  | string[]                                                     | no       | iOS/Android | yes               |
| onValueChange       | 选择器调色板更改的回调               | (value: string, colorInfo: ColorInfo) => void                | no       | iOS/Android | yes               |
| testID              | 用于端到端测试的测试 ID                                    | string                                                       | no       | iOS/Android | yes               |
| value               | 所选色样的数值                             | string                                                       | no       | iOS/Android | yes               |

**ColorSwatch**：颜色样板组件。

| Name        | Description                                                  | Type                                          | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | --------------------------------------------- | -------- | ----------- | ----------------- |
| animated    | 首次渲染是否应动画化                           | boolean                                       | no       | iOS/Android | yes               |
| color       | ColorSwatch 的颜色                                 | string                                        | no       | iOS/Android | yes               |
| index       | 如果在数组中，色样的索引                          | number                                        | no       | iOS/Android | yes               |
| onPress     | 按下事件的回调                                    | (value: string, colorInfo: ColorInfo) => void | no       | iOS/Android | yes               |
| selected    | 初始状态是否被选中                             | boolean                                       | no       | iOS/Android | yes               |
| size        | 颜色色样尺寸                                            | number                                        | no       | iOS/Android | yes               |
| style       | 组件的样式                                            | ViewStyle                                     | no       | iOS/Android | yes               |
| testID      | 用于端到端测试的测试 ID                                    | string                                        | no       | iOS/Android | yes               |
| unavailable | 初始状态是否不可用                          | boolean                                       | no       | iOS/Android | yes               |
| value       | 必须与同一组中的其他 ColorSwatch 不同，ColorSwatch 调色板中 ColorSwatch 的标识符值 | string                                        | no       | iOS/Android | yes               |

**DateTimePicker**：时间选择组件，该组件扩展了[TextField](https://wix.github.io/react-native-ui-lib/docs/components/form/TextField)属性，依赖[@react-native-community/datetimepicker](/zh-cn/react-native-community-datetimepicker)库。

| Name                              | Description                                                  | Type                                              | Required | Platform    | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------------------------- | -------- | ----------- | ----------------- |
| dateTimeFormatter                 | 用于格式化时间或日期的回调函数               | (value: Date, mode: DateTimePickerMode) => string | no       | iOS/Android | yes               |
| dialogProps                       | 传递给 Dialog 组件的属性                           | DialogProps                                       | no       | iOS/Android | yes               |
| display                           | 定义选择器的视觉显示。iOS 上的默认值为"spinner"，Android 上的默认值为"default"。所有可能值的列表包括 Android 上的 default、spinner、calendar 或 clock，以及 iOS 上的 default、spinner、compact 或 inline。完整列表可以在这里找到：[react-native-datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker#display-optional) | string                                            | no       | iOS/Android | yes               |
| editable                          | 此输入是否应可编辑或禁用                    | boolean                                           | no       | iOS/Android | yes               |
| headerStyle                       | 应用于 iOS 对话框标题的样式                      | ViewStyle                                         | no       | iOS/Android | yes               |
| is24Hour                          | 仅限 Android，允许将时间选择器更改为 24 小时格式 | boolean                                           | no       | Android     | no                |
| locale                            | 仅限 iOS，允许更改组件的区域设置     | string                                            | no       | iOS         | yes               |
| maximumDate                       | 要使用的最大日期或时间值                        | Date                                              | no       | iOS/Android | yes               |
| minimumDate                       | 要使用的最小日期或时间值                        | Date                                              | no       | iOS/Android | yes               |
| minuteInterval                    | 仅限 iOS，可以选择分钟的间隔。可能的值是：1、2、3、4、5、6、10、12、15、20、30 | number                                            | no       | iOS         | yes               |
| mode                              | 要显示的选择器类型（'date' 或 'time'）             | DATE \|TIME                                       | no       | iOS/Android | yes               |
| onChange                          | 当日期/时间更改时调用                             | () => Date                                        | no       | iOS/Android | yes               |
| renderInput                       | 渲染自定义输入                                          | JSX.Element                                       | no       | iOS/Android | yes               |
| themeVariant                      | 覆盖日期选择器使用的系统主题变体（深色或浅色模式） | LIGHT \|DARK                                      | no       | iOS/Android | yes               |
| timeZoneOffsetInMinutes           | 仅限 iOS，允许更改日期选择器的时区。默认使用设备的时区 | number                                            | no       | iOS         | yes               |
| value                             | 默认为设备的日期和时间，设置选择器的初始值 | Date                                              | no       | iOS/Android | yes               |
| backgroundColor<sup>7.43.1+</sup> | 滚轮选择器的背景颜色                        | string                                            | no       | iOS/Android | yes               |
| textColor<sup>7.43.1+</sup>       | 滚轮选择器项目的文本颜色                        | string                                            | no       | iOS/Android | no                |

**MaskedInput**：掩码输入组件，该组件扩展了[TextInput](https://reactnative.dev/docs/textinput)属性。

| Name             | Description                                                  | Type               | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------------------ | -------- | ----------- | ----------------- |
| containerStyle   | 掩码输入容器的容器样式               | ViewStyle          | no       | iOS/Android | yes               |
| renderMaskedText | 用于从实际输入返回的值渲染自定义输入的回调 | React.ReactElement | no       | iOS/Android | yes               |

**NumberInput**：数字输入框组件。

| Name              | Description                                                  | Type                            | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------------------- | -------- | ----------- | ----------------- |
| containerStyle    | 整个组件的容器样式                       | ViewStyle                       | no       | iOS/Android | yes               |
| contextMenuHidden | 需要安装 @react-native-community/clipboard。如果为 true，则上下文菜单隐藏。 | boolean                         | no       | iOS/Android | yes               |
| fractionDigits    | 小数点后的位数。必须在 0 - 20 的范围内（含）。 | number                          | no       | iOS/Android | yes               |
| initialNumber     | 有效的数字（在 en 区域设置中，即仅数字和小数点）。 | number                          | no       | iOS/Android | yes               |
| leadingText       | 前导文本                                               | string                          | no       | iOS/Android | yes               |
| leadingTextStyle  | 前导文本的样式                                | TextStyle                       | no       | iOS/Android | yes               |
| onChangeNumber    | 当数字值更改时调用的回调。   | (data: NumberInputData) => void | no       | iOS/Android | yes               |
| textFieldProps    | 除了通过命名属性直接传递的属性外，可以应用大多数 TextField 的属性。 | TextFieldProps                  | no       | iOS/Android | yes               |
| trailingText      | 尾随文本                                              | string                          | no       | iOS/Android | yes               |
| trailingTextStyle | 尾随文本的样式                               | ViewStyle                       | no       | iOS/Android | yes               |

**Picker**：弹窗选择组件。

| Name                                     | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| customPickerProps                        | 自定义选择器属性（使用 renderPicker 时，将应用于按钮包装器） | object                                                       | no       | iOS/Android | yes               |
| enableModalBlur                          | 仅限 iOS，为选择器模态添加模糊效果                   | boolean                                                      | no       | iOS         | yes               |
| fieldType                                | 为不同的字段类型 UI 传递（表单、过滤器或设置）  | PickerFieldTypes                                             | no       | iOS/Android | yes               |
| getLabel                                 | 返回所选 Picker 值要显示的标签的函数 | (value: string \| number) => void                            | no       | iOS/Android | yes               |
| items                                    | Picker 的数据源                                       | {label: string, value: string \| number}[]                   | no       | iOS/Android | yes               |
| listProps                                | 传递给包装选择器选项的列表组件的属性（允许控制 FlatList 行为） | FlatListProps                                                | no       | iOS/Android | yes               |
| migrate                                  | 迁移到 Picker 新 API 所需的临时属性    | boolean                                                      | no       | iOS/Android | yes               |
| mode                                     | 单选模式或多选模式                                    | SINGLE \| MULTI                                              | no       | iOS/Android | yes               |
| onChange                                 | 当选择器值更改时的回调                        | (value: string \| number) => void                            | no       | iOS/Android | yes               |
| onPress                                  | 为按下选择器时添加 onPress 回调            | () => void                                                   | no       | iOS/Android | yes               |
| onSearchChange                           | 选择器模态搜索输入文本更改的回调（仅在传递 showSearch 时） | V7.29.1:<br/>(searchValue: string) => void<br/>V7.43.1:<br/>(searchValue: string, filteredItems?: PickerFilteredItems) => void | no       | iOS/Android | yes               |
| pickerModalProps                         | 传递给选择器模态的属性                               | ModalProps                                                   | no       | iOS/Android | yes               |
| renderCustomModal                        | 渲染自定义选择器模态                                   | ({visible, children, toggleModal}) => void)                  | no       | iOS/Android | yes               |
| renderCustomSearch                       | 渲染自定义搜索输入（仅在传递 showSearch 时）    | (props) => void                                              | no       | iOS/Android | yes               |
| renderItem                               | 渲染自定义选择器项                                    | (value, {{...props, isSelected}}, itemLabel) => void         | no       | iOS/Android | yes               |
| renderPicker                             | 渲染自定义选择器 - 输入将是值（见上文）\示例：\renderPicker = (selectedItem) => {...} | (selectedItem, itemLabel) => void                            | no       | iOS/Android | yes               |
| searchPlaceholder                        | 搜索输入的占位符文本（仅在传递 showSearch 时） | string                                                       | no       | iOS/Android | yes               |
| searchStyle                              | 搜索输入的样式对象（仅在传递 showSearch 时） | {color: string, placeholderTextColor: string, selectionColor: string} | no       | iOS/Android | yes               |
| selectionLimit                           | 限制所选项目的数量                           | number                                                       | no       | iOS/Android | yes               |
| showSearch                               | 显示搜索输入以按标签过滤选择器项            | boolean                                                      | no       | iOS/Android | yes               |
| topBarProps                              | 选择器模态顶部栏属性                               | Modal's TopBarProps                                          | no       | iOS/Android | yes               |
| useSafeArea                              | 在选择器模态视图中添加安全区域                       | boolean                                                      | no       | iOS/Android | yes               |
| useWheelPicker                           | 使用滚轮选择器而不是列表选择器                    | boolean                                                      | no       | iOS/Android | yes               |
| value                                    | 选择器当前值                                         | string \| number                                             | no       | iOS/Android | yes               |
| renderCustomTopElement<sup>7.43.1+</sup> | 渲染自定义顶部元素                                    | (value?: PickerValue) =>  React.ReactElement                 | no       | iOS/Android | yes               |
| showLoader<sup>7.43.1+</sup>             | 显示加载器（当项目正在加载/获取时）            | boolean                                                      | no       | iOS/Android | yes               |
| customLoaderElement<sup>7.43.1+</sup>    | 自定义加载器元素                                        | ReactNode                                                    | no       | iOS/Android | yes               |

**Picker.Item**：弹窗选择Item组件，配合Picker组件使用。

| Name              | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| disabled          | 项目是否禁用                                         | boolean                                                      | no       | iOS/Android | yes               |
| getItemLabel      | 项目标签的自定义函数                           | (value: string \| number) => string                          | no       | iOS/Android | yes               |
| isSelected        | 项目是否被选中                                         | boolean                                                      | no       | iOS/Android | yes               |
| label             | 项目的标签                                                 | string                                                       | no       | iOS/Android | yes               |
| labelStyle        | 项目的标签样式                                           | ViewStyle                                                    | no       | iOS/Android | yes               |
| onPress           | onPress 操作的回调，如果返回 false 将停止选择 | (selected: boolean \| undefined, props: any) => void \| Promise<boolean>; | no       | iOS/Android | yes               |
| onSelectedLayout  | onLayout 事件的回调                                  | (event: LayoutChangeEvent) => void                           | no       | iOS/Android | yes               |
| selectedIcon      | 传递以更改选中图标                             | string                                                       | no       | iOS/Android | yes               |
| selectedIconColor | 传递以更改选中图标的颜色                       | ImageSource                                                  | no       | iOS/Android | yes               |
| value             | 项目的值                                                 | string \| number                                             | no       | iOS/Android | yes               |

**SectionsWheelPicker**：滚动选择组件。

| Name                | Description                                         | Type             | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| activeTextColor     | 聚焦行的文本颜色                      | string           | no       | iOS/Android | yes               |
| faderProps          | 淡入淡出器的自定义属性。                             | FaderProps       | no       | iOS/Android | yes               |
| inactiveTextColor   | 其他非聚焦行的文本颜色              | string           | no       | iOS/Android | yes               |
| itemHeight          | 描述 WheelPicker 中每个项目的高度 | number           | no       | iOS/Android | yes               |
| numberOfVisibleRows | 描述可见行数                 | number           | no       | iOS/Android | yes               |
| sections            | 部分数组                                   | WheelPickerProps | no       | iOS/Android | yes               |
| testID              | 组件测试 ID                               | string           | no       | iOS/Android | yes               |
| textStyle           | 行文本样式                                      | TextStyle        | no       | iOS/Android | yes               |

**SegmentedControl**：切换值组件。

| Name                         | Description                                     | Type                      | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ----------------------------------------------- | ------------------------- | -------- | ----------- | ----------------- |
| activeBackgroundColor        | 活动段落的背景颜色      | string                    | no       | iOS/Android | yes               |
| activeColor                  | 活动段落标签的颜色           | string                    | no       | iOS/Android | yes               |
| backgroundColor              | 非活动段落的背景颜色   | string                    | no       | iOS/Android | yes               |
| borderRadius                 | SegmentedControl 的边框半径               | number                    | no       | iOS/Android | yes               |
| containerStyle               | 容器的额外间距样式     | ViewStyle                 | no       | iOS/Android | yes               |
| iconOnRight                  | 图标是否应在标签的右侧        | boolean                   | no       | iOS/Android | yes               |
| initialIndex                 | 初始激活的索引                      | number                    | no       | iOS/Android | yes               |
| onChangeIndex                | 当索引更改时的回调。             | (index: number) => void   | no       | iOS/Android | yes               |
| outlineColor                 | 活动段落的轮廓颜色         | string                    | no       | iOS/Android | yes               |
| outlineWidth                 | 活动段落的轮廓宽度         | number                    | no       | iOS/Android | yes               |
| segmentLabelStyle            | 段落标签样式                             | TextStyle                 | no       | iOS/Android | yes               |
| segments                     | 段落数组                               | SegmentedControlItemProps | no       | iOS/Android | yes               |
| segmentsStyle                | 段落的额外样式               | ViewStyle                 | no       | iOS/Android | yes               |
| style                        | 内部容器的自定义样式                 | ViewStyle                 | no       | iOS/Android | yes               |
| testID                       | 组件测试 ID                               | string                    | no       | iOS/Android | yes               |
| throttleTime                 | 更改索引的尾随节流时间（毫秒）。 | number                    | no       | iOS/Android | yes               |
| label<sup>7.43.1+</sup>      | SegmentedControl 标签                          | string                    | no       | iOS/Android | yes               |
| labelProps<sup>7.43.1+</sup> | 为 SegmentedControl 标签传递属性      | TextProps                 | no       | iOS/Android | yes               |

**Stepper**：步进器组件。

| Name                   | Description                                         | Type                                     | Required | Platform    | HarmonyOS Support |
| ---------------------- | --------------------------------------------------- | ---------------------------------------- | -------- | ----------- | ----------------- |
| accessibilityLabel     | 组件无障碍标签                       | string                                   | no       | iOS/Android | yes               |
| disabled               | 禁用与步进器的交互               | boolean                                  | no       | iOS/Android | yes               |
| maxValue               | 最大值                                       | number                                   | no       | iOS/Android | yes               |
| minValue               | 最小值                                       | number                                   | no       | iOS/Android | yes               |
| onValueChange          | 值更改回调函数                      | (value: number, testID?: string) => void | no       | iOS/Android | yes               |
| small                  | 渲染小尺寸的步进器                       | boolean                                  | no       | iOS/Android | yes               |
| step                   | 增加和减少的步长（默认为 1） | number                                   | no       | iOS/Android | yes               |
| testID                 | 组件测试 ID                               | string                                   | no       | iOS/Android | yes               |
| value                  | 步进器值                                       | number                                   | no       | iOS/Android | yes               |
| type<sup>7.43.1+</sup> | 步进器样式类型                                  | StepperType                              | no       | iOS/Android | yes               |

**TextField**：文本域组件，扩展了[TextInput](https://reactnative.dev/docs/textinput)属性。

| Name                                     | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| centered                                 | 是否居中 TextField - 容器和标签        | boolean                                                      | no       | iOS/Android | yes               |
| charCounterStyle                         | 为字符计数器文本传递自定义样式                  | TextStyle                                                    | no       | iOS/Android | yes               |
| color                                    | 输入颜色                                                  | ColorType                                                    | no       | iOS/Android | yes               |
| containerProps                           | 整个组件的容器属性                       | Omit<ViewProps, 'style'>                                     | no       | iOS/Android | yes               |
| containerStyle                           | 整个组件的容器样式                       | ViewStyle                                                    | no       | iOS/Android | yes               |
| enableErrors                             | 是否应支持显示验证错误消息              | boolean                                                      | no       | iOS/Android | yes               |
| fieldStyle                               | 用于设置字段下划线、轮廓和填充颜色的字段容器的内部样式 | ViewStyle \| (context: FieldContextType, props) => ViewStyle | no       | iOS/Android | yes               |
| floatOnFocus                             | 占位符是否应在聚焦或开始输入时浮动       | boolean                                                      | no       | iOS/Android | yes               |
| floatingPlaceholder                      | 传递以添加浮动占位符支持                     | boolean                                                      | no       | iOS/Android | yes               |
| floatingPlaceholderColor                 | 浮动占位符颜色                               | ColorType                                                    | no       | iOS/Android | yes               |
| floatingPlaceholderStyle                 | 浮动占位符的自定义样式                    | TextStyle                                                    | no       | iOS/Android | yes               |
| formatter                                | 输入值的自定义格式化器（仅在输入未聚焦时使用） | (value) => string \| undefined                               | no       | iOS/Android | yes               |
| hint                                     | 聚焦字段时显示的提示文本               | string                                                       | no       | iOS/Android | yes               |
| label                                    | 字段标签                                                  | string                                                       | no       | iOS/Android | yes               |
| labelColor                               | 字段标签颜色。可以是字符串或按状态映射的颜色（{default, focus, error, disabled, readonly}） | ColorType                                                    | no       | iOS/Android | yes               |
| labelProps                               | 为标签文本元素传递额外属性                   | TextProps                                                    | no       | iOS/Android | yes               |
| labelStyle                               | 字段标签的自定义样式                             | TextStyle                                                    | no       | iOS/Android | yes               |
| leadingAccessory                         | 传递以渲染前导元素                             | ReactElement                                                 | no       | iOS/Android | yes               |
| onChangeValidity                         | 当字段有效性更改时的回调                 | (isValid: boolean) => void                                   | no       | iOS/Android | yes               |
| onValidationFailed                       | 当字段验证失败时的回调                 | (failedValidatorIndex: number) => void                       | no       | iOS/Android | yes               |
| placeholder                              | 字段的占位符                                | string                                                       | no       | iOS/Android | yes               |
| placeholderTextColor                     | 占位符文本颜色                                       | ColorType                                                    | no       | iOS/Android | yes               |
| preset                                   | 用于设置字段样式的预定义预设               | 'default' \| null \|string                                   | no       | iOS/Android | yes               |
| readonly                                 | 只读状态的 UI 预设                              | boolean                                                      | no       | iOS/Android | yes               |
| recorderTag                              | 记录器标签                                                 | 'mask' \| 'unmask'                                           | no       | iOS/Android | yes               |
| retainValidationSpace                    | 即使没有验证消息也保留验证空间 | boolean                                                      | no       | iOS/Android | yes               |
| showCharCounter                          | 是否应显示字符计数器（仅在使用 maxLength 时有效）  | boolean                                                      | no       | iOS/Android | yes               |
| showMandatoryIndication                  | 是否显示必填字段指示                 | boolean                                                      | no       | iOS/Android | yes               |
| trailingAccessory                        | 传递以渲染尾随元素                            | ReactElement                                                 | no       | iOS/Android | yes               |
| useGestureHandlerInput                   | 为基础 TextInput 使用 react-native-gesture-handler 而不是 react-native | boolean                                                      | no       | iOS/Android | yes               |
| validate                                 | 单个或多个验证器。可以是字符串（required, email）或自定义函数。 | Validator \| Validator []                                    | no       | iOS/Android | yes               |
| validateOnBlur                           | 是否应在失去 TextField 焦点时验证               | boolean                                                      | no       | iOS/Android | yes               |
| validateOnChange                         | 是否应在 TextField 值更改时验证             | boolean                                                      | no       | iOS/Android | yes               |
| validateOnStart                          | 是否应在 TextField 挂载时验证                    | boolean                                                      | no       | iOS/Android | yes               |
| validationMessage                        | 当字段无效时显示的验证消息（取决于 validate） | string \| string[]                                           | no       | iOS/Android | yes               |
| validationMessagePosition                | 验证消息的位置（顶部/底部）          | ValidationMessagePosition                                    | no       | iOS/Android | yes               |
| validationMessageStyle                   | 验证消息的自定义样式                      | TextStyle                                                    | no       | iOS/Android | yes               |
| validationDebounceTime<sup>7.43.1+</sup> | 发送 validateOnChange 时添加去超时时间         | number                                                       | no       | iOS/Android | yes               |
| innerFlexBehavior<sup>7.43.1+</sup>      | 设置内部容器使用 flex 行为来解决使用前导或尾随附件时的文本溢出问题（当字段在行容器内时可能会导致 flex 问题） | boolean                                                      | no       | iOS/Android | yes               |

**WheelPicker**：轮式拾取器组件。

| Name                | Description                                                  | Type                                            | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | ----------------------------------------------- | -------- | ----------- | ----------------- |
| activeTextColor     | 聚焦行的文本颜色                               | string                                          | no       | iOS/Android | yes               |
| align               | 将内容对齐到中心、右侧或左侧                   | WheelPickerAlign                                | no       | iOS/Android | yes               |
| flatListProps       | 要发送给 FlatList 的属性。                            | FlatListProps                                   | no       | iOS/Android | yes               |
| inactiveTextColor   | 其他非聚焦行的文本颜色                       | string                                          | no       | iOS/Android | yes               |
| initialValue        | 初始值（非受控）                                 | number \| string                                | no       | iOS/Android | yes               |
| itemHeight          | WheelPicker 中每个项目的高度                       | number                                          | no       | iOS/Android | yes               |
| items               | WheelPicker 的数据源                                  | WheelPickerItemProps[]                          | no       | iOS/Android | yes               |
| label               | 在项目文本旁边渲染的额外标签            | string                                          | no       | iOS/Android | yes               |
| labelProps          | 额外标签的属性                                     | TextProps                                       | no       | iOS/Android | yes               |
| labelStyle          | 额外标签的样式                                     | TextStyle                                       | no       | iOS/Android | yes               |
| numberOfVisibleRows | 可见行数                                       | number                                          | no       | iOS/Android | yes               |
| onChange            | 更改项目事件回调                                   | (item: string \| number, index: number) => void | no       | iOS/Android | yes               |
| separatorsStyle     | 分隔符的额外样式                               | ViewStyle                                       | no       | iOS/Android | yes               |
| style               | 高度根据 itemHeight * numberOfVisibleRows 计算。容器的自定义样式 | ViewStyle                                       | no       | iOS/Android | yes               |
| testID              | 测试标识符                                              | string                                          | no       | iOS/Android | yes               |
| textStyle           | 行文本自定义样式                                        | TextStyle                                       | no       | iOS/Android | yes               |

**Incubator.Dialog**：弹出对话框组件。

| Name                  | Description                                                  | Type                          | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------------------------- | -------- | ----------- | ----------------- |
| containerProps        | 容器的额外属性                                | ViewProps                     | no       | iOS/Android | yes               |
| containerStyle        | Dialog 的容器样式（设置为 {position: 'absolute'}） `ViewStyle ` | ViewStyle                     | no       | iOS/Android | yes               |
| direction             | 对话框动画/平移的方向（默认为向下）。 | up \|down \|left \|right      | no       | iOS/Android | yes               |
| headerProps           | Dialog 的标题（标题、副标题等）                    | DialogHeaderProps             | no       | iOS/Android | yes               |
| ignoreBackgroundPress | 是否忽略背景按下。                   | boolean                       | no       | iOS/Android | yes               |
| modalProps            | 传递给对话框模态的属性                               | ModalProps                    | no       | iOS/Android | yes               |
| onDismiss             | 在对话框关闭后调用的回调（动画结束后）。 | (props?: DialogProps) => void | no       | iOS/Android | yes               |
| testID                | 用于在端到端测试中定位此视图。容器具有原始 ID。支持的内部元素 ID：`${TestID}.modal` - Modal 的 ID。`${TestID}. overlayFadingBackground` - 淡入淡出背景的 ID。 | string                        | no       | iOS/Android | yes               |
| visible               | 对话框的可见性                                 | boolean                       | no       | iOS/Android | yes               |

**Dialog.Header**：弹窗头部组件。

| Name                  | Description                                                  | Type                 | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | -------------------- | -------- | ----------- | ----------------- |
| bottomAccessory       | 传递以在副标题下方渲染底部元素           | ReactElement         | no       | iOS/Android | yes               |
| contentContainerStyle | 前导 + 内容 + 尾随组件的样式（不含底部附件） | ViewProps['style']   | no       | iOS/Android | yes               |
| leadingAccessory      | 传递以渲染前导元素                             | ReactElement         | no       | iOS/Android | yes               |
| onPress               | 内部内容的 onPress 回调                       | () => void           | no       | iOS/Android | yes               |
| showDivider           | 显示标题的分隔符                                    | boolean              | no       | iOS/Android | yes               |
| showKnob              | 显示标题的旋钮                                       | boolean              | no       | iOS/Android | yes               |
| subtitle              | 副标题                                                     | string               | no       | iOS/Android | yes               |
| subtitleProps         | 副标题的额外属性                                         | TextProps            | no       | iOS/Android | yes               |
| subtitleStyle         | 副标题文本样式                                          | StyleProp<TextStyle> | no       | iOS/Android | yes               |
| title                 | 标题                                                        | string               | no       | iOS/Android | yes               |
| titleProps            | 标题的额外属性                                            | TextProps            | no       | iOS/Android | yes               |
| titleStyle            | 标题文本样式                                             | StyleProp<TextStyle> | no       | iOS/Android | yes               |
| topAccessory          | 传递以在标题上方渲染顶部元素                 | ReactElement         | no       | iOS/Android | yes               |
| trailingAccessory     | 传递以渲染尾随元素                            | ReactElement         | no       | iOS/Android | yes               |

**Incubator.Slider**：滑块组件。

| Name                   | Description                                                  | Type                                  | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------- | -------- | ----------- | ----------------- |
| accessible             | 如果为 true，组件将启用无障碍功能 | boolean                               | no       | iOS/Android | yes               |
| activeThumbStyle       | 活动时（按下时）的拇指样式                        | ViewStyle                             | no       | iOS/Android | yes               |
| containerStyle         | 容器样式                                          | ViewStyle                             | no       | iOS/Android | yes               |
| disableActiveStyling   | 如果为 true，Slider 在按下时不会改变其样式       | boolean                               | no       | iOS/Android | yes               |
| disableRTL             | 如果为 true，即使应用程序处于 RTL 模式，Slider 也将保持在 LTR 模式 | boolean                               | no       | iOS/Android | yes               |
| disabled               | 如果为 true，Slider 将被禁用并以禁用颜色显示 | boolean                               | no       | iOS/Android | yes               |
| disabledThumbTintColor | 禁用的拇指颜色                                         | string                                | no       | iOS/Android | yes               |
| enableThumbShadow      | 拇指是否会有阴影（仅在 'migrate' 为 true 时） | boolean                               | no       | iOS/Android | yes               |
| initialMaximumValue    | 仅当 `useRange` 为 true 时。初始最大值          | number                                | no       | iOS/Android | yes               |
| initialMinimumValue    | 仅当 `useRange` 为 true 时。初始最小值          | number                                | no       | iOS/Android | yes               |
| maximumTrackTintColor  | 轨道颜色                                              | string                                | no       | iOS/Android | yes               |
| maximumValue           | 轨道最大值                                          | number                                | no       | iOS/Android | yes               |
| minimumTrackTintColor  | 从最小值到当前值的轨道颜色 | string                                | no       | iOS/Android | yes               |
| minimumValue           | 轨道最小值                                          | number                                | no       | iOS/Android | yes               |
| onRangeChange          | onRangeChange 的回调。返回包含最小值和最大值的值对象 | SliderOnRangeChange                   | no       | iOS/Android | yes               |
| onReset                | 当重置功能被调用时通知的回调   | () => void                            | no       | iOS/Android | yes               |
| onSeekEnd              | 通知滑块寻道已完成时的回调      | () => void                            | no       | iOS/Android | yes               |
| onSeekStart            | 通知滑块寻道开始时的回调       | () => void                            | no       | iOS/Android | yes               |
| onValueChange          | onValueChange 的回调                                   | SliderOnValueChange                   | no       | iOS/Android | yes               |
| renderTrack            | 自定义渲染而不是渲染轨道                 | () => ReactElement  \| ReactElement[] | no       | iOS/Android | yes               |
| step                   | 滑块的步长值。该值应介于 0 与（最大值 - 最小值）之间 | number                                | no       | iOS/Android | yes               |
| testID                 | 组件测试 ID                                        | string                                | no       | iOS/Android | yes               |
| throttleTime           | 控制 onValueChange 和 onRangeChange 回调的节流时间 | number                                | no       | iOS/Android | yes               |
| thumbHitSlop           | 定义触摸事件可以从拇指开始多远  | number                                | no       | iOS/Android | yes               |
| thumbStyle             | 拇指样式                                              | ViewStyle                             | no       | iOS/Android | yes               |
| thumbTintColor         | 拇指颜色                                                  | string                                | no       | iOS/Android | yes               |
| trackStyle             | 轨道样式                                              | ViewStyle                             | no       | iOS/Android | yes               |
| useGap                 | 如果为 true，最小值和最大值的拇指将不会重叠              | boolean                               | no       | iOS/Android | yes               |
| useRange               | 如果为 true，Slider 将显示第二个拇指用于最小值 | boolean                               | no       | iOS/Android | yes               |
| value                  | 初始值                                                | number                                | no       | iOS/Android | yes               |

**Incubator.Toast**：非中断式弹窗组件。

| Name                 | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| action               | 用户的单个操作（showLoader 将覆盖此操作） | ButtonProps                                                  | no       | iOS/Android | yes               |
| autoDismiss          | 自动调用 onDismiss 回调的毫秒时间 | number                                                       | no       | iOS/Android | yes               |
| backgroundColor      | Toast 的背景颜色                                   | string                                                       | no       | iOS/Android | yes               |
| centerMessage        | 消息是否应在 Toast 中居中                      | boolean                                                      | no       | iOS/Android | yes               |
| containerStyle       | Toast 容器样式                                        | ViewStyle                                                    | no       | iOS/Android | yes               |
| elevation            | 仅限 Android。自定义高程                               | number                                                       | no       | Android     | no                |
| enableHapticFeedback | 是否在 Toast 显示时触发触觉反馈（需要 react-native-haptic-feedback 依赖） | boolean                                                      | no       | iOS/Android | yes               |
| icon                 | 在 Toast 左侧渲染的自定义图标        | ImageSourcePropType                                          | no       | iOS/Android | yes               |
| iconColor            | 图标颜色                                               | string                                                       | no       | iOS/Android | yes               |
| message              | Toast 消息                                                | string                                                       | no       | iOS/Android | yes               |
| messageProps         | Toast 消息属性                                          | TextProps                                                    | no       | iOS/Android | yes               |
| messageStyle         | Toast 消息样式                                          | StyleProp <TextStyle>                                        | no       | iOS/Android | yes               |
| onAnimationEnd       | Toast 动画结束时的回调                          | (visible?: boolean) => void                                  | no       | iOS/Android | yes               |
| onDismiss            | Toast 关闭时的回调                             | () => void                                                   | no       | iOS/Android | yes               |
| position             | Toast 的位置。'top' 或 'bottom'。                | 'top' \| 'bottom'                                            | no       | iOS/Android | yes               |
| preset               | 传递以使用预设 UI                                       | ToastPreset ('success' \| 'failure' \| 'general' \| 'offline') | no       | iOS/Android | yes               |
| renderAttachment     | 渲染一个自定义视图，该视图将永久显示在 Toast 的上方或下方，取决于 Toast 的位置，并在 Toast 可见或关闭时随之动画 | () => JSX.Element \| undefined                               | no       | iOS/Android | yes               |
| showLoader           | 是否显示加载器                                     | boolean                                                      | no       | iOS/Android | yes               |
| style                | Toast 样式                                                  | ViewStyle                                                    | no       | iOS/Android | yes               |
| swipeable            | 是否支持通过滑动手势关闭 Toast。需要传递 onDismiss 方法来控制可见性 | boolean                                                      | no       | iOS/Android | yes               |
| testID               | 组件测试 ID                                        | string                                                       | no       | iOS/Android | yes               |
| visible              | 是否显示或隐藏 Toast                            | boolean                                                      | no       | iOS/Android | yes               |
| zIndex               | Toast 的自定义 zIndex                                      | number                                                       | no       | iOS/Android | yes               |

**Dash**：阔折现组件。

| Name           | Description                           | Type      | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------- | --------- | -------- | ----------- | ----------------- |
| color          | 虚线的颜色               | string    | no       | iOS/Android | yes               |
| containerStyle | 容器样式                   | ViewStyle | no       | iOS/Android | yes               |
| gap            | 虚线之间的间距            | number    | no       | iOS/Android | yes               |
| length         | 虚线的长度              | number    | no       | iOS/Android | yes               |
| style          | 虚线的额外样式        | ViewStyle | no       | iOS/Android | yes               |
| thickness      | 虚线的厚度           | number    | no       | iOS/Android | yes               |
| vertical       | 虚线是否应为垂直 | boolean   | no       | iOS/Android | yes               |

**ExpandableSection**：展开收起组件。

| Name          | Description                                              | Type            | Required | Platform    | HarmonyOS Support |
| ------------- | -------------------------------------------------------- | --------------- | -------- | ----------- | ----------------- |
| children      | 可展开的子项                                | React.ReactNode | no       | iOS/Android | yes               |
| expanded      | ExpandableSection 是否应展开                 | boolean         | no       | iOS/Android | yes               |
| onPress       | 当按下 ExpandableSection 的标题时调用 | () => void      | no       | iOS/Android | yes               |
| sectionHeader | 标题元素                                           | JSX.Element     | no       | iOS/Android | yes               |
| testID        | 测试标识符                                       | string          | no       | iOS/Android | yes               |
| top           | 是否应在 'sectionHeader' 上方打开                 | boolean         | no       | iOS/Android | yes               |

**Fader**：渐变淡入淡出组件。

| Name      | Description                                        | Type                           | Required | Platform    | HarmonyOS Support |
| --------- | -------------------------------------------------- | ------------------------------ | -------- | ----------- | ----------------- |
| position  | 淡入淡出器的位置（图像不同） | START  \|END \| TOP  \| BOTTOM | no       | iOS/Android | yes               |
| size      | 更改淡入淡出视图的大小                   | number                         | no       | iOS/Android | yes               |
| tintColor | 更改淡入淡出视图的色调颜色             | string                         | no       | iOS/Android | yes               |
| visible   | 淡入淡出器是否可见（默认为 true）     | boolean                        | no       | iOS/Android | yes               |

**Gradient**：渐变色组件。

| Name          | Description                       | Type          | Required | Platform    | HarmonyOS Support |
| ------------- | --------------------------------- | ------------- | -------- | ----------- | ----------------- |
| color         | 渐变的颜色         | string        | no       | iOS/Android | yes               |
| numberOfSteps | 步数               | number        | no       | iOS/Android | yes               |
| style         | 组件的额外样式 | ViewStyle     | no       | iOS/Android | yes               |
| type          | 色调 \| 亮度 \| 饱和度    | GradientTypes | no       | iOS/Android | yes               |

**KeyboardAccessoryView**：键盘附件视图。

| Name                  | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| kbComponent           | 键盘 ID（发送到 KeyboardRegistry 的 componentID）   | string                   | no       | iOS/Android | no                |
| kbInitialProps        | 将发送到 KeyboardComponent 的属性         | any                      | no       | iOS/Android | no                |
| kbInputRef            | 仅限 iOS。实际文本输入的引用（否则键盘可能无法在指示时重置等）。 | any                      | no       | iOS         | no                |
| onHeightChanged       | 高度更改时的回调                    | (height: number) => void | no       | iOS/Android | no                |
| onItemSelected        | 当键盘上的项目被按下时将调用的回调。 | () => void               | no       | iOS/Android | no                |
| onKeyboardResigned    | 键盘关闭后将调用的回调 | () => void               | no       | iOS/Android | no                |
| onRequestShowKeyboard | 如果调用 KeyboardRegistry.requestShowKeyboard 将调用的回调。 | () => void               | no       | iOS/Android | no                |
| renderContent         | 在键盘上方渲染的内容                    | () => React.ReactElement | no       | iOS/Android | yes               |

**KeyboardAwareInsetsView**：用于在使用键盘时添加插入，可能会隐藏部分屏幕，该组件扩展了[KeyboardTrackingView](https://wix.github.io/react-native-ui-lib/docs/components/infra/KeyboardTrackingView)属性，此组件仅适用与iOS。

| Name                    | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| KeyboardAwareInsetsView | 在使用键盘时添加插入，可能会隐藏部分屏幕。 | Component | no       | iOS      | no                |

**KeyboardRegistry**：用于注册键盘并在键盘上执行某些操作。

| Name                | Description                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | --------------- | -------- | ----------- | ----------------- |
| addListener         | 为回调添加监听器。globalID（字符串）- 包含 componentID 和事件名称的 ID（例如，如果 componentID='kb1' globalID='kb1.onItemSelected'）callback（函数）- 当所述事件发生时调用的回调 | static function | no       | iOS/Android | yes               |
| getAllKeyboards     | 获取所有键盘                                            | static function | no       | iOS/Android | yes               |
| getKeyboard         | 获取特定键盘 componentID（字符串）- 键盘的 ID。 | static function | no       | iOS/Android | yes               |
| getKeyboards        | 按 ID 获取键盘 componentIDs（字符串[]）- 键盘的 ID。 | static function | no       | iOS/Android | yes               |
| notifyListeners     | 通知事件已发生。globalID（字符串）- 包含 componentID 和事件名称的 ID（例如，如果 componentID='kb1' globalID='kb1.onItemSelected'）args（对象）- 要发送给监听器的数据。 | static function | no       | iOS/Android | yes               |
| onItemSelected      | 当键盘上的项目被按下时使用的默认事件。componentID（字符串）- 键盘的 ID。args（对象）- 要发送给监听器的数据。 | static function | no       | iOS/Android | yes               |
| registerKeyboard    | 注册新键盘。componentID（字符串）- 键盘的 ID。generator（函数）- 用于创建键盘的函数。params（对象）- 在使用其他方法（即 getKeyboards 和 getAllKeyboards）时返回。 | static function | no       | iOS/Android | yes               |
| removeListeners     | 为回调移除监听器。globalID（字符串）- 包含 componentID 和事件名称的 ID（例如，如果 componentID='kb1' globalID='kb1.onItemSelected'） | static function | no       | iOS/Android | yes               |
| requestShowKeyboard | 请求显示键盘 componentID（字符串）- 键盘的 ID。 | static function | no       | iOS/Android | yes               |

**KeyboardTrackingView**：为该视图及其子视图启用"键盘跟踪"的 UI 组件。通常用于该视图内有 TextField 或 TextInput 的情况，该组件仅适用于iOS。

| Name                                 | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ------------------------------------ | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| addBottomView                        | 在 KeyboardAccessoryView 下方添加视图。                | boolean   | no       | iOS      | no                |
| allowHitsOutsideBounds               | 允许命中放置在视图边界之外的子视图。 | boolean   | no       | iOS      | no                |
| bottomViewColor                      | 底部视图的颜色。                                     | string    | no       | iOS      | no                |
| manageScrollView                     | 设置为 false 以关闭插入管理并自行管理。 | boolean   | no       | iOS      | no                |
| ref                                  | 引用                                                          | any       | no       | iOS      | no                |
| requiresSameParentToManageScrollView | 如果 manageScrollView 设置为 true 但仍然不起作用，则设置为 true，这意味着找到的 ScrollView 是错误的，您必须将 KeyboardAccessoryView 和 ScrollView 作为兄弟节点并设置此项为 true。 | boolean   | no       | iOS      | no                |
| revealKeyboardInteractive            | 在负滚动时显示键盘。                      | boolean   | no       | iOS      | no                |
| scrollBehavior                       | 滚动行为（使用 KeyboardTrackingView. scrollBehaviors.NONE \|SCROLL_TO_BOTTOM_INVERTED_ONLY \| FIXED_OFFSET） | number    | no       | iOS      | no                |
| scrollToFocusedInput                 | ScrollView 是否应滚动到聚焦的输入            | boolean   | no       | iOS      | no                |
| style                                | 样式                                                        | ViewStyle | no       | iOS      | no                |
| trackInteractive                     | 在键盘以交互方式关闭时启用跟踪（默认为 false）。为什么？当使用外部键盘（BT）时，您仍然会收到键盘事件，并且当您聚焦输入时视图只是悬停。此外，如果您不使用交互式关闭键盘的样式（或者如果您在此视图内没有输入），无论如何跟踪它都没有意义。（这是由于使用 inputAccessory 能够跟踪键盘交互更改而导致的，它引入了这个错误） | boolean   | no       | iOS      | no                |
| useSafeArea                          | 是否处理 SafeArea。                           | boolean   | no       | iOS      | no                |
| usesBottomTabs                       | 是否包括底部标签栏插入。              | boolean   | no       | iOS      | no                |

**Overlay**：带类型覆盖视图，为Image组件属性，扩展了[image](https://reactnative.dev/docs/image)组件。

| Name          | Description                                               | Type                                                  | Required | Platform    | HarmonyOS Support |
| ------------- | --------------------------------------------------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| color         | 覆盖颜色                                         | string                                                | no       | iOS/Android | yes               |
| customContent | 在图像顶部渲染的自定义覆盖内容 | JSX.Element                                           | no       | iOS/Android | yes               |
| intensity     | 渐变的强度。                            | low \|medium \|high                                   | no       | iOS/Android | yes               |
| type          | 设置在图像顶部的覆盖类型            | vertical \| top  \| bottom \| solid (OverlayTypeType) | no       | iOS/Android | yes               |

**Card**：卡片组件，扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)组件，依赖[@react-native-community/blur](/zh-cn/react-native-community-blur.md)。

| Name             | Description                                                  | Type                 | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------------------- | -------- | ----------- | ----------------- |
| blurOptions      | 根据 @react-native-community/blur 库的模糊效果选项（确保 enableBlur 开启） | object               | no       | iOS/Android | yes               |
| borderRadius     | 卡片边框半径（将传递给内部 Card.Image 组件） | number               | no       | iOS/Android | yes               |
| containerStyle   | 卡片容器的额外样式                     | ViewStyle            | no       | iOS/Android | yes               |
| elevation        | 仅限 Android。高程值                                | number               | no       | Android     | no                |
| enableBlur       | 仅限 iOS。启用模糊效果                                 | boolean              | no       | iOS         | no                |
| enableShadow     | 卡片是否应有阴影                   | boolean              | no       | iOS/Android | yes               |
| height           | 卡片自定义高度                                           | number \| string     | no       | iOS/Android | yes               |
| onPress          | 卡片按下事件的回调函数                       | function             | no       | iOS/Android | yes               |
| row              | 内部卡片流动方向是否应为水平               | boolean              | no       | iOS/Android | yes               |
| selected         | 添加视觉指示表明卡片被选中             | boolean              | no       | iOS/Android | yes               |
| selectionOptions | 样式化选择指示的自定义选项          | CardSelectionOptions | no       | iOS/Android | yes               |
| width            | 卡片自定义宽度                                            | number  \| string    | no       | iOS/Android | yes               |

**Card.Image**：Card 组件的内部组件（最好是直接子组件），扩展了[Image](https://wix.github.io/react-native-ui-lib/docs/components/media/Image)组件。

| Name     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| height   | 高度                                                       | number   | no       | iOS/Android | yes               |
| position | 图像位置，确定图像的适当弹性度和边框半径（对于 Android）如果作为 Card 父组件的直接子组件渲染，则此属性会自动从 Card 父组件派生 | string[] | no       | iOS/Android | yes               |
| width    | 宽度                                                        | number   | no       | iOS/Android | yes               |

**Card.Section**：用于在 Card 组件内轻松渲染内容的内部组件，扩展了[View](https://wix.github.io/react-native-ui-lib/docs/components/basic/View)组件。

| Name            | Description                                                  | Type                | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------------- | -------- | ----------- | ----------------- |
| backgroundColor | 背景颜色                                             | string              | no       | iOS/Android | yes               |
| content         | 文本内容。示例：content={[{text: 'You’re Invited!', text70: true, grey10: true}]} | ContentType[]       | no       | iOS/Android | yes               |
| contentStyle    | 组件的容器样式                                  | ViewStyle           | no       | iOS/Android | yes               |
| imageProps      | 将传递给图像的其他图像属性           | ImageProps          | no       | iOS/Android | yes               |
| imageSource     | 提供时将用作背景                | ImageSourcePropType | no       | iOS/Android | yes               |
| imageStyle      | 背景图像的样式                           | ImageStyle          | no       | iOS/Android | yes               |
| leadingIcon     | 在文本之前渲染的前导图标的图像属性     | ImageProps          | no       | iOS/Android | yes               |
| trailingIcon    | 在文本之后渲染的尾随图标的图像属性     | ImageProps          | no       | iOS/Android | yes               |

**Carousel**：轮播组件，扩展了[ScrollView](https://reactnative.dev/docs/scrollview)组件。

| Name                      | Description                                                  | Type                                    | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | --------------------------------------- | -------- | ----------- | ----------------- |
| allowAccessibleLayout     | 是否为无障碍布局 Carousel                 | boolean                                 | no       | iOS/Android | yes               |
| animated                  | 容器是否应动画化（通过 containerStyle 发送动画样式） | boolean                                 | no       | iOS/Android | yes               |
| animatedScrollOffset      | 传递以附加到 ScrollView 的 Animated.event，以便基于 Carousel 滚动偏移动画元素（传递新的 Animated.ValueXY()） | Animated.ValueXY                        | no       | iOS/Android | yes               |
| autoplay                  | 启用自动在页面之间切换             | boolean                                 | no       | iOS/Android | yes               |
| autoplayInterval          | 在切换到下一页之前等待的时间（毫秒）（需要启用 'autoplay'） | number                                  | no       | iOS/Android | yes               |
| containerMarginHorizontal | Carousel 容器的水平边距                 | number                                  | no       | iOS/Android | yes               |
| containerPaddingVertical  | Carousel 容器的垂直内边距（有时在 Android 中需要，当有溢出被截断时）。 | number                                  | no       | iOS/Android | yes               |
| containerStyle            | Carousel 容器样式                                 | ViewStyle                               | no       | iOS/Android | yes               |
| counterTextStyle          | 计数器的文本样式                                     | ViewStyle                               | no       | iOS/Android | yes               |
| horizontal                | 页面将水平渲染还是垂直渲染    | boolean                                 | no       | iOS/Android | yes               |
| initialPage               | 开始的初始页面                                 | number                                  | no       | iOS/Android | yes               |
| itemSpacings              | 页面之间的间距                                | number                                  | no       | iOS/Android | yes               |
| loop                      | 如果为 true，将具有无限滚动（仅适用于水平 Carousel） | boolean                                 | no       | iOS/Android | yes               |
| onChangePage              | 页面更改事件的回调                               | (pageIndex, oldPageIndex, info) => void | no       | iOS/Android | yes               |
| onScroll                  | 为内部 ScrollView 的 onScroll 事件附加回调 | function                                | no       | iOS/Android | yes               |
| pageControlPosition       | PageControl 组件的位置 ['over', 'under']，否则不会显示 | PageControlPosition                     | no       | iOS/Android | yes               |
| pageControlProps          | PageControl 组件属性                                  | PageControlProps                        | no       | iOS/Android | yes               |
| pageHeight                | 页面高度（所有页面应具有相同的高度）。     | number                                  | no       | iOS/Android | yes               |
| pageWidth                 | 页面宽度（所有页面应具有相同的宽度）。如果传递 'loop' 属性则不起作用 | number                                  | no       | iOS/Android | yes               |
| pagingEnabled             | 将阻止多页面滚动（如果使用 'pageWidth' 属性则不起作用） | boolean                                 | no       | iOS/Android | yes               |
| showCounter               | 是否显示页面计数器（如果使用 'pageWidth' 属性则不起作用） | boolean                                 | no       | iOS/Android | yes               |

**LoaderScreen**：全屏显示组件，通常用于页面加载loading，扩展了[Activityindicator](https://reactnative.dev/docs/activityindicator)组件。

| Name            | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| backgroundColor | 加载器背景的颜色（仅在传递 'overlay' 时） | string           | no       | iOS/Android | yes               |
| containerStyle  | 自定义容器样式                                       | ViewStyle        | no       | iOS/Android | yes               |
| customLoader    | 自定义加载器                                                | React.ReactChild | no       | iOS/Android | yes               |
| loaderColor     | 加载指示器的颜色                               | string           | no       | iOS/Android | yes               |
| message         | 加载器消息                                               | string           | no       | iOS/Android | yes               |
| messageStyle    | 消息样式                                                | TextStyle        | no       | iOS/Android | yes               |
| overlay         | 将屏幕显示为绝对覆盖                       | boolean          | no       | iOS/Android | yes               |

**StackAggregator**：堆栈聚合器组件。

| Name                  | Description                                                  | Type                         | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ---------------------------- | -------- | ----------- | ----------------- |
| buttonProps           | 传递给"显示更少"按钮的属性                       | ButtonProps                  | no       | iOS/Android | yes               |
| children              | 组件子项                                           | JSX.Element \| JSX.Element[] | no       | iOS/Android | yes               |
| collapsed             | 堆栈的初始状态                               | boolean                      | no       | iOS/Android | yes               |
| containerStyle        | 容器样式                                          | ViewStyle                    | no       | iOS/Android | yes               |
| contentContainerStyle | 内容容器样式                                  | ViewStyle                    | no       | iOS/Android | yes               |
| disablePresses        | 禁用卡片可按下性的设置                | boolean                      | no       | iOS/Android | yes               |
| itemBorderRadius      | 项目的边框半径                                      | number                       | no       | iOS/Android | yes               |
| onCollapseChanged     | 折叠状态更改的回调（值是折叠状态） | (changed: boolean) => void   | no       | iOS/Android | yes               |
| onCollapseWillChange  | 折叠状态将要更改的回调（值是未来的折叠状态） | (changed: boolean) => void   | no       | iOS/Android | yes               |
| onItemPress           | 项目按下的回调                                    | (index: number) => void      | no       | iOS/Android | yes               |

**StateScreen**：显示全屏组件。

| Name        | Description                                                  | Type           | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------------- | -------- | ----------- | ----------------- |
| ctaLabel    | 在 CTA 按钮中显示的文本                            | string         | no       | iOS/Android | yes               |
| imageSource | 顶部显示的图像源。使用本地需要的图像 | ImageURISource | no       | iOS/Android | yes               |
| onCtaPress  | CTA 按钮的操作处理程序                                | () => void     | no       | iOS/Android | yes               |
| testID      | 用于在测试中标识容器                       | string         | no       | iOS/Android | yes               |
| title       | 显示为标题                                      | string         | no       | iOS/Android | yes               |

**Drawer**：抽屉组件，如果您的应用程序与 RNN 配合使用，则您的屏幕必须使用"react-native-gesture-handler"中的gestureHandlerRootHOC 进行包装。请参阅[这里](https://kmagiera.github.io/react-native-gesture-handler/docs/getting-started.html#with-wix-react-native-navigation-https-githubcom-wix-react-native-navigation)。

| Name                 | Description                                                  | Type                                                  | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| bounciness           | 抽屉动画的弹性度                              | number                                                | no       | iOS/Android | yes               |
| customValue          | 传递给组件并在操作回调中接收的任何类型的自定义值 | any                                                   | no       | iOS/Android | yes               |
| disableHaptic        | 是否禁用触觉                                | boolean                                               | no       | iOS/Android | yes               |
| fullLeftThreshold    | 左全滑动的阈值（0-1）                        | number                                                | no       | iOS/Android | yes               |
| fullRightThreshold   | 右全滑动的阈值（0-1）                       | number                                                | no       | iOS/Android | yes               |
| fullSwipeLeft        | 是否允许左全滑动                           | boolean                                               | no       | iOS/Android | yes               |
| fullSwipeRight       | 是否允许右全滑动                          | boolean                                               | no       | iOS/Android | yes               |
| itemsIconSize        | 项目的图标大小                                         | number                                                | no       | iOS/Android | yes               |
| itemsMinWidth        | 设置不同的最小宽度                                | number                                                | no       | iOS/Android | yes               |
| itemsTextStyle       | 项目的文本样式                                        | TextStyle                                             | no       | iOS/Android | yes               |
| itemsTintColor       | 项目的文本和图标色调的颜色            | string                                                | no       | iOS/Android | yes               |
| leftItem             | 从左侧打开时出现的底层项目（单个项目） | ItemProps                                             | no       | iOS/Android | yes               |
| onDragStart          | 当拖动手势开始时调用                              | () => any                                             | no       | iOS/Android | yes               |
| onFullSwipeLeft      | 左项目全滑动的回调                            | () => void                                            | no       | iOS/Android | yes               |
| onFullSwipeRight     | 右项目全滑动的回调                           | () => void                                            | no       | iOS/Android | yes               |
| onSwipeableWillClose | 关闭操作的回调                                    | () => void                                            | no       | iOS/Android | yes               |
| onSwipeableWillOpen  | 打开操作的回调                                     | () => void                                            | no       | iOS/Android | yes               |
| onToggleSwipeLeft    | 左项目切换滑动的回调                          | () => {rowWidth, leftWidth, dragX, resetItemPosition} | no       | iOS/Android | yes               |
| onWillFullSwipeLeft  | 左项目全滑动之前的回调                | () => void                                            | no       | iOS/Android | yes               |
| onWillFullSwipeRight | 右项目全滑动之前的回调               | () => void                                            | no       | iOS/Android | yes               |
| rightItems           | 从右侧打开时出现的底层项目 | ItemProps[]                                           | no       | iOS/Android | yes               |
| style                | 组件的样式                                            | ViewStyle                                             | no       | iOS/Android | yes               |
| testID               | 用于端到端测试的测试 ID                                    | string                                                | no       | iOS/Android | yes               |
| useNativeAnimations  | 在本机执行动画                            | boolean                                               | no       | iOS/Android | yes               |

**GridList**：网格列表组件，扩展了[FlatList](https://reactnative.dev/docs/flatlist)组件。

| Name                  | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| containerWidth        | 当您想要使用自定义容器宽度进行计算时传递 | number                              | no       | iOS/Android | yes               |
| contentContainerStyle | 自定义内容容器样式                               | ScrollView[ contentContainerStyle ] | no       | iOS/Android | yes               |
| itemSpacing           | 每个项目之间的间距                                    | number                              | no       | iOS/Android | yes               |
| keepItemSize          | 当方向更改时是否保持项目的初始大小，在这种情况下将自动计算适当的列数。 | boolean                             | no       | iOS/Android | yes               |
| listPadding           | 列表内边距（用于项目大小计算）                | number                              | no       | iOS/Android | yes               |
| maxItemWidth          | 允许响应式项目宽度到最大项目宽度      | number                              | no       | iOS/Android | yes               |
| numColumns            | 一行中显示的项目数（传递 maxItemWidth 时忽略） | number                              | no       | iOS/Android | yes               |

**GridListItem**：单个网格视图/列表项组件。

| Name                      | Description                                                 | Type                               | Required | Platform    | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------- | ---------------------------------- | -------- | ----------- | ----------------- |
| alignToStart              | 内容是否应对齐到开始                            | boolean                            | no       | iOS/Android | yes               |
| containerProps            | 传递给可触摸容器的属性                 | TouchableOpacityProps \| ViewProps | no       | iOS/Android | yes               |
| containerStyle            | 自定义容器样式                                      | ViewStyle                          | no       | iOS/Android | yes               |
| description               | 描述内容文本                                    | string \| React.ReactElement       | no       | iOS/Android | yes               |
| descriptionColor          | 描述内容颜色                                   | string                             | no       | iOS/Android | yes               |
| descriptionLines          | 描述内容行数                         | number                             | no       | iOS/Android | yes               |
| descriptionTypography     | 描述内容排版                              | string                             | no       | iOS/Android | yes               |
| horizontalAlignment       | 内容水平对齐                                | HorizontalAlignment                | no       | iOS/Android | yes               |
| imageProps                | 用于渲染图像项目的图像属性对象              | ImageProps                         | no       | iOS/Android | yes               |
| itemSize                  | 项目大小                                               | number \| ImageSize                | no       | iOS/Android | yes               |
| onPress                   | 项目的操作处理程序                                   | TouchableOpacityProps ['onPress']  | no       | iOS/Android | yes               |
| overlayText               | 在项目内部渲染标题、副标题和描述 | boolean                            | no       | iOS/Android | yes               |
| overlayTextContainerStyle | 内联文本的自定义容器样式                    | ViewStyle                          | no       | iOS/Android | yes               |
| renderCustomItem          | 在 GridView 中渲染的自定义 GridListItem          | () => React.ReactElement           | no       | iOS/Android | yes               |
| renderOverlay             | 在图像顶部渲染覆盖层                      | () => React.ReactElement           | no       | iOS/Android | yes               |
| subtitle                  | 副标题内容文本                                       | string \| React.ReactElement       | no       | iOS/Android | yes               |
| subtitleColor             | 副标题内容颜色                                      | string                             | no       | iOS/Android | yes               |
| subtitleLines             | 副标题内容行数                            | number                             | no       | iOS/Android | yes               |
| subtitleTypography        | 副标题内容排版                                 | string                             | no       | iOS/Android | yes               |
| testID                    | 组件测试 ID                                       | string                             | no       | iOS/Android | yes               |
| title                     | 标题内容文本                                          | string \| React.ReactElement       | no       | iOS/Android | yes               |
| titleColor                | 标题内容颜色                                         | string                             | no       | iOS/Android | yes               |
| titleLines                | 标题内容行数                               | number                             | no       | iOS/Android | yes               |
| titleTypography           | 标题内容排版                                    | string                             | no       | iOS/Android | yes               |

**GridView**：网格视图组件。

| Name                 | Description                                                  | Type                                            | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------------- | -------- | ----------- | ----------------- |
| itemSpacing          | 每个项目之间的间距                                    | number                                          | no       | iOS/Android | yes               |
| items                | 基于 GridListItem 属性的项目列表                | GridListItemProps[]                             | no       | iOS/Android | yes               |
| keepItemSize         | 当方向更改时是否保持项目的初始大小，在这种情况下将自动计算适当的列数。 | boolean                                         | no       | iOS/Android | yes               |
| lastItemLabel        | 最后一个项目的覆盖标签                              | string \| number                                | no       | iOS/Android | yes               |
| lastItemOverlayColor | 最后一个项目的覆盖标签颜色                     | string                                          | no       | iOS/Android | yes               |
| numColumns           | 一行中显示的项目数                             | number                                          | no       | iOS/Android | yes               |
| renderCustomItem     | 传递以渲染自定义项目                                 | (item: GridListItemProps) => React.ReactElement | no       | iOS/Android | yes               |
| viewWidth            | 传递所需的网格视图宽度（将改善加载时间） | number                                          | no       | iOS/Android | yes               |

**ListItem**：列表中列表项组件，该组件扩展了[TouchableOpacity](https://reactnative.dev/docs/touchableopacity)属性。

| Name             | Description                                | Type                                                         | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| containerElement | 包装 ListItem 的容器元素 | React.ComponentType <ListItemProps \| TouchableOpacityProps> | no       | iOS/Android | yes               |
| containerStyle   | 顶部容器的额外样式    | ViewStyle                                                    | no       | iOS/Android | yes               |
| height           | 列表项高度                       | ViewStyle['height']                                          | no       | iOS/Android | yes               |
| onLongPress      | 长按项目时的操作     | () => void                                                   | no       | iOS/Android | yes               |
| onPress          | 按下项目时的操作          | () => void                                                   | no       | iOS/Android | yes               |
| style            | 内部元素样式                    | ViewStyle                                                    | no       | iOS/Android | yes               |
| testID           | 用于端到端测试的测试 ID                  | string                                                       | no       | iOS/Android | yes               |
| underlayColor    | 内部元素按下时的背景颜色  | string                                                       | no       | iOS/Android | yes               |

**ListItem.Part**：用于在 ListItem 内进行布局的子 ListItem 组件。

| Name           | Description                                   | Type      | Required | Platform    | HarmonyOS Support |
| -------------- | --------------------------------------------- | --------- | -------- | ----------- | ----------------- |
| column         | 此部分内容方向将为列    | boolean   | no       | iOS/Android | yes               |
| containerStyle | 容器样式                               | ViewStyle | no       | iOS/Android | yes               |
| left           | 此部分内容将对齐到左     | boolean   | no       | iOS/Android | yes               |
| middle         | 此部分内容将对齐到展开 | boolean   | no       | iOS/Android | yes               |
| right          | 此部分内容将对齐到右    | boolean   | no       | iOS/Android | yes               |
| row            | 此部分内容方向将为行       | boolean   | no       | iOS/Android | yes               |

**SortableGridList**：可排序网格列表组件，该组件扩展了[GridList](https://wix.github.io/react-native-ui-lib/docs/components/lists/GridList)组件属性。

| Name          | Description                                                  | Type                                         | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | -------------------------------------------- | -------- | ----------- | ----------------- |
| data          | 不要在 'onOrderChange' 中更新 'data'（即每次顺序更改时）；仅在更改项目时更新它（即添加和删除项目）。具有 id 属性作为唯一标识符的项目数据 | any[] & {id: string}                         | no       | iOS/Android | yes               |
| extraData     | 传递任何应触发重新渲染的额外数据          | any                                          | no       | iOS/Android | yes               |
| onOrderChange | 顺序更改回调                                        | (newData: T[], newOrder: ItemsOrder) => void | no       | iOS/Android | yes               |
| renderItem    | 自定义渲染项目回调                                  | FlatListProps ['renderItem']                 | no       | iOS/Android | yes               |

**SortableList**：可排序列表组件，该组件扩展了[FlatList](https://reactnative.dev/docs/flatlist)组件属性。

| Name          | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| data          | 不要在 'onOrderChange' 中更新 'data'（即每次顺序更改时）；仅在更改项目时更新它（即添加和删除项目）。列表的数据，具有 id 属性作为唯一标识符。 | ItemT[] (ItemT extends {id: string})                         | no       | iOS/Android | yes               |
| enableHaptic  | 是否启用触觉反馈。（请注意，react-native-haptic-feedback 从某个未知版本开始不支持 Android 上的特定触觉类型，您可以使用 1.8.2 使其正常工作） | boolean                                                      | no       | iOS/Android | yes               |
| itemProps     | 项目的额外属性。                                    | {margins?: {marginTop?: number; marginBottom?: number; marginLeft?: number; marginRight?: number}} | no       | iOS/Android | yes               |
| onOrderChange | 获取新顺序（或交换项目）的回调。          | (data: ItemT[]) => void                                      | no       | iOS/Android | yes               |
| scale         | 拖动时缩放项目。                                 | number                                                       | no       | iOS/Android | yes               |

**Timeline**：时间线组件，该组件扩展了[View](https://reactnative.dev/docs/view)组件属性。

| Name            | Description                                                  | Type                               | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------------------------- | -------- | ----------- | ----------------- |
| backgroundColor | 项目的背景颜色                                | string                             | no       | iOS/Android | yes               |
| bottomLine      | 底部线的属性                                        | LineProps                          | no       | iOS/Android | yes               |
| point           | 点的属性                                              | PointProps                         | no       | iOS/Android | yes               |
| renderContent   | 渲染到时间线指示器右侧的自定义内容     | any                                | no       | iOS/Android | yes               |
| state           | 时间线的状态。将影响指示的颜色（使用静态 'states'） | current \| next \| error \|success | no       | iOS/Android | yes               |
| testID          | 用于端到端测试的测试 ID                                    | string                             | no       | iOS/Android | yes               |
| topLine         | 顶部线的属性                                           | LineProps                          | no       | iOS/Android | yes               |

**AnimatedImage**：图像加载后以动画淡入的图像组件，该组件扩展了[Image](https://wix.github.io/react-native-ui-lib/docs/components/media/Image)组件属性。

| Name                          | Description                                              | Type        | Required | Platform    | HarmonyOS Support |
| ----------------------------- | -------------------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| animationDuration             | 图像加载时淡入动画的持续时间 | number      | no       | iOS/Android | yes               |
| containerStyle                | 容器的额外间距样式              | ViewStyle   | no       | iOS/Android | yes               |
| loader                        | 图像加载时渲染的组件         | JSX.element | no       | iOS/Android | yes               |
| onLoadStart<sup>7.43.1+</sup> | 加载开始回调                                   | () => void  | no       | iOS/Android | yes               |

**AnimatedScanner**：该组件扩展了[Animated.View](https://reactnative.dev/docs/animated)组件属性。

| Name            | Description                                              | Type                         | Required | Platform    | HarmonyOS Support |
| --------------- | -------------------------------------------------------- | ---------------------------- | -------- | ----------- | ----------------- |
| backgroundColor | 背景颜色                                         | string                       | no       | iOS/Android | yes               |
| containerStyle  | 组件的容器样式                              | ViewStyle                    | no       | iOS/Android | yes               |
| duration        | 当前中断的持续时间（可以在中断之间更改） | number                       | no       | iOS/Android | yes               |
| hideScannerLine | 是否隐藏扫描线                         | boolean                      | no       | iOS/Android | yes               |
| onBreakpoint    | 断点回调                                      | ({progress, isDone}) => void | no       | iOS/Android | yes               |
| opacity         | 不透明度                                                  | number                       | no       | iOS/Android | yes               |
| progress        | 0 到 100 之间的动画值                         | number                       | no       | iOS/Android | yes               |
| testID          | 用作测试标识符                             | string                       | no       | iOS/Android | yes               |

**Avatar**：头像组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)，[Image](https://wix.github.io/react-native-ui-lib/docs/components/media/Image)组件属性。

| Name                                 | Description                                                  | Type                                              | Required | Platform    | HarmonyOS Support |
| ------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------- | -------- | ----------- | ----------------- |
| animate                              | 当 Avatar 图像加载时添加淡入动画               | boolean                                           | no       | iOS/Android | yes               |
| autoColorsConfig                     | 发送此项以使用名称推断 backgroundColor         | AutoColorsProps                                   | no       | iOS/Android | yes               |
| backgroundColor                      | Avatar 的背景颜色                                  | string                                            | no       | iOS/Android | yes               |
| badgePosition                        | Avatar 上的徽章位置                                     | TOP_RIGHT \|TOP_LEFT \|BOTTOM_RIGHT \|BOTTOM_LEFT | no       | iOS/Android | yes               |
| badgeProps                           | 传递给 Badge 组件的徽章属性                   | BadgeProps                                        | no       | iOS/Android | yes               |
| containerStyle                       | 容器的额外间距样式                  | ViewStyle                                         | no       | iOS/Android | yes               |
| customRibbon                         | 自定义丝带                                                | JSX.Element                                       | no       | iOS/Android | yes               |
| imageProps                           | 图像属性对象                                           | ImageProps                                        | no       | iOS/Android | yes               |
| imageStyle                           | 用于通过组件传递额外样式属性的图像样式对象 | ImageStyle                                        | no       | iOS/Android | yes               |
| isOnline                             | 确定是否显示在线徽章                            | boolean                                           | no       | iOS/Android | yes               |
| label                                | 可以表示首字母的标签                            | string                                            | no       | iOS/Android | yes               |
| labelColor                           | 标签颜色                                              | string                                            | no       | iOS/Android | yes               |
| name                                 | 头像用户的名称。如果未提供标签，将从名称生成首字母。autoColorsConfig 将使用名称创建 Avatar 的背景颜色。 | string                                            | no       | iOS/Android | yes               |
| onImageLoadEnd                       | 当图像的（uri）加载成功或失败时的监听器回调（等同于 Image.onLoadEnd()）。 | ImagePropsBase ['onLoadEnd']                      | no       | iOS/Android | yes               |
| onImageLoadError                     | 当图像的（uri）加载失败时的监听器回调（等同于 Image.onError()）。 | ImagePropsBase ['onError']                        | no       | iOS/Android | yes               |
| onImageLoadStart                     | 当图像的（uri）加载开始时的监听器回调（等同于 Image.onLoadStart()）。 | ImagePropsBase ['onLoadStart']                    | no       | iOS/Android | yes               |
| onPress                              | 按下处理程序                                                | (props: any) => void                              | no       | iOS/Android | yes               |
| ribbonLabel                          | 在头像上显示的丝带标签                        | string                                            | no       | iOS/Android | yes               |
| ribbonLabelStyle                     | 丝带标签自定义样式                                    | TextStyle                                         | no       | iOS/Android | yes               |
| ribbonStyle                          | 丝带自定义样式                                          | ViewStyle                                         | no       | iOS/Android | yes               |
| size                                 | Avatar 的自定义大小                                   | number                                            | no       | iOS/Android | yes               |
| source                               | 图像源（外部或来自资源）                   | ImageSourcePropType                               | no       | iOS/Android | yes               |
| status                               | AWAY、ONLINE、OFFLINE 或 NONE 模式（如果设置为 'NONE' 以外的值，将覆盖 isOnline 属性） | StatusModes                                       | no       | iOS/Android | yes               |
| testID                               | 测试标识符                                              | string                                            | no       | iOS/Android | yes               |
| useAutoColors                        | 哈希名称（或标签）以获取颜色，因此每个名称将具有特定颜色。默认为 false。 | boolean                                           | no       | iOS/Android | yes               |
| labelEllipsizeMode<sup>7.43.1+</sup> | 标签的省略号模式，默认为 clip            | TextProps['ellipsizeMode']                        | no       | iOS/Android | yes               |

**Icon**：图标组件，该组件扩展了[Image](https://reactnative.dev/docs/image)组件属性。

| Name        | Description                                              | Type              | Required | Platform    | HarmonyOS Support |
| ----------- | -------------------------------------------------------- | ----------------- | -------- | ----------- | ----------------- |
| assetGroup  | 资源组，默认为 icons                        | string            | no       | iOS/Android | yes               |
| assetName   | 如果提供，图标源将从资源名称驱动   | string            | no       | iOS/Android | yes               |
| recorderTag | 记录器标签                                             | 'mask' \|'unmask' | no       | iOS/Android | yes               |
| size        | 图标大小                                            | number            | no       | iOS/Android | yes               |
| supportRTL  | 图像是否应在 RTL 本地环境中水平翻转 | boolean           | no       | iOS/Android | yes               |
| tintColor   | 图标色调                                            | string            | no       | iOS/Android | yes               |

**Image**：图片组件，该组件扩展了[Image](https://reactnative.dev/docs/image)组件属性。

| Name                   | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| aspectRatio            | 图像的宽高比                               | number                              | no       | iOS/Android | yes               |
| assetGroup             | 资源组，默认为 icons                            | string                              | no       | iOS/Android | yes               |
| assetName              | 如果提供，图像源将从资源名称驱动      | string                              | no       | iOS/Android | yes               |
| cover                  | 将图像显示为封面，全宽图像（根据宽高比，默认：16:8） | boolean                             | no       | iOS/Android | yes               |
| customOverlayContent   | 渲染带有自定义内容的覆盖层                        | JSX.Element                         | no       | iOS/Android | yes               |
| errorSource            | 错误情况下的默认图像源                     | ImageSourcePropType                 | no       | iOS/Android | yes               |
| imageId                | 可以在 sourceTransformer 逻辑中使用的 imageId       | string                              | no       | iOS/Android | yes               |
| overlayColor           | 为覆盖层传递自定义颜色                          | string                              | no       | iOS/Android | yes               |
| overlayIntensity       | 覆盖强度类型                                         | LOW \|MEDIUM \|HIGH                 | no       | iOS/Android | yes               |
| overlayType            | 图像必须具有适当的大小，设置在图像顶部的覆盖层类型。 | VERTICAL \|TOP \|BOTTOM \|SOLID     | no       | iOS/Android | yes               |
| recorderTag            | 记录器标签                                                 | 'mask' \| 'unmask'                  | no       | iOS/Android | yes               |
| sourceTransformer      | 用于操作图像源的自定义源转换处理程序（非常适合大小控制） | (props: any) => ImageSourcePropType | no       | iOS/Android | yes               |
| supportRTL             | 图像是否应在 RTL 本地环境中水平翻转     | boolean                             | no       | iOS/Android | yes               |
| tintColor              | 资源色调                                               | string                              | no       | iOS/Android | yes               |
| useBackgroundContainer | 为图像使用容器，这可以解决在需要对同一视图执行动画时 Android 上的问题；即 Android 上与动画相关的崩溃。 | boolean                             | no       | iOS/Android | yes               |

**Marquee**：滑动文本组件。

| Name           | Description                             | Type               | Required | Platform    | HarmonyOS Support |
| -------------- | --------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| containerStyle | 自定义容器样式                  | ViewProps['style'] | no       | iOS/Android | yes               |
| direction      | 滑动方向                       | MarqueeDirections  | no       | iOS/Android | yes               |
| duration       | 滑动动画持续时间              | number             | no       | iOS/Android | yes               |
| label          | 滑动标签                           | string             | no       | iOS/Android | yes               |
| labelStyle     | 滑动标签样式                     | TextProps['style'] | no       | iOS/Android | yes               |
| numberOfReps   | 滑动动画重复次数 | number             | no       | iOS/Android | yes               |

**ProgressiveImage**：带动画的图像组件，该组件扩展了[AnimatedImage](https://wix.github.io/react-native-ui-lib/docs/components/media/AnimatedImage)组件属性。

| Name            | Description                                                  | Type        | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ----------- | -------- | ----------- | ----------------- |
| thumbnailSource | 全尺寸图像加载时显示的小缩略图源 | ImageSource | no       | iOS/Android | yes               |

**PageControl**：页面指示器组件。

| Name            | Description                                                  | Type                               | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------------------------- | -------- | ----------- | ----------------- |
| color           | 所选页面点和（如果未传递 inactiveColor）未选页面的边框的颜色 | string                             | no       | iOS/Android | yes               |
| containerStyle  | 顶部容器的额外样式                      | ViewStyle                          | no       | iOS/Android | yes               |
| currentPage     | 当前页面的从零开始的索引                         | number                             | no       | iOS/Android | yes               |
| enlargeActive   | 是否放大活动页面指示器。当 limitShownPages 生效时无关。 | boolean                            | no       | iOS/Android | yes               |
| inactiveColor   | 未选页面点和未选页面的边框的颜色 | string                             | no       | iOS/Android | yes               |
| limitShownPages | 限制显示的页面指示器数量。\在此状态下 enlargeActive 属性被禁用，当设置为 true 时最多显示 7 个。\仅当 numOfPages > 5 时相关。 | boolean                            | no       | iOS/Android | yes               |
| numOfPages      | 总页数                                        | number                             | no       | iOS/Android | yes               |
| onPagePress     | 点击页面指示器的操作处理程序              | (index: number) => void            | no       | iOS/Android | yes               |
| size            | 页面指示器的大小。\当设置 limitShownPages 时，中等大小将是 size 的 2/3，小大小将是 size 的 1/3。\另一种选择是发送数组 [smallSize, mediumSize, largeSize]。 | number \| [number, number, number] | no       | iOS/Android | yes               |
| spacing         | 兄弟页面指示器之间的间距               | number                             | no       | iOS/Android | yes               |
| testID          | 用于在测试中标识页面控件                    | string                             | no       | iOS/Android | yes               |

**TabController**：具有延迟加载机制的选项卡控制器组件，该组件基于react-native-gesture-handler，使用react-native-navigation时，请确保使用gestureHandlerRootHOC包裹屏幕。

| Name                                 | Description                                                  | Type                                               | Required | Platform    | HarmonyOS Support |
| ------------------------------------ | ------------------------------------------------------------ | -------------------------------------------------- | -------- | ----------- | ----------------- |
| asCarousel                           | 当使用 TabController.PageCarousel 时，应开启此选项 | boolean                                            | no       | iOS/Android | yes               |
| carouselPageWidth                    | 为自定义轮播页面宽度传递                          | number                                             | no       | iOS/Android | yes               |
| initialIndex                         | 初始选中的索引                                       | number                                             | no       | iOS/Android | yes               |
| items                                | 标签栏项目列表                                    | TabControllerItemProps []                          | no       | iOS/Android | yes               |
| onChangeIndex                        | 当索引更改时的回调（不会在忽略的项目上调用） | (index: number, prevIndex: number \| null) => void | no       | iOS/Android | yes               |
| nestedInScrollView<sup>7.43.1+</sup> | 当 TabController 渲染在 ScrollView 内部时传递（带有标题） | boolean                                            | no       | iOS/Android | yes               |

**TabController.PageCarousel**：TabController 的 PageCarousel 组件，该组件扩展了[ScrollView](https://reactnative.dev/docs/scrollview)组件属性。

| Name                       | Description                                                  | Type      | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | --------- | -------- | ----------- | ----------------- |
| TabController.PageCarousel | TabController 的 PageCarousel 组件，您必须将 asCarousel 标志传递给 TabController，并在 PageCarousel 内部渲染您的 TabPages | Component | no       | iOS/Android | yes               |

**TabController.TabBar**：TabController的TabBar组件。

| Name                  | Description                                  | Type      | Required | Platform    | HarmonyOS Support |
| --------------------- | -------------------------------------------- | --------- | -------- | ----------- | ----------------- |
| activeBackgroundColor | 为标签项按下时应用背景颜色 | string    | no       | iOS/Android | yes               |
| backgroundColor       | TabBar 背景颜色                  | string    | no       | iOS/Android | yes               |
| centerSelected        | 传递以居中选中项目                 | boolean   | no       | iOS/Android | yes               |
| containerStyle        | 容器的额外样式          | ViewStyle | no       | iOS/Android | yes               |
| containerWidth        | TabBar 容器宽度                   | number    | no       | iOS/Android | yes               |
| enableShadow          | 显示标签栏底部阴影                   | boolean   | no       | iOS/Android | yes               |
| height                | 标签栏高度                               | number    | no       | iOS/Android | yes               |
| iconColor             | 图标色调颜色                              | string    | no       | iOS/Android | yes               |
| indicatorInsets       | 指示器内边距                         | number    | no       | iOS/Android | yes               |
| indicatorStyle        | 选中指示器的自定义样式      | ViewStyle | no       | iOS/Android | yes               |
| labelColor            | 默认标签颜色                      | string    | no       | iOS/Android | yes               |
| labelStyle            | 自定义标签样式                           | TextStyle | no       | iOS/Android | yes               |
| selectedIconColor     | 图标选中色调颜色                     | string    | no       | iOS/Android | yes               |
| selectedLabelColor    | 选中标签颜色                     | string    | no       | iOS/Android | yes               |
| selectedLabelStyle    | 自定义选中标签样式                  | TextStyle | no       | iOS/Android | yes               |
| shadowStyle           | 自定义阴影样式                          | ViewStyle | no       | iOS/Android | yes               |
| spreadItems           | 标签栏是否应展开          | boolean   | no       | iOS/Android | yes               |
| testID                | 组件测试 ID                        | string    | no       | iOS/Android | yes               |
| uppercase             | 是否将文本更改为大写      | boolean   | no       | iOS/Android | yes               |

**TabController.TabBarItem**：TabController的TabBarItem组件。

| Name                  | Description                                          | Type                    | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------- | ----------------------- | -------- | ----------- | ----------------- |
| activeBackgroundColor | 为 TouchableOpacity 按下时应用背景颜色 | string                  | no       | iOS/Android | yes               |
| activeOpacity         | 按下标签时的活动不透明度               | number                  | no       | iOS/Android | yes               |
| backgroundColor       | 为标签栏项应用背景颜色          | string                  | no       | iOS/Android | yes               |
| badge                 | 在项目标签旁边显示的徽章组件属性 | BadgeProps              | no       | iOS/Android | yes               |
| icon                  | 标签的图标                                      | number                  | no       | iOS/Android | yes               |
| iconColor             | 图标色调颜色                                      | string                  | no       | iOS/Android | yes               |
| ignore                | 忽略标签按下                                   | boolean                 | no       | iOS/Android | yes               |
| label                 | 标签的标签                                     | string                  | no       | iOS/Android | yes               |
| labelColor            | 默认标签颜色                              | string                  | no       | iOS/Android | yes               |
| labelProps            | 传递给标签文本元素的额外标签属性      | TextProps               | no       | iOS/Android | yes               |
| labelStyle            | 自定义标签样式                                   | TextStyle               | no       | iOS/Android | yes               |
| leadingAccessory      | 传递以渲染前导元素                     | ReactElement            | no       | iOS/Android | yes               |
| onPress               | 按下标签时的回调                     | (index: number) => void | no       | iOS/Android | yes               |
| selectedIconColor     | 图标选中色调颜色                             | string                  | no       | iOS/Android | yes               |
| selectedLabelColor    | 选中标签颜色                             | string                  | no       | iOS/Android | yes               |
| selectedLabelStyle    | 自定义选中标签样式                          | TextStyle               | no       | iOS/Android | yes               |
| style                 | 传递自定义样式                                    | ViewStyle               | no       | iOS/Android | yes               |
| testID                | 用作测试标识符                         | string                  | no       | iOS/Android | yes               |
| trailingAccessory     | 传递以渲染尾随元素                    | ReactElement            | no       | iOS/Android | yes               |
| uppercase             | 是否将文本更改为大写              | boolean                 | no       | iOS/Android | yes               |
| width                 | 项目的固定宽度                           | number                  | no       | iOS/Android | yes               |

**TabController.TabPage**：TabController的TabPage 组件。

| Name          | Description                                                  | Type              | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| index         | TabPage 的索引                                 | number            | no       | iOS/Android | yes               |
| lazy          | 此页面是否应延迟加载                    | boolean           | no       | iOS/Android | yes               |
| lazyLoadTime  | 延迟加载完成前等待的时间（适合显示加载器屏幕） | number            | no       | iOS/Android | yes               |
| renderLoading | 延迟加载时渲染自定义加载页面               | () => JSX.Element | no       | iOS/Android | yes               |
| testID        | 组件测试 ID                                        | string            | no       | iOS/Android | yes               |

**Wizard**：向导组件。

| Name                 | Description                                                  | Type                    | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------- | -------- | ----------- | ----------------- |
| activeConfig         | 活动步骤的配置（参见 Wizard.Step.propTypes） | WizardStepProps         | no       | iOS/Android | yes               |
| activeIndex          | 活动步骤的索引                                      | number                  | no       | iOS/Android | yes               |
| containerStyle       | 添加或覆盖容器的样式                       | ViewStyle               | no       | iOS/Android | yes               |
| onActiveIndexChanged | 当活动步骤更改时调用的回调（即单击了某个步骤）。新的 activeIndex 将是回调的输入 | (index: number) => void | no       | iOS/Android | yes               |
| testID               | 组件测试 ID                                        | string                  | no       | iOS/Android | yes               |

**Wizard.Step**：向导组件中Step组件。

| Name                  | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| accessibilityInfo     | 在无障碍模式下读取的额外文本                  | string           | no       | iOS/Android | yes               |
| circleBackgroundColor | 圆圈的背景颜色                                    | string           | no       | iOS/Android | yes               |
| circleColor           | 圆圈的颜色                                          | string           | no       | iOS/Android | yes               |
| circleSize            | 步骤的圆圈大小（直径）                            | number           | no       | iOS/Android | yes               |
| color                 | 步骤索引的颜色（或提供图标时的图标颜色）      | string           | no       | iOS/Android | yes               |
| connectorStyle        | 连接器的额外样式                          | ViewStyle        | no       | iOS/Android | yes               |
| enabled               | 步骤是否应启用                           | boolean          | no       | iOS/Android | yes               |
| icon                  | 替换（默认）索引的图标                          | ImageProps       | no       | iOS/Android | yes               |
| indexLabelStyle       | 索引标签的额外样式（当未提供图标时） | TextStyle        | no       | iOS/Android | yes               |
| label                 | 项目的标签                                        | string           | no       | iOS/Android | yes               |
| labelStyle            | 标签的额外样式                              | TextStyle        | no       | iOS/Android | yes               |
| state                 | 步骤的状态（Wizard.States.X）                      | WizardStepStates | no       | iOS/Android | yes               |

**ActionSheet**：弹窗选择组件。

| Name                   | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| cancelButtonIndex      | 表示取消操作的选项的索引（将显示为分离的底部粗体按钮） | number                                                       | no       | iOS/Android | yes               |
| containerStyle         | 添加或覆盖操作表的样式（包装标题和操作） | ViewStyle                                                    | no       | iOS/Android | yes               |
| destructiveButtonIndex | 表示破坏性操作的选项的索引（将显示红色文本。通常用于删除或中止操作） | number                                                       | no       | iOS/Android | yes               |
| dialogStyle            | 添加或覆盖包装操作表的对话框样式 | ViewStyle                                                    | no       | iOS/Android | yes               |
| message                | 操作表的消息                                  | string                                                       | no       | iOS/Android | yes               |
| onDismiss              | 关闭操作表时调用（通常用于将 'visible' 属性设置为 false） | DialogProps['onDismiss']                                     | no       | iOS/Android | yes               |
| onModalDismissed       | 仅限 iOS，仅模态。模态关闭后调用一次 | DialogProps ['onDialogDismissed']                            | no       | iOS         | no                |
| options                | 操作表的选项列表，遵循 Button 属性类型（提供 'label' 字符串和 'onPress' 函数） | Array<ButtonProps>                                           | no       | iOS/Android | yes               |
| optionsStyle           | 添加或覆盖选项列表的样式                    | ViewStyle                                                    | no       | iOS/Android | yes               |
| renderAction           | 您需要调用 'onOptionPress' 以便选项的 'onPress' 被调用。渲染自定义操作 | ( option: ButtonProps, index: number, onOptionPress: ActionSheetOnOptionPress ) => JSX.Element | no       | iOS/Android | yes               |
| renderTitle            | 渲染自定义标题                                          | () => JSX.Element                                            | no       | iOS/Android | yes               |
| showCancelButton       | 当传递时（仅与 useNativeIOS 一起使用），将在底部显示取消按钮（覆盖 cancelButtonIndex） | boolean                                                      | no       | iOS/Android | yes               |
| testID                 | 用于端到端测试的测试 ID                                    | string                                                       | no       | iOS/Android | yes               |
| title                  | 如果未传递 'title' 和 'message'，则根本不会渲染标题视图。操作表的标题 | string                                                       | no       | iOS/Android | yes               |
| useNativeIOS           | 是否应为 iOS 使用原生操作表                   | boolean                                                      | no       | iOS/Android | yes               |
| useSafeArea            | 在 iOS 中，使用安全区域，以防组件附加到底部 | boolean                                                      | no       | iOS/Android | yes               |
| visible                | 是否显示操作表                      | boolean                                                      | no       | iOS/Android | yes               |

**Dialog**：弹窗组件。

| Name                   | Description                                                  | Type                        | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------- | ----------------- |
| containerStyle         | 组件的容器样式                                  | ViewStyle                   | no       | iOS/Android | yes               |
| height                 | 高度                                                       | string \|number             | no       | iOS/Android | yes               |
| ignoreBackgroundPress  | 是否忽略背景按下                    | boolean                     | no       | iOS/Android | yes               |
| onDialogDismissed      | 对话框完全关闭后调用         | (props: any) => void        | no       | iOS/Android | yes               |
| onDismiss              | 点击背景时调用                       | (props?: any) => void       | no       | iOS/Android | yes               |
| overlayBackgroundColor | 覆盖背景的颜色                          | string                      | no       | iOS/Android | yes               |
| panDirection           | 允许平移的方向                             | UP \|DOWN \|LEFT \|RIGHT    | no       | iOS/Android | yes               |
| pannableHeaderProps    | 将传递给可平移标题的属性         | any                         | no       | iOS/Android | yes               |
| renderPannableHeader   | 如果添加此项，则只有标题是可平移的。属性将传递给 'renderPannableHeader'。对于可滚动内容（对话框的子项） | (props: any) => JSX.Element | no       | iOS/Android | yes               |
| testID                 | 用于端到端测试的测试 ID                                    | string                      | no       | iOS/Android | yes               |
| useSafeArea            | 在 iOS 中，使用安全区域，以防组件附加到底部 | boolean                     | no       | iOS/Android | yes               |
| visible                | 控制组件的可见性                          | boolean                     | no       | iOS/Android | yes               |
| width                  | 宽度                                                        | string \| number            | no       | iOS/Android | yes               |

**FeatureHighlight**：功能发现组件，FeatureHighlight 组件必须是 render() 返回的根视图的直接子级，如果要突出显示的元素没有样式属性，请添加 'style={{opacity: 1}}' 以便 Android 操作系统可以检测到它，FeatureHighlight 使用native库，你需要引入它。

| Name                 | Description                                                  | Type                                      | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------- | -------- | ----------- | ----------------- |
| borderColor          | 高亮元素周围边框的颜色           | string                                    | no       | iOS/Android | yes               |
| borderRadius         | 高亮元素周围边框角的边框半径 | number                                    | no       | iOS/Android | yes               |
| borderWidth          | 高亮元素周围边框的宽度           | number                                    | no       | iOS/Android | yes               |
| confirmButtonProps   | 将传递给关闭按钮的属性              | ButtonProps                               | no       | iOS/Android | yes               |
| getTarget            | 提取要高亮元素的引用的回调 | () => any                                 | no       | iOS/Android | yes               |
| highlightFrame       | 要高亮区域的框架 {x, y, width, height}         | HighlightFrame                            | no       | iOS/Android | yes               |
| innerPadding         | 高亮框架围绕高亮元素框架的内边距（仅在 'getTarget' 中传递引用时） | number                                    | no       | iOS/Android | yes               |
| message              | 要显示的消息                                      | string                                    | no       | iOS/Android | yes               |
| messageNumberOfLines | 消息的最大行数                                | number                                    | no       | iOS/Android | yes               |
| messageStyle         | 消息文本样式                                           | TextStyle                                 | no       | iOS/Android | yes               |
| minimumRectSize      | Android API 21+，并且仅在 'getTarget' 中传递引用时。高亮组件的最小大小 | RectSize                                  | no       | iOS/Android | yes               |
| onBackgroundPress    | 背景按下时调用                                | TouchableWithoutFeedbackProps ['onPress'] | no       | iOS/Android | yes               |
| overlayColor         | 内容背景的颜色（通常包括 alpha 透明度） | string                                    | no       | iOS/Android | yes               |
| pageControlProps     | PageControl 组件的属性                                | PageControlProps                          | no       | iOS/Android | yes               |
| testID               | 用于端到端测试的测试 ID                                    | string                                    | no       | iOS/Android | yes               |
| textColor            | 内容文本的颜色                                  | string                                    | no       | iOS/Android | yes               |
| title                | 要显示的内容标题                         | string                                    | no       | iOS/Android | yes               |
| titleNumberOfLines   | 标题的最大行数                                  | number                                    | no       | iOS/Android | yes               |
| titleStyle           | 标题文本样式                                             | TextStyle                                 | no       | iOS/Android | yes               |
| visible              | 确定是否呈现功能高亮组件     | boolean                                   | no       | iOS/Android | yes               |

**FloatingButton**：具有渐变的悬浮按钮。

| Name                  | Description                                                  | Type                  | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | --------------------- | -------- | ----------- | ----------------- |
| bottomMargin          | 按钮的底部边距，如果传递了辅助按钮则为辅助按钮的底部边距 | number                | no       | iOS/Android | yes               |
| button                | Button 组件的属性                               | ButtonProps           | no       | iOS/Android | yes               |
| buttonLayout          | 按钮布局方向：垂直或水平              | FloatingButtonLayouts | no       | iOS/Android | yes               |
| duration              | 按钮动画的持续时间（显示/隐藏）          | number                | no       | iOS/Android | yes               |
| fullWidth             | 仅与垂直布局相关。按钮是否获取容器的全宽 | boolean               | no       | iOS/Android | yes               |
| hideBackgroundOverlay | 是否显示背景覆盖                           | boolean               | no       | iOS/Android | yes               |
| secondaryButton       | 辅助 Button 组件的属性                     | ButtonProps           | no       | iOS/Android | yes               |
| testID                | 为主按钮使用 `testID.button` 或为辅助按钮使用 `testID.secondaryButton`。用于端到端测试的测试 ID | string                | no       | iOS/Android | yes               |
| visible               | 组件是否可见                             | boolean               | no       | iOS/Android | yes               |
| withoutAnimation      | 是否在没有动画的情况下显示/隐藏按钮            | boolean               | no       | iOS/Android | yes               |

**Modal**：模态框组件，该组件扩展了[Modal](https://reactnative.dev/docs/modal)组件属性。

| Name                      | Description                                                  | Type                                   | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | -------------------------------------- | -------- | ----------- | ----------------- |
| accessibilityLabel        | 覆盖屏幕阅读器在用户与元素交互时读取的文本。\默认情况下，标签是通过遍历所有子项并累积所有由空格分隔的文本节点来构建的。 | string                                 | no       | iOS/Android | yes               |
| blurView                  | 用作 BlurView 的自定义视图而不是默认视图 | JSX.Element                            | no       | iOS/Android | yes               |
| enableModalBlur           | 仅限 iOS。透明时模糊模态背景        | boolean                                | no       | iOS         | no                |
| onBackgroundPress         | 允许在单击其背景时关闭模态     | (event: GestureResponderEvent) => void | no       | iOS/Android | yes               |
| overlayBackgroundColor    | 覆盖的背景颜色                          | string                                 | no       | iOS/Android | yes               |
| testID                    | 模态的端到端测试标识符                       | string                                 | no       | iOS/Android | yes               |
| useGestureHandlerRootView | 仅限 Android。应添加 GestureHandlerRootView            | boolean                                | no       | Android     | no                |

**Modal.TopBar**：模态框的TopBar组件。

| Name              | Description                                                | Type                                   | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------------- | -------------------------------------- | -------- | ----------- | ----------------- |
| cancelButtonProps | 取消操作属性                                        | ButtonProps                            | no       | iOS/Android | yes               |
| cancelIcon        | 取消操作图标                                         | ImageSource                            | no       | iOS/Android | yes               |
| cancelLabel       | 取消操作标签                                        | string                                 | no       | iOS/Android | yes               |
| containerStyle    | TopBar 容器的样式                             | ViewStyle                              | no       | iOS/Android | yes               |
| doneButtonProps   | 完成操作属性                                          | ButtonProps                            | no       | iOS/Android | yes               |
| doneIcon          | 完成操作图标                                           | ImageSource                            | no       | iOS/Android | yes               |
| doneLabel         | 完成操作标签                                          | string                                 | no       | iOS/Android | yes               |
| includeStatusBar  | 是否包括状态栏（高度计算） | boolean                                | no       | iOS/Android | yes               |
| leftButtons       | 在顶部栏左侧渲染的按钮          | topBarButtonProp\| topBarButtonProp[]  | no       | iOS/Android | yes               |
| onCancel          | 取消操作回调                                     | (props?: any) => void                  | no       | iOS/Android | yes               |
| onDone            | 完成操作回调                                       | (props?: any) => void                  | no       | iOS/Android | yes               |
| rightButtons      | 在顶部栏右侧渲染的按钮         | topBarButtonProp \| topBarButtonProp[] | no       | iOS/Android | yes               |
| subtitle          | 在顶部栏标题下方显示的副标题                | string                                 | no       | iOS/Android | yes               |
| subtitleStyle     | 副标题自定义样式                                      | TextStyle                              | no       | iOS/Android | yes               |
| title             | 在顶部栏中心显示的标题              | string                                 | no       | iOS/Android | yes               |
| titleStyle        | 标题自定义样式                                         | TextStyle                              | no       | iOS/Android | yes               |

**Toast**：非中断式弹窗组件， 请考虑转向我们新的 Toast 实现并使用 Incubator.Toast 代替。

| Name  | Description                    | Type      | Required | Platform    | HarmonyOS Support |
| ----- | ------------------------------ | --------- | -------- | ----------- | ----------------- |
| Toast | 可自定义的 Toast 组件 | Component | no       | iOS/Android | yes               |

**Badge**：圆形彩色徽章组件。

| Name                | Description                                                  | Type                       | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------------------------- | -------- | ----------- | ----------------- |
| backgroundColor     | 背景颜色                                             | string                     | no       | iOS/Android | yes               |
| borderColor         | 徽章周围边框的颜色                             | ImageStyle ['borderColor'] | no       | iOS/Android | yes               |
| borderRadius        | 徽章周围边框的半径                            | number                     | no       | iOS/Android | yes               |
| borderWidth         | 徽章周围边框的宽度                             | number                     | no       | iOS/Android | yes               |
| containerStyle      | 顶部容器的额外样式                      | ViewStyle                  | no       | iOS/Android | yes               |
| customElement       | 渲染而不是图标的自定义元素                  | JSX.Element                | no       | iOS/Android | yes               |
| hitSlop             | 定义触摸事件可以从徽章开始多远  | ViewProps['hitSlop']       | no       | iOS/Android | yes               |
| icon                | 渲染图标徽章                                        | ImageSourcePropType        | no       | iOS/Android | yes               |
| iconProps           | 传递给图标的额外属性                              | ImageProps                 | no       | iOS/Android | yes               |
| iconStyle           | 徽章图标的额外样式                             | ImageStyle                 | no       | iOS/Android | yes               |
| label               | 传递标签（undefined）将呈现斑点徽章。徽章内显示的文本 | string                     | no       | iOS/Android | yes               |
| labelFormatterLimit | 超过该数字长度的最大数字，将在末尾显示 '+'。如果设置为不包含在 LABEL_FORMATTER_VALUES 中的值，则不会进行格式化。示例：labelLengthFormatter={2}, label={124}, 标签将显示 '99+' 接收从 1 到 4 的数字，代表标签的最大数字长度 | LabelFormatterValues       | no       | iOS/Android | yes               |
| labelStyle          | 徽章标签的额外样式                        | TextStyle                  | no       | iOS/Android | yes               |
| onPress             | 当徽章被按下时调用                             | (props: any) => void       | no       | iOS/Android | yes               |
| size                | 徽章的大小                                                 | number                     | no       | iOS/Android | yes               |

**ConnectionStatusBar**：顶部栏显示无网络连接状态，该组件依赖[@react-native-community/netinfo](/zh-cn/react-native-community-netinfo.md) 库。

| Name                | Description                                         | Type                                               | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------- | -------------------------------------------------- | -------- | ----------- | ----------------- |
| allowDismiss        | 是否允许用户关闭               | boolean                                            | no       | iOS/Android | yes               |
| label               | 显示为状态的文本                          | string                                             | no       | iOS/Android | yes               |
| onConnectionChange  | 处理连接更改事件传播的处理程序 | (isConnected: boolean, isInitial: boolean) => void | no       | iOS/Android | yes               |
| useAbsolutePosition | 为组件使用绝对位置             | boolean                                            | no       | iOS/Android | yes               |

**ProgressBar**：进度条组件。

| Name          | Description                                              | Type        | Required | Platform    | HarmonyOS Support |
| ------------- | -------------------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| customElement | 在动画进度顶部渲染的自定义元素 | JSX.Element | no       | iOS/Android | yes               |
| fullWidth     | 全宽 UI 预设                                      | boolean     | no       | iOS/Android | yes               |
| progress      | 从 0 到 100 的进度条进度                    | number      | no       | iOS/Android | yes               |
| progressColor | 进度颜色                                           | string      | no       | iOS/Android | yes               |
| style         | 覆盖容器样式                                 | ViewStyle   | no       | iOS/Android | yes               |

**SkeletonView**：骨架视图组件，用于内容还未加载临时显示骨架，该组件需要安装[react-native-shimmer-placeholder](/zh-cn/react-native-shimmer-placeholder.md)和[react-native-linear-gradient](/zh-cn/react-native-linear-gradient.md)库。

| Name          | Description                                                  | Type                                   | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | -------------------------------------- | -------- | ----------- | ----------------- |
| borderRadius  | 骨架视图的边框半径                       | number                                 | no       | iOS/Android | yes               |
| circle        | 骨架是否为圆形（将覆盖 borderRadius） | boolean                                | no       | iOS/Android | yes               |
| colors        | 骨架视图的颜色，数组长度必须 >=2 | string[]                               | no       | iOS/Android | yes               |
| customValue   | 传递给 SkeletonView 并在 renderContent 回调中接收的任何类型的自定义值。 | any                                    | no       | iOS/Android | yes               |
| height        | 骨架视图的高度                              | number                                 | no       | iOS/Android | yes               |
| listProps     | 使用 template={SkeletonView.templates.LIST_ITEM} 时可用的属性 | SkeletonListProps                      | no       | iOS/Android | yes               |
| renderContent | 一旦内容准备好（即 showContent 为 true）将渲染内容的函数。该方法将使用 Skeleton 的 customValue 调用（即 renderContent(props?.customValue)） | (customValue?: any) => React.ReactNode | no       | iOS/Android | yes               |
| shimmerStyle  | 骨架视图的额外样式                        | ViewStyle                              | no       | iOS/Android | yes               |
| showContent   | 内容已加载，开始淡出骨架并淡入内容 | boolean                                | no       | iOS/Android | yes               |
| style         | 覆盖容器样式                                    | ViewStyle                              | no       | iOS/Android | yes               |
| template      | 可通过 SkeletonView.templates.xxx 访问。骨架视图的类型。 | listItem \|content                     | no       | iOS/Android | yes               |
| testID        | 组件测试 ID                                        | string                                 | no       | iOS/Android | yes               |
| times         | 生成重复骨架                                | number                                 | no       | iOS/Android | yes               |
| timesKey      | 重复 SkeletonViews 的键前缀                | string                                 | no       | iOS/Android | yes               |
| width         | 骨架视图的宽度                               | number                                 | no       | iOS/Android | yes               |

**searchInput**：<sup>7.43.1+</sup>用于过滤目的的搜索输入组件。

| Name               | Description                                                  | Type               | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | ------------------ | -------- | ----------- | ----------------- |
| onDismiss          | 关闭操作的回调                                  | () => void         | no       | iOS/Android | yes               |
| onClear            | 清除按钮回调                                     | () => void         | no       | iOS/Android | yes               |
| showLoader         | 是否显示加载器而不是左侧搜索图标。    | boolean            | no       | iOS/Android | yes               |
| customLoader       | 渲染而不是默认加载器的自定义加载器元素 | React.ReactElement | no       | iOS/Android | yes               |
| customRightElement | 自定义右侧元素                                         | React.ReactElement | no       | iOS/Android | yes               |
| cancelButtonProps  | 取消按钮的属性                                  | ButtonProps        | no       | iOS/Android | yes               |
| inaccessible       | 关闭此视图及其嵌套子视图的无障碍功能 | boolean            | no       | iOS/Android | yes               |
| useSafeArea        | 如果 SearchInput 渲染在安全区域中（屏幕顶部） | boolean            | no       | iOS/Android | yes               |
| containerStyle     | 覆盖输入的样式                                | ViewStyle          | no       | iOS/Android | yes               |
| style              | 覆盖容器的样式                                | ViewStyle          | no       | iOS/Android | yes               |

**PieChart**：<sup>7.43.1+</sup>圆形统计图组件。

| Name         | Description                                   | Type                   | Required | Platform    | HarmonyOS Support |
| ------------ | --------------------------------------------- | ---------------------- | -------- | ----------- | ----------------- |
| segments     | 饼图段数组                      | PieChartSegmentProps[] | no       | iOS/Android | yes               |
| diameter     | 饼图直径                            | number                 | no       | iOS/Android | yes               |
| dividerWidth | 段之间分隔线的宽度 | number                 | no       | iOS/Android | yes               |
| dividerColor | 段之间分隔线的颜色 | ColorValue             | no       | iOS/Android | yes               |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Color**: 可以进行全局样式预设，通过Color获取预设样式。

| Name         | Description                                                  | Type                                             | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------ | -------- | ----------- | ----------------- |
| loadColors   | 加载一组要在应用程序中使用的颜色。                  | ({[key: string]: string}) => void                | no       | iOS/Android | yes               |
| loadSchemes  | 加载一组方案颜色以支持深色/浅色模式。      | ({[name: string]: {[key: string]: any}}) => void | no       | iOS/Android | yes               |
| rgba         | 返回带有颜色和透明度的 rgba 字符串               | (color: string, num: number) => string           | no       | iOS/Android | yes               |
| getColorTint | 获取颜色色调                                               | (color: string, num: number) => string           | no       | iOS/Android | yes               |
| isDark       | 如果颜色被认为是深色则返回 `true`（亮色将返回 `false`） | (color: string) => boolean                       | no       | iOS/Android | yes               |

**ThemeManager**: 使用 ThemeManager 为您的应用程序设置默认的全局行为。

| Name              | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| setComponentTheme | 通过传递对象或回调为组件设置默认属性 | (componentName, defaultPropsObject) => void \| (componentName, componentProps => newDefaultPropsObject) => void | no       | iOS/Android | yes               |

**Typography**: 设置样式属性，可直接通过"属性"的方式给组件设置样式。

| Name             | Description                   | Type                                             | Required | Platform    | HarmonyOS Support |
| ---------------- | ----------------------------- | ------------------------------------------------ | -------- | ----------- | ----------------- |
| loadTypographies | 设置样式属性变量 | ({[name: string]: {[key: string]: any}}) => void | no       | iOS/Android | yes               |

**Spacings**: 设置空间大小变量，可通过 "属性-变量名" 的方式设置样式。

| Name             | Description             | Type                                | Required | Platform    | HarmonyOS Support |
| ---------------- | ----------------------- | ----------------------------------- | -------- | ----------- | ----------------- |
| loadTypographies | 设置空间大小变量 | ({ [key: string]: number }) => void | no       | iOS/Android | yes               |

## 遗留问题

- [ ] KeyboardTrackingView组件，将输入框子节点保持在键盘上方后点击事件位置异常: [issue#4](https://github.com/react-native-oh-library/react-native-ui-lib/issues/4)
- [ ]  原生组件KeyboardAccessoryView切换自定义键盘未实现: [issue#3](https://github.com/react-native-oh-library/react-native-ui-lib/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wix/react-native-ui-lib/blob/master/LICENSE) ，请自由地享受和参与开源。

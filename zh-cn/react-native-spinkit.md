> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-spinkit</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/maxs15/react-native-spinkit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-spinkit)

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 1.5.1  | @react-native-oh-tpl/react-native-spinkit | [Github](https://github.com/react-native-oh-library/react-native-spinkit) | [Github Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases) | 0.72 |
| 1.6.0 | @react-native-ohos/react-native-spinkit   | [Github](https://github.com/react-native-oh-library/react-native-spinkit) | [Github Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases) | 0.77 |

## 安装与使用

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 1.5.1
npm install @react-native-oh-tpl/react-native-spinkit

# 1.6.0
npm install @react-native-ohos/react-native-spinkit
```

#### **yarn**

```bash
# 1.5.1
yarn add @react-native-oh-tpl/react-native-spinkit

# 1.6.0
yarn add @react-native-ohos/react-native-spinkit
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import Spinkit from 'react-native-spinkit';

const SpinKitDemo: React.FC = (): JSX.Element => {
    return (
    	<Spinkit 
        	type='9CubeGrid' 
        	color='#e74032' 
        	size={60} 
			style={{ backgroundColor: '#fcc424' }} 
            isVisible={true} 
		/>
    )
};

export default SpinKit;
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
- 1.5.1
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-spinkit": "file:../../node_modules/@react-native-oh-tpl/react-native-spinkit/harmony/spinKit.har"
  }
```
- 1.6.0
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-spinkit": "file:../../node_modules/@react-native-ohos/react-native-spinkit/harmony/spinKit.har"
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

### 3.在 ArkTs 侧引入 SpinKitView 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
  // 1.5.1
+ import { SpinKitView } from "@react-native-oh-tpl/react-native-spinkit"

  // 1.6.0
+ import { SpinKitView } from "@react-native-ohos/react-native-spinkit"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SpinKitView.NAME) {
+   SpinKitView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+   })
+ }
 ...
}
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SpinKitView.NAME
  ];
```
### 4.在 ArkTs 侧引入 SpinKitPackage Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
  // 1.5.1
+ import { RNSpinKitPackage } from '@react-native-oh-tpl/react-native-spinkit/ts';

  // 1.6.0
+ import { RNSpinKitPackage } from '@react-native-ohos/react-native-spinkit/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSpinKitPackage(ctx)
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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**SpinKit**：加载动画渲染组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props。

| props  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| type                  | 加载动画类型                                    | string  | No       | All      | Yes               |
| type: Plane           | 单向翻转加载动画                        | string  | No       | All      | Yes               |
| type: CircleFlip      | 圆形翻转加载动画                            | string  | No       | All      | Yes               |
| type: Bounce          | 圆形嵌套弹跳加载动画 | string | No | All | Yes |
| type: Wave | 五条柱状组合加载动画 | string | No | All | Yes |
| type: WanderingCubes | 两个方块跳跃加载动画 | string | No | All | Yes |
| type: Pulse | 圆形扩散加载动画 | string | No | All | Yes |
| type: ChasingDots | 双圆弹跳加载动画 | string | No | All | Yes |
| type: ThreeBounce | 三个圆点依次显示的加载动画 | string | No | All | Yes |
| type: Circle | 多个圆点循环运动加载动画 | string | No | All | Yes |
| type: 9CubeGrid | 九个方块依次显示的加载动画 | string | No | All | Yes |
| type: WordPress | 圆形轮辐内嵌空心圆旋转加载动画 | string | No | IOS | Yes |
| type: FadingCircle | 多个方块环形运动加载动画 | string | No | All | Yes |
| type: FadingCircleAlt | 多个圆点环形运动加载动画 | string | No | All | Yes |
| type: Arc | 带缺口旋转环状加载动画 | string | No | IOS | Yes |
| type: ArcAlt | 圆形进度条样式加载动画 | string | No | IOS | Yes |
| isVisible | 加载动画显示状态 | boolean | No | All | Yes |
| color | 加载动画颜色 | string | No | All | Yes |
| size | 加载动画尺寸 | number | No | All | Yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE) ，请自由地享受和参与开源。

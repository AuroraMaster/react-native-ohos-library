> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-content-loader</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/danilowoz/react-content-loader">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/danilowoz/react-content-loader/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-content-loader)

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`react-content-loader`，具体版本所属关系如下：

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| 7.0.2  | @react-native-oh-tpl/react-content-loader | [Github](https://github.com/react-native-oh-library/react-content-loader) | [Github Releases](https://github.com/react-native-oh-library/react-content-loader/releases) | 0.72 |
| 7.1.0 | @react-native-ohos/react-content-loader   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-content-loader) | [GitCode Releases]() | 0.77 |

## 安装与使用

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V7.0.2 for RN0.72
npm install @react-native-oh-tpl/react-content-loader

# V7.1.0 for RN0.77
npm install @react-native-ohos/react-content-loader
```

#### **yarn**

```bash
# V7.0.2 for RN0.72
yarn add @react-native-oh-tpl/react-content-loader

# V7.1.0 for RN0.77
yarn add @react-native-ohos/react-content-loader
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import ContentLoader, { Facebook, Code, List, BulletList, Instagram, Rect, Circle } from 'react-content-loader/native'
import { View, ScrollView } from "react-native"

export function AppExample() {
    return <View style={{ flex: 1, backgroundColor: 'white' }}>
        <ScrollView >
            <ContentLoader
                width={'100%'}
                height={80}
                animate={false}
                viewBox="0 0 380 70"
            >
                <Circle cx="30" cy="30" r="30" />
                <Rect x="80" y="17" rx="4" ry="4" width="300" height="13" />
                <Rect x="80" y="40" rx="3" ry="3" width="250" height="10" />
            </ContentLoader>
            <Facebook></Facebook>
            <Code></Code>
            <List></List>
            <BulletList></BulletList>
            <Instagram></Instagram>
        </ScrollView>
    </View>
}

```
## Link

本库依赖@react-native-oh-tpl/react-native-svg，如已在鸿蒙工程中引入过该库，则无需再次引入。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档](/zh-cn/react-native-svg-capi.md)进行引入


## 约束与限制

### 兼容性


要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH：0.72.96; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release SDK; IDE：DevEco Studio 5.1.1.840; ROM：6.0.0;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Options

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| animate  | 设置为 false 以禁用动画         | boolean  | no | all      | yes |
| speed  | 动画速度（以秒为单位）         | number  | no | all      | yes |
| rtl  | 内容从右到左         | boolean  | no | all      | yes |
| backgroundColor  | 用作动画的背景         | string  | no | all      | yes |
| viewBox  | 使用 viewBox 属性设置自定义 viewBox 值，有关如何使用的更多信息，请阅读文章 [How to Scale SVG](https://css-tricks.com/scale-svg/)         | string  | no | all      | yes |
| foregroundColor  | 用作动画的前景         | string  | no | all      | yes |
| interval  |  动画间隔（以秒为单位）         | number  | no | all      | yes |
| beforeMask  | 在内容之前定义自定义形状         | JSX.Element  | no | all      | partially |
| uniqueKey  | 使用相同的 prop key 值，这将解决 SSR 中的不一致性问题         | string  | no | React DOM only      | no |
| title  |  用于描述元素是什么。使用 ''（空字符串）来移除。    | string  | no | React DOM only      | no |
| baseUrl  | 如果你在文档的 <head/> 中使用<base url="/" />，那么这个属性是必需的。这个属性通常这样使用：<ContentLoader baseUrl={window.location.pathname} />`，它将用相对路径填充 SVG 属性。相关[#93](https://github.com/danilowoz/react-content-loader/issues/93). | string  | no | React DOM only      | no |
| backgroundOpacity  |  背景透明度（0 = 透明，1 = 不透明）用于解决 [Safari](#safari--ios)中的一个问题     | number  | no | React DOM only      | no |
| foregroundOpacity  |  动画透明度（0 = 透明，1 = 不透明）用于解决 [Safari](#safari--ios)中的一个问题    | number  | no | React DOM only      | no |
| style  |  css 样式     | React.CSSProperties  | no | React DOM only      | no |


## 遗留问题
- [ ]  beforeMask属性设置非svg暴露出来的组件时无效: [issue#256](https://github.com/react-native-oh-library/react-native-harmony-svg/issues/256) 
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/danilowoz/react-content-loader/blob/master/LICENSE) ，请自由地享受和参与开源。
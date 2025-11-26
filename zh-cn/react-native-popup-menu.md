> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-popup-menu</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/instea/react-native-popup-menu/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/instea/react-native-popup-menu/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/instea/react-native-popup-menu/tree/58b78642808ab28012f429d59a2c302dc41b5924)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 0.16.1               |  0.72 |
| 0.18.0               |  0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-popup-menu@0.16.1 --save

# 0.77
npm install react-native-popup-menu@0.18.0 --save
```

#### **yarn**

```bash
# 0.72
yarn add react-native-popup-menu@0.16.1

# 0.77
yarn add react-native-popup-menu@0.18.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
// your entry point
import {
  MenuProvider,
  Menu,
  MenuOptions,
  MenuOption,
  MenuTrigger,
} from "react-native-popup-menu";

export const App = () => (
  <MenuProvider>
    <YourComponent />
  </MenuProvider>
);

// somewhere in your app
import {
    Text,
    View,
    Alert,
} from "react-native";
export const YourComponent = () => (
  <View>
    <Text>Hello world!</Text>
    <Menu>
      <MenuTrigger text="Select action" />
      <MenuOptions>
        <MenuOption onSelect={() => Alert.alert(`Save`)} text="Save" />
        <MenuOption onSelect={() => Alert.alert(`Delete`)}>
          <Text style={{ color: "red" }}>Delete</Text>
        </MenuOption>
        <MenuOption
          onSelect={() => Alert.alert(`Not called`)}
          disabled={true}
          text="Disabled"
        />
      </MenuOptions>
    </Menu>
  </View>
);
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-popup-menu](https://github.com/instea/react-native-popup-menu/blob/master/doc/api.md)

#### MenuProvider

| Name              | Description                                                                                                                                                                                                             | Type             | Required | Platform    | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| style             | 包装View组件的样式                                                                                                                                                                                       | Style            | No       | IOS/Android | Yes               |
| customStyles      | 定义包装器、可触摸和文本样式的对象                                                                                                                                                                      | Object           | No       | IOS/Android | Yes               |
| backHandler       | 按下返回按钮时是否关闭菜单，如果传递函数则为自定义返回按钮处理程序（需要RN >= 0.44）                                                                                | boolean/Function | No       | IOS/Android | Yes               |
| skipInstanceCheck | 通常应用程序应该只有一个菜单提供者。如果确实需要更多实例，请将skipInstanceCheck设置为true以禁用检查（和随后的警告消息） | boolean          | No       | IOS/Android | Yes               |

#### Menu

| Name            | Description                                                                                                           | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| name            | 菜单的唯一名称                                                                                                   | String   | No       | IOS/Android | Yes               |
| opened          | 声明菜单是否打开。当提供此属性时，菜单是受控的，命令式API将不起作用 | Boolean  | No       | IOS/Android | Yes               |
| renderer        | 定义位置、动画和基本菜单样式。有关更多详细信息，请参阅渲染器部分                             | Function | No       | IOS/Android | Yes               |
| rendererProps   | 将传递给渲染器的附加属性                                                                 | Object   | No       | IOS/Android | Yes               |
| onSelect        | 选择菜单选项时触发。当事件处理程序返回false时，弹出菜单保持打开状态                  | Function | No       | IOS/Android | Yes               |
| onOpen          | 菜单打开时触发                                                                                         | Function | No       | IOS/Android | Yes               |
| onClose         | 菜单关闭时触发                                                                                         | Function | No       | IOS/Android | Yes               |
| onBackdropPress | 用户按下背景（打开的菜单外部）时触发                                                       | Function | No       | IOS/Android | Yes               |

#### MenuTrigger

| Name                | Description                                                                           | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| disabled            | 指示触发器是否可以被按下                                                   | Boolean  | No       | IOS/Android | Yes               |
| children            | 作为菜单触发器渲染的React元素。与text属性互斥                | Elements | No       | IOS/Android | Yes               |
| text                | 要渲染的文本。当提供此属性时，不会渲染触发器的子元素 | String   | No       | IOS/Android | Yes               |
| customStyles        | 定义包装器、可触摸和文本样式的对象                                    | Object   | No       | IOS/Android | Yes               |
| triggerOnLongPress  | 如果为true，菜单将在onLongPress上触发而不是onPress                             | Boolean  | No       | IOS/Android | Yes               |
| testID              | 用于e2e测试以获取可触摸元素                                         | String   | No       | IOS/Android | Yes               |
| onPress             | 按下触发器时触发（取决于triggerOnLongPress，可能是长按）    | Function | No       | IOS/Android | Yes               |
| onAlternativeAction | 长按触发器时触发（取决于triggerOnLongPress，可能是按下）    | Function | No       | IOS/Android | Yes               |

#### MenuOptions

| Name                   | Description                                                                                                                                                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| optionsContainerStyle  | 选项容器的自定义样式。注意：此选项已弃用，请改用customStyles选项                                                                                        | Style    | No       | IOS/Android | Yes               |
| renderOptionsContainer | \<MenuOptions />的自定义渲染函数。它以选项组件作为参数并返回组件。例如：options => \<SomeCustomContainer>{options}\</SomeCustomContainer>（已弃用） | Function | No       | IOS/Android | Yes               |
| customStyles           | 定义包装器、可触摸和文本样式的对象                                                                                                                                           | Object   | No       | IOS/Android | Yes               |

#### MenuOption

| Name             | Description                                                                                                                                                                                                    | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| value            | 选项的值                                                                                                                                                                                                | Any      | No       | IOS/Android | Yes               |
| children         | 作为菜单选项渲染的React元素。与text属性互斥                                                                                                                                          | Elements | No       | IOS/Android | Yes               |
| text             | 要渲染的文本。当提供此属性时，不会渲染选项的子元素                                                                                                                           | String   | No       | IOS/Android | Yes               |
| disabled         | 指示选项是否可以被按下                                                                                                                                                                             | Boolean  | No       | IOS/Android | Yes               |
| disableTouchable | 禁用可触摸包装器（无按下效果且不执行onSelect）。注意：如果要在菜单中渲染"不可选择"的内容（例如分隔符），可以完全不使用MenuOption | Boolean  | No       | IOS/Android | Yes               |
| customStyles     | 定义包装器、可触摸和文本样式的对象                                                                                                                                                             | Object   | No       | IOS/Android | Yes               |
| testID           | 用于e2e测试以获取可触摸元素。如果disableTouchable=true，则不可用                                                                                                                   | String   | No       | IOS/Android | Yes               |
| onSelect         | 选择选项时触发。当事件处理程序返回false时，弹出菜单保持打开状态。注意：如果定义了此事件处理程序，它将抑制\<Menu />的onSelect处理程序                             | Function | No       | IOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/instea/react-native-popup-menu/blob/master/LICENSE) ，请自由地享受和参与开源。
> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-material-dropdown</code> </h1>
</p>

本项目基于 [react-native-material-dropdown@0.11.1](https://github.com/n4kz/react-native-material-dropdown) 开发。

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.11.1   |[@react-native-oh-tpl/react-native-material-dropdown Releases](https://github.com/react-native-oh-library/react-native-material-dropdown/releases)| 0.72       |
| 0.12.0   |[@react-native-ohos/react-native-material-dropdown Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-material-dropdown/releases)     | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

本库依赖[@react-native-ohos/react-native-material-textfield 文档](/zh-cn/react-native-material-textfield.md) 和 [@react-native-ohos/react-native-material-buttons 文档](/zh-cn/react-native-material-buttons.md)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72 
npm install @react-native-oh-tpl/react-native-material-dropdown

# 0.77 
npm install @react-native-ohos/react-native-material-dropdown
```

#### **yarn**

```bash
# 0.72 
yarn add @react-native-oh-tpl/react-native-material-dropdown

# 0.77 
yarn add @react-native-ohos/react-native-material-dropdown
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import { Dropdown } from 'react-native-material-dropdown';

class Example extends Component {
  render() {
    let data = [{
      value: 'Banana',
    }, {
      value: 'Mango',
    }, {
      value: 'Pear',
    }];

    return (
      <Dropdown
        label='Favorite Fruit'
        data={data}
      />
    );
  }
}
```



## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-material-textfield和@react-native-oh-tpl/react-native-material-buttons 的代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-material-textfield 文档](/zh-cn/react-native-material-textfield.md) 

和 [@react-native-oh-tpl/react-native-material-buttons 文档](/zh-cn/react-native-material-buttons.md)进行引入



## 约束与限制

### 兼容性

本文档内容基于以下环境验证通过：

1. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

### 此组件有以下属性:

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|         Name          |                 Description                 |   Type   | Required |  Platform   | HarmonyOS Support |
| :-------------------: | :-----------------------------------------: | :------: | :------: | :---------: | :---------------: |
|       **label**       |            标签文本            |  String  |    No    | iOS/Android |        Yes        |
|       **error**       |            错误提示文本            |  String  |    No    | iOS/Android |        Yes        |
| **animationDuration** |     动画持续时间（毫秒）     |  Number  |    No    | iOS/Android |        Yes        |
|     **fontSize**      |            字体大小             |  Number  |    No    | iOS/Android |        Yes        |
|   **labelFontSize**   |         标签字体大小          |  Number  |    No    | iOS/Android |        Yes        |
|     **baseColor**     |            基础颜色            |  String  |    No    | iOS/Android |        Yes        |
|     **textColor**     |            文本颜色            |  String  |    No    | iOS/Android |        Yes        |
|     **itemColor**     |  下拉项文本颜色（未激活项）   |  String  |    No    | iOS/Android |        Yes        |
| **selectedItemColor** |   下拉项文本颜色（激活项）    |  String  |    No    | iOS/Android |        Yes        |
| **disabledItemColor** |  下拉项文本颜色（禁用项）   |  String  |    No    | iOS/Android |        Yes        |
| **dropdownPosition**  |  下拉菜单位置（未定义时为动态）   |  Number  |    No    | iOS/Android |        Yes        |
|     **itemCount**     |         可见下拉项数量         |  Number  |    No    | iOS/Android |        Yes        |
|    **itemPadding**    |       下拉项垂直内边距        |  Number  |    No    | iOS/Android |        Yes        |
|   **itemTextStyle**   |          下拉项文本样式          |  Object  |    No    | iOS/Android |        Yes        |
|  **dropdownOffset**   |               下拉菜单偏移量               |  Object  |    No    | iOS/Android |        Yes        |
|  **dropdownMargins**  |              下拉菜单外边距               |  Object  |    No    | iOS/Android |        Yes        |
|       **data**        |             下拉项数据              | Array[]  |    No    | iOS/Android |        Yes        |
|       **value**       |               选中值                |  String  |    No    | iOS/Android |        Yes        |
|  **containerStyle**   |          容器样式          |  Object  |    No    | iOS/Android |        Yes        |
|   **overlayStyle**    |           覆盖层样式           |  Object  |    No    | iOS/Android |        Yes        |
|    **pickerStyle**    |         选择器样式         |  Object  |    No    | iOS/Android |        Yes        |
|   **shadeOpacity**    |      下拉项阴影透明度       |  Number  |    No    | iOS/Android |        Yes        |
|   **rippleOpacity**   |          涟漪效果透明度          |  Number  |    No    | iOS/Android |        Yes        |
|   **rippleInsets**    |     涟漪效果内边距     |  Object  |    No    | iOS/Android |        Yes        |
|  **rippleCentered**   | 涟漪效果是否居中 | Boolean  |    No    | iOS/Android |        Yes        |
|    **renderBase**     |            渲染基础组件            | Function |    No    | iOS/Android |        Yes        |
|  **renderAccessory**  |         渲染文本字段附件         | Function |    No    | iOS/Android |        Yes        |
|  **valueExtractor**   | 值提取函数（参数：item, index） | Function |    No    | iOS/Android |        Yes        |
|  **labelExtractor**   | 从项中提取标签 (参数: item, index) | Function |    No    | iOS/Android |        Yes        |
|  **propsExtractor**   | 属性提取函数（参数：item, index） | Function |    No    | iOS/Android |        Yes        |
|   **onChangeText**    |            值变更回调函数             | Function |    No    | iOS/Android |        Yes        |

## **API**

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name         |       Description       |  Type   | Required |  Platform   | HarmonyOS Support |
| :-----------------: | :---------------------: | :-----: | :------: | :---------: | :---------------: |
|     **focus()**     |      获取焦点      |         |    No    | iOS/Android |        Yes        |
|     **blur()**      |      释放焦点      |         |    No    | iOS/Android |        Yes        |
| **selectedIndex()** |   获取选中项索引    | Number  |    No    | iOS/Android |        Yes        |
|     **value()**     |    获取当前值    | String  |    No    | iOS/Android |        Yes        |
| **selectedItem()**  |    获取选中项    | Object  |    No    | iOS/Android |        Yes        |
|   **isFocused()**   | 获取当前焦点状态 |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他
- renderAccessory属性：需要指定renderRightAccessory或者renderLeftAccessory

## 开源协议

本项目基于 [The BSD License (BSD )](https://github.com/n4kz/react-native-material-dropdown/blob/master/license.txt) ，请自由地享受和参与开源。


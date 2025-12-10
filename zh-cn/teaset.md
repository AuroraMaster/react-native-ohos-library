> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>teaset</code> </h1>
</p>

本项目基于 [teaset@0.7.5](https://github.com/rilyu/teaset) 开发。

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-ohos/teaset Releases](https://github.com/react-native-oh-library/teaset/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

| 三方库版本                 | 发布信息                                      |  支持RN版本                 |
| ------------------------- | ------------------------------------------------- |  -------------------------- |
| 0.7.6                 | [@react-native-ohos/teaset Releases](https://github.com/react-native-oh-library/teaset/releases)  | 0.72/0.77 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/teaset

# 0.72
npm install @react-navigation/native-stack@6.9.26
npm install @react-navigation/native@6.1.7
npm install @react-native-oh-tpl/react-native-screens

# 0.77
npm install @react-navigation/native-stack@7.2.0
npm install @react-navigation/native@7.1.17
npm install @react-native-ohos/react-native-screens

```

#### **yarn**

```bash
yarn add @react-native-ohos/teaset

# 0.72
yarn add @react-navigation/native-stack@6.9.26
yarn add @react-navigation/native@^6.1.7
yarn add @react-native-oh-tpl/react-native-screens

# 0.77
yarn add @react-navigation/native-stack@7.2.0
yarn add @react-navigation/native@7.1.17
yarn add @react-native-ohos/react-native-screens
```

<!-- tabs:end -->

下面的代码展示了该库的基本使用场景：

**Hello world**  
从 teaset 包中 import 组件即可使用
```
import React, {Component} from 'react';
import {View, AppRegistry} from 'react-native';

import {Label} from 'teaset';

class HelloWorldApp extends Component {
  render() {
    return (
      <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
        <Label size='xl' text='Hello world!' />
      </View>
    );
  }
}

AppRegistry.registerComponent('HelloWorldApp', () => HelloWorldApp);
```
**按需加载**  
使用单独 import 组件实现按需加载
```
import Label from 'teaset/components/Label/Label';
```

## Link

本库 HarmonyOS 侧实现依赖 react-native-screens 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[ react-native-screens 文档](/zh-cn/react-native-screens.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下环境验证通过：

1. RNOH: 0.72.x/0.77.x; SDK：HarmonyOS 6.0.0.47 (API Version 20 Release); IDE：DevEco Studio 6.0.0 Release; ROM：6.0.0.108 SP6;

## 组件

> [!TIP] "Platform" 列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 1. Theme - 主题

Theme 是 Teaset 的组件样式定义对象, 用于定义 Teaset 组件的默认样式。

**静态方法：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set | 设置主题配色方案，支持完整主题对象或部分属性修改 | function | yes | iOS/Android | yes |
| themes | 获取所有内置主题配色方案 (default、black、violet) | object | yes | iOS/Android | yes |

**主题属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isLandscape | 是否横屏 | bool | no | iOS/Android | yes |
| statusBarHeight | 获取状态栏高度 | number | no | iOS/Android | yes |
| screenInset | 屏幕内容内嵌区域 | object | no | iOS/Android | yes |

### 2. Label - 标签

Label 组件用于文本显示, 一般为单行的少量文字。

- Label 组件继承 **[Text](https://reactnative.dev/docs/text.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 标签类型 (default, title, detail, danger) | string | no | iOS/Android | yes |
| size | 显示尺寸大小 (xl, lg, md, sm, xs) | string | no | iOS/Android | yes |
| text | 文本内容 | string/number | no | iOS/Android | yes |
| numberOfLines | 显示行数 (继承自 Text 组件并修改默认值)| number | no | iOS/Android | yes |

### 3. Button - 按钮

Button 组件定义一个按钮, 可视、可触摸且有触摸反馈。

- Button 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 按钮类型 (default, primary, secondary, danger, link) | string | no | iOS/Android | yes |
| size | 显示尺寸大小 (xl, lg, md, sm, xs) | string | no | iOS/Android | yes |
| title | 按钮标题 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| disabled | 是否禁用 (为 true 时组件显示为半透明且不可触摸。) | bool | no | iOS/Android | yes |
| onPress | 点击事件 | function | no | iOS/Android | yes |

### 4. Checkbox - 复选框

Checkbox 组件定义一个复选框, 具有选中、非选中两种状态。

- Checkbox 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| checked | 是否选中 | bool | no | iOS/Android | yes |
| defaultChecked | 默认是否选中 | bool | no | iOS/Android | yes |
| size | 显示尺寸大小 (lg, md, sm) | string | no | iOS/Android | yes |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| checkedIcon | 选中图标 | element | no | iOS/Android | yes |
| checkedIconStyle | 选中图标样式 | ImageStyle | no | iOS/Android | yes |
| uncheckedIcon | 未选中图标 | element | no | iOS/Android | yes |
| uncheckedIconStyle | 未选中图标样式 | ImageStyle | no | iOS/Android | yes |
| disabled | 是否禁用 (继承自 TouchableOpacity, 为 true 时组件显示为半透明且不可触摸) | bool | no | iOS/Android | yes |
| hitSlop | 触摸区域扩展 (继承自 TouchableOpacity 并修改默认值) | object | no | iOS/Android | yes |
| onChange | 状态改变事件 | function | no | iOS/Android | yes |

### 5. Input - 输入框

Input 组件定义一个输入编辑框。

- Input 组件继承 **[TextInput](https://reactnative.dev/docs/textinput.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | 显示尺寸大小 (lg, md, sm) | string | no | iOS/Android | yes |
| disabled | 是否禁用 (为 true 时组件显示为半透明且不可聚焦) | bool | no | iOS/Android | yes |
| underlineColorAndroid | Android 下划线颜色 (继承自 TextInput 并修改默认值) | string/'rgba(0, 0, 0, 0)' | no | Android |yes |
| onChangeText | 文本改变事件 | function | no | iOS/Android | yes |

### 6. Select - 选择框

Select 组件定义一个选择框。

- Select 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | 显示尺寸大小 (lg, md, sm) | string | no | iOS/Android | yes |
| value | 选中值 | any | no | iOS/Android | yes |
| valueStyle | 选中值文本样式 | style | no | iOS/Android | yes |
| items | 下拉列表项数组 | array | no | iOS/Android | yes |
| getItemValue | 获取列表项值函数 (取 items 数组元素的 value 值, 传入参数为(item, index), item = items[index], 默认直接使用 item) | function | no | iOS/Android | yes |
| getItemText | 获取列表项显示文本函数 (取 items 数组元素的显示文本或 React Native 组件, 传入参数为(item, index), item = items[index], 默认直接使用 item) | function | no | iOS/Android | yes |
| pickerType | 选择器类型 (auto, pull, popover) | string | no | iOS/Android | yes |
| pickerTitle | PullPicker 选择器标题 | string | no | iOS/Android | yes |
| editable | 是否可编辑 | bool | no | iOS/Android | yes |
| icon | 右侧指示图标 (none:无图标、default:默认图标) | string/ImageSource/element | no | iOS/Android | yes |
| iconTintColor | 图标颜色 | string | no | iOS/Android | yes |
| placeholder | 占位文本 | string | no | iOS/Android | yes |
| placeholderTextColor | 占位文本颜色 (value 为空时显示此字符串) | string | no | iOS/Android | yes |
| disabled | 是否禁用 | bool | no | iOS/Android | yes |
| onSelected | 选中事件 (当选择器选择 items 数组某项时调用, item = items[index]) | function | no | iOS/Android | yes |

### 7. Stepper - 步进器

Stepper 组件定义一个步进器。

- Stepper 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| defaultValue | 默认值 (仅在组件初始化时使用一次, 如不想传入 value 并监听 onChange 保持状态同步, 可使用 defaultValue 代替) | number | no | iOS/Android | yes |
| value | 当前值 | number | no | iOS/Android | yes |
| step | 步进值 (整数或小数) | number | no | iOS/Android | yes |
| max | 最大值 (默认不限制) | number | no | iOS/Android | yes |
| min | 最小值 (默认不限制) | number | no | iOS/Android | yes |
| valueStyle | 值显示样式 | style | no | iOS/Android | yes |
| valueFormat | 值格式化函数 (传入参数为 value, 默认直接使用 value) | function | no | iOS/Android | yes |
| subButton | “减“按钮 | string/element | no | iOS/Android | yes |
| addButton | “加“按钮 | string/element | no | iOS/Android | yes |
| showSeparator | 是否显示分隔线 (如需完全自定义组件样式可设置为 false) | bool | no | iOS/Android | yes |
| disabled | 是否禁用 (为 true 时组件显示为半透明且不可触摸) | bool | no | iOS/Android | yes |
| editable | 是否可编辑 | bool | no | iOS/Android | yes |
| onChange | 值改变事件 (当 value 值发生改变时调用) | function | no | iOS/Android | yes |

### 8. SearchInput - 搜索输入框

SearchInput 组件定义一个搜索输入框, 与 Input 的区别是有多一个放大镜图标, 在内容为空时且不在编辑状态时居中显示, 否则左对齐。

- SearchInput 组件继承 **[TextInput](https://reactnative.dev/docs/textinput.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | 组件样式 (组件的容器 View 的样式) | ViewStyle | no | iOS/Android | yes |
| inputStyle | 输入框样式 | style | no | iOS/Android | yes |
| iconSize | 放大镜图标长宽尺寸 (默认值在 Theme 中设置) | number | no | iOS/Android | yes |
| disabled | 是否禁用 (为 true 时组件显示为半透明且不可触摸) | bool | no | iOS/Android | yes |
| underlineColorAndroid | Android 下划线颜色 (继承自 TextInput 并修改默认值) | string/'rgba(0, 0, 0, 0)' | no | Android | yes |
| onChangeText| 文本改变事件 | function | no | iOS/Android | yes |

### 9. Badge - 徽章

Badge 组件定义一个徽章, 可用于图标角标显示数字、字母、原点等, 也可以自定义显示其它内容。

- Badge 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 徽章类型 (capsule, square, dot) | string | no | iOS/Android | yes |
| count | 徽章显示数字 | string/number | no | iOS/Android | yes |
| countStyle |徽章显示数字样式 | style | no | iOS/Android | yes |
| maxCount | 最大显示数字 (当 count 大于此值时显示为 maxCount 后接一个加号, 如'99+', 当 count 不是数字时无效) | number | no | iOS/Android | yes |

### 10. Popover - 气泡

Popover 组件定义一个气泡, 是一个可在边框任意位置显示一个三角形箭头的圆角矩形容器, 常用于聊天信息显示或弹出提示等。

- Popover 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| arrow | 三角形箭头的位置 ( none, topLeft, top, topRight, rightTop, right, rightBottom, bottomRight, bottom, bottomLeft, leftBottom, left, leftTop)| string | no | iOS/Android | yes |
| paddingCorner | 三角形箭头与角点距离 ( 与 arrow 值有关, 如 arrow = 'topLeft' 时表示三角形箭头与左上角的距离, 默认值在 Theme 中设置) | number | no | iOS/Android | yes |

### 11. NavigationBar - 导航栏

NavigationBar 组件定义一个页面导航条, 用于页面顶部显示页面标题及按钮等。

- NavigationBar 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 风格类型 (auto, ios, android, harmony) | string | no | iOS/Android | yes |
| title | 导航条标题 (传入字符串时使用<NavigationBar.Title />组件渲染) | string/element | no | iOS/Android | yes |
| titleStyle | 	导航条标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| leftView | 导航条左视图 | element | no | iOS/Android | yes |
| rightView | 导航条右视图 | element | no | iOS/Android | yes |
| tintColor | 导航条左、右视图文字与图像颜色 (默认值在 Theme 中设置) | string | no | iOS/Android | yes |
| background | 导航条背景视图 | element | no | iOS/Android | yes |
| hidden | 是否隐藏导航条 | bool | no | iOS/Android | yes |
| animated | 显示/隐藏导航条和状态栏时是否有动画效果 | bool | no | iOS/Android | yes |
| statusBarStyle | 系统状态栏样式 (default, light-content, dark-content) | string | no | iOS/Android | yes |
| statusBarColor | 导航条背景颜色 (默认值在 Theme 中设置) | string | no | iOS/Android | yes |
| statusBarHidden | 是否隐藏系统状态栏 | bool | no | iOS/Android | yes |
| statusBarInsets | 是否自动增加状态栏占位空间 | bool | no | iOS | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Title | 导航条标题组件 | class | no | iOS/Android | yes |
| Button | 导航条按钮组件 | class | no | iOS/Android | yes |
| LinkButton| 导航条链接按钮组件, 继承自 NavigationBar.Button | class | no | iOS/Android | yes |
| IconButton | 导航条图标按钮组件, 继承自 NavigationBar.Button | class | no | iOS/Android | yes |
| BackButton | 导航条返回按钮组件, 继承自 NavigationBar.Button | class | no | iOS/Android | yes |

**NavigationBar.Title**

- NavigationBar.Title 组件继承 **[Text](https://reactnative.dev/docs/text.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | 显示文本 | string/number | no | iOS/Android | yes |
| numberOfLines | 显示行数 (继承自 Text 组件并修改默认值) | number | no | iOS/Android | yes |
| allowFontScaling| 是否允许系统自动缩放字体大小 (继承自 Text 组件并修改默认值。) | bool | no | iOS | yes |

**allowFontScaling** 属性依赖应用配置，具体配置方案参考[如何设置应用内字体是否跟随系统变化](https://developer.huawei.com/consumer/cn/doc/architecture-guides/common-v1_26-ts_20-0000002298448781) 或者以下步骤：

- 1.新建配置文件“AppScope/resources/base/profile/configuration.json”
```
{
  "configuration": {
    // nonFollowSystem不跟随系统变化；followSystem跟随系统变化
    "fontSizeScale": "followSystem",
    "fontSizeMaxScale": "3.2"
  }
}

```
- 2.在“AppScope/app.json5”文件中引用该配置
```
{
  "app": {
    "bundleName": "com.example.temp_demo",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:app_icon",
    "label": "$string:app_name",
    // 在此处引用
    "configuration": "$profile:configuration"
  },
}
```

**NavigationBar.Button**

- NavigationBar.Button 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| hitSlop | 触摸区域扩展 (继承 TouchableOpacity 组件并修改默认值) | class | no | iOS/Android | yes |

**NavigationBar.LinkButton**

- NavigationBar.LinkButton 组件继承 **[NavigationBar.Button](#navigationbar-button-props)** 组件的全部属性。


| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 按钮标题 | string/number | no | iOS/Android | yes |

**NavigationBar.IconButton**

- NavigationBar.IconButton 组件继承 **[NavigationBar.Button](#navigationbar-button-props)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| icon | 按钮图标 | ImageSource | no | iOS/Android | yes |

**NavigationBar.BackButton**

- NavigationBar.BackButton 组件继承 **[NavigationBar.Button](#navigationbar-button-props)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 标题 (默认值在 Theme 中设置) | string\number | no | iOS/Android | yes |
| icon | 按钮图标 | ImageSource | no | iOS/Android | yes |

<a id="listrow"></a>
### 12. ListRow - 列表行

ListRow 组件用于显示一个列表行, 定义了一系列易于使用的元素属性, 使得可以快速开发出基于 ListView、ScrollView 的应用。

- ListRow 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| detail | 详细内容 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| detailStyle | 详细内容样式 (当 detail 类型为 element 时无效) | style | no | iOS/Android | yes |
| detailMultiLine | 详细内容是否支持多行 (默认为 titlePlace = 'top' 时为 true, 否则为 false) | bool | no | iOS/Android | yes |
| icon | 左侧图标 | element/ImageSource | no | iOS/Android | yes |
| accessory | 右侧指示图标 (**none**: 无;<br/>**auto**: 自动, 当设置了 onPress 属性时为'indicator', 否则为'none';<br/>**empty**: 空, 不显示指示图标, 但占用'check'或'indicator'大小的位置;<br/>**check**: 小勾图标, 一般用于表示该行已被选中;<br/>**indicator**: 大于号图标, 一般用于表示点击此行打开新页面;) | string/element/ImageSource | no | iOS/Android | yes |
| topSeparator | 顶部分隔线 (none, full, indent) (缩进分隔线仅左侧缩进) | string/element | no | iOS/Android | yes |
| bottomSeparator | 底部分隔线 (none, full, indent) (缩进分隔线仅左侧缩进)| string/element | no | iOS/Android | yes |
| titlePlace | 标题位置 (left, top, none) | string | no | iOS/Android | yes |
| swipeActions | 向左滑动时显示的操作按钮列表 (建议使用 ListRow.SwipeActionButton 组件) | array | no | iOS/Android | yes |
| activeOpacity | 点击不透明度 (继承自 TouchableOpacity 并修改默认值, 传入 onPress 时默认为 0.2, 否则为 1) | number | no | iOS/Android | yes |
| onPress | 点击事件 | function | no | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| SwipeActionButton | 滑动按钮组件 | class | no | iOS/Android | yes |

**ListRow.SwipeActionButton**

- SwipeActionButton 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 显示样式类型(default, danger) | string | no | iOS/Android | yes |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |

### 13. Carousel - 走马灯

Carousel 组件定义一个跑马灯组件, 一般用于图片、信息页面轮播, 也可用于内容分页显示。

- Carousel 组件继承 **[ScrollView](https://reactnative.dev/docs/scrollview.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| carousel | 是否开启轮播 (为 false 时停止轮播, 可以调用 scrollToPage 或 scrollToNextPage 方法滚动到页面) | bool | no | iOS/Android | yes |
| interval | 每页停留时间(单位为毫秒, carousel = true 时有效) | number | no | iOS/Android | yes |
| direction | 轮播方向 (carousel = true 时有效) <br/>**forward**: 正向轮播，页面从右往左滚动;<br/>**backward**: 反向轮播, 页面从左往右滚动  | string | no | iOS/Android | yes |
| startIndex | 起始页面索引 | number | no | iOS/Android | yes |
| cycle | 是否循环播放 (carousel = true 时有效) | bool | no | iOS/Android | yes |
| control | 页面指示器 (为 true 时显示默认页面控制器, 也可以传入自定义的页面控制器, 建议使用 Carousel.Control 组件) | bool/element | no | iOS/Android | yes |
| horizontal |  横向滚动 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| pagingEnabled | 分页滚动 (继承自 ScrollView 并修改默认值)| bool | no | iOS/Android | yes |
| showsHorizontalScrollIndicator | 显示横向滚动条 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| showsVerticalScrollIndicator | 显示竖向滚动条 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| alwaysBounceHorizontal | 总是横向弹性滚动 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| alwaysBounceVertical | 总是纵向弹性滚动 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| bounces | 弹性滚动 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| automaticallyAdjustContentInsets | 自动调整内容内边距 (继承自 ScrollView 并修改默认值) | bool | no | iOS/Android | yes |
| scrollEventThrottle | 滚动事件的触发频率 (继承自 ScrollView 并修改默认值)| number | no | iOS/Android | yes |
| onChange | 页面改变事件 | function | no | iOS/Android | yes |
| scrollToPage | 滚动到指定页面 | function | no | iOS/Android | yes |
| scrollToNextPage | 滚动到下一页 | function | no | iOS/Android | yes |

**Carousel.Control 组件：**

- Carousel.Control 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| dot | 页面指示点元素 | element | no | iOS/Android | yes |
| activeDot | 当前页面指示点元素 | element | no | iOS/Android | yes |

### 14. Projector - 幻灯机

Projector 组件定义一个幻灯机组件, 这是一个自动保持状态的多页显示组件, 并且具有视图缓存功能的, 切换页面就像切换幻灯机胶片一样, 原页面的内容和状态不会消失, 再切换回这个页面时原样呈现而无需重新渲染。

- Projector 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| index | 当前胶片(页面)序号 | number | no | iOS/Android | yes |
| slideStyle | 胶片(页面)样式 | ViewStyle | no | iOS/Android | yes |

### 15. SegmentedBar - 分段工具条

SegmentedBar 组件定义一个分段工具条组件, 与 <Carousel /> 或 <Projector /> 搭配使用可实现同一页面中多项内容分段显示。

- SegmentedBar 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| justifyItem | Item 排列模式。(<br/>**fixed**: 固定位置等宽排列;<br/>**scrollable**: 可滚动，Item 数量较多一屏显示不下时使用这种模式) | string | no | iOS/Android | yes |
| indicatorType | 激活指示器类型。(<br/>**none**: 无<br/>**boxWidth**: 等分区间宽度<br/>**itemWidth**: Item 内容宽度<br/>**customWidth**: 指定宽度) | string | no | iOS/Android | yes |
| indicatorPosition | 激活指示器位置 (top, bottom) | string | no | iOS/Android | yes |
| indicatorLineColor | 指示器线条颜色 (默认值在 Theme 中设置) | string | no | iOS/Android | yes |
| indicatorLineWidth | 指示器线条高度 (默认值在 Theme 中设置) | number | no | iOS/Android | yes |
| indicatorWidth | 激活指示器线宽度 (当 indicatorType 为 customWidth 时起作用) | number | no | iOS/Android | yes |
| indicatorPositionPadding |激活指示器与上边界或下边界的距离 (默认值在 Theme 中设置)  | number | no | iOS/Android | yes |
| animated | 改变激活 Item 时是否有动画效果 | bool | no | iOS/Android | yes |
| autoScroll | 是否自动滚动激活 Item 到容器中间 (仅 justifyItem 为 'scrollable' 时有效) | bool | no | iOS/Android | yes |
| activeIndex | 激活 Item 序号 | number | no | iOS/Android | yes |
| onChange | 选项改变事件 | function | no | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | 分段工具条组件 Item 组件 | class | no | iOS/Android | yes |

**SegmentedBar.Item 属性：**

- SegmentedBar.Item 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| activeTitleStyle | 激活状态标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| badge | 徽章 (为字符串、数字时使用 `<Badge />` 组件渲染) | string/number/element | no | iOS/Android | yes |
| active | 是否激活 | bool | no | iOS/Android | yes |

### 16. SegmentedView - 分段器

SegmentedView 组件定义一个分段器组件, 一般用于同一页面中多项内容分段显示。<br/>SegmentedView 组件为 `<SegmentedBar />` 、 `<Projector />` /  `<Carousel />` 的易用性封装复合组件。

- SegmentedView 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 分段器类型。(<br/>**projector**: 幻灯机, 内容页面使用`<Projector />`组件渲染<br/>**carousel**: 走马灯, 内容页面使用`<Carousel />`组件渲) | string | no | iOS/Android | yes |
| barPosition | 分段工具条位置 (top, bottom) | string | no | iOS/Android | yes |
| barStyle | 分段工具条样式 | style | no | iOS/Android | yes |
| justifyItem | Item 排列模式。(<br/>**fixed**: 固定位置等宽排列;<br/>**scrollable**: 可滚动，Item 数量较多一屏显示不下时使用这种模式) | string | no | iOS/Android | yes |
| indicatorType | 分段工具条激活指示器类型。(<br/>**none**: 无<br/>**boxWidth**: 等分区间宽度<br/>**itemWidth**: Item 内容宽度) | string | no | iOS/Android | yes |
| indicatorPosition | 分段工具条激活指示器位置 (top, bottom) | string | no | iOS/Android | yes |
| indicatorLineColor | 激活指示器颜色 (默认值在 Theme 中设置) | string | no | iOS/Android | yes |
| indicatorLineWidth | 激活指示器线宽度 (默认值在 Theme 中设置) | number | no | iOS/Android | yes |
| indicatorPositionPadding | 激活指示器与上边界或下边界的距离 (默认值在 Theme 中设置) | number | no | iOS/Android | yes |
| animated | 分段工具条改变激活 Item 时是否有动画效果 | bool | no | iOS/Android | yes |
| autoScroll | 分段工具条是否自动滚动激活 Item 到容器中间 (仅 justifyItem 为 'scrollable' 时有效) | bool | no | iOS/Android | yes |
| activeIndex | 分段工具条激活 Item 序号 | number | no | iOS/Android | yes |
| onChange | 页面改变事件 | function | no | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Sheet | 分段器 Sheet 组件 | class | no | iOS/Android | yes |

**SegmentedView.Sheet 属性：**

- SegmentedView.Sheet 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| activeTitleStyle | 激活标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| badge | 徽章 (为字符串、数字时使用 `<Badge />`组件渲染) | string/number/element | no | iOS/Android | yes |

### 17. TabView - 标签页

TabView 组件定义一个标签页组件, 用于在一个页面上显示多个子页面, 通过页面底部的 TabBar 切换子页面。

- TabView 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 标签页类型。(<br/>**projector**: 幻灯机, 子页面使用`<Projector />`组件渲染<br/>**carousel**: 走马灯, 子页面使用`<Carousel />`组件渲染) | string | no | iOS/Android | yes |
| barStyle | TabBar 工具条样式 | style | no | iOS/Android | yes |
| activeIndex | 活动 Sheet 序号 | number | no | iOS/Android | yes |
| onChange | 页面改变事件 (改变当前页面时调用, index 为当前 Sheet 序号) | function | no | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Sheet | 标签页 Sheet 组件 | class | no | iOS/Android | yes |
| Button | 标签页按钮组件 (此组件由 Sheet 组件自动渲染, 无须代码显式声明, 但可以修改 TabView.Button 为自定义类以更改标签页按钮组件) | class | no | iOS/Android | yes |

**TabView.Sheet 属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Sheet类型 (sheet, button) | string | no | iOS/Android | yes |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| icon | 激活状态按钮图标 | ImageSource/element | no | iOS/Android | yes |
| activeIcon | 激活图标 | ImageSource/element | no | iOS/Android | yes |
| badge | 徽章 (为字符串、数字时使用 `<Badge />`组件渲染) | string/number/element | no | iOS/Android | yes |
| onPress | 点击事件 | function | no | iOS/Android | yes |

**TabView.Button 属性：**

- TabView.Button 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| titleStyle | 标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| activeTitleStyle | 激活状态标题样式 (当 title 类型为 element 时无效) | style | no | iOS/Android | yes |
| icon | 按钮图标 | ImageSource/element | no | iOS/Android | yes |
| activeIcon | 激活状态按钮图标 | ImageSource/element | no | iOS/Android | yes |
| badge | 徽章 (为字符串、数字时使用 `<Badge />`组件渲染) | string/number/element | no | iOS/Android | yes |
| active | 是否激活 | bool | no | iOS/Android | yes |

### 18. TransformView - 可变视图

TransformView 组件定义一个可变视图, 支持双指按捏缩放、单指触摸移动手势。

- TransformView 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| containerStyle | 内部容器样式 | style | no | iOS/Android | yes |
| maxScale | 最大缩放倍数 | number | no | iOS/Android | yes |
| minScale | 最小缩放倍数 | number | no | iOS/Android | yes |
| magnetic | 磁性边框 (当缩放后尺寸小于视图尺寸时自动放大到视图大小) | bool | no | iOS/Android | yes |
| tension | 拉拽阻力 (当图片边缘在视图内时继续拉拽有阻力效果) | number | no | iOS/Android | yes |
| onWillTransform | Transform 开始 (三个参数分别为 x 坐标、y 坐标、缩放倍数) | function | no | iOS/Android | yes |
| onTransforming | Transform 进行中 (三个参数分别为 x 坐标、y 坐标、缩放倍数) | function | no | iOS/Android | yes |
| onDidTransform | Transform 结束 (三个参数分别为 x 坐标、y 坐标、缩放倍数) | function | no | iOS/Android | yes |
| onWillMagnetic | 磁性边框效果开始前调用 (返回 true 允许磁性边框效果，否则阻止磁性边框效果效果， magnetic = true 时有效) | function | no | iOS/Android | yes |
| onDidMagnetic | 磁性边框效果结束时调用 (三个参数分别为 x 坐标、y 坐标、缩放倍数) | function | no | iOS/Android | yes |
| onPress | 单击事件 (触摸结束时调用, 与 TouchableOpacity.onPress 一致) | function | no | iOS/Android | yes |
| onLongPress | 长按事件 (按压组件超过 500ms 时调用, 与 TouchableOpacity.onLongPress 一致) | function | no | iOS/Android | yes |

### 19. AlbumView - 相册视图

AlbumView 组件定义一个相册视图, 支持多图左右切换显示，支持双指按捏缩放、单指触摸移动手势。

- AlbumView 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| images | 相册图片数组 (数组元素为 ImageSource 或 React Native 组件) | array | yes | iOS/Android | yes |
| thumbs | 相册缩略图数组 (数组元素为 ImageSource ) | array | no | iOS/Android | yes |
| index | 显示图片索引 (设置此属性需要监听 onChange 事件并自行维护状态) | number | no | iOS/Android | yes |
| defaultIndex | 默认显示图片索引 | number | no | iOS/Android | yes |
| maxScale | 最大缩放倍数 | number | no | iOS/Android | yes |
| space | 相册图片间隔空间 | number | no | iOS/Android | yes |
| control | 页面控制器 (为 true 时显示默认页面控制器, 也可以传入自定义的页面控制器, 建议使用 Carousel.Control 组件) | element | no | iOS/Android | yes |
| onWillChange | 改变当前页面前时调用 (index 为当前页面索引值, newIndex 为将要改变的页面索引值) | function | no | iOS/Android | yes |
| onChange | 改变当前页面完成后调用 (index 为改变后页面索引值, oldIndex 为改变前页面索引值) | function | no | iOS/Android | yes |
| onPress | 单击事件 (触摸结束时调用) | function | no | iOS/Android | yes |
| onLongPress | 长按事件 (按压组件超过 500ms 时调用) | function | no | iOS/Android | yes |
| onWillLoadImage | 加载图片前调用 | function | no | iOS/Android | yes |
| onLoadImageSuccess | 加载图片成功时调用 | function | no | iOS/Android | yes |
| onLoadImageFailure | 加载图片失败时调用 | function | no | iOS/Android | yes |

### 20. Wheel - 滚轮

Wheel 组件定义一个滚轮, 可用于滚轮式选择器。

- Wheel 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | 可选项列表 (数组元素可以是字符串、数字或 React Native 组件) | array | yes | iOS/Android | yes |
| itemStyle | 选项样式 (当 items 数组元素是 React Native 组件时无效) | style | no | iOS/Android | yes |
| holeStyle | 当前项窗口样式 (需指定 height 属性) | style | no | iOS/Android | yes |
| maskStyle | 当前项上下蒙版样式 | style | no | iOS/Android | yes |
| holeLine | 当前项窗口分隔线 | number/element | no | iOS/Android | yes |
| index | 当前索引 (设置此属性需要监听 onChange 事件并自行维护状态) | number | no | iOS/Android | yes |
| defaultIndex | 默认当前项索引值 (仅在组件创建时使用一次，如不想设置 index 并维护状态，可在此属性传入初始项索引值) | number | no | iOS/Android | yes |
| onChange | 改变当前项完成后调用 (index 为改变后当前项索引值) | function | no | iOS/Android | yes |

<a id="overlay"></a>
### 21. Overlay - 浮层

Overlay 为浮层静态类, 是 Teaset 里非常重要的组成部分。

一般而言内容展示页面是二维的平面结构, 有一些辅助性的 UI 界面, 比如菜单、提示框、选择列表框等, 这并不属于主体内容的一部分, 但却是不可缺少的, 在开发时需要投入大量的时间来开发这部分代码，而且这部分代码会与主体内容的代码搅在一起, 增加代码维护的复杂度。

Overlay 使得 React Native 开发从二维变成三维的, 你可以在页面上覆盖任意层的浮层, 而且浮层界面使用函数方法来激活显示, 你完全可以把浮层代码从页面主体内容的 JSX 中剥离出来。

另外, Overlay 支持多种动画效果, 如淡入淡出、弹出、抽屉效果等, 让你的交互生动起来。

**静态方法：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 显示一个浮层视图 (输入参数 overlayView 为浮层视图, 推荐使用 Overlay.View 组件, 返回唯一的浮层 key 值) | function | yes | iOS/Android | yes |
| hide | 隐藏一个浮层视图 (输入参数 key 为浮层的 key 值) | function | yes | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| View | 浮层组件 (传入 Overlay.show 函数的组件都应是 Overlay.View 组件或继承自 Overlay.View 的组件。 Overlay.View 是浮层的根组件, 你可以在上面显示任何内容) | class | yes | iOS/Android | yes |
| PullView | 拖拉效果浮层组件 (继承自 Overlay.View, 具有类似抽屉一样的拖拉效果) | class | no | iOS/Android | yes |
| PopView | 弹出效果浮层组件 (继承自 Overlay.View) | class | no | iOS/Android | yes |
| PopoverView | 气泡效果浮层组件 (继承自 Overlay.View) | class | no | iOS/Android | yes |

<a id="overlay-view"></a>
**Overlay.View - 浮层**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | 浮层样式 | style | no | iOS/Android | yes |
| modal | 是否为模态浮层 (非模态浮层在点击内容之外的半透明区域可关闭浮层, 模态浮层则需要代码手动关闭) | bool | no | iOS/Android | yes |
| animated | 是否支持动画效果 | bool | no | iOS/Android | yes |
| overlayOpacity | 浮层非内容区域透明度 (值从 0 到 1, 透明度从全透明到不透明。默认值在 Theme 中设置) | number | no | iOS/Android | yes |
| overlayPointerEvents | 背景触摸事件 (auto, none) | string | no | iOS/Android | yes |
| autoKeyboardInsets | 在弹出键盘时是否自动缩减键盘高度空间 | bool | no | iOS/Android | yes |
| onAppearCompleted | 在浮层显示完毕时调用 | function | no | iOS/Android | yes |
| onDisappearCompleted | 在浮层隐藏完毕后调用 | function | no | iOS/Android | yes |
| onCloseRequest | 浮层关闭请求事件(在点击内容之外的半透明区域时调用,如设置此值 modal 将无效) | function | no | iOS/Android | yes |

<a id="overlay-pullview"></a>
**Overlay.PullView - 拖拉浮层**

- Overlay.PullView 组件继承 **[Overlay.View](#overlay-view)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| side | 抽屉弹出方向 (top, bottom, left, right) | string | no | iOS/Android | yes |
| containerStyle | 抽屉容器样式 | style | no | iOS/Android | yes |
| rootTransform | 浮层弹出时根组件转换动画 (<br/>**none**: 无转换<br/>**translate**: 位移转换, 把根组件往浮层弹出方向移动<br/>**scale**: 缩小转换, 缩小倍数在 Theme 中定义<br/>**Transform** 目前支持 translateX 、 translateY 、 scaleX 、 scaleY, 类型定义：<br/>type Transform {<br/>&ensp;&ensp;translateX: number,<br/>&ensp;&ensp;translateY: number,<br/>&ensp;&ensp;scaleX: number,<br/>&ensp;&ensp;scaleY: number,<br/>}<br/>) | string/array | no | iOS/Android | yes |
| animated | 是否支持动画效果 (继承自 Overlay.View 并修改默认属性) | style | no | iOS/Android | yes |

**Overlay.PopView - 弹出浮层**

- Overlay.PopView 组件继承 **[Overlay.View](#overlay-view)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 弹出效果。(<br/>**zoomOut**: 缩小, 弹出框放大后动画过度到原大<br/>**zoomIn**: 放大, 弹出框缩小后动画过度到原大<br/>**custom**: 自定义, 弹出框从 customBounds 位置和大小动画过度到原大) | string | no | iOS/Android | yes |
| containerStyle | 弹出框容器样式 | style | no | iOS/Android | yes |
| customBounds | 弹出框动画过度起始位置和大小 (type = 'custom' 时有效。<br/>type Rect {<br/>&ensp;&ensp;x: number,<br/>&ensp;&ensp;y: number,<br/>&ensp;&ensp;width: number,<br/>&ensp;&ensp;height: number,<br/>}) | object | no | iOS/Android | yes |
| animated | 是否支持动画效果 (继承自 Overlay.View 并修改默认属性) | style | no | iOS/Android | yes |

<a id="overlay-popoverview"></a>
**Overlay.PopoverView - 气泡浮层**

Overlay.PopoverView 组件继承 **[Overlay.View](#overlay-view)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| popoverStyle | 气泡样式 | style | no | iOS/Android | yes |
| fromBounds | 弹出气泡源组件 bounds, 气泡箭头将指向这个组件。<br/>type Rect {<br/>&ensp;&ensp;x: number,<br/>&ensp;&ensp;y: number,<br/>&ensp;&ensp;width: number,<br/>&ensp;&ensp;height: number,<br/>} | object | yes | iOS/Android | yes |
| direction | 箭头方向 (up, down, left, right) | string | no | iOS/Android | yes |
| autoDirection | 是否自动调整弹出方向 (为 true 时, 如弹出方向屏幕空间不足则往反方向弹出, 例如 direction = 'down' 时, 如 fromBounds 下方的空间不足则往上方弹出。)  | bool | no | iOS/Android | yes |
| directionInsets | 气泡与弹出组件 fromBounds 之间的距离 | number | no | iOS/Android | yes |
| align | 气泡与弹出组件 fromBounds 的对齐方式。(<br/>**start**: 起始位置对齐, 上边或左边<br/>**center**: 居中对齐<br/>**end**: 起始位置对齐, 下边或右边) | string | no | iOS/Android | yes |
| alignInsets | 对齐方向偏移量 | number | no | iOS/Android | yes |
| showArrow | 是否显示气泡箭头 | bool | no | iOS/Android | yes |
| paddingCorner | 箭头与对齐角的距离 (默认值在 Theme 中设置) | number | no | iOS/Android | yes |
| overlayOpacity | 气泡不透明度 (继承自 Overlay.View 并修改默认值) | number | no | iOS/Android | yes |

### 22. Toast - 轻提示

Toast 为轻提示静态类, 与 Android 的 Toast 作用类似。  
Toast 基于 [Overlay](#overlay){} 实现。

- Toast 继承 **[Overlay](#overlay)** 的全部静态方法。

**静态方法：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 	显示一个轻提示, 重写 Overlay{} 中的同名函数, 输入参数 options 为 duration 与 [ToastView](#toasttoastview--props) 的属性合集, 返回唯一的浮层 key 值。<br/>**一般不直接调用此函数** | function | no | iOS/Android | yes |
| message | 显示一个纯文本轻提示框。(<br/>duration 默认为 'short', position 默认为 'bottom' 。<br/>默认值可通过 Toast.messageDefaultDuration 、 Toast.messageDefaultPosition 修改) | function | no | iOS/Android | yes |
| success | 显示一个成功轻提示框, 提示框中有一个打勾图标。(<br/>duration 默认为 'short', position 默认为 'center' 。<br/>默认值可通过 Toast.defaultDuration 、 Toast.defaultPosition 修改)<br/>**下同** | function | no | iOS/Android | yes |
| fail | 显示一个失败轻提示框, 提示框中有一个打叉图标 | function | no | iOS/Android | yes |
| smile | 显示一个笑脸轻提示框, 提示框中有一个笑脸表情图标 | function | no | iOS/Android | yes |
| sad | 显示一个难过轻提示框, 提示框中有一个难过表情图标 | function | no | iOS/Android | yes |
| info | 显示一个信息轻提示框, 提示框中有一个 Info 图标 | function | no | iOS/Android | yes |
| stop | 显示一个停止轻提示框, 提示框中有一个图标 | function | no | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|ToastView| Toast 内容显示组件 | class | yes | iOS/Android | yes |
| defaultDuration | success, fail, smile, sad, info, stop 函数的 duration 参数默认值, 轻提示框显示时长。(<br/>**short**: 2000 毫秒<br/>**long**: 3500毫秒) | string | no | iOS/Android | yes |
| defaultPosition | success, fail, smile, sad, info, stop 函数的 position 参数默认值, 轻提示框显示位置 (参见 [Toast.ToastView](#toasttoastview--props)) | string | no | iOS/Android | yes |
| messageDefaultDuration | message 函数的 duration 参数默认值 | string | no | iOS/Android | yes |
| messageDefaultPosition | message 函数的 position 参数默认值 | string | no | iOS/Android | yes |

<a id="toasttoastview--props"></a>
**Toast.ToastView**

- Toast.ToastView 组件继承 **[View](https://reactnative.dev/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | 轻提示文本 | string/number/element | no | iOS/Android | yes |
| icon | 	图标 (<br/>**none**: 无图标<br/>**success**: 成功, 打勾图标<br/>**fail**: 失败, 打叉图标<br/>**smile**: 笑脸表情图标<br/>**sad**: 难过表情图标<br/>**info**: 信息, 圆圈里一个字母 "i"<br/>**stop**: 停止, 圆圈里一个感叹号 "!")| string/ImageSource/element | no | iOS/Android | yes |
| position | 轻提示框显示位置 (<br/>**top**: 窗口靠上位置<br/>**bottom**: 窗口靠下位置<br/>**center**: 窗口中间位置<br/>top 、 bottom 位置可在 Theme 中设置) | string | no | iOS/Android | yes |

### 23. ActionSheet - 操作选单

ActionSheet 为操作选单静态类, 一般用于触发一个多项子操作供用户选择, 表现形式为从屏幕下方拖出抽屉。  
ActionSheet 基于 [Overlay](#overlay){} 实现。

**静态方法：**

- ActionSheet 继承 **[Overlay](#overlay)** 的全部静态方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 显示一个操作选单, 重写 Overlay{} 中的同名函数, 输入参数 items 为操作选单项列表, cancelItem(可空)为取消操作项, options(可空)为 ActionSheet.ActionSheetView 其它属性, 参数类型参见 [ActionSheetView](#actionsheetactionsheetview--props)。<br/>返回唯一的浮层 key 值。 | function | yes | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActionSheetView| ActionSheet 内容显示组件 | class | no | iOS/Android | yes |

<a id="actionsheetactionsheetview--props"></a>
**ActionSheet.ActionSheetView**

- ActionSheet.ActionSheetView 组件继承 **[Overlay.PullView](#overlay-pullview)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | 操作选单项列表 (数组元素类型为:<br/>type ActionSheetItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;onPress: func,<br/>&ensp;&ensp;disabled: bool,<br/>}) | array | yes | iOS/Android | yes |
| cancelItem | 取消操作项 (<br/>type ActionSheetItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;onPress: func,<br/>&ensp;&ensp;disabled: bool,<br/>}) | object | no | iOS/Android | yes |

**ActionSheet.ActionSheetView 静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item| ActionSheet 操作选单项显示组件 | class | no | iOS/Android | yes |

**ActionSheet.ActionSheetView.Item**

- ActionSheet.ActionSheetView.Item 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)**  组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | 类型 | string | no | iOS/Android | yes |
| title | 标题 | string/number/element | yes | iOS/Android | yes |
| topSeparator | 上分隔线(none, full, indent) (缩进分隔线仅左侧缩进)  | string/element | no | iOS/Android | yes |
| bottomSeparator | 下分隔线(none, full, indent) (缩进分隔线仅左侧缩进)  | string/element | no | iOS/Android | yes |
| disabled | 是否禁用 (继承自 TouchableOpacity, 为 true 时组件显示为半透明且不可触摸) | bool | no | iOS/Android | yes |

### 24. ActionPopover - 操作气泡

ActionPopover 为操作气泡静态类, 一般用于触发一个多项子操作供用户选择, 表现形式为从触发源组件弹出的气泡。  
ActionPopover 基于 [Overlay](#overlay){} 实现。

**静态方法：**

- ActionPopover 继承 **[Overlay](#overlay)** 的全部静态方法

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 显示一个操作气泡, 重写 Overlay{} 中的同名函数, 输入参数 fromBounds 为弹出气泡源组件 bounds, items 为操作项列表, options(可空)为 ActionPopover.ActionPopoverView 其它属性, 参数类型参见 [ActionPopoverView](#actionpopoveractionpopoverview--props)。<br/>返回唯一的浮层 key 值。 | function | yes | iOS/Android | yes |

**静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActionPopoverView	 | ActionPopover 内容显示组件 | class | yes | iOS/Android | yes |

<a id="actionpopoveractionpopoverview--props"></a>
**ActionPopover.ActionPopoverView**

- ActionPopover.ActionPopoverView 组件继承 **[Overlay.PopoverView](#overlay-popoverview)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | 操作项列表 (数组元素类型为:<br/>type ActionPopoverItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;onPress: func,<br/>}) | array | yes | iOS/Android | yes |
| direction | 气泡方向 (up, down, left, right) (继承自 Overlay.PopoverView 并修改默认值) | string | no | iOS/Android | yes |
| align | 对齐方式 (start, center, end) (继承自 Overlay.PopoverView 并修改默认值) | string | no | iOS/Android | yes |
| showArrow | 是否显示箭头 (继承自 Overlay.PopoverView 并修改默认值) | bool | no | iOS/Android | yes |

**ActionPopover.ActionPopoverView 静态属性**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | ActionPopover 操作项显示组件 | class | yes | iOS/Android | yes |

**ActionPopover.ActionPopoverView.Item属性：**

- ActionPopover.ActionPopoverView.Item 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 项标题 | string/number/element | yes | iOS/Android | yes |
| leftSeparator | 是否显示左分隔线 | bool | no | iOS/Android | yes |
| rightSeparator | 是否显示右分隔线 | bool | no | iOS/Android | yes |

### 25. PullPicker - 上拉选择器

PullPicker 为上拉选择器静态类, 一般用于触发显示一个数据列表供用户选择, 表现形式为从屏幕下方拖出抽屉。  
PullPicker 基于 [Overlay](#overlay){} 实现。

**静态方法:**

- PullPicker 继承 **[Overlay](#overlay)** 的全部静态方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 显示一个上拉选择器, 重写 Overlay{} 中的同名函数, 输入参数 title 为列表标题, items 为可选项列表, selectedIndex 为已选项编号, onSelected 为选择某项时的回调函数, options(可空)为 PullPicker.PullPickerView 其它属性, 参数类型参见 [PullPickerView](#pullpickerpullpickerview--props)。<br/>返回唯一的浮层 key 值。 | function | yes | iOS/Android | yes |

**静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| PullPickerView | PullPicker 内容显示组件 | class | yes | iOS/Android | yes |

<a id="pullpickerpullpickerview--props"></a>
**PullPicker.PullPickerView**

- PullPicker.PullPickerView 组件继承 **[Overlay.PullView](#overlay-pullview)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 列表标题 | string | no | iOS/Android | yes |
| items | 可选项列表 | array | yes | iOS/Android | yes |
| selectedIndex | 当前已选择项编号 | 	number | no | iOS/Android | yes |
| getItemText | 取 items 数组元素的显示文本, 传入参数为(item, index), item = items[index], 默认直接使用 item | function | no | iOS/Android | yes |
| onSelected | 当选择器选择 items 数组某项时调用, item = items[index] | function | no | iOS/Android | yes |

**PullPicker.PullPickerView静态属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| item | PullPicker 可选项显示组件 | class | no | iOS/Android | yes |

**PullPicker.PullPickerView.Item属性**

- PullPicker.PullPickerView.Item 组件继承 **[ListRow](#listrow)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| selected | 	是否已选中 | bool | no | iOS/Android | yes |

### 26. PopoverPicker - 气泡选择器

PopoverPicker 为气泡选择器静态类, 一般用于触发显示一个数据列表供用户选择, 表现形式为从触发源组件弹出的气泡。  
PopoverPicker 基于 [Overlay](#overlay){} 实现。

**静态方法:**

- PopoverPicker 继承 **[Overlay](#overlay)** 的全部静态方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 显示一个气泡选择器, 重写 Overlay{} 中的同名函数, 输入参数 fromBounds 为弹出气泡源组件 bounds, items 为可选项列表, selectedIndex 为已选项编号, onSelected 为选择某项时的回调函数, options(可空)为 PopoverPicker.PopoverPickerView 其它属性, 参数类型参见 [PopoverPickerView](#popoverpickerpopoverpickerview--props)。<br/>返回唯一的浮层 key 值 | function | yes | iOS/Android | yes |

**静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| PopoverPickerView | PopoverPicker 内容显示组件 | class | yes | iOS/Android | yes |

<a id="popoverpickerpopoverpickerview--props"></a>
**PopoverPicker.PopoverPickerView属性**

- PopoverPicker.PopoverPickerView 组件继承 **[Overlay.PopoverView](#overlay-popoverview)** 组件的全部属性和事件。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | 选项数组 | array | yes | iOS/Android | yes |
| selectedIndex | 当前已选择项编号 | number | no | iOS/Android | yes |
| getItemText |取 items 数组元素的显示文本, 传入参数为(item, index), item = items[index], 默认直接使用 item | function | no | iOS/Android | yes |
| shadow | 是否显示阴影 | bool | no | iOS | yes |
| direction | 箭头方向 (up, down, left, right) (继承自 Overlay.PopoverView 并修改默认值) | string | no | iOS/Android | yes |
| align | 对齐方式 (start, center, end) (继承自 Overlay.PopoverView 并修改默认值) | string | no | iOS/Android | yes |
| showArrow | 是否显示箭头 (继承自 Overlay.PopoverView 并修改默认值) | bool | no | iOS/Android | yes |
| onSelected | 当选择器选择 items 数组某项时调用, item = items[index] | function | no | iOS/Android | yes |

**PopoverPicker.PopoverPickerView静态属性**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | PopoverPicker 可选项显示组件 | class | no | iOS/Android | yes |

**PopoverPicker.PopoverPickerView.Item属性**

- PopoverPicker.PopoverPickerView.Item 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 标题 | string/number/element | no | iOS/Android | yes |
| selected | 是否已选中 | bool | no | iOS/Android | yes |

### 27. Menu - 菜单

Menu 为菜单静态类, 用于触发显示一个弹出菜单供用户选择, 表现形式为从触发源组件弹出的气泡。  
Menu 基于 [Overlay](#overlay){} 实现。

**静态方法:**

- Menu 继承 **[Overlay](#overlay)** 的全部静态方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 显示一个弹出菜单, 重写 Overlay{} 中的同名函数, 输入参数 fromBounds 为弹出菜单源组件 bounds, items 为菜单项列表, options(可空)为 Menu.MenuView 其它属性, 参数类型参见 [MenuView](#menumenuview--props)。<br/>返回唯一的浮层 key 值 | function | yes | iOS/Android | yes |

**静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| MenuView | Menu 内容显示组件 | class | no | iOS/Android | yes |

<a id="menumenuview--props"></a>
**Menu.MenuView属性：**

- Menu.MenuView 组件继承 **[Overlay.PopoverView](#overlay-popoverview)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | 菜单项列表 (数组元素类型为: <br/>type MenuViewItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;icon: any,<br/>&ensp;&ensp;onPress: func,<br/>}<br/>icon 详细类型参见[Menu.MenuView.Item](#menumenuviewitem--props) )| array | no | iOS/Android | yes |
| shadow | 是否显示阴影 | bool | no | iOS | yes |
| direction | 箭头方向 (up, down, left, right) (继承自 Overlay.PopoverView 并修改默认值)| string | no | iOS/Android | yes |
| align | 对齐方式 (start, center, end) (继承自 Overlay.PopoverView 并修改默认值)| string | no | iOS/Android | yes |
| showArrow | 是否显示箭头 (继承自 Overlay.PopoverView 并修改默认值)| bool | no | iOS/Android | yes |

**Menu.MenuView静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item| Menu 菜单项显示组件 | class | no | iOS/Android | yes |

<a id="menumenuviewitem--props"></a>
**Menu.MenuView.Item属性:**

- Menu.MenuView.Item 组件继承 **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 项标题 | string/number/element | no | iOS/Android | yes |
| icon | 图标 (<br/>**none**: 无图标<br/>**empty**: 空图标, 显示为空白并占用图标显示大小的空间) | string/element/ImageSource | no | iOS/Android | yes |

### 28. Drawer - 抽屉

Drawer 为抽屉静态类, 内部视图为 [Overlay.PullView](#overlay-pullview) 的易用性简单封装。  
Drawer 基于 [Overlay](#overlay){} 实现。

**静态方法:**

- Drawer 继承 **[Overlay](#overlay)** 的全部静态方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| open | 打开一个抽屉。 参数说明：<br/>**view**: 抽屉内部视图内容<br/>**side**: 抽屉拉出边, 默认为 'left'<br/>**rootTransform**: 根组件转换动画, 默认为 'none'<br/>**options**: Drawer.DrawerView 其它属性, 参数类型参见 [DrawerView](#drawerdrawerview--props)<br/>返回值为一个对象, 对象属性说明：<br>**key**: 浮层唯一键值<br/>**close**: 关上抽屉函数, 调用该函数将关上抽屉 | function | yes | iOS/Android | yes |

**静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| DrawerView | Drawer 内容显示组件 | class | no | iOS/Android | yes |

<a id="drawerdrawerview--props"></a>
**Drawer.DrawerView属性**

- Drawer.DrawerView 组件继承 **[Overlay.PullView](#overlay-pullview)** 组件的全部属性和事件。

### 29. ModalIndicator - 模态指示器

ModalIndicator 为模态指示器静态类, 一般在需要阻止用户操作时使用, 比如提交数据等, 表现形式为一个覆盖全屏的模态指示器。  
ModalIndicator 基于 **[Overlay](#overlay)** 实现。

**静态方法:**

- ModalIndicator 继承 **[Overlay](#overlay)** 的全部静态方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | 弹出模态指示器, 重写 Overlay{} 中的同名函数, 输入参数 text 为模态指示器下显示的文本，如调用此函数前已显示模态指示器则仅更换文本。 | function | yes | iOS/Android | yes |
| hide | 隐藏指示器 | function | yes | iOS/Android | yes |

**静态属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| IndicatorView | ModalIndicator 内容显示组件 | class | no | iOS/Android | yes |

**ModalIndicator.IndicatorView参数：**

-	ModalIndicator.IndicatorView 组件继承 **[View](https://facebook.github.io/react-native/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | 提示文本 | string/number/element | no | iOS/Android | yes |
| position | 显示位置 | 模态指示器显示位置。<br/>**top**: 窗口靠上位置<br/>**bottom**: 窗口靠下位置<br/>**center**: 窗口中间位置<br/>top 、 bottom 位置可在 Theme 中设置。 | no | iOS/Android | yes |
| size | 指示器大小 | string | no | iOS/Android | yes |
| color | 指示器颜色 (默认值在 Theme 中设置) | string | no | iOS/Android | yes |

### 30. TeaNavigator - Tea导航器

应用根导航器组件。

**属性:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| rootView | 根组件 | element | yes | iOS/Android | yes |

**上下文：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| navigator | 返回 navigator 组件 | function | yes | iOS/Android | yes |

### 31. BasePage - 基础页面

BasePage 定义一个基础页面组件, 是 Page 的抽象封装, 需要派生出新的类来使用, 提供一系列易于使用的可重写方法。

- BasePage 组件继承 **[View](https://facebook.github.io/react-native/docs/view.html)** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scene | 转场效果 | object | no | iOS/Android | yes |
| autoKeyboardInsets | 在弹出键盘时是否自动插入键盘占用空间, 插入键盘占用空间的目的是避免页面内容被键盘遮挡。 | bool | no | iOS/Android | yes |
| keyboardTopInsets | 键盘顶部偏移 | number | no | iOS/Android | yes |

对于 **autoKeyboardInsets** 属性，**HarmonyOS的软键盘默认避让输入框**，如果需要关闭系统默认的软键盘避让可以参考[软键盘布局适配](https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-keyboard-layout-adapt#section19987195213425)或者以下步骤：

- 在“harmony/entry/src/main/ets/pages/Index.ets”中添加以下配置
```diff
...
+ import { KeyboardAvoidMode } from '@kit.ArkUI';
...

  aboutToAppear() {
    ...
+   this.getUIContext().setKeyboardAvoidMode(KeyboardAvoidMode.NONE);
    ...
  }
```

**变量：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| navigator | 导航器对象 (只读属性变量) | object | yes | iOS/Android | yes |
| didMount | 是否已挂载 | bool | yes | iOS/Android | yes |
| isFocused | 是否已聚焦到此页面 | bool | yes | iOS/Android | yes |

**生命周期方法：**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onWillFocus | 将要聚焦到此页面, 在页面转场动画开始前调用。<br/>在派生类中重写此函数执行所需操作。 | function | no | iOS/Android | yes |
| onDidFocus | 已经聚焦到此页面, 在页面转场动画结束后调用。<br/>在派生类中重写此函数执行所需操作。<br/>如果页面初始化有较耗时的操作, 在初始化过程中容易引起页面转场动画卡顿, 建议把复杂的初始化代码放到此函数中处理。 | function | no | iOS/Android | yes |
| onHardwareBackPress | 当用户按下返回键(物理键, Android only)时调用 | function | no | Android | no |
| renderPage | 页面渲染函数, BasePage 所有派生类都应该重写此函数渲染界面, 而不是 render 函数 | function | yes | iOS/Android | yes |

### 32. NavigationPage - 导航页面

NavigationPage 定义一个导航页面组件, 继承自 BasePage, 在 BasePage 的基础上添加一个 NavigationBar 导航条。

- NavigationPage 组件继承 **BasePage** 组件的全部属性。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | 导航栏标题 | string | no | iOS/Android | yes |
| showBackButton | 是否显示返回按钮 | bool | no | iOS/Android | yes |
| navigationBarInsets | 是否为内容区域增加导航条占用空间。(此属性默认为 true, 使得内容不被导航条遮挡, 如果页面内容实用 ScrollView 且需要自行控制 NavigationBar 导航条的显示/隐藏, 那么你需要将此属性设置为 false 并自行在 ScrollView 容器里增加导航条的占用空间, 这样可以在导航条隐藏后把顶部空间利用起来) | bool | no | iOS/Android | yes |
| scene | 转场效果 (继承自 BasePage 并修改默认值) | object | no | iOS/Android | yes |

**方法：**

- NavigationPage 组件继承 **BasePage** 组件的全部方法。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| renderNavigationTitle | 导航条标题渲染函数 | function | no | iOS/Android | yes |
| renderNavigationLeftView | 导航条左按钮渲染函数, 默认根据 this.props.showBackButton 值决定返回值, 为 true 时返回 NavigationBar.BackButton 组件实例, 否则返回 null。<br/>注: 可以通过 Theme 修改返回按钮的默认标题。 | function | no | iOS/Android | yes |
| renderNavigationRightView | 导航条右侧按钮渲染函数 | function | no | iOS/Android | yes |
| renderNavigationBar | 导航条渲染函数 (一般应重写上面三个函数, 而不是此函数) | function | no | iOS/Android | yes |

## 遗留问题


## 其他


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/teaset/blob/master/LICENSE) ，请自由地享受和参与开源。

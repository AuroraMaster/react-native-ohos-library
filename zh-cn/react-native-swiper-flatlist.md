> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-swiper-flatlist</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gusgard/react-native-swiper-flatlist">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="支持的平台" />
    </a>
    <a href="https://github.com/gusgard/react-native-swiper-flatlist/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="许可证" />
    </a>
</p>

> [!提示] [GitHub 地址](https://github.com/gusgard/react-native-swiper-flatlist)

## 安装与使用

进入项目目录并执行以下指令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-swiper-flatlist@3.2.5
```

#### **yarn**

```bash
yarn add react-native-swiper-flatlist@3.2.5
```

<!-- tabs:end -->

### 示例

下面的代码演示了这个库的一个用例：

> [!警告] 该库在使用时，其导入名称保持不变。

```javascript
import React from 'react';
import { Text, Dimensions, StyleSheet, View } from 'react-native';
import { SwiperFlatList } from 'react-native-swiper-flatlist';

const colors = ['tomato', 'thistle', 'skyblue', 'teal'];

const App = () => (
  <View style={styles.container}>
    <SwiperFlatList
      autoplay
      autoplayDelay={2}
      autoplayLoop
      index={2}
      showPagination
      data={colors}
      renderItem={({ item }) => (
        <View style={[styles.child, { backgroundColor: item }]}>
          <Text style={styles.text}>{item}</Text>
        </View>
      )}
    />
  </View>
);

const { width } = Dimensions.get('window');
const styles = StyleSheet.create({
    container: { backgroundColor: 'white', height: height * 0.7 },
    child: { width, justifyContent: 'center', height: height * 0.5 },
    text: { fontSize: width * 0.5, textAlign: 'center' },
});

export default App;
```
## 链接

该库的 HarmonyOS 端实现依赖于 @react-native-oh-tpl/react-native-safe-area-context 和 @react-native-oh-tpl/react-native-gesture-handler 的原生代码。如果您的 HarmonyOS 项目中已经引入了这些库，则无需重新引入。您可以跳过本节中的步骤，直接进入使用环节。

如果您尚未引入 react-native-safe-area-context，请参考 [@react-native-oh-tpl/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md) 进行安装。

如果您尚未引入 react-native-gesture-handler，请参考 [@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md) 进行安装。

## 兼容性

本文档基于以下版本验证：

react-native-harmony：0.72.86；SDK：HarmonyOS 5.1.0.125；IDE：DevEco Studio 5.1.0.849；ROM：5.0.0.150；

react-native-harmony：0.77.18；SDK：HarmonyOS 5.1.0.125；IDE：DevEco Studio 5.1.0.849；ROM：5.0.0.150；

## 属性

> [!提示] "平台" 列表示原始第三方库支持的平台。

> [!提示] 在 "HarmonyOS 支持" 列中，`是` 表示该属性在 HarmonyOS 平台上受支持，`否` 表示不支持，`部分` 表示部分支持。其用法在各平台间保持一致，效果旨在与 iOS 或 Android 的实现相匹配。

### SwiperFlatList 属性

| 名称 | 描述 | 类型 | 必填 | 平台 | HarmonyOS 支持 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | 用于 renderItem 的数据 | 数组 | 否 | 全平台 | 是 |
| `children` | 子元素 | 节点 | 否 | 全平台 | 是 |
| `renderItem` | 从 data 中取出一个项目并将其渲染到列表中 | FlatListProps<T>[renderItem] | 否 | 全平台 | 是 |
| `onMomentumScrollEnd` | 滚动结束后调用，第一个参数是当前索引 | (item: { index: number }, event: any) => void | 否 | 全平台 | 是 |
| `vertical` | 显示垂直轮播 | 布尔值 | 否 | 全平台 | 是 |
| `index` | 起始索引 | 数字 | 否 | 全平台 | 是 |
| `renderAll` | 渲染所有项目 | 布尔值 | 否 | 全平台 | 是 |
| `showPagination` | 显示分页指示器 | 布尔值 | 否 | 全平台 | 是 |
| `onChangeIndex` | 每次索引改变时执行，当用户到达下一个屏幕的 60% 时索引改变 | ({ index: number, prevIndex: number}) => void | 否 | 全平台 | 是 |
| `PaginationComponent` | 覆写分页组件 | 节点 | 否 | 全平台 | 是 |
| `onViewableItemsChanged` | RN 中原生可见项发生变化 | FlatListProps<T>['onViewableItemsChanged'] | 否 | 全平台 | 是 |
| `autoplay` | 自动改变索引 | 布尔值 | 否 | 全平台 | 是 |
| `autoplayDelay` | 每页之间的延迟（秒） | 数字 | 否 | 全平台 | 是 |
| `autoplayLoop` | 到达末尾后继续播放 | 布尔值 | 否 | 全平台 | 是 |
| `autoplayLoopKeepAnimation` | 到达列表末尾时显示动画 | 布尔值 | 否 | 全平台 | 是 |
| `autoplayInvertDirection` | 反转自动播放方向 | 布尔值 | 否 | 全平台 | 是 |
| `disableGesture` | 禁用滑动手势 | 布尔值 | 否 | 全平台 | 是 |
| `e2eID` | 用于自动化测试的 TestID | 字符串 | 否 | 全平台 | 是 |
| `viewabilityConfig` | 可见性配置 | ViewabilityConfig | 否 | 全平台 | 是 |
| `useReactNativeGestureHandler` | 使用 react-native-gesture-handler 的 FlatList 代替原生 FlatList | 布尔值 | 否 | 全平台 | 是 |
| `paginationAccessibilityLabels` | 分页项目的无障碍标签。此为可选，用于屏幕阅读器。 | 字符串数组 | 否 | 全平台 | 否 |

### Pagination 属性

| 名称 | 描述 | 类型 | 必填 | 平台 | HarmonyOS 支持 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `paginationDefaultColor` | 分页默认颜色 | 字符串 | 否 | 全平台 | 是 |
| `paginationActiveColor` | 分页激活状态颜色 | 字符串 | 否 | 全平台 | 是 |
| `paginationStyle` | 容器的样式对象 | ViewStyle | 否 | 全平台 | 是 |
| `paginationStyleItem` | 分页项的样式对象 | ViewStyle | 否 | 全平台 | 是 |
| `paginationStyleItemActive` | 激活状态分页项的样式对象 | ViewStyle | 否 | 全平台 | 是 |
| `paginationStyleItemInactive` | 非激活状态分页项的样式对象 | ViewStyle | 否 | 全平台 | 是 |
| `onPaginationSelectedIndex` | 当用户按下分页索引时执行，类似于 onChangeIndex 属性 | () => void | 否 | 全平台 | 是 |
| `size` | 分页指示器大小 | 数字 | 是 | 全平台 | 是 |
| `paginationIndex` | 选中的分页索引 | 数字 | 否 | 全平台 | 是 |
| `e2eID` | 用于自动化测试的 TestID | 字符串 | 否 | 全平台 | 是 |
| `paginationAccessibilityLabels` | 分页项目的无障碍标签。此为可选，用于屏幕阅读器。 | 字符串数组 | 否 | 全平台 | 否 |
| `paginationTapDisabled` | 防止点击分页点 | 布尔值 | 否 | 全平台 | 是 |

### SwiperFlatList 函数

| 名称 | 描述 | 类型 | 必填 | 平台 | HarmonyOS 支持 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `scrollToIndex` | 滚动到指定索引 | ({ item: ScrollToIndex}) => void | 否 | 全平台 | 是 |
| `getCurrentIndex` | 返回当前索引 | () => number | 否 | 全平台 | 是 |
| `getPrevIndex` | 返回上一个索引 | () => number | 否 | 全平台 | 是 |
| `goToFirstIndex` | 跳转到第一个索引 | () => void | 否 | 全平台 | 是 |
| `goToLastIndex` | 跳转到最后一个索引 | () => void | 否 | 全平台 | 是 |

### Pagination 函数

| 名称 | 描述 | 类型 | 必填 | 平台 | HarmonyOS 支持 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `scrollToIndex` | 滚动到指定索引 | ({ index: number}) => void | 是 | 全平台 | 是 |

## 遗留问题

## 其他

paginationAccessibilityLabels: 原生平台测试无效果

## 许可证

此项目根据 [The MIT License (MIT)](https://github.com/gusgard/react-native-swiper-flatlist/blob/master/LICENSE) 许可证授权。
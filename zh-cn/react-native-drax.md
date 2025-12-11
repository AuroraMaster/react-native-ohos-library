> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drax</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nuclearpasta/react-native-drax">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/nuclearpasta/react-native-drax/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-drax)

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                             | Repository                                                   | Release                                                      | Version for RN |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 0.10.3 | @react-native-oh-tpl/react-native-drax  | [Github](https://github.com/react-native-oh-library/react-native-drax) | [Github Releases](https://github.com/react-native-oh-library/react-native-drax/releases) | 0.72       |
| 0.11.1                        | @react-native-ohos/react-native-drax | [Github](https://github.com/react-native-oh-library/react-native-drax/tree/br_rnoh0.77) | [Github Releases](https://github.com/react-native-oh-library/react-native-drax/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# for RN0.72
npm install @react-native-oh-tpl/react-native-drax

# for RN0.77
npm install @react-native-ohos/react-native-drax
```

#### **yarn**

```bash
# for RN0.72
yarn add @react-native-oh-tpl/react-native-drax

# for RN0.77
yarn add @react-native-ohos/react-native-drax
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { View, StyleSheet } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import { DraxProvider, DraxView } from 'react-native-drax';


export const GestureHandleExample = () => {
  const viewPropsExtractor = (data: any) => {
    return {
      style: {
        backgroundColor: data.isDragging ? 'lightblue' : 'white',
      },
    };
  };
  return (
    <DraxProvider>
      <GestureHandlerRootView>
        <View style={styles.container}>
          <DraxView
            style={styles.draggable}
            onDragStart={() => {
              console.log('start drag');
            }}
            payload="world"
          />
          <DraxView
            style={styles.receiver}
            onReceiveDragEnter={({ dragged: { payload } }) => {
              console.log(`hello ${payload}`);
            }}
            onReceiveDragExit={({ dragged: { payload } }) => {
              console.log(`goodbye ${payload}`);
            }}
            onReceiveDragDrop={({ dragged: { payload } }) => {
              console.log(`received ${payload}`);
            }}
          />
        </View>
      </GestureHandlerRootView>
    </DraxProvider>
  );
};

const styles = StyleSheet.create({
  box: {
    width: 100,
    height: 100,
    backgroundColor: 'blue',
    marginTop: 100,
    marginLeft: 100
  },
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    width: '100%',
    height: 800,
    paddingTop: 500
  },
  draggable: {
    width: 100,
    height: 100,
    backgroundColor: 'blue',
  },
  receiver: {
    width: 100,
    height: 100,
    backgroundColor: 'green',
  },
});
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler 的原生端代码，如已在鸿蒙工程中引入过这个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-gesture-handler.md)  进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### DraxView

|               Name                |                         Description                          |     Type      | Required |  Platform   | HarmonyOS Support |
| :-------------------------------: | :----------------------------------------------------------: | :-----------: | :------: | :---------: | :---------------: |
|            onDragStart            | 拖拽开始时的回调函数          |   function    |    no    | iOS/Android |        Yes        |
|              onDrag               | 拖拽过程中的回调函数               |   function    |    no    | iOS/Android |        Yes        |
|            onDragEnter            | 拖拽进入时的回调函数           |   function    |    no    | iOS/Android |        Yes        |
|            onDragOver             | 在浮动视图上方拖拽时的回调函数       |   function    |    no    | iOS/Android |        Yes        |
|            onDragExit             | 拖拽退出时的回调函数             |   function    |    no    | iOS/Android |        Yes        |
|             onDragEnd             | 拖拽结束时的回调函数           |   function    |    no    | iOS/Android |        Yes        |
|            onDragDrop             | 拖拽释放时的回调函数         |   function    |    no    | iOS/Android |        Yes        |
|           onSnapbackEnd           | 回弹动画结束时的回调函数     |   function    |    no    | iOS/Android |        Yes        |
|        onReceiveDragEnter         | 接收拖拽进入时的回调函数           |   function    |    no    | iOS/Android |        Yes        |
|         onReceiveDragOver         | 接收拖拽悬停时的回调函数         |   function    |    no    | iOS/Android |        Yes        |
|         onReceiveDragExit         | 接收拖拽退出时的回调函数             |   function    |    no    | iOS/Android |        Yes        |
|         onReceiveDragDrop         | 接收拖拽释放时的回调函数         |   function    |    no    | iOS/Android |        Yes        |
|        onMonitorDragStart         | 监测到拖拽开始时的回调函数    |   function    |    no    | iOS/Android |        Yes        |
|        onMonitorDragEnter         | 监测到拖拽进入时的回调函数        |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragOver         | 监测到拖拽进行时的回调函数          |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragExit         | 监测到拖拽退出时的回调函数        |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragEnd          | 监测到拖拽结束时的回调函数    |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragDrop         | 监测到拖拽释放后的回调函数      |   function    |    no    | iOS/Android |        Yes        |
|          animateSnap          | 是否在拖拽释放后为悬停视图快照添加回弹动画 |    boolean    |    no    | iOS/Android |        Yes        |
|              payload              | 拖拽时传递的数据                   |      any      |    no    | iOS/Android |        Yes        |
|            dragPayload            | 拖拽方传输的数据              |      any      |    no    | iOS/Android |        Yes        |
|          receiverPayload          | 接收方传输的数据               |      any      |    no    | iOS/Android |        Yes        |
|         dragInactiveStyle         | 拖拽前拖拽方的样式            |    object     |    no    | iOS/Android |        Yes        |
|           draggingStyle           | 拖拽过程中应用于拖拽方的样式      |    object     |    no    | iOS/Android |        Yes        |
|     draggingWithReceiverStyle     | 当拖拽方直接在接收方上方时应用于拖拽方的样式 |    object     |    no    | iOS/Android |        Yes        |
|   draggingWithoutReceiverStyle    | 当拖拽方不在接收方上方时应用于拖拽方的样式 |    object     |    no    | iOS/Android |        Yes        |
|         dragReleasedStyle         | 当拖拽方释放时应用于拖拽方的样式 |    object     |    no    | iOS/Android |        Yes        |
|            hoverStyle             | 当快照悬停时应用于拖拽方快照的样式 |    object     |    no    | iOS/Android |        Yes        |
|        hoverDraggingStyle         | 拖拽时应用于拖拽方快照的样式 |    object     |    no    | iOS/Android |        Yes        |
|  hoverDraggingWithReceiverStyle   | 当拖拽方直接在接收方上方时应用于拖拽方快照的样式 |    object     |    no    | iOS/Android |        Yes        |
| hoverDraggingWithoutReceiverStyle | 当拖拽方不在接收方上方时应用于拖拽方快照的样式 |    object     |    no    | iOS/Android |        Yes        |
|      hoverDragReleasedStyle       | 当拖拽停止时应用于拖拽方快照的样式 |    object     |    no    | iOS/Android |        Yes        |
|       receiverInactiveStyle       |  拖拽开始前应用于接收方的样式   |    object     |    no    | iOS/Android |        Yes        |
|          receivingStyle           | 当拖拽直接在接收方上方时应用于接收方的样式 |    object     |    no    | iOS/Android |        Yes        |
|        otherDraggingStyle         | 其他拖拽方拖拽期间应用于拖拽方的样式      |    object     |    no    | iOS/Android |        Yes        |
|  otherDraggingWithReceiverStyle   | 当其他拖拽方直接在接收方上方时应用于拖拽方的样式 |    object     |    no    | iOS/Android |        Yes        |
| otherDraggingWithoutReceiverStyle | 当其他拖拽方不在接收方上方时应用于拖拽方的样式 |    object     |    no    | iOS/Android |        Yes        |
|           renderContent           | 渲染拖拽组件内部子节点的内容 |   function    |    no    | iOS/Android |        Yes        |
|        renderHoverContent         | 用于渲染拖拽复制组件内部子节点的内容 |   function    |    no    | iOS/Android |        Yes        |
|           registration            | 回调函数，可接收组件内部传输的数据 |   function    |    no    | iOS/Android |        Yes        |
|             onMeasure             | 回调函数，可接收组件内部传输的数据 |   function    |    no    | iOS/Android |        Yes        |
|         lockDragXPosition         | 指示是否在水平方向（x轴）锁定拖拽 |    boolean    |    no    | iOS/Android |        Yes        |
|         lockDragYPosition         | 指示是否在垂直方向（y轴）锁定拖拽 |    boolean    |    no    | iOS/Android |        Yes        |
|             children              | 渲染拖拽组件内部子节点的内容。仅当 renderContent 渲染方法不存在时此参数有效 | React Element |    no    | iOS/Android |        Yes        |
|              noHover              | 设置是否禁用拖拽复制功能    |    boolean    |    no    | iOS/Android |        Yes        |
|          longPressDelay           | 设置视图识别触摸和长按手势的最短时间（以毫秒为单位） |    number     |    no    | iOS/Android |        Yes        |
|             draggable             | 指示是否允许拖拽。默认值为 true |    boolean    |    no    | iOS/Android |        Yes        |

###  DraxScrollView

|   Name   |          Description          |     Type      | Required |  Platform   | HarmonyOS Support |
| :------: | :---------------------------: | :-----------: | :------: | :---------: | :---------------: |
| children | 组件子节点  | React Element |    no    | iOS/Android |        Yes        |
| onScroll | 滑动事件回调函数 |   function    |    no    | iOS/Android |        Yes        |

### DraxList

|                      Name                      |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :--------------------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|                      data                      | DraxList 组件的数据源             |  array   |   yes    | iOS/Android |        Yes        |
|          flatListStyle<sup>废弃</sup>          | 设置内部 FlatList 组件的样式       |  object  |    no    | iOS/Android |        Yes        |
|           itemStyles<sup>废弃</sup>            | 设置内部 FlatList 组件中项目的样式 |  object  |    no    | iOS/Android |        Yes        |
|        renderItemContent<sup>废弃</sup>        | DraxList 组件中项目项的渲染方法   | function |    no    | iOS/Android |        Yes        |
|     renderItemHoverContent<sup>废弃</sup>      | DraxList 组件中项目快照的渲染方法 | function |    no    | iOS/Android |        Yes        |
|       viewPropsExtractor<sup>废弃</sup>        | 可以根据每个项目的数据返回属性     | function |    no    | iOS/Android |        Yes        |
|            onScroll<sup>废弃</sup>             | 滑动事件回调方法                 | function |    no    | iOS/Android |        Yes        |
|         itemsDraggable<sup>废弃</sup>          | 指示 FlatList 组件中的项目是否可以被拖拽 | boolean  |    no    | iOS/Android |        Yes        |
| monitoringExternalDragStyle <sup>0.11.1+</sup> | 在监测外部项目拖拽时应用于父 DraxView 的样式属性 |  object  |    no    | iOS/Android |        Yes        |
|                onItemDragStart                 | 当列表项重新排序拖拽动作开始时的回调处理程序 | function |    no    | iOS/Android |        Yes        |
|            onItemDragPositionChange            | 当列表项位置（索引）在重新排序拖拽期间发生变化时的回调处理程序 | function |    no    | iOS/Android |        Yes        |
|                 onItemDragEnd                  | 当列表项重新排序拖拽动作结束时的回调处理程序 | function |    no    | iOS/Android |        Yes        |
|                 onItemReorder                  | 当列表项在列表内移动，重新排序列表时的回调处理程序 | function |    no    | iOS/Android |        Yes        |
|                  reorderable                   | 列表是否可以通过拖拽项目来重新排序？如果设置了 onItemReorder，则默认为 true | boolean  |    no    | iOS/Android |        Yes        |
|            lockItemDragsToMainAxis             | 如果为 true，将项目拖拽锁定到列表的主轴       | boolean  |    no    | iOS/Android |        Yes        |
|                 longPressDelay                 | 视图在拖拽开始前需要被按压的时间（以毫秒为单位） |  number  |    no    | iOS/Android |        Yes        |
|          renderItem<sup>0.11.1+</sup>          | 渲染 DraxList 中每个项目的函数。这扩展了 React Native 标准的 FlatList renderItem，通过为每个列表项提供拖拽相关的属性来增加 Drax 特定的功能 | function |   yes    | iOS/Android |        Yes        |
|     parentDraxViewProps<sup>0.11.1+</sup>      | 应用于包装 FlatList 的父 DraxView 的属性 |  object  |    no    | iOS/Android |        Yes        |
|         centerShift<sup>0.11.1+</sup>          | 当为 true 时，项目将基于它们的中心而不是边缘进行移动 | boolean  |    no    | iOS/Android |        Yes        |

### DraxListItem<sup>0.11.1+</sup>

|          Name           | Description                                                  |   Type   | Required |  Platform   | HarmonyOS Support |
| :---------------------: | ------------------------------------------------------------ | :------: | :------: | :---------: | :---------------: |
|          index          | 项目在列表中的当前渲染索引                 |  number  |   yes    | iOS/Android |        Yes        |
|          item           | 正在渲染的数据项目                                 |    T     |   yes    | iOS/Android |        Yes        |
|      originalIndex      | 在任何重新排序发生前项目的原始索引 |  number  |   yes    | iOS/Android |        Yes        |
|       horizontal        | 列表是否水平布局                    | boolean  |   yes    | iOS/Android |        Yes        |
| lockItemDragsToMainAxis | 拖拽移动是否被限制在列表的主轴上 | boolean  |   yes    | iOS/Android |        Yes        |
|       draggedItem       | 跟踪当前拖拽项目索引的 Reanimated 共享值 |  object  |   yes    | iOS/Android |        Yes        |
|        shiftsRef        | 在拖拽操作期间跟踪位置偏移的共享值 |  object  |   yes    | iOS/Android |        Yes        |
|   itemMeasurementsRef   | 存储所有列表项目测量值的可变引用           |  object  |   yes    | iOS/Android |        Yes        |
| prevItemMeasurementsRef | 存储列表项目先前测量值的可变引用      |  object  |   yes    | iOS/Android |        Yes        |
|    resetDraggedItem     | 重置拖拽项目状态的函数                     | function |   yes    | iOS/Android |        Yes        |
|      keyExtractor       | 用于从项目中提取唯一键的可选函数          | function |   yes    | iOS/Android |        Yes        |
|    previousShiftsRef    | 跟踪先前位置偏移的共享值               |  object  |   yes    | iOS/Android |        Yes        |
|    registrationsRef     | 存储视图注册数据的可变引用                   |  object  |   yes    | iOS/Android |        Yes        |
|          data           | DraxList 使用的完整数据数组                 |  array   |   yes    | iOS/Android |        Yes        |

## 遗留问题

- [ ] DraxList和DraxScrollView组件存在拖拽不流畅的情况，[issue#1](https://github.com/react-native-oh-library/react-native-drax/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License(MIT)](https://github.com/nuclearpasta/react-native-drax/blob/main/LICENSE.md)，请自由地享受和参与开源。

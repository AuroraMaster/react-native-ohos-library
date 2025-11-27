> 模板版本：v0.2.1  

  <p align="center">  
  <h1 align="center"> <code>react-native-chart-kit</code> </h1>  
  </p >  
  <p align="center">
      <a>
       <a href="https://github.com/indiespirit/react-native-chart-kit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
     <a>
        <a href="https://github.com/indiespirit/react-native-chart-kit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p> 

> [!TIP] 
>
> [Github 地址](https://github.com/indiespirit/react-native-chart-kit)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 6.12.0      | 0.72/0.77      |

<!-- tabs:start -->

进入到工程目录并输入以下命令：

<!-- tabs:start -->

**npm**

```bash
npm install react-native-chart-kit@^6.12.0
```

**yarn**

```bash
yarn add react-native-chart-kit@^6.12.0
```



<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。


```js
import React from 'react';
import { View, Dimensions, StyleSheet } from 'react-native';
import { LineChart } from 'react-native-chart-kit';

const data = {
  labels: ['January', 'February', 'March', 'April', 'May', 'June'],
  datasets: [{
    data: [20, 45, 28, 80, 99, 43]
  }]
};

const MyChart = () => {
  const screenWidth = Dimensions.get('window').width;

  return (
    <View style={styles.container}>
      <LineChart
        data={data}
        width={screenWidth - 20} // Adjust width to fit the screen with some margin
        height={220}
        yAxisLabel={'$'}
        chartConfig={{
          backgroundColor: '#e26a00',
          backgroundGradientFrom: '#fb8c00',
          backgroundGradientTo: '#ffa726',
          decimalPlaces: 2, // Adjust decimal places to 2
          color: (opacity = 1) => `rgba(255, 255, 255, ${opacity})`,
          labelColor: (opacity = 1) => `rgba(255, 255, 255, ${opacity})`,
          style: {
            borderRadius: 16
          },
          propsForDots: {
            r: '6',
            strokeWidth: '2',
            stroke: '#ffa726'
          }
        }}
        bezier
        style={styles.chart}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF'
  },
  chart: {
    marginVertical: 8,
    borderRadius: 16
  }
});

export default MyChart;
```


## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-library/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-library/react-native-svg文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.300SP1; ROM：3.0.0.18;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Chart style 

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `backgroundGradientFrom` | 定义图表背景线性渐变的起始颜色 | String | No | All | Yes |
| `backgroundGradientFromOpacity` | 定义图表背景线性渐变起始颜色的不透明度 | Number | No | All | Yes |
| `backgroundGradientTo` | 定义图表背景线性渐变的结束颜色 | String | No | All | Yes |
| `backgroundGradientToOpacity` | 定义图表背景线性渐变结束颜色的不透明度 | Number | No | All | Yes |
| `fillShadowGradientFrom` | 定义数据下方区域线性渐变的起始颜色 | String | No | All | Yes |
| `fillShadowGradientFromOpacity` | 定义数据下方区域线性渐变起始颜色的不透明度 | Number | No | All | Yes |
| `fillShadowGradientFromOffset` | 定义数据下方区域线性渐变起始颜色的偏移量 (0-1) | Number | No | All | Yes |
| `fillShadowGradientTo` | 定义数据下方区域线性渐变的结束颜色 | String | No | All | Yes |
| `fillShadowGradientToOpacity` | 定义数据下方区域线性渐变结束颜色的不透明度 | Number | No | All | Yes |
| `fillShadowGradientToOffset` | 定义数据下方区域线性渐变结束颜色的偏移量 (0-1) | Number | No | All | Yes |
| `useShadowColorFromDataset` | 定义是否对每个图表数据使用数据集中的颜色的选项。默认为 false | Boolean | No | All | Yes |
| `color` | 定义用于计算图表中标签和扇区颜色的基础颜色函数 | Function => String | No | All | Yes |
| `strokeWidth` | 定义图表中的基础描边宽度 | Number | No | All | Yes |
| `barPercentage` | 定义图表中每个条形宽度占可用宽度的百分比 (0-1) | Number | No | All | Yes |
| `barRadius` | 定义每个条形的圆角半径 | Number | No | All | Yes |
| `propsForBackgroundLines` | 覆盖背景线的样式，参考 react-native-svg 的 Line 文档 | Props | No | All | Yes |
| `propsForLabels` | 覆盖标签的样式，参考 react-native-svg 的 Text 文档 | Props | No | All | Yes |
| `propsForVerticalLabels` | 覆盖垂直标签的样式，参考 react-native-svg 的 Text 文档 | Props | No | All | Yes |
| `propsForHorizontalLabels` | 覆盖水平标签的样式，参考 react-native-svg 的 Text 文档 | Props | No | All | Yes |

### Line Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | 图表数据  | Object | No | All | Yes |
| `width` | 图表的宽度，使用 'Dimensions' 库获取屏幕宽度以实现响应式布局 | Number | No | All | Yes |
| `height` | 图表的高度 | Number | No | All | Yes |
| `withDots` | 在折线上显示点 - 默认值：True | boolean | No | All | Yes |
| `withShadow` | 显示折线阴影 - 默认值：True | boolean | No | All | Yes |
| `withInnerLines` | 显示内部虚线 - 默认值：True | boolean | No | All | Yes |
| `withOuterLines` | 显示外部虚线 - 默认值：True | boolean | No | All | Yes |
| `withVerticalLines` | 显示垂直线 - 默认值：True | boolean | No | All | Yes |
| `withHorizontalLines` | 显示水平线 - 默认值：True | boolean | No | All | Yes |
| `withVerticalLabels` | 显示垂直标签 - 默认值：True | boolean | No | All | Yes |
| `withHorizontalLabels` | 显示水平标签 - 默认值：True | boolean | No | All | Yes |
| `fromZero` | 从 0 开始渲染图表，而不是从最小值开始 - 默认值：False | boolean | No | All | Yes |
| `yAxisLabel` | 在水平标签前添加文本 -- 默认值：'' | string | No | All | Yes |
| `yAxisSuffix` | 在水平标签后添加文本 -- 默认值：'' | string | No | All | Yes |
| `xAxisLabel` | 在垂直标签前添加文本 -- 默认值：'' | string | No | All | Yes |
| `yAxisInterval` | 每隔 {x} 个输入显示一条 Y 轴线 -- 默认值：1 | string | No | All | Yes |
| `chartConfig` | 图表的配置对象 | Object | No | All | Yes |
| `decorator` | 此函数接收大量参数，可用于渲染额外元素，例如数据点信息或其他标记。 | Function | No | All | Yes |
| `onDataPointClick` | 接收 {value, dataset, getColor} 的回调函数 | Function | No | All | Yes |
| `horizontalLabelRotation` | 水平标签的旋转角度 - 默认值 0 | number (degree) | No | All | Yes |
| `verticalLabelRotation` | 垂直标签的旋转角度 - 默认值 0 | number (degree) | No | All | Yes |
| `getDotColor` | 定义用于计算折线图中点颜色的函数，接收 (dataPoint, dataPointIndex) | function => string | No | All | Yes |
| `renderDotContent` | 为点渲染额外内容。接收 ({x, y, index, indexData}) 作为参数。 | Function | No | All | Yes |
| `yLabelsOffset` | Y 轴标签的偏移量 | number | No | All | Yes |
| `xLabelsOffset` | X 轴标签的偏移量 | number | No | All | Yes |
| `hidePointsAtIndex` | 你不想显示的数据点的索引 | number[] | No | All | Yes |
| `formatYLabel` | 此函数更改 Y 轴标签显示值的格式。接收 Y 值作为参数，并应返回所需的字符串。 | Function | No | All | Yes |
| `formatXLabel` | 此函数更改 X 轴标签显示值的格式。接收 X 值作为参数，并应返回所需的字符串。 | Function | No | All | Yes |
| `getDotProps` | 这是 chartConfig 中 propsForDots 的替代方案 | (value, index) => props | No | All | Yes |
| `segments` | 水平线的数量 - 默认值 4 | number | No | All | Yes |

### Bezier Line Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `bezier` | 使折线图平滑弯曲 | boolean | No | All | Yes |

### Progress Ring

| Property | Type | Description | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Object | 图表数据  | No | ALL | YES |
| `width` | Number | 图表的宽度，使用 'Dimensions' 库获取屏幕宽度以实现响应式布局 | No | ALL | YES |
| `height` | Number | 图表的高度 | No | ALL | YES |
| `strokeWidth` | Number | 图表的描边宽度 - 默认值：16 | No | ALL | YES |
| `radius` | Number | 图表的内半径 - 默认值：32 | No | ALL | YES |
| `chartConfig` | Object | 图表的配置对象 | No | ALL | YES |
| `hideLegend` | Boolean | 隐藏图表图例的开关（默认为 false） | No | ALL | YES |

### Bar chart

| Property | Type | Description | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Object | 图表数据  | No | ALL | YES |
| `width` | Number | 图表的宽度，使用 'Dimensions' 库获取屏幕宽度以实现响应式布局 | No | ALL | YES |
| `height` | Number | 图表的高度 | No | ALL | YES |
| `withVerticalLabels` | boolean | 显示垂直标签 - 默认值：True | No | ALL | YES |
| `withHorizontalLabels` | boolean | 显示水平标签 - 默认值：True | No | ALL | YES |
| `fromZero` | boolean | 从 0 开始渲染图表，而不是从最小值开始 - 默认值：False | No | ALL | YES |
| `withInnerLines` | boolean | 显示内部虚线 - 默认值：True | No | ALL | YES |
| `yAxisLabel` | string | 在水平标签前添加文本 -- 默认值：'' | No | ALL | YES |
| `yAxisSuffix` | string | 在水平标签后添加文本 -- 默认值：'' | No | ALL | YES |
| `chartConfig` | Object | 图表的配置对象 | No | ALL | YES |
| `horizontalLabelRotation` | number | 水平标签的旋转角度 - 默认值 0 | No | ALL | YES |
| `verticalLabelRotation` | number | 垂直标签的旋转角度 - 默认值 0 | No | ALL | YES |
| `showBarTops` | boolean | 显示柱顶 | No | ALL | YES |
| `showValuesOnTopOfBars` | boolean | 在柱子上方显示数值 | No | ALL | YES |

### StackedBar chart

| Property | Type | Description | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Object | 图表数据 | No | ALL | YES |
| `width` | Number | 图表的宽度，使用 'Dimensions' 库获取屏幕宽度以实现响应式布局 | No | ALL | YES |
| `height` | Number | 图表的高度 | No | ALL | YES |
| `withVerticalLabels` | boolean | 显示垂直标签 - 默认值：True | No | ALL | YES |
| `withHorizontalLabels` | boolean | 显示水平标签 - 默认值：True | No | ALL | YES |
| `chartConfig` | Object | 图表的配置对象 | No | ALL | YES |
| `barPercentage` | Number | 定义图表中每个条形宽度占可用宽度的百分比 (0-1) | No | ALL | YES |
| `hideLegend` | boolean | 显示图例 - 默认值：True | No | ALL | YES |

### Pie chart

| Property | Type | Description | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Object | 图表数据  | No | ALL | YES |
| `width` | Number | 图表的宽度，使用 'Dimensions' 库获取屏幕宽度以实现响应式布局 | No | ALL | YES |
| `height` | Number | 图表的高度 | No | ALL | YES |
| `chartConfig` | Object | 图表的配置对象 | No | ALL | YES |
| `accessor` | string | 数据对象中用于提取数值的属性 | No | ALL | YES |
| `bgColor` | string | 背景颜色 - 如果想要设置为透明，请输入 transparent 或 none。 | No | ALL | YES |
| `paddingLeft` | string | 饼图的左边距 | No | ALL | YES |
| `center` | array | 用于定位图表的 x 和 y 坐标偏移量 | No | ALL | YES |
| `absolute` | boolean | 以绝对数值显示值 | No | ALL | YES |
| `hasLegend` | boolean | 默认为 true，设置为 false 可移除图例 | No | ALL | YES |
| `avoidFalseZero` | boolean | 默认为 false，设置为 true 可显示 “<1%” 而不是四舍五入等于 “0%” 的值 | No | ALL | YES |
### Contribution graph (heatmap)

| Property | Type | Description | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Object | 图表数据 | No | ALL | YES |
| `width` | Number | 图表的宽度，使用 'Dimensions' 库获取屏幕宽度以实现响应式布局 | No | ALL | YES |
| `height` | Number | 图表的高度 | No | ALL | YES |
| `gutterSize` | Number | 图表中方块之间的间隙大小 | No | ALL | YES |
| `squareSize` | Number | 图表中方块的大小 | No | ALL | YES |
| `horizontal` | boolean | 图表是否应水平布局？默认为 true | No | ALL | YES |
| `showMonthLabels` | boolean | 图表是否应包含月份标签？默认为 true | No | ALL | YES |
| `showOutOfRangeDays` | boolean | 图表是否应填充方块，包括范围之外的日期？默认为 false | No | ALL | YES |
| `chartConfig` | Object | 图表的配置对象 | No | ALL | YES |
| `accessor` | string | 数据对象中用于提取数值的属性；默认为 count | No | ALL | YES |
| `getMonthLabel` | function | 返回每个月标签的函数，接收月份索引 (0 - 11) 作为参数 | No | ALL | YES |
| `onDayPress` | function | 当用户点击图表上的日期方块时调用的回调；接收一个 value-item 对象 | No | ALL | YES |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/indiespirit/react-native-chart-kit/blob/master/LICENSE) ，请自由地享受和参与开源。
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>victory-native-xl</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/FormidableLabs/victory-native-xl">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/victory-native-xl)

| 三方库版本 |   包 名  |   仓库地址  | 发布信息 | 支持RN版本 |
| -------- | -------- | --------- |---------|----------|
| 41.1.0  | @react-native-oh-tpl/victory-native-xl | [Github](https://github.com/react-native-oh-library/victory-native-xl)| [Github Releases](https://github.com/react-native-oh-library/victory-native-xl/releases) | 0.72       | 
| 41.17.5   | @react-native-ohos/victory-native-xl | [Github](https://github.com/react-native-oh-library/victory-native-xl)| [Github Releases](https://github.com/react-native-oh-library/victory-native-xl/releases)  | 0.77       |


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
# V41.1.0
npm install @react-native-oh-tpl/victory-native-xl

# V41.17.5
npm install @react-native-ohos/victory-native-xl
```

#### **yarn**

```bash
# V41.1.0
yarn add @react-native-oh-tpl/victory-native-xl

# V41.17.5
yarn add @react-native-ohos/victory-native-xl
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import * as React from "react";
import { useState } from "react";
import { View, Text } from "react-native";
import { CartesianChart, Line } from "victory-native";

function randomNumber() {
  return Math.floor(Math.random() * 26) + 12;
}
const DATA = (numberPoints = 13) =>
  Array.from({ length: numberPoints }, (_, index) => ({
    day: index + 1,
    highTmp: randomNumber(),
  }));

const [data, setData] = useState(DATA());

export default function LineChartExample() {
  return (
    <>
      <View style={{height: 300}}>
      <Text>Line Chart</Text>
      <CartesianChart
        data={data}
        xKey="day"
        yKeys={["highTmp"]}
      >
        {({ points }) => (
          <>
          <Line 
            points={points.highTmp} 
            color="red" 
            strokeWidth={3} 
            curveType="catmullRom"
            animate={{ type: "timing", duration: 300}}
            connectMissingData={true}
          />
          </>
        )}
      </CartesianChart>
      </View>
      </>
  );
}
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated、 @react-native-oh-tpl/react-native-skia的原生端代码，如已在鸿蒙工程中引入过这两个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-skia](/zh-cn/react-native-skia.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## 属性

详情见 [victory-native-xl](https://github.com/FormidableLabs/victory-native-xl) Props tables

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Cartesian Chart

| Name                                    | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| --------------------------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| data                                    | 用作图表数据点的数组  | array[]  | yes      | all      | yes               |
| xKey                                    | 一个string[]数组字符串表示的每个数据(数量)对象的键使用依赖(x)轴的图表 | string   | yes      | all      | yes               |
| yKeys                                   | 一个string[]数组字符串表示的每个数据(数量)对象的键使用依赖(y)轴的图表 | string[] | yes      | all      | yes               |
| children                                | children属性是一个渲染函数，它的唯一参数是一个对象，该对象暴露了转换后的数据，供你在绘图操作中使用) | function | yes      | all      | yes               |
| padding                                 | 它指定Skia画布的外部边界和绘图边界将发生的位置之间的填充 | number   | no       | all      | yes               |
| domain                                  | 可以指定控制每个轴的上限和下限。它的默认值分别是每个范围的最小值和最大值 | object   | no       | all      | yes               |
| domainPadding                           | 指定绘图区域的外部边界（例如，轴所在的位置）和绘制图表元素的位置之间的填充 | object   | no       | all      | yes               |
| axisOptions                             | axisOptions是一个可选的属性，允许您配置图表的轴和网格。如果它不存在，那么图表将不会渲染任何轴或网格 | object   | no       | all      | yes               |
| chartPressState                         | chartPressState属性允许你传入重新激活的SharedValues，它将用于跟踪图表上用户的“按下”手势。这通常是用来创建某种工具提示/活跃值指标。更深入的信息,请参阅图表手势页面如何使用这个属性 | object   | no       | all      | yes               |
| renderOutside                           | renderOutside属性与form中的children属性相同，但它将渲染Skia画布的根元素（而不是在裁剪组内）。这允许你在已配置的任何坐标轴的边界之外渲染元素 | object   | no       | all      | yes               |
| onChartBoundsChange                     | onChartBoundsChange属性是方法onChartBoundsChange?： (bounds: ChartBounds) => void；这将显示图表的边界，如果您需要为自己的自定义绘图目的访问图表的边界，这将非常有用 | function | no       | all      | yes               |
| gestureLongPressDelay                   | gestureLongPressDelay支持允许您设置的延迟毫秒平移手势之前激活。默认为100 | number   | no       | all      | yes               |
| viewport<sup>41.17.5+</sup>             | 控制图表的可见范围。与domain设置数据的绝对边界不同，viewport确定图表窗口中当前可见的数据部分。 | object   | no       | all      | yes               |
| xAxis<sup>41.17.5+</sup>                | X轴是一个可选的属性，允许你配置图表的X轴。如果它不存在，那么图表将不会渲染任何X轴。 | object   | no       | all      | yes               |
| yAxis<sup>41.17.5+</sup>                | yAxis是一个可选的属性，允许你配置图表的Y轴。如果它不存在，那么图表将不会渲染任何y轴。要渲染多个Y轴，需要向数组中传入多个Y轴对象。| object   | no       | all      | yes               |
| frame<sup>41.17.5+</sup>                | frame是一个可选的prop，允许你配置图表的帧数据。如果它不存在，那么图表将不会渲染任何帧。 | object   | no       | all      | yes               |
| chartPressConfig<sup>41.17.5+</sup>     | chartPressConfig支持允许您配置平移手势处理程序用于图表交互。 | object   | no       | all      | yes               |
| transformState<sup>41.17.5+</sup>       | transformState支持允许您通过允许平移和缩放变换状态对象交互图。 | object   | no       | all      | yes               |
| transformConfig<sup>41.17.5+</sup>      | 一个可选的配置对象当transformState提供定制转换行为 | object   | no       | all      | yes               |
| customGestures<sup>41.17.5+</sup>       | customgesture属性允许你提供自定义手势处理程序，它将与默认的图表按下手势一起工作（或代替）。它从react-native手势处理程序接受一个composdgesture。 | object   | no       | all      | yes               |
| actionsRef<sup>41.17.5+</sup>           | actionsRef属性允许你程序化地访问某些图表动作。它接受一个ref对象，该对象将用控制图表行为的方法填充。 | object   | no       | all      | yes               |
| onScaleChange<sup>41.17.5+</sup>        | 一个回调函数，当图表的刻度发生变化时，由于数据更新或缩放/平移转换，该函数将被调用。该函数接收两个参数：·xScale：当前x轴刻度（d3线性刻度）·yScale：当前y轴刻度（d3线性刻度）。| function | no       | all      | yes               |
| gestureHandlerConfig<sup>41.17.5+</sup> | gestureHandlerConfig属性允许你配置底层的React Native手势处理程序实例。这是用于微调手势交互,比如启用/禁用web平台上的上下文菜单或调整触摸行为。 | object   | no       | web      | no                |

### Line Chart

| Name               | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| points             | 来自points对象字段的PointsArray数组暴露给CartesianChart的子渲染函数，如上面的示例所示 | array[] | no       | all      | yes               |
| animate            | animate prop接受一个PathAnimationConfig对象，并在点发生变化时对路径进行动画 | object  | no       | all      | yes               |
| curveType          | 一个CurveType值，表示应该绘制的曲线类型 (例如: linear or natural) | string  | no       | all      | yes               |
| connectMissingData | connectMissingData:布尔值,用于显示缺失的数据应该插值生成的路径。如果设置为true，输出将是单个连接的折线图路径（即使缺少数据值）。如果设置为false，如果缺少数据值-路径将由多个断开连接的“部分”组成 | boolean | no       | all      | yes               |
| children           | children属性是Skia Path元素内部渲染的子通道,用于渐变路径| object  | no       | all      | yes               |
| strokeWidth        | 设置线条的宽度                                  | number  | no       | all      | yes               |
| color              | 设置线条的颜色                                    | string  | no       | all      | yes               |

### Area Chart

| Name               | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| points             | 来自points对象字段的PointsArray数组暴露给CartesianChart的子渲染函数，如上面的示例所示 | array[] | no       | all      | yes               |
| y0                 | 指示区域路径“底部”应该运行的位置的数字。这个数字是画布坐标 | number  | no       | all      | yes               |
| animate            | animate prop接受一个PathAnimationConfig对象，并在点发生变化时对路径进行动画 | object  | no       | all      | yes               |
| curveType          | 一个CurveType值，表示应该绘制的曲线类型（例如线性或自然）。 | string  | no       | all      | yes               |
| connectMissingData | 一个将在Skia Path元素内部渲染的子通道，如果你想制作一个渐变路径，这很有用| boolean | no       | all      | yes               |
| children           | 一个将在Skia Path元素内部渲染的子通道，如果你想制作一个渐变路径，这很有用 | object  | no       | all      | yes               |
| color              | 设置区域的颜色                                  | string  | no       | all      | yes               |

### Bar Chart

| Name                      | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| points                    | 来自points对象的字段的PointsArray数组暴露了CartesianChart的子呈现函数，如上面的示例所示 | array[] | no       | all      | yes               |
| chartBounds               | 一个用于正确绘制条形图的ChartBounds对象。这通常来自于CartesianChart的chartBounds渲染参数 | object  | no       | all      | yes               |
| innerPadding              | 一个介于0和1之间的可选数字，表示第一个和最后一个条之间的水平空间应该是“空白”的百分比。默认为0.2。使用0表示条形条之间没有间隙，使用接近1的值表示条形条越来越窄 | number  | no       | all      | yes               |
| animate                   | animate prop接受一个PathAnimationConfig对象，并在点改变时对路径进行动画 | object  | no       | all      | yes               |
| roundedCorners            | roundedCorners属性允许你自定义BarGroup的每个角的角度。Bar组件。它是一个对象类型,定义了左上的半径,右上图右下角,左下侧的角落 | object  | no       | all      | yes               |
| barWidth                  |  barWidth prop接受一个数字，并将表的宽度设置为该数字。如果未提供，则默认值由该组条的总可用宽度、组中的条数以及组中条之间的填充量的组合决定。优先于barCount prop。将此用于最精细的条形表宽度控制 | no       | all      | yes               |
| barCount                  | barCount prop接受一个数字，并将条形的宽度设置为X个数据点。如果没有提供，则默认值由chartBounds和数据点数决定。无论数据点的数量如何，都可以获得固定的条宽度。将此用于更一般的条宽度控制 | number  | no       | all      | yes               |
| children                  | 一个在Skia路径元素中渲染的子通道，如果你想做一个渐变路径，它会很有用 | object  | no       | all      | yes               |
| color                     | 设置表的颜色                                    | string  | no       | all      | yes               |
| labels<sup>41.17.5+</sup> | labels属性允许您启用和自定义Bar组件的数据标签。数据标签文本是与Bar组件关联的y轴值。 | object  | no       | all      | yes               |

### BarGroup Chart

| Name                | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| chartBounds         | 一个用于正确绘制条形图的ChartBounds对象。这通常来自于CartesianChart的chartBounds渲染参数 | object   | no       | all      | yes               |
| betweenGroupPadding | 一个介于0和1之间的可选数字，表示第一个和最后一个条组之间的水平空间应该是“空白”的百分比。默认为0.2。使用0表示组之间没有间隙，使用接近1的值表示条形图越来越窄 | number   | no       | all      | yes               |
| withinGroupPadding  | 一个介于0到1之间的可选数字，表示组中第一个条和最后一个条之间的水平空间应该是“空白”的比例。默认为0.2。使用0表示组内条之间没有间隙，使用接近1的值表示条越来越窄 | number   | no       | all      | yes               |
| barWidth            | barWidth prop接受一个数字，并将表的宽度设置为该数字。如果未提供，则默认值由该组条的总可用宽度、组中的条数以及组中条之间的填充量的组合决定。优先于barCount prop。将此用于最精细的条形表宽度控制 | number   | no       | all      | yes               |
| barCount            | barCount prop接受一个数字，并设置条形图的宽度，就好像有X个数据点一样。如果没有提供，默认值由chartBounds和数据点的数量决定。无论数据点的数量如何，都可以获得固定的条形宽度。用它来控制表宽 | number   | no       | all      | yes               |
| onBarSizeChange     | 当条形/表的大小发生变化时，它会提醒用户，这对于构建自定义工具提示并需要知道条形/表的大小很有用 | function | no       | all      | yes               |
| roundedCorners      | roundedCorners属性允许你自定义BarGroup的每个角的角度。Bar组件。它是一个对象类型,定义了左上的半径,右上图右下角,左下侧的角落 | object   | no       | all      | yes               |
| children            | BarGroup的数组。Bar元素（见下文），表示要添加到Bar组中的Bar | object   | no       | all      | yes               |
| color               | 设置表的颜色                                     | string   | no       | all      | yes               |

### Scatter Chart

| Name        | Description                                                  | Type         | Required | Platform | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | ------------ | -------- | -------- | ----------------- |
| points      | PointsArray数组来自points对象的一个字段，它暴露给CartesianChart的子渲染函数，如上面的示例所示 | array[]      | no       | all      | yes               |
| radius      | 圆的半径，正方形宽度的一半          | number       | no       | all      | yes               |
| shape       | 下列散点形状值之一，用于确定要绘制的每个点的形状 | ScatterShape | no       | all      | yes               |
| animate     | animate属性的参数是一个PathAnimationConfig对象，它会在点发生变化时为路径添加动画 | object       | no       | all      | yes               |
| children    | BarGroup的数组。Bar元素（见下文），表示要添加到Bar组中的Bar | object       | no       | all      | yes               |
| style       | 设置样式描边或填充                                    | string       | no       | all      | yes               |
| strokeWidth | 设置线条的宽度                                    | number       | no       | all      | yes               |
| color       | 设置表的颜色                                     | string       | no       | all      | yes               |

### Polar Chart

| Name           | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| data           | 用作图表数据点的对象数组  | array[] | yes      | all      | yes               |
| labelKey       | 一个字符串值，指示要使用的每个数据[number]对象的键。目前只在图表的图例部分使用 | string  | yes      | all      | yes               |
| valueKey       | 一个字符串值，表示绘制饼图的每个data[number]对象的键 | string  | yes      | all      | yes               |
| colorKey       | 一个字符串值，表示绘制饼图的每个data[number]对象的键 | string  | yes      | all      | yes               |
| children       | PolarChart目前唯一支持的子程序是Pie。详情参见饼状图 | object  | no       | all      | yes               |
| containerStyle | ViewStyle&gt；这将样式化包装Polar图表画布的视图 | object  | no       | all      | yes               |
| canvasStyle    | ViewStyle&gt；它为绘制极坐标图的画布设置样式  | object  | no       | all      | yes               |

### Pie.Chart

**制作条形图所需的条形相关属性**

| Name               | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| innerRadius        | 一个数字或字符串(百分比),把饼图变成一个甜甜圈图。innerRadius属性是甜甜圈图内圆的半径。如果没有提供，图表仍然是饼状图 | number   | no       | all      | yes               |
| circleSweepDegrees | 定义图表应该绘制多少度的数字。默认值是360，它将绘制一个完整的圆。如果您想绘制一个局部圆，可以将该道具设置为0到360之间的值  | number   | no       | all      | yes               |
| startAngle         | 定义图表起始角度的数字。更改此属性将旋转图表 | number   | no       | all      | yes               |
| children           | children属性是一个渲染函数，它通过数据进行映射，其唯一的参数是饼图的每个单独的切片，允许您根据需要自定义每个切片 | function | no       | all      | yes               |
| angularStrokeWidth | 表示饼状图切片宽度的数字             | number   | no       | all      | yes               |
| angularStrokeColor | 一个字符串，用于改变饼图切片的颜色            | string   | no       | all      | yes               |

## 遗留问题

## 其他

- V41.17.5 新增属性gestureHandlerConfig，该属性只支持web端，无需鸿蒙化，详细参照：
   [Cartesian Chart | Victory Native](https://nearform.com/open-source/victory-native/docs/cartesian/cartesian-chart/) 、 [GestureDetector | React Native Gesture Handler](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/gesture-detector/#userselect-web-only)

## 开源协议

本项目基于 [The MIT License (MIT)]( https://www.mit-license.org/) ，请自由地享受和参与开源。

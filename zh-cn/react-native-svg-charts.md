> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-svg-charts</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/JesperLekland/react-native-svg-charts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/JesperLekland/react-native-svg-charts/blob/dev/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-svg-charts)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[https://github.com/react-native-oh-library/react-native-svg-charts Releases](https://github.com/react-native-oh-library/react-native-svg-charts/releases) 。

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 5.3.0      | [https://github.com/react-native-oh-library/react-native-svg-charts Releases](https://github.com/react-native-oh-library/react-native-svg-charts/releases) | 0.72       |
| 5.4.0      | [https://github.com/react-native-ohos/react-native-svg-charts Releases]() | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#0.72
npm install @react-native-oh-tpl/react-native-svg-charts
#0.77
npm install @react-native-ohos/react-native-svg-charts
```

#### **yarn**

```bash
#0.72
yarn add  @react-native-oh-tpl/react-native-svg-charts
#0.77
yarn add  @react-native-ohos/react-native-svg-charts
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

areaChart：
```jsx
import React from 'react'
import { Path } from 'react-native-svg'
import { AreaChart, Grid } from 'react-native-svg-charts'
import * as shape from 'd3-shape'

class AreaChartExample extends React.PureComponent {

    render() {

        const data = [50, 10, 40, 95, -4, -24, 85, 91, 35, 53, -53, 24, 50, -20, -80]

        const Line = ({ line }) => (
            <Path
                key={'line'}
                d={line}
                stroke={'rgb(134, 65, 244)'}
                fillOpacity={0}
            />
        )

        return (
            <AreaChart
                style={{ height: 200 }}
                data={data}
                contentInset={{ top: 30, bottom: 30 }}
                curve={shape.curveNatural}
                svg={{ fill: 'rgba(134, 65, 244, 0.2)' }}
                animate={true}
                animationDuration={2000}
            >
                <Grid />
                <Line />
            </AreaChart>
        )
    }
}

export default AreaChartExample
```
barChart:
```jsx
import React from 'react'
import { BarChart, Grid } from 'react-native-svg-charts'

class GroupedBarChartExample extends React.PureComponent {

    render() {

        const data1 = [ 14, -1, 100, -95, -94, -24, -8, 85, -91, 35, -53, 53, -78, 66, 96, 33, -26, -32, 73, 8 ]
            .map((value) => ({ value }))
        const data2 = [ 24, 28, 93, 77, -42, -62, 52, -87, 21, 53, -78, -62, -72, -6, 89, -70, -94, 10, 86, 84 ]
            .map((value) => ({ value }))

        const barData = [
            {
                data: data1,
                svg: {
                    fill: 'rgb(134, 65, 244)',
                },
            },
            {
                data: data2,
            },
        ]

        return (
            <BarChart
                style={ { height: 200 } }
                data={ barData }
                yAccessor={({ item }) => item.value}
                svg={{
                    fill: 'green',
                }}
                contentInset={ { top: 30, bottom: 30 } }
                { ...this.props }
            >
                <Grid/>
            </BarChart>
        )
    }

}

export default GroupedBarChartExample
```

StackedBarChart：
```jsx
import React from 'react'
import { Grid, StackedBarChart } from 'react-native-svg-charts'

const colors = ['#33691E', '#689F38', '#9CCC65', '#DCEDC8']
const data = [
    {
        broccoli: {
            value: 3840,
            svg: {
                onPress: () => console.log('onPress => 0:broccoli:3840'),
            },
        },
        celery: {
            value: 1920,
            svg: {
                onPress: () => console.log('onPress => 0:celery:1920'),
            },
        },
        onions: {
            value: 960,
            svg: {
                onPress: () => console.log('onPress => 0:onions:960'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 0:tomato:400'),
            },
        },
    },
    {
        broccoli: {
            value: 1600,
            svg: {
                onPress: () => console.log('onPress => 1:broccoli:1600'),
            },
        },
        celery: {
            value: 1440,
            svg: {
                onPress: () => console.log('onPress => 1:celery:1440'),
            },
        },
        onions: {
            value: 960,
            svg: {
                onPress: () => console.log('onPress => 1:onions:960'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 1:tomato:400'),
            },
        },
    },
    {
        broccoli: {
            value: 640,
            svg: {
                onPress: () => console.log('onPress => 2:broccoli:640'),
            },
        },
        celery: {
            value: 960,
            svg: {
                onPress: () => console.log('onPress => 2:celery:960'),
            },
        },
        onions: {
            value: 3640,
            svg: {
                onPress: () => console.log('onPress => 2:onions:3640'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 2:tomato:400'),
            },
        },
    },
    {
        broccoli: {
            value: 3320,
            svg: {
                onPress: () => console.log('onPress => 3:broccoli:3320'),
            },
        },
        celery: {
            value: 480,
            svg: {
                onPress: () => console.log('onPress => 3:celery:480'),
            },
        },
        onions: {
            value: 640,
            svg: {
                onPress: () => console.log('onPress => 3:onions:640'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 3:tomato:400'),
            },
        },
    },
]

const keys = ['broccoli', 'celery', 'onions', 'tomato']

class StackedBarChartWithOnPressExample extends React.PureComponent {
    render() {
        return (
            <StackedBarChart
                style={{ height: 300 }}
                colors={colors}
                contentInset={{ top: 30, bottom: 30 }}
                data={data}
                keys={keys}
                valueAccessor={({ item, key }) => item[key].value}
            >
                <Grid />
            </StackedBarChart>
        )
    }
}

export default StackedBarChartWithOnPressExample
```

lineChart：
```jsx
import React from 'react'
import { LineChart, Path, Grid } from 'react-native-svg-charts'

class LineChartExample extends React.PureComponent {

    render() {

        const data = [50, 10, 40, 95, -4, -24, 85, 91, 35, 53, -53, 24, 50, -20, -80]

        const Shadow = ({ line }) => (
            <Path
                key={'shadow'}
                y={2}
                d={line}
                fill={'none'}
                fillOpacity={0}
                strokeWidth={4}
                stroke={'rgba(134, 65, 244, 0.2)'}
            />
        )

        return (
            <LineChart
                style={{ height: 200, position: 'relative', zIndex: 0 }}
                data={data}
                svg={{ stroke: 'rgb(134, 65, 244)', fillOpacity: 0 }}
                contentInset={{ top: 20, bottom: 20 }}
            >
                <Grid />
                <Shadow />
            </LineChart>
        )
    }

}

export default LineChartExample
```

StackedAreaChart：
```jsx
import React from 'react'
import { StackedAreaChart, YAxis, Grid } from 'react-native-svg-charts'
import * as shape from 'd3-shape'
import { View } from 'react-native'

class AreaStackWithAxisExample extends React.PureComponent {

    render() {

        const data = [
            {
                month: new Date(2015, 0, 1),
                apples: 3840,
                bananas: 1920,
                cherries: 960,
                dates: 400,
            },
            {
                month: new Date(2015, 1, 1),
                apples: 1600,
                bananas: 1440,
                cherries: 960,
                dates: 400,
            },
            {
                month: new Date(2015, 2, 1),
                apples: 640,
                bananas: 960,
                cherries: 3640,
                dates: 400,
            },
            {
                month: new Date(2015, 3, 1),
                apples: 3320,
                bananas: 480,
                cherries: 640,
                dates: 400,
            },
        ]

        const colors = ['rgba(138, 0, 230, 0.8)', 'rgba(173, 51, 255, 0.8)', 'rgba(194, 102, 255, 0.8)', 'rgba(214, 153, 255, 0.8)']
        const keys = ['apples', 'bananas', 'cherries', 'dates']

        return (
            <View style={{ flexDirection: 'row', height: 200 }}>
                <StackedAreaChart
                    style={{ flex: 1 }}
                    contentInset={{ top: 10, bottom: 10 }}
                    data={data}
                    keys={keys}
                    colors={colors}
                    curve={shape.curveNatural}
                >
                    <Grid />
                </StackedAreaChart>
                <YAxis
                    style={{ position: 'absolute', top: -10, bottom: 10, width: 40 }}
                    data={StackedAreaChart.extractDataPoints(data, keys)}
                    contentInset={{ top: 10, bottom: 10 }}
                    numberOfTicks={8}
                    svg={{
                        fontSize: 8,
                        fill: 'white',
                        stroke: 'black',
                        strokeWidth: 0.1,
                        alignmentBaseline: 'baseline',
                        baselineShift: '3'
                    }}
                />
            </View>
        )
    }
}

export default AreaStackWithAxisExample
```

ProgressCircle：
```jsx
import React from 'react'
import { ProgressCircle } from 'react-native-svg-charts'

class ProgressCircleExample extends React.PureComponent {

    render() {

        return (
            <ProgressCircle
                style={ { height: 200 } }
                progress={ 0.7 }
                progressColor={'rgb(134, 65, 244)'}
                startAngle={ -Math.PI * 0.8 }
                endAngle={ Math.PI * 0.8 }
            />
        )
    }

}

export default ProgressCircleExample
```

PieChart：
```jsx
import React from 'react'
import { PieChart } from 'react-native-svg-charts'
import { Circle, G, Line } from 'react-native-svg'

class PieChartWithLabelExample extends React.PureComponent {

    render() {

        const data = [ 50, 10, 40, 95, -4, -24, 85, 91 ]

        const randomColor = () => ('#' + (Math.random() * 0xFFFFFF << 0).toString(16) + '000000').slice(0, 7)

        const pieData = data
            .filter(value => value > 0)
            .map((value, index) => ({
                value,
                svg: { fill: randomColor() },
                key: `pie-${index}`,
            }))

        const Labels = ({ slices }:any) => {
            return slices.map((slice, index) => {
                const { labelCentroid, pieCentroid, data } = slice;
                return (
                    <G key={ index }>
                        <Line
                            x1={ labelCentroid[ 0 ] }
                            y1={ labelCentroid[ 1 ] }
                            x2={ pieCentroid[ 0 ] }
                            y2={ pieCentroid[ 1 ] }
                            stroke={ data.svg.fill }
                        />
                        <Circle
                            cx={ labelCentroid[ 0 ] }
                            cy={ labelCentroid[ 1 ] }
                            r={ 15 }
                            fill={ data.svg.fill }
                        />
                    </G>
                )
            })
        }

        return (
            <PieChart
                style={ { height: 200 } }
                data={ pieData }
                innerRadius={ 20 }
                outerRadius={ 55 }
                labelRadius={ 80 }
            >
                <Labels/>
            </PieChart>
        )
    }

}

export default PieChartWithLabelExample
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

在下述版本验证通过:

1. react-native-harmony: 0.72.26-CAPI; SDK：HarmonyOS NEXT Developer Cannary3 SP2; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.22(Canary3);
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 属性

详情见[react-native-svg-charts](https://github.com/JesperLekland/react-native-svg-charts)

### 共有属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | 一组任意数据 - 使用属性 xAccessor/yAccessor 告诉图表数据的结构         | array  | YES | ALL      | YES |
yAccessor | 一个函数，它接收每条数据（称为“item”）以及索引，并返回该条目的 y 值 |  function | NO | ALL | YES |
xAccessor | 与 yAccessor 相同，但返回该条目的 x 值 | function | NO | ALL | YES |
yScale | 一个确定所述坐标轴比例的函数（仅在 scaleLinear、scaleTime 和 scaleBand 下测试过） | d3Scale.scaleLinear | NO | ALL | YES |
xScale | 与 y 轴的 yScale 相同，但用于 x 轴 | d3Scale.scaleLinear | NO | ALL | YES |
svg | 一个包含所有应传递到底层 react-native-svg 组件的属性的对象。请参阅可用属性 | object | NO | ALL | YES |
animate | PropTypes.bool | boolean |   NO | ALL | YES |
animationDuration | PropTypes.number | number |   NO | ALL | YES |
style | 支持所有视图样式属性 | ViewStyleProps |   NO | ALL | YES |
curve | 设置curve曲线 | d3.curveLinear  |   NO | ALL | YES |
contentInset | 一个对象，用于指定在 SVG 画布内部使用多少假“边距”。这在 Android 上特别有用，因为 overflow: "visible" 不被支持，可能会导致裁剪。注意：在轴和图表上保持相同的 contentInset 很重要 | object |   NO | ALL | YES |
numberOfTicks | 我们使用 d3-array 在 y 轴上均匀分布网格和数据点。这个属性指定了我们应尝试渲染的“刻度”数量。注意：重要的是这个属性在图表和 y 轴上必须相同 | 数字/未定义 |   NO | ALL | YES |
showGrid | 是否显示网格线  | boolean |   NO | ALL | YES |
yMin | 更改图表边界的计算方式  | number/undefined |   NO | ALL | YES |
yMax | 更改图表边界的计算方式  |  number/undefined |   NO | ALL | YES |
xMin | 更改图表边界的计算方式  |  number/undefined |   NO | ALL | YES |
xMax | 更改图表边界的计算方式  |  number/undefined |   NO | ALL | YES |
children | 一个或多个 react-native-svg 组件，将用于增强您的图表 |  ReactNode |   NO | ALL | YES |

### 属性children
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| x  | 一个通常接受数据点索引并返回其在画布上的 'x' 位置的函数         |  nunmber/string  | NO | ALL      | YES |
| y  | 一个函数，通常接受数据点的值并返回其在画布上的“y”位置        |  nunmber/string  | NO | ALL      | YES |
| width  | 画布的像素宽度        |  number/srting  | NO | ALL      | YES |
| height  | 画布的像素高度        |   number/srting  | NO | ALL      | YES |
| data  | 将提供给图表的相同数据数组，如果你想在每个点上添加装饰器，可以使用它来映射你的数据点       |  array  | YES | ALL      | YES |
| ticks  | 如果图表提供了 numberOfTicks，则此数组将包含计算出的刻度值（对于网格很有用）       |  array  | NO | ALL      | YES |

### 组件特有属性

#### Area
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| start  | 面积应开始的值（将始终在数据点结束）   |  number/undefined  | NO | ALL      | YES |

#### StackedAreaChart
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | 数据条目的数组    |  array  | YES | ALL      | YES |
| keys  | 该数组应包含感兴趣的对象键（参见上面的示例）   |  array  | YES | ALL      | YES |
| colors  | 一个与键大小相同的数组，用于存放每个键的颜色    |  array  | YES | ALL      | YES |
| order  | 排序区域的顺序    |  d3.stackOrderNone  | NO | ALL      | YES |
| offset  | 一个用于确定区域偏移的函数    |  d3.stackOffsetNone  | NO | ALL  | YES |

#### BarChart
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | barChart 中的 data 属性看起来可以完全像 LineChart 或 AreaChart 中的那样，即一个仅包含数字的数组或复杂对象的数组。然而，它也可以是包含多个数据集的数组。一个数据对象可以包含一个 svg 属性，这允许你覆盖该特定对象的样式。     |  array  | YES | ALL      | YES |
| horizontal  | 布尔值，表示条形图是否应为水平   |  boolean  | NO | ALL      | YES |
| svg  | 所有柱状图的默认 SVG 属性。支持 SVG 路径通常支持的所有 SVG 属性。如果某个数据对象有特定样式，这些样式将被覆盖。  |  object  | NO | ALL      | YES |
| spacingInner  | 条形（或条形组）之间的间距    |  number/undefined   | NO | ALL      | YES |
| spacingOuter  | 条形（或条形组）外的间距。相当于一个条形宽度的百分比    |  number/undefined   | NO | ALL      | YES |
| contentInset  | PropTypes.shape    |  object  | NO | ALL      | YES |
| children.bandwidth  | 带（即条形）的宽度    |  number  | NO | ALL      | YES |

#### StackedBarChart
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | 数据条目的数组：每个值可以是一个数字，也可以是带有自定义 SVG 属性的复杂对象，例如    |  array  | YES | ALL      | YES |
| keys  | 该数组应包含感兴趣的对象键（参见上面的示例）   |  array  | YES | ALL      | YES |
| colors  | 一个与键大小相同的数组，用于存放每个键的颜色    |  array  | YES | ALL      | YES |
| valueAccessor  | 与其他图表的 yAccessor 非常相似，通常在使用复杂对象作为值时需要   |  function  | NO | ALL      | YES |
| horizontal  | 布尔值，表示条形图是否应为水平   |  boolean  | NO | ALL      | YES |
| order  | 排序区域的顺序    |  d3.stackOrderNone  | NO | ALL      | YES |
| offset  | 一个用于确定区域偏移的函数    |  d3.stackOffsetNone | NO | ALL  | YES |

#### PieChart
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | 与我们其他图表的数据属性非常相似，唯一的区别是饼图只接受复杂对象（不仅仅是数字）。一个项目还可以包含 arc 属性，这允许你覆盖该特定弧的设置    |  array  | YES | ALL      | YES |
| valueAccessor  | 与其他图表的 yAccessor 非常相似    |  function  | NO | ALL      | YES |
| outerRadius  | 外半径，用来调整你的饼图与容器边缘的距离。可以使用百分比或绝对数值（像素）    |  number/string/undefined  | NO | ALL      | YES |
| innerRadius  | 内半径，用于创建甜甜圈图。可以使用百分比或绝对数值（像素）    |  number/string/undefined  | NO | ALL      | YES |
| labelRadius  | 用于帮助你布置标签的圆的半径。可以使用百分比或绝对数值（像素）   |  number/string/undefined  | NO | ALL      | YES |
| padAngle  | 切片之间的角度    |  number/undefined  | NO | ALL      | YES |
| startAngle  | 整个饼图的起始角度（弧度）    |  number/undefined  | NO | ALL      | YES |
| endAngle  | 整个饼图的结束角度（弧度）    |  number/undefined  | NO | ALL      | YES |
| sort  | 像任何普通的排序函数一样，它期望返回值为 0、正数或负数。参数是来自 dataPoints 数组的每个对象   |  function  | NO | ALL      | YES |
| children.slices  | 饼图切片的数组。请参阅源代码和示例以了解其包含内容    |  array  | NO | ALL      | YES |

#### ProgressCircle
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| progress  | 进度值    |  number  | YES | ALL  | YES |
| progressColor  | 进度条颜色    |  string/undefined  | NO | ALL  | YES |
| backgroundColor  | 进度条背景颜色    |  string/undefined  | NO | ALL  | YES |
| startAngle  | 开始的角度    |  number/undefined  | NO | ALL  | YES |
| endAngle  | 结束的角度    |  number/undefined  | NO | ALL  | YES |
| strokeWidth  | 进度条的宽度    |  number/undefined  | NO | ALL  | YES |
| cornerRadius  | 圆角的大小    |  number/undefined | NO | ALL  | YES |

#### YAxis
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scale  | 应该与传入图表的 yScale 相同，或者在与水平条形图一起使用时，与 d3Scale.scaleBand 相同   |  d3Scale.scaleLinear  | NO | ALL  | YES |
| svg  | 支持所有 SVG 属性以及 SVG 文本通常支持的属性   |  object  | NO | ALL      | YES |
| spacingInner  | 标签之间的间距。仅在 scale=d3Scale.scaleBand 时适用，此时应等于实际 BarChart 上的 spacingInner 属性  |  number/undefined   | NO | ALL      | YES |
| spacingOuter  | 	标签外的间距。仅在 scale=d3Scale.scaleBand 时适用，并且应等于实际条形图上的 spacingOuter 属性   |  number/undefined  | NO | ALL      | YES |
| formatLabel  | 一个用于在文本显示之前进行格式化的实用函数，例如 `value => "$" + value`   |  function|NO  | YES | ALL      | YES |
| contentInset  | 用于与图表同步布局（如果在那里使用了相同的属性）   |  object  | NO | ALL      | YES |
| min  | 用于与图表同步布局（如果使用了 gridMin）  | number/undefined | NO | ALL      | YES |
| max  | 用于与图表同步布局（如果使用了 gridMax）  | number/undefined | NO | ALL      | YES |

#### XAxis
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | 要在 x 轴上渲染的一组值或对象。最好与图表的数据点长度相同。如果使用的是复杂对象而不是简单值，则需要 xAccessor 属性来计算轴的范围。数据对象可以包含一个 svg 属性，该属性允许你覆盖该特定对象的样式  |  array  | YES | ALL      | YES |
| scale  | 应该与传入图表的 xScale 相同   |  d3Scale.scaleLinear  | NO | ALL  | YES |
| spacingInner  | 标签之间的间距。仅在 scale=d3Scale.scaleBand 时适用，此时应等于实际 BarChart 上的 spacingInner 属性   |  number/undefined   | NO | ALL      | YES |
| spacingOuter  | 	标签之间的间距。仅在 scale=d3Scale.scaleBand 时适用，此时应等于实际 BarChart 上的 spacingOuter 属性   |  number/undefined  | NO | ALL      | YES |
| svg  | 所有标签的默认 SVG 属性。支持 SVG 文本通常支持的所有 SVG 属性。如果针对特定数据对象有特定样式，这些样式将被覆盖。   |  object  | NO | ALL      | YES |
| formatLabel  | 一个实用函数，用于在显示文本之前进行格式化，例如 value => "day" value。返回 xAccessor 提供的值   |  function  | NO | ALL      | YES |
| contentInset  | 用于与图表同步布局（如果在那里使用了相同的属性）  |  object  | NO | ALL      | YES |


#### Grid
| 名称 | 描述 | 类型 | 是否必需 | 支持的平台 | 是否支持HarmonyOS  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| svg  | 一个包含所有应传递给底层 react-native-svg 组件的属性的对象。   |  object  | NO | ALL      | YES |
| direction  | 网格线的方向。  |  Grid.Direction  | NO | ALL      | YES |
| belowChart  | 是否在图表下方呈现。  |  boolean  | NO | ALL      | YES |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/JesperLekland/react-native-svg-charts/blob/dev/LICENSE) ，请自由地享受和参与开源。
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-calendars</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wix/react-native-calendars">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wix/react-native-calendars/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/wix/react-native-calendars/tree/1.1304.1)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 1.1304.1               |  0.72 |
| 1.1313.0               |  0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
#0.72
npm install --save react-native-calendars@1.1304.1
#0.77
npm install --save react-native-calendars@1.1313.0
```

#### **yarn**

```bash
#0.72
yarn add react-native-calendars@1.1304.1
#0.77
yarn add react-native-calendars@1.1313.0
```

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from "react";
import { Calendar, CalendarList, Agenda ,AgendaList,CalendarProvider,ExpandableCalendar,Timeline,WeekCalendar} from "react-native-calendars";
import { View, StyleSheet, Text } from "react-native";

const MySvgComponent = () => {
  const [selected, setSelected] = useState("");
  const data = [
    {
        title: "Main",
        data: ["Pizza"]
    },
    {
        title: "sides",
        data: ["French Fries"]
    }
  ]
  return (
    <View style={styles.container}>
      <Calendar
        onDayPress={(day) => {
          setSelected(day.dateString);
        }}
        markedDates={{
          [selected]: {
            selected: true,
            disableTouchEvent: true,
            selectedColor: "orange",
          },
        }}
      />
      <Agenda
        items={{
        '2012-05-22': [{name: 'item 1 - any js object', height: 80, day: ''}],
        '2012-05-23': [{name: 'item 2 - any js object', height: 80, day: ''}],
        '2012-05-24': [],
        '2012-05-25': [{name: 'item 3 - any js object', height: 80, day: ''}, {name: 'any js object', height: 80, day: ''}]
       }}
      />
       <AgendaList
        sections={data}
        renderItem={({ item }) => (
            <View style={{ padding: 20 }}>
                <Text>{ item.name } - { item.data } </Text>
            </View>
        )}
        scrollToNextEvent={true}
      />
       <CalendarProvider
        date={'yyyy-MM-dd'}
      />
       <ExpandableCalendar
        disablePan={false}
      />
       <Timeline
        theme={{
                backgroundColor: '#ffffff',
                calendarBackground: '#ffffff',
                textSectionTitleColor: '#b6c1cd',
                textSectionTitleDisabledColor: '#d9e1e8',
                selectedDayBackgroundColor: '#00adf5',
                selectedDayTextColor: '#ffffff',
                todayTextColor: '#00adf5',
                dayTextColor: '#2d4150',                          
              }}
      />
       <WeekCalendar
        hideDayNames={true}
      />
    </View>
  );
 
};

const styles = StyleSheet.create({
  container: {
    position: "absolute",
    bottom: 210,
    width: "100%",
    alignItems: "center",
    justifyContent: "center",
    borderWidth: 1,
    backgroundColor: "#CC00FF",
  },
});
export default MySvgComponent;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证：

1. RNOH: 0.72.28; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio  5.0.3.535; ROM：5.0.0.31;
2. RNOH： 0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Agenda

| Name              | Description                                                  | Type           | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------------- | -------- | -------- | ----------------- |
| items             | 必须在议程中显示的项目列表。如果你想将项目呈现为空日期，日期键的值必须是一个空数组[]。如果日期键没有值，则认为相关日期尚未加载 | AgendaSchedule | no       | All      | yes               |
| selected          | 初始选中的日期                                       | string         | no       | All      | yes               |
| hideKnob          | 是否隐藏旋钮                                     | boolean        | no       | All      | yes               |
| showClosingKnob   | 旋钮是否应始终可见（hideKonb=false时） | boolean        | no       | All      | yes               |
| loadItemsForMonth | 当需要加载特定月份时（该月变得可见）执行的处理函数 | function       | no       | All      | yes               |
| onDayChange       | 当日期发生变化时执行的处理函数 | function       | no       | All      | yes               |
| onCalendarToggled | 打开或关闭日历时执行的处理函数 | function       | no       | All      | yes               |
| renderKnob        | 将默认议程的旋钮替换为自定义旋钮              | function       | no       | All      | yes               |
| renderList        | 用自定义实现的组件覆盖内部列表      | function       | no       | All      | yes               |
| showOnlySelectedDayItems        | 是否仅显示所选日期的项目      | boolean       | no       | All      | yes               |
| renderEmptyData        | 将默认ActivityIndicator替换为自定义ActivityIndicator      | function       | no       | All      | yes               |

### AgendaList

| Name              | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| theme             | 指定主题属性以覆盖日历零件的特定样式 | Theme     | no       | All      | yes               |
| dayFormat         | 章节标题中的日期格式。格式化值： http://arshaw.com/xdate/#Formatting | string    | no       | All      | yes               |
| useMoment         | 是否使用moment.js进行日期字符串格式化          | boolean   | no       | All      | yes               |
| markToday         | 是否将今日标题标记为"Today, ..."字符串   | boolean   | no       | All      | yes               |
| avoidDateUpdates  | 议程滚动时是否阻止日历（和日历上下文提供程序）中的日期更改 | boolean   | no       | All      | yes               |
| scrollToNextEvent | 当按下没有内容的一天时，是否启用将议程列表滚动到下一个有内容的日期 | boolean   | no       | All      | yes               |
| viewOffset        | 滚动的偏移量                                 | number    | no       | All      | yes               |
| sectionStyle      | 传递给日期段标题容器的样式                         | ViewStyle | no       | All      | yes               |
| dayFormatter      | 用于自定义日期标题格式的函数       | function  | no       | All      | yes               |
| infiniteListProps | 若定义此参数，则使用InfiniteList而不是SectionList。此为实验性功能，后续可能发生变更 | object    | no       | All      | yes               |

### Calendar

| Name                                    | Description                                                  | Type                 | Required | Platform | HarmonyOS Support |
| --------------------------------------- | ------------------------------------------------------------ | -------------------- | -------- | -------- | ----------------- |
| theme                                   | 用于覆盖日历组件特定样式的主题配置 | Theme                | no       | All      | yes               |
| style                                   | 用于设置日历容器元素的样式                 | ViewStyle | no       | All      | yes               |
| current                                 | 初始显示的月份                                      | string               | no       | All      | yes               |
| initialDate                             | 初始显示的月份（若变更将以此值重新初始化日历） | string               | no       | All      | yes               |
| minDate                                 | 可选择的最小日期，此日期之前的日期将显示为灰色 | string               | no       | All      | yes               |
| maxDate                                 | 可选择的最大日期，此日期之后的日期将显示为灰色 | string               | no       | All      | yes               |
| markedDates                             | 需要被标记的日期集合                   | MarkedDates          | no       | All      | yes               |
| hideExtraDays                           | 是否在月份页面中隐藏其他月份的日期               | boolean              | no       | All      | yes               |
| showSixWeeks                            | 是否始终在每个月份显示六周（当hideExtraDays=false时） | boolean              | no       | All      | yes               |
| disableMonthChange                      | 当点击其他月份的日期时是否禁用月份切换（当hideExtraDays为false时） | boolean              | no       | All      | yes               |
| enableSwipeMonths                       | 是否启用月份滑动切换功能                    | boolean              | no       | All      | yes               |
| disabledByDefault                       | 是否默认禁用所有日期                                      | boolean              | no       | All      | yes               |
| headerStyle                             | 传递给标题头的样式                                   | ViewStyle | no       | All      | yes               |
| customHeader                            | 允许渲染完全自定义的标题头                      | any                  | no       | All      | yes               |
| onDayPress                              | 日期被点击时执行的处理函数                     | function             | no       | All      | yes               |
| onDayLongPress                          | 日期被长按时执行的处理函数                | function             | no       | All      | yes               |
| onMonthChange                           | 日历中月份变更时执行的处理函数   | function             | no       | All      | yes               |
| onVisibleMonthsChange                   | 日历中可见月份变更时执行的处理函数 | function             | no       | All      | yes               |
| disabledByWeekDays<sup> 1.1313.0+</sup> | 按星期几禁用日期（周日=0）                 | number[]             | no       | All      | yes               |
| testID | Test ID                 | string             | no       | All      | yes               |
| allowSelectionOutOfRange                | 是否允许选择minDate之前或maxDate之后的日期     | boolean              | no       | All      | yes               |
| firstDay                                  | 若firstDay=1，则周从周一开始。注意：dayNames和dayNamesShort仍应从周日开始                                                     | number               | no       | All      | yes               |
| displayLoadingIndicator                                  | 是否显示加载指示器                                                      | boolean               | no       | All      | yes               |
| showWeekNumbers                                  | 是否显示周数                                                      | boolean               | no       | All      | yes               |
| monthFormat                                  | 标题头的月份格式，格式化值参考： <http://arshaw.com/xdate/#Formatting>                                                      | string               | no       | All      | yes               |
| hideDayNames                                  | 是否隐藏日期名称                                                       | boolean               | no       | All      | yes               |
| hideArrows                                  | 是否隐藏箭头                                                      | boolean               | no       | All      | yes               |
| arrowsHitSlop                                  | 左右箭头，按钮外部的附加距离，在此距离内检测到按下（默认：20）                                                      | number               | no       | All      | yes               |
| disableArrowLeft                                  | 是否禁用左箭头                                                      | boolean               | no       | All      | yes               |
| disableArrowRight                                  | 是否禁用右箭头                                                      | boolean               | no       | All      | yes               |
| renderArrow                                  | 用自定义箭头替换默认箭头（方向：'left','right'）                                                      | function               | no       | All      | yes               |
| onPressArrowLeft                                  | 按下左箭头时执行的处理函数，接收跳转到上个月的回调                                                      | function               | no       | All      | yes               |
| onPressArrowRight                                  | 按下右箭头时执行的处理函数，接收跳转到下个月的回调                                                      | function               | no       | All      | yes               |
| disabledDaysIndexes                                  | 是否为选定的日期索引应用自定义禁用颜色                                                      | number[]               | no       | All      | yes               |
| renderHeader                                  | 用自定义标题替换默认标题                                                      | function               | no       | All      | yes               |
| customHeaderTitle                                  | 用自定义元素替换默认标题                                                      | JSX.Element               | no       | All      | yes               |
| dayComponent                                  | 用自定义日期渲染组件替换默认日期组件                                                       | JSX.Element               | no       | All      |yes               |
| disableAllTouchEventsForDisabledDays                                  | 是否为禁用的日期禁用所有触摸事件（可通过markedDates中的'disableTouchEvent'覆盖）                                                      | boolean               | no       | All      |yes               |
| disableAllTouchEventsForInactiveDays                                  | 是否为非活动日期禁用所有触摸事件（可通过markedDates中的'disableTouchEvent'覆盖）                                                      | boolean               | no       | All      |yes               |

### CalendarList

| Name                | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| pastScrollRange     | 允许向过去方向滚动显示的最大月份数量           | number    | no       | All      | yes               |
| futureScrollRange   | 允许向未来方向滚动显示的最大月份数量         | number    | no       | All      | yes               |
| calendarStyle       | 用于设置日历容器元素的样式                 | ViewStyle | no       | All      | yes               |
| calendarHeight      | 动态设置日历高度                                      | number    | no       | All      | yes               |
| calendarWidth       | 在水平滚动日历且分页未启用时使用（当pagingEnabled = false） | number    | no       | All      | yes               |
| staticHeader        | 是否使用固定不滚动的标题头（当horizontal = true时） | boolean   | no       | All      | yes               |
| showScrollIndicator | 是否启用垂直/水平滚动指示器 | boolean   | no       | All      | yes               |
| animateScroll       | 是否启用月份自动滚动的动画效果                     | boolean   | no       | All      | yes               |
| contentContainerStyle       | 应用于包裹所有子视图的滚动视图内容容器的样式                     | StyleProp\<ViewStyle>   | no       | All      | yes               |

### CalendarProvider

| Name                                        | Description                                                  | Type                      | Required | Platform | HarmonyOS Support |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------- | -------- | -------- | ----------------- |
| theme                                       | 用于覆盖日历组件特定样式的主题配置 | Theme                     | no       | All      | yes               |
| style                                       | 用于设置日历容器元素的样式                 | ViewStyle                 | no       | All      | yes               |
| date                                        | 初始日期，格式为'yyyy-MM-dd'                          | string                    | no       | All      | yes               |
| showTodayButton                             | 是否显示"今天"按钮                             | boolean                   | no       | All      | yes               |
| todayButtonStyle                            | "今天"按钮的样式                                         | ViewStyle                 | no       | All      | yes               |
| todayBottomMargin                           | "今天"按钮距离底部的边距                                  | number                    | no       | All      | yes               |
| disabledOpacity                             | 禁用状态下"今天"按钮的透明度（0-1）              | number                    | no       | All      | yes               |
| onDateChanged                               | 日期变更时执行的处理函数            | function                  | no       | All      | yes               |
| onMonthChange                               | 月份变更时执行的处理函数   | function                  | no       | All      | yes               |
| disableAutoDaySelection<sup>1.1313.0+</sup> | 在特定日历导航类型中禁用自动日期选择（选项来自ExpandableCalendar.navigationTypes） | CalendarNavigationTypes[] | no       | All      | yes               |
| numberOfDays                                | 在时间线日历中显示的天数       | number                    | no       | All      | yes               |
| timelineLeftInset                           | 时间线日历的左侧插入距离（侧边栏宽度），默认为72 | number                    | no       | All      | yes               |

### ExpandableCalendar

| Name                  | Description                                                  | Type                | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------- | -------- | -------- | ----------------- |
| initialPosition       | 日历的初始位置（'open' 展开或 'closed' 收起）    | Positions           | no       | All      | yes               |
| disablePan            | 是否禁用平移手势并禁用日历的打开和关闭（initialPosition将保持固定） | boolean             | no       | All      | yes               |
| hideKnob              | 是否隐藏拖拽手柄                                     | boolean             | no       | All      | yes               |
| leftArrowImageSource  | 左侧箭头图片的资源地址                          | ImageSourcePropType | no       | All      | yes               |
| rightArrowImageSource | 右侧箭头图片的资源地址                         | ImageSourcePropType | no       | All      | yes               |
| allowShadow           | 是否为日历添加阴影/ elevation 效果            | boolean             | no       | All      | yes               |
| disableWeekScroll     | 在收起状态下是否禁用周滚动        | boolean             | no       | All      | yes               |
| openThreshold         | 通过拖拽手势展开日历的触发阈值  | number              | no       | All      | yes               |
| closeThreshold        | 通过拖拽手势收起日历的触发阈值                                               | number              | no       | All      | yes               |
| onCalendarToggled     | 日历展开或收起时执行的处理函数 | function            | no       | All      | yes               |
| closeOnDayPress       | 点击日期时是否自动收起日历，默认=true   | boolean             | no       | All      | yes               |

### Timeline

| Name                     | Description                                                  | Type               | Required | Platform | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------ | ------------------ | -------- | -------- | ----------------- |
| theme                    | 用于覆盖时间线组件特定样式的主题配置 | Theme              | no       | All      | yes               |
| styles                    | 用于设置时间线容器元素的样式                 | Theme          | no       | All      | yes               |
| events                   | 要在时间线上渲染的事件列表                     | Event[]            | no       | All      | yes               |
| start                    | 时间线一天的开始时间                                  | number             | no       | All      | yes               |
| end                      | 时间线一天的结束时间                                    | number             | no       | All      | yes               |
| scrollToFirst            | 是否滚动到第一个事件                         | boolean            | no       | All      | yes               |
| format24h                | 是否使用24小时制显示时间线小时        | boolean            | no       | All      | yes               |
| onEventPress             | 事件被点击时执行的处理函数            | function           | no       | All      | yes               |
| onBackgroundLongPress    | 背景被长按时执行的处理函数，用于处理新事件的创建 | function           | no       | All      | yes               |
| onBackgroundLongPressOut | 背景长按释放时执行的处理函数，用于处理新事件的创建 | function           | no       | All      | yes               |
| renderEvent              | 指定自定义事件块的渲染函数                                 | function           | no       | All      | yes               |
| date                     | 此时间线实例的日期，ISO格式（如2011-10-25） | string \|string[]  | no       | All      | yes               |
| eventTapped <sup>deprecated from 1.1304.1+</sup>             | 已弃用（从1.1304.1+版本开始），请使用onEventPress代替                                     | function           | no       | All      | yes               |
| scrollToNow              | 加载时是否滚动到当前时间                    | boolean            | no       | All      | yes               |
| initialTime              | 初始滚动到的时间                                    | object             | no       | All      | yes               |
| showNowIndicator         | 是否显示当前时间指示器                                | boolean            | no       | All      | yes               |
| scrollOffset             | 时间线组件将同步的滚动偏移值       | number              | no       | All      | yes               |
| onChangeOffset           | 监听时间线组件的滚动事件           | function           | no       | All      | yes               |
| overlapEventsSpacing     | 重叠事件之间的间距                           | number             | no       | All      | yes               |
| rightEdgeSpacing         | 右侧边缘保留的间距（用于背景按压）     | number             | no       | All      | yes               |
| unavailableHours         | 不可用小时的时间范围                                     | UnavailableHours[] | no       | All      | yes               |
| unavailableHoursColor    | 不可用时间段的背景颜色                       | string             | no       | All      | yes               |
| numberOfDays             | 在时间线日历中显示的天数       | number             | no       | All      | yes               |
| timelineLeftInset        | 时间线日历的左侧插入距离（侧边栏宽度），默认为72 | number             | no       | All      | yes               |
| testID        | 测试标识 | string             | no       | All      | yes               |

### WeekCalendar

| Name        | Description                                       | Type    | Required | Platform | HarmonyOS Support |
| ----------- | ------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| allowShadow | 是否为日历添加阴影/ elevation 效果       | boolean | no       |All      | yes               |
| hideDayNames | 是否隐藏星期几的名称 | boolean | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wix/react-native-calendars/blob/master/LICENSE) ，请自由地享受和参与开源。

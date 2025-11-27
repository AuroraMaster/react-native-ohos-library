> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-tourguide</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/xcarpentier/rn-tourguide">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/xcarpentier/rn-tourguide/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


本项目基于[rn-tourguide](https://github.com/react-native-oh-library/rn-tourguide).

该第三方库的仓库已迁移至 Gitcode，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/rn-tourguide`。具体版本所属关系如下：

| Version                   | Package Name                                      | Repository         | Release                    |Support RN version|
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |-------------------|
| 3.3.0  | @react-native-oh-tpl/rn-tourguide | [Github](https://github.com/react-native-oh-library/rn-tourguide) | [Github Releases](https://github.com/react-native-oh-library/rn-tourguide/releases) |0.72       |
| 3.4.0     | @react-native-ohos/rn-tourguide   | [GitCode](https://gitcode.com/openharmony-sig/rntpc_rn-tourguide) | [GitCode Releases]() |0.77       |


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash

# 0.72
npm install @react-native-oh-tpl/rn-tourguide

# 0.77
npm install @react-native-ohos/rn-tourguide
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/rn-tourguide

# 0.77
yarn add @react-native-ohos/rn-tourguide
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import * as React from 'react'
import {
  Image,
  Platform,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native'
import {
  TourGuideProvider,
  TourGuideZone,
  TourGuideZoneByPosition,
  useTourGuideController
} from 'rn-tourguide'

const uri =
  'https://pbs.twimg.com/profile_images/1223192265969016833/U8AX9Lfn_400x400.jpg'

export default function () {
  return (
    <TourGuideProvider {...{ borderRadius: 16, androidStatusBarVisible: true }}>
      <AppContent />
    </TourGuideProvider>
  )
}

const AppContent = () => {
  const iconProps = { size: 40, color: '#888' }

  const { start, canStart, stop, eventEmitter } = useTourGuideController()

  React.useEffect(() => {
    if (canStart) {
      start()
    }
  }, [canStart]) 

  React.useEffect(() => {
    eventEmitter?.on('start', () => console.log('start'))
    eventEmitter?.on('stop', () => console.log('stop'))
    eventEmitter?.on('stepChange', () => console.log(`stepChange`))
    return () => eventEmitter?.off('*', () => {})
  }, [])
  return (
    <View style={styles.container}>
      <TourGuideZone
        keepTooltipPosition
        zone={1}
        text={'A react-native-copilot remastered! 🎉'}
        borderRadius={16}
      >
        <Text style={styles.title}>
          {'Welcome to the demo of\n"rn-tourguide"'}
        </Text>
      </TourGuideZone>
      <View style={styles.middleView}>
        <TouchableOpacity style={styles.button} onPress={() => start()}>
          <Text style={styles.buttonText}>START THE TUTORIAL!</Text>
        </TouchableOpacity>

        <TourGuideZone zone={2} shape={'rectangle_and_keep'}>
          <TouchableOpacity style={styles.button} onPress={() => start(4)}>
            <Text style={styles.buttonText}>Step 4</Text>
          </TouchableOpacity>
        </TourGuideZone>
        <TouchableOpacity style={styles.button} onPress={() => start(2)}>
          <Text style={styles.buttonText}>Step 2</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.button} onPress={stop}>
          <Text style={styles.buttonText}>Stop</Text>
        </TouchableOpacity>
        <TourGuideZone
          zone={6}
          shape='circle'
          text={'With animated SVG morphing with awesome flubber 🍮💯'}
        >
          <Image source={{uri}} style={styles.profilePhoto} />
        </TourGuideZone>
      </View>
      <View style={styles.row}>
        <TourGuideZone zone={3} shape={'circle'} tooltipBottomOffset={200}>
          <Text style={styles.text}>Text1</Text>
        </TourGuideZone>
        <Text style={styles.text}>Text2</Text>
        <Text style={styles.text}>Text3</Text>
     
        <TourGuideZone zone={4} shape={'rectangle'}>
          <Text style={styles.text}>Text4</Text>
        </TourGuideZone>
        <TourGuideZone zone={5} shape={'circle'}>
          <Text style={styles.text}>Text5</Text>
        </TourGuideZone>
      </View>
      {Platform.OS !== 'web' ? (
        <TourGuideZoneByPosition
          zone={1}
          shape={'circle'}
          isTourGuide
          top={250}
          left={50}
          width={64}
          height={64}
        />
      ) : null}
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    paddingTop: 40,
  },
  title: {
    fontSize: 24,
    textAlign: 'center',
  },
  profilePhoto: {
    width: 140,
    height: 140,
    borderRadius: 70,
    marginVertical: 20,
  },
  middleView: {
    flex: 1,
    alignItems: 'center',
  },
  button: {
    backgroundColor: '#2980b9',
    paddingVertical: 10,
    paddingHorizontal: 15,
    margin: 2,
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
  },
  row: {
    width: '100%',
    padding: 15,
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  text: {
    fontSize: 20,
  }
})

```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

1. RNOH: 0.72.27; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 属性

详情见[rn-tourguide](https://github.com/xcarpentier/rn-tourguide)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### TourGuideProvider
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| tooltipComponent  |  提示框组件  | React.ComponentType<TooltipProps>  | NO | ALL      | YES |
| tooltipStyle  |   提示框样式 | StyleProp<ViewStyle>  | NO | ALL      | YES |
| labels  | 提示框中显示的按钮文本（跳过、上一步、下一步、完成） | Labels | NO | ALL      | YES |
| startAtMount  |         | boolean/string | NO | ALL      | YES |
| androidStatusBarVisible  | 安卓状态栏是否显示安卓状态栏 | boolean | NO | Android      | NO |
| backdropColor  | 背景颜色 | string | NO | ALL      | YES |
| verticalOffset | 垂直偏移量 | number | NO | ALL      | YES |
| wrapperStyle  | 包裹器样式 | StyleProp<ViewStyle> | NO | ALL      | YES |
| maskOffset  | 区域周围的偏移量 | number | NO | ALL      | YES |
| borderRadius  | 矩形时的圆角 | number | NO | ALL      | YES |
| animationDuration  | 动画持续时间 | number | NO | ALL      | YES |
| children  | React.ReactNode 组件 | React.ReactNode | YES | ALL      | YES |
| dismissOnPress  | 是否显示可点击区域 | boolean | NO | ALL      | YES |
| preventOutsideInteraction  | 阻止默认事件 | boolean | NO | ALL      | YES |

### TourGuideZone
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| zone  | 一个正数，表示整个引导流程中步骤的顺序 | number  | YES | ALL      | YES |
| tourKey  |        | string  | NO | ALL      | YES |
| isTourGuide  | 如果为 false，则返回子组件而不进行包裹 | boolean  | NO | ALL      | YES |
| text  |     提示框中的文本     | string  | NO | ALL      | YES |
| shape  |     形状     | Shape  | NO | ALL      | YES |
| maskOffset  | 区域周围的偏移量 | number  | NO | ALL      | YES |
| borderRadius  |  矩形时的圆角 | number  | NO | ALL      | YES |
| children  | React.ReactNode 组件 | React.ReactNode  | NO | ALL      | YES |
| style  |         | StyleProp<ViewStyle>  | NO | ALL      | YES |
| keepTooltipPosition  | 提示框定位 | boolean  | NO | ALL      | YES |
| tooltipBottomOffset  | 提示框与容器底部的距离 | number  | NO | ALL      | YES |
| borderRadiusObject  | 遮罩层高亮区域的圆角设置 | BorderRadiusObject  | NO | ALL      | YES |

### Tooltip
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isFirstStep  | 是否为第一步 | boolean  | NO | ALL      | YES |
| isLastStep  | 是否为最后一步 | boolean  | NO | ALL      | YES |
| currentStep  | 当前步骤 | IStep  | YES | ALL      | YES |
| labels  |     提示框中显示的按钮文本（跳过、上一步、下一步、完成）     | Labels  | NO | ALL      | YES |
| handleNext  |  处理下一步的函数  | Function  | NO | ALL      | YES|
| handlePrev  | 处理上一步的函数 | Function  | NO | ALL      | YES|
| handleStop  | 处理停止的函数 | Function  | NO | ALL      | YES|

### TourGuideZoneByPosition
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| zone  |         | number  | YES | ALL      | YES |
| tourKey  |         | string  | NO | ALL      | YES |
| isTourGuide  | 如果为 false，则返回子组件而不进行包裹 | boolean  | NO | ALL      | YES |
| top  | 引导区域距离顶部的距离 | number/string  | NO | ALL      | YES |
| left  | 引导区域距离左侧的距离 | number/string  | NO | ALL      | YES |
| right  | 引导区域距离右侧的距离 | number/string  | NO | ALL      | YES |
| bottom  | 引导区域距离底部的距离 | number/string  | NO | ALL      | YES |
| width  | 遮罩层高亮区域的宽度  | number/string  | NO | ALL      | YES |
| height  | 遮罩层高亮区域的高度    | number/string  | NO | ALL      | YES |
| shape  |   形状    | Shape  | NO | ALL      | YES |
| borderRadiusObject  | 遮罩层高亮区域的圆角设置 | BorderRadiusObject  | NO | ALL      | YES |
| containerStyle  | 遮罩层包裹层样式 | StyleProp<ViewStyle>  | NO | ALL      | YES |
| keepTooltipPosition  |   提示框定位  | boolean  | NO | ALL      | YES |
| tooltipBottomOffset  | 提示框与容器底部的距离 | number  | NO | ALL      | YES |
| text  | 提示框中的文本 | string  | NO | ALL      | YES |

### useTourGuideController
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| start  | 开始引导     | Funtion  | YES | ALL      | YES |
| eventEmitter  | 事件发射器      | Funtion/undefined  | YES | ALL      | YES |
| getCurrentStep  | 获取遮罩层弹出组件 | Funtion/undefined  | YES | ALL      | YES |
| canStart  | 是否支持引导   | boolean/undefined  | YES | ALL      | YES |
| tourKey  | 引导键      | string  | YES | ALL      | YES |
| TourGuideZone  | 引导区域     | Funtion  | YES | ALL      | YES |
| TourGuideZoneByPosition  | 引导区域位置 | Funtion  | YES | ALL      | YES |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/xcarpentier/rn-tourguide/blob/master/LICENSE) ，请自由地享受和参与开源。

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-step-indicator</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/24ark/react-native-step-indicator">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/24ark/react-native-step-indicator/blob/master/LICENSE">
        <!-- <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" /> -->
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/24ark/react-native-step-indicator)

| 三方库版本   | 支持RN版本 |
| ----------- | ---------- |
| 1.0.3       |  0.72/0.77 |
	
对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-step-indicator@1.0.3 --save
```

#### **yarn**

```bash
yarn add react-native-step-indicator@1.0.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

#### Using a Component

```js
import * as React from 'react';
import { StyleSheet, View, Text } from 'react-native';
import StepIndicator from 'react-native-step-indicator';

const firstIndicatorStyles = {
  stepIndicatorSize: 30,
  currentStepIndicatorSize: 40,
  separatorStrokeWidth: 3,
  currentStepStrokeWidth: 5,
  separatorFinishedColor: '#4aae4f',
  separatorUnFinishedColor: '#a4d4a5',
  stepIndicatorFinishedColor: '#4aae4f',
  stepIndicatorUnFinishedColor: '#a4d4a5',
  stepIndicatorCurrentColor: '#ffffff',
  stepIndicatorLabelFontSize: 15,
  currentStepIndicatorLabelFontSize: 15,
  stepIndicatorLabelCurrentColor: '#000000',
  stepIndicatorLabelFinishedColor: '#ffffff',
  stepIndicatorLabelUnFinishedColor: 'rgba(255,255,255,0.5)',
  labelColor: '#666666',
  labelSize: 12,
  currentStepLabelColor: '#4aae4f',
};

const secondIndicatorStyles = {
  stepIndicatorSize: 30,
  currentStepIndicatorSize: 40,
  separatorStrokeWidth: 2,
  currentStepStrokeWidth: 3,
  stepStrokeCurrentColor: '#fe7013',
  stepStrokeWidth: 3,
  separatorStrokeFinishedWidth: 4,
  stepStrokeFinishedColor: '#fe7013',
  stepStrokeUnFinishedColor: '#aaaaaa',
  separatorFinishedColor: '#fe7013',
  separatorUnFinishedColor: '#aaaaaa',
  stepIndicatorFinishedColor: '#fe7013',
  stepIndicatorUnFinishedColor: '#ffffff',
  stepIndicatorCurrentColor: '#ffffff',
  stepIndicatorLabelFontSize: 13,
  currentStepIndicatorLabelFontSize: 13,
  stepIndicatorLabelCurrentColor: '#fe7013',
  stepIndicatorLabelFinishedColor: '#ffffff',
  stepIndicatorLabelUnFinishedColor: '#aaaaaa',
  labelColor: '#999999',
  labelSize: 13,
  currentStepLabelColor: '#fe7013',
};

const thirdIndicatorStyles = {
  stepIndicatorSize: 25,
  currentStepIndicatorSize: 30,
  separatorStrokeWidth: 2,
  currentStepStrokeWidth: 3,
  stepStrokeCurrentColor: '#7eaec4',
  stepStrokeWidth: 3,
  stepStrokeFinishedColor: '#7eaec4',
  stepStrokeUnFinishedColor: '#dedede',
  separatorFinishedColor: '#7eaec4',
  separatorUnFinishedColor: '#dedede',
  stepIndicatorFinishedColor: '#7eaec4',
  stepIndicatorUnFinishedColor: '#ffffff',
  stepIndicatorCurrentColor: '#ffffff',
  stepIndicatorLabelFontSize: 0,
  currentStepIndicatorLabelFontSize: 0,
  stepIndicatorLabelCurrentColor: 'transparent',
  stepIndicatorLabelFinishedColor: 'transparent',
  stepIndicatorLabelUnFinishedColor: 'transparent',
  labelColor: '#999999',
  labelSize: 13,
  currentStepLabelColor: '#7eaec4',
};

export default function App() {
  const [currentPage, setCurrentPage] = React.useState<number>(0);

  const onStepPress = (position: number) => {
    setCurrentPage(position);
  };

  const renderStepIndicator = (params: any) => (
    <Text>棒</Text>
  );

  const renderLabel = ({
    position,
    stepStatus,
    label,
    currentPosition,
  }: {
    position: number;
    stepStatus: string;
    label: string;
    currentPosition: number;
  }) => {
    return (      
      <Text
        style={
          position === currentPosition
            ? styles.stepLabelSelected
            : styles.stepLabel
        }
      >
        {label}
      </Text>
    );
  };

  return (
    <View style={styles.container}>
      <View style={styles.stepIndicator}>
        <StepIndicator
          customStyles={firstIndicatorStyles}
          currentPosition={currentPage}
          labels={['Account', 'Profile', 'Band', 'Membership', 'Dashboard']}
          renderLabel={renderLabel}
          onPress={onStepPress}
        />
      </View>
      <View style={styles.stepIndicator}>
        <StepIndicator
          customStyles={secondIndicatorStyles}
          currentPosition={currentPage}
          onPress={onStepPress}
          renderStepIndicator={renderStepIndicator}
          labels={[
            'Cart',
            'Delivery Address',
            'Order Summary',
            'Payment Method',
            'Track',
          ]}
        />
      </View>
      <View style={styles.stepIndicator}>
        <StepIndicator
          stepCount={4}
          customStyles={thirdIndicatorStyles}
          currentPosition={currentPage}
          onPress={onStepPress}
          labels={['Approval', 'Processing', 'Shipping', 'Delivery']}
        />
      </View>
      
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#ffffff',
  },
  stepIndicator: {
    marginVertical: 50,
  },
  page: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  stepLabel: {
    fontSize: 12,
    textAlign: 'center',
    fontWeight: '500',
    color: '#999999',
  },
  stepLabelSelected: {
    fontSize: 12,
    textAlign: 'center',
    fontWeight: '500',
    color: '#4aae4f',
  },
});
```

### 在 ArkTs 侧引入和注册字体文件(非必选配置项)

> [!TIP] 本项非必配项，当使用 customStyles 自定义属性中的 labelFontFamily 属性指定字体时才需配置

步骤一：
复制字体文件到 `entry/src/main/resources/rawfile/assets/assets/fonts` 目录下(如使用了外部字体文件，需要将\*.ttf 文件复制过来)

步骤二：
打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

    const fonts: Record<string, Resource> = {
      "Pacifico-Regular": $rawfile("assets/assets/fonts/Pacifico-Regular.ttf")
    }

    @Entry
    @Component
    struct Index {
      //...
      build() {
        Column(){
          //...

          //注册字体文件
          RNApp({
            rnInstanceConfig: {
              //...
              fontResourceByFontFamily: fonts
            },
            //...
          })

        }
        //...
      }
    }

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; OH SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio: 5.0.3.400; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Default | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |------------ |
| currentPosition  | 步骤中的当前位置         | number  |    no    | 0 |  iOS,Android  |         yes        |
| stepCount  | 步骤数量         | number  |    no    | 5 |  iOS,Android  |         yes        |
| direction  | 步骤的方向         | 'horizontal' \| 'vertical'  |    no    | 'horizontal' |  iOS,Android  |         yes        |
| customStyles  | 组件的样式         | object  |    no    | {} |  iOS,Android  |         yes        |
| labels  | 每个步骤的标签         | Array\<string\>  |    no    | null |  iOS,Android  |         yes        |
| onPress  | 点击步骤时触发的回调         | Function (position: Number) => void |    no    | null |  iOS,Android  |         yes        |
| renderStepIndicator  | 用于在指定位置的步骤内渲染自定义内容         | Function (position: Number, stepStatus: String) => React.ReactNode |    no    | null |  iOS,Android  |         yes        |
| renderLabel  | 使用此属性为每个步骤渲染自定义标签         | Function (position: Number, stepStatus: String, label: String, currentPosition: Number) => React.ReactNode |    no    | null |  iOS,Android  |         yes        |

### Custom Styles
| Name | Description | Type | Required | Default | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |------------ |
| stepIndicatorSize  |    步骤指示器圆圈的大小    | number  |    no    | 30 |  iOS,Android  |         yes        |
| currentStepIndicatorSize  |    	当前步骤指示器圆圈的大小    | number  |    no    | 40 |  iOS,Android  |         yes        |
| separatorStrokeWidth  |    步骤间分隔线的描边粗细    | number  |    no    | 2 |  iOS,Android  |         yes        |
| separatorStrokeUnfinishedWidth  |    未完成步骤间分隔线的描边粗细    | number  |    no    | 0 |  iOS,Android  |         yes        |
| separatorStrokeFinishedWidth  |    已完成步骤间分隔线的描边粗细    | number  |    no    | 0 |  iOS,Android  |         yes        |
| stepStrokeWidth  |    每个步骤周围描边的粗细    | number  |    no    | 3 |  iOS,Android  |         yes        |
| currentStepStrokeWidth  |    当前步骤周围描边的粗细    | number  |    no    | 3 |  iOS,Android  |         yes        |
| stepStrokeCurrentColor  |    当前步骤的描边颜色     | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| stepStrokeFinishedColor  |    已完成步骤的描边颜色    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| stepStrokeUnFinishedColor  |    未完成步骤的描边颜色    | string  |    no    | '#aaaaaa' |  iOS,Android  |         yes        |
| separatorFinishedColor  |    已完成项目的分隔线颜色    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| separatorUnFinishedColor  |    未完成项目的分隔线颜色    | string  |    no    | '#aaaaaa' |  iOS,Android  |         yes        |
| stepIndicatorFinishedColor  |    	已完成步骤圆圈的颜色    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| stepIndicatorUnFinishedColor  |    	未完成步骤圆圈的颜色    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorCurrentColor  |    当前步骤圆圈的颜色    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorLabelFontSize  |    每个步骤圆圈内数字的字体大小    | number  |    no    | 15 |  iOS,Android  |         yes        |
| currentStepIndicatorLabelFontSize  |    当前步骤圆圈内数字的字体大小    | number  |    no    | 15 |  iOS,Android  |         yes        |
| stepIndicatorLabelCurrentColor  |    当前步骤标签的颜色   | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorLabelFinishedColor  |    已完成步骤标签的颜色    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorLabelUnFinishedColor  |    未完成步骤标签的颜色    | string  |    no    | 'rgba(255,255,255,0.5)' |  iOS,Android  |         yes        |
| labelColor  |    标签文本的颜色    | string  |    no    | '#000000' |  iOS,Android  |         yes        |
| currentStepLabelColor  |    当前步骤标签的颜色    | string  |    no    | '#4aae4f' |  iOS,Android  |         yes        |
| labelSize  |    标签的字体大小    | number  |    no    | 13 |  iOS,Android  |         yes        |
| labelAlign  |    	标签对齐方式    | 'center' \| 'flex-start' \| 'flex-end' \| 'stretch' \| 'baseline' \| undefined  |    no    | 'center' |  iOS,Android  |         yes        |
| labelFontFamily  |    自定义字体的标签字体族    | string  |    no    |   |  iOS,Android  |         yes        |


## 遗留问题

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/24ark/react-native-step-indicator/blob/master/LICENSE) ，请自由地享受和参与开源。

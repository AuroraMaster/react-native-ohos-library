> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-ratings</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Monte9/react-native-ratings">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Monte9/react-native-ratings/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/Monte9/react-native-ratings/tree/v8.1.0)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| :--- | :--- |
| 8.1.0 | 0.72/0.77 |

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-ratings@8.1.0
```

#### **yarn**

```bash
yarn add react-native-ratings@8.1.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from 'react';
import { View, Text, StyleSheet } from 'react-native';
import { Rating, AirbnbRating } from 'react-native-ratings';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f2f2f2',
  },
  title: {
    fontSize: 18,
    fontWeight: 'bold',
    marginTop: 20,
    marginBottom: 10,
  }
});

export function RatingsDemo () {
  const [rating, setRating] = useState(3);

  const ratingCompleted = (rating: number) => {
    console.log("Rating is: " + rating);
    setRating(rating);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Standard Rating</Text>
      <Rating
        type="star"
        ratingCount={5}
        imageSize={30}
        showRating
        onFinishRating={ratingCompleted}
      />

      <Text style={styles.title}>Custom Icon Rating</Text>
      <Rating
        type="custom"
        ratingImage={require('../assets/expo.png')}
        ratingColor="#3498db"
        ratingBackgroundColor="#c8c7c8"
        ratingCount={6}
        imageSize={40}
        onFinishRating={ratingCompleted}
        style={{ paddingVertical: 10 }}
      />

      <Text style={styles.title}>Airbnb Rating</Text>
      <AirbnbRating
        count={5}
        reviews={["Terrible", "Bad", "Okay", "Good", "Great"]}
        defaultRating={3}
        size={20}
        onFinishRating={ratingCompleted}
      />

      <Text style={styles.title}>Read-only Rating</Text>
      <Rating
        readonly
        startingValue={rating}
        ratingCount={5}
        imageSize={30}
      />

      <Text style={styles.title}>Fractional Rating</Text>
      <Rating
        fractions={2}
        startingValue={2.5}
        ratingCount={5}
        imageSize={30}
        onFinishRating={ratingCompleted}
      />
    </View>
  );
};

```

## 约束与限制

#### 兼容性

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

### 此组件有以下属性:
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|           Name            |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **type**     |       选择内置类型之一：star、rocket、bell、heart，或者使用 type='custom' 来渲染自定义图片（可选）。        |                         String                           |    No    | iOS/Android |        Yes        |
|     **ratingImage**             |                   传入自定义图片资源；需配合上述 type='custom' 属性使用（可选）。                   |                         String                           |    No    | iOS/Android |        Yes        |
|      **ratingColor**       |                 传入评分图标的自定义填充颜色；需配合上述 type='custom' 属性使用（可选）。              |                         String                           |    No    | iOS/Android |        Yes        |
|  **ratingBackgroundColor**   |       传入评分图标的自定义背景填充颜色；需配合上述 type='custom' 属性使用（可选）。      |                         String                           |    No    | iOS/Android |        Yes        |
|     **tintColor**     |       用于改变评分图标背景的颜色（可选）。        |                         String                           |    No    | iOS/Android |        Yes        |
|     **ratingCount**     |       显示的评分图片数量（可选）。        |                         number                           |    No    | iOS/Android |        Yes        |
|     **ratingTextColor**     |       	文本标签的颜色。         |                         String                           |    No    | iOS/Android |        Yes        |
|     **imageSize**     |       每个评分图片的大小（可选）。         |                         number                           |    No    | iOS/Android |        Yes        |
|     **showRating**     |       显示内置的评分 UI 以实时展示评分值（可选）。         |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **readonly**     |       用户是否可以修改评分。         |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **startingValue**     |       渲染时的初始评分。        |                         number                           |    No    | iOS/Android |        Yes        |
|     **fractions**     |       评分值的小数位数；必须在 0 到 20 之间。         |                         number                           |    No    | iOS/Android |        Yes        |
|     **minValue**     |       用户可以选择的最小值。         |                         number                           |    No    | iOS/Android |        Yes        |
|     **style**     |       暴露样式属性以向容器视图添加额外样式（可选）。         |                         style                           |    No    | iOS/Android |        Yes        |
|     **jumpValue**     |       评分值变化时的跳跃值（如果 jumpValue === 0.5，评分值将按 0, 0.5, 1.0, 1.5... 增减）。默认为 0（不跳跃）。        |                         number                           |    No    | iOS/Android |        Yes        |
|     **onStartRating**     |       用户开始评分时的回调方法。提供整数形式的开始评分值。         |                         function                           |    No    | iOS/Android |        Yes        |
|     **onSwipeRating**     |       用户滑动时的回调方法。提供整数形式的当前评分值。         |                         function                           |    No    | iOS/Android |        Yes        |
|     **onFinishRating**     |       用户完成评分时的回调方法。提供整数形式的最终评分值（必填）。         |                         function                           |    Yes   | iOS/Android |        Yes        |

## **API（AirbnbRating）**
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|           Name            |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **defaultRating**   |           评分的初始值。           |                         number                           |    No    | iOS/Android |        Yes        |
|     **reviews**  |   点击每个值时显示的标签，例如：如果点击了第一颗星，则使用索引 0 处的值作为标签。  |                         string                           |    No    | iOS/Android |        Yes        |
|     **count**  |   显示的评分总数。  |                         number                           |    No    | iOS/Android |        Yes        |
|     **selectedColor**  |   传入评分图标的自定义填充颜色。  |                         string                           |    No    | iOS/Android |        Yes        |
|     **unSelectedColor**  |   传入评分图标的自定义未填充颜色。  |                         string                           |    No    | iOS/Android |        Yes        |
|     **reviewColor**  |   传入评分文本的自定义颜色。  |                         string                           |    No    | iOS/Android |        Yes        |
|     **size**  |   每个评分图片的大小（可选）。  |                         number                           |    No    | iOS/Android |        Yes        |
|     **reviewSize**  |   传入评论文本的自定义字体大小。  |                         number                           |    No    | iOS/Android |        Yes        |
|     **showRating**  |   决定是否在评分上方显示评论。  |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **isDisabled**  |   用户是否可以修改评分。  |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **onFinishRating**  |   用户完成评分时的回调方法。提供整数形式的最终评分值。  |                         function                           |    No    | iOS/Android |        Yes        |
|     **starContainerStyle**  |   应用于星星容器的自定义样式。  |                         object                            |    No    | iOS/Android |        Yes        |
|     **ratingContainerStyle**  |   应用于评分容器的自定义样式。  |                         object                            |    No    | iOS/Android |        Yes        |
|     **starImage**  |   传入自定义基础图片资源（可选）。  |                         string                           |    No    | iOS/Android |        Yes        |
|     **starStyle**  |   应用于星星的自定义样式（可选）。  |                         object                           |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/Monte9/react-native-ratings/blob/master/LICENSE) ，请自由地享受和参与开源。
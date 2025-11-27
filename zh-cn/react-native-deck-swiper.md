> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-deck-swiper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alexbrillant/react-native-deck-swiper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/alexbrillant/react-native-deck-swiper/blob/master/LICENSE">
         <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/alexbrillant/react-native-deck-swiper)

## 安装与使用

| Version| Version for RN |
| ---------- | ---------- |
| 2.0.17     | 0.72/0.77  |

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-deck-swiper@2.0.17
```

#### **yarn**

```bash
yarn add react-native-deck-swiper@2.0.17
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component, useState } from 'react'
import Swiper from 'react-native-deck-swiper'
import { Button, StyleSheet, Text, View, ScrollView } from 'react-native'

function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield i
  }
}

export default class DeckSwiperExample extends Component {

  constructor(props) {
    super(props)
    this.state = {
      cards: [...range(1, 10)],
      swipedAllCards: false,
      swipeDirection: '操作卡片滑动，此处显示滑动方向',
      cardIndex: 0,
      //是否显示下一张卡片
      showSecondCardState:true,
      //卡片移动时候的索引
      indexWhenmove:'请移动卡片',
      positionWhenmove:'请移动卡片',
      dragStartState:'拖动开始触发',
      dragEndState:'拖动结束触发'
    }
  }

  renderCard = (card, index) => {
    return (
      <View style={styles.card}>
        <Text style={styles.text}>{card} - {index}</Text>
      </View>
    )
  };

  onSwiped = (type) => {
    console.log(`on swiped ${type}`)
  }

  onSwipedAllCards = () => {
    this.setState({
      swipedAllCards: this.state.swipedAllCards = true
    })
  };

  //轻触时，卡片滑动的方向
  swipeLeft = () => {
    this.swiper.swipeLeft()
  };
  swipeRight = () => {
    this.swiper.swipeRight()
  };
  swipeTop = () => {
    this.swiper.swipeTop()
  };
  swipeBottom = () => {
    this.swiper.swipeBottom()
  };
  //卡片拖动时，调用的函数
  Swiping = (index, position) => {
    this.setState({
      ...this.props,
      indexWhenmove:index,
      positionWhenmove:position
    })
  };
  //拖动开始时候要调用的函数
  dragStart = () => {
    this.setState({
      ...this.props,
      dragStartState:'拖动已经开始了！！！！'
    })
  } 
  //拖动结束时候要调用的函数
  dragEnd = () => {
    this.setState({
      ...this.props,
      dragEndState:'拖动已经结束了！！！！'
    })
  } 

  //显示堆叠卡片
  useShowSecondCard = () =>{
    this.setState({
      ...this.props,
      showSecondCardState:true
    })
  }
  //不显示堆叠卡片
  disuseShowSecondCard = () =>{
    this.setState({
      ...this.props,
      showSecondCardState:false
    })
  }
  //显示堆叠卡片
  useShowSecondCard = () =>{
      this.setState({
        ...this.props,
        showSecondCardState:true
      })
  }

  render() {
    return (
              <Text>该整体效果涉及属性和接口</Text>
              <Text>onSwiped,滑动方向：{this.state.swipeDirection}</Text>
              <Text>onTapCard,轻触时，卡片调用的函数:这里设置的是swipeLeft向左滑动</Text>
              <Text>onSwipedAllCards,刷卡时候调用的函数,刷卡完毕置位true.刷卡完毕的情况下使用'回退按键',该状态不会重置:{JSON.stringify(this.state.swipedAllCards)}</Text>
              <Text>onSwiping,卡片移动时触发的回调: Swiping card at index {this.state.indexWhenmove}, position: {this.state.positionWhenmove}</Text>
              <Text>dragStart,卡片开始拖动时候触发的回调:{this.state.dragStartState}</Text>
              <Text>dragEnd,卡片拖动结束时候触发的回调:{this.state.dragEndState}</Text>
              <View style={styles.container}>
                <Swiper
                  ref={swiper => {
                    this.swiper = swiper
                  }}
                  //滑动方向
                  onSwiped={() => this.setState({ swipeDirection: this.state.swipeDirection = 'general' })}
                  onSwipedLeft={() => this.setState({ swipeDirection: this.state.swipeDirection = 'left' })}
                  onSwipedRight={() => this.setState({ swipeDirection: this.state.swipeDirection = 'right' })}
                  onSwipedTop={() => this.setState({ swipeDirection: this.state.swipeDirection = 'top' })}
                  onSwipedBottom={() => this.setState({ swipeDirection: this.state.swipeDirection = 'bottom' })}
                  //轻触卡时要调用的函数，这里是向左滑动
                  onTapCard={this.swipeLeft}
                  //需要渲染的卡片组，必填
                  cards={this.state.cards}
                  //首张卡片，这里为设置为0
                  cardIndex={this.state.cardIndex}
                  //卡片的垂直边距，默认为60
                  cardVerticalMargin={200}
                  //卡片的水平边距，默认为20
                  cardHorizontalMargin={80}
                  //卡片渲染的参数，必填
                  renderCard={this.renderCard}
                  //卡片移动时触发的回调
                  onSwiping={this.Swiping}
                  //当卡片滑完后触发的回调
                  onSwipedAll={this.onSwipedAllCards}
                  //拖动开始触发的函数
                  dragStart={this.dragStart}
                  //拖动结束触发的函数
                  dragEnd={this.dragEnd}
                  //显示堆叠卡片,只有当showSecondCard为true的时候,才会生效
                  stackSize={3}
                  //卡之间的垂直间隔f,具体表现为卡片的堆叠样式,例如此处为-100，成多米诺形式
                  stackSeparation={20}
                  //是否显示第二张卡
                  showSecondCard={this.state.showSecondCardState}
                  //滑动覆盖标签，滑动时候卡片上的覆盖样式
                  overlayLabels={{
                    bottom: {
                      title: '向下',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'center',
                          justifyContent: 'center'
                        }
                      }
                    },
                    left: {
                      title: '向左',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'flex-end',
                          justifyContent: 'flex-start',
                          marginTop: 30,
                          marginLeft: -30
                        }
                      }
                    },
                    right: {
                      title: '向右',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'flex-start',
                          justifyContent: 'flex-start',
                          marginTop: 30,
                          marginLeft: 30
                        }
                      }
                    },
                    top: {
                      title: '向上',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'center',
                          justifyContent: 'center'
                        }
                      }
                    }
                  }}
                  //动画卡覆盖标签不透明度，默认为false
                  animateOverlayLabelsOpacity
                  animateCardOpacity
                  //回退卡片动画
                  swipeBackCard
                  //背景图
                  containerStyle={
                    {
                        height: 700,
                        zIndex: 0,
                        position: 'absolute',
                        top: 0,
                        left: 0,
                    }}
                >
                  <Button onPress={() => this.swiper.swipeBack()} title='Swipe Back' />
                  <Button onPress={() => this.useShowSecondCard()} title='显示堆叠卡片(默认为堆叠；重置后，需要滑动一张卡片生效)' />
                  <Button onPress={() => this.disuseShowSecondCard()} title='不显示堆叠卡片(点击后，需要滑动一张卡片生效)' />
                </Swiper>
              </View>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
    width: '100%',
    height: '700',
    display: 'flex', 
    position: 'relative'
  },
  card: {
    flex: 1,
    borderRadius: 4,
    borderWidth: 2,
    borderColor: '#E8E8E8',
    justifyContent: 'center',
    backgroundColor: 'white',
  },
  text: {
    textAlign: 'center',
    fontSize: 50,
    backgroundColor: 'transparent'
  },
  done: {
    textAlign: 'center',
    fontSize: 30,
    color: 'white',
    backgroundColor: 'transparent'
  }
})

export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 5.1.0.150 (API Version 12); IDE：DevEco Studio 5.1.1.830; ROM：5.1.0.150;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Card props

| Name            | Description                                                  | Type                      | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------------------- | -------- | ----------- | ----------------- |
| cards           | 要渲染的卡片数据数组                   | array                     | yes      | iOS/Android | yes               |
| renderCard      | 基于数据渲染卡片的函数                | func(cardData, cardIndex) | yes      | iOS/Android | yes               |
| keyExtractor    | 获取卡片react key的函数                         | func(cardData)            | no       | iOS/Android | yes               |
| cardIndex       | 起始卡片索引                                      | number                    | no       | iOS/Android | yes               |
| infinite        | 无限滑动                                    | bool                      | no       | iOS/Android | yes               |
| horizontalSwipe | 启用/禁用水平滑动                            | bool                      | no       | iOS/Android | yes               |
| verticalSwipe   | 启用/禁用垂直滑动                              | bool                      | no       | iOS/Android | yes               |
| showSecondCard  | 滑动时启用/禁用显示第二张卡片                     | bool                      | no       | iOS/Android | yes               |
| stackSize       | 要显示的底层卡片数量（必须启用showSecondCard） | number                    | no       | iOS/Android | yes               |

### Swipe animation props

| Name                   | Description                     | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------- | ------ | -------- | ----------- | ----------------- |
| verticalThreshold      | 垂直滑动阈值        | number | no       | iOS/Android | yes               |
| horizontalThreshold    | 水平滑动阈值      | number | no       | iOS/Android | yes               |
| swipeAnimationDuration | 滑动动画持续时间 | number | no       | iOS/Android | yes               |
| disableBottomSwipe     | 禁用向下滑动            | bool   | no       | iOS/Android | yes               |
| disableLeftSwipe       | 禁用向左滑动              | bool   | no       | iOS/Android | yes               |
| disableRightSwipe      | 禁用向右滑动             | bool   | no       | iOS/Android | yes               |
| disableTopSwipe        | 禁用向上滑动               | bool   | no       | iOS/Android | yes               |

### Stack props

| Name                   | Description                                            | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| stackSeparation        | 底层卡片之间的垂直间距          | number | no       | iOS/Android | yes               |
| stackScale             | 每个底层卡片尺寸缩小的百分比 | number | no       | iOS/Android | yes               |
| stackAnimationFriction | 弹簧动画摩擦系数（弹性）                 | number | no       | iOS/Android | yes               |
| stackAnimationTension  | 弹簧动画张力（速度）                       | number | no       | iOS/Android | yes               |

### Rotation animation props

| Name                | Description                                            | Type  | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------ | ----- | -------- | ----------- | ----------------- |
| inputRotationRange  | 旋转输出对应的x值范围                 | array | no       | iOS/Android | yes               |
| outputRotationRange | inputRotationRange中x值对应的旋转值 | array | no       | iOS/Android | yes               |

### Opacity animation props

| Name                              | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| animateCardOpacity                | 启用卡片透明度动画                                         | bool   | no       | iOS/Android | yes               |
| inputCardOpacityRangeX            | 平移X轴卡片透明度输入范围                               | array  | no       | iOS/Android | yes               |
| outputCardOpacityRangeX           | inputCardOpacityRangeX值对应的透明度      | array  | no       | iOS/Android | yes               |
| inputCardOpacityRangeY            | 平移Y轴卡片透明度输入范围                               | array  | no       | iOS/Android | yes               |
| outputCardOpacityRangeY           | inputCardOpacityRangeY值对应的透明度      | array  | no       | iOS/Android | yes               |
| animateOverlayLabelsOpacity       | 启用卡片覆盖标签透明度动画                          | bool   | no       | iOS/Android | yes               |
| inputOverlayLabelsOpacityRangeX   | 平移X轴覆盖标签透明度输入范围                     | array  | no       | iOS/Android | yes               |
| outputOverlayLabelsOpacityRangeX  | inputOverlayLabelsOpacityRangeX值对应的透明度 | array  | no       | iOS/Android | yes               |
| inputOverlayLabelsOpacityRangeY   | 平移X轴覆盖标签透明度输入范围                     | array  | no       | iOS/Android | yes               |
| outputOverlayLabelsOpacityRangeY  | inputOverlayLabelsOpacityRangeY值对应的透明度 | array  | no       | iOS/Android | yes               |
| overlayOpacityVerticalThreshold   | 覆盖标签的垂直阈值                         | number | no       | iOS/Android | yes               |
| overlayOpacityHorizontalThreshold | 覆盖标签的水平阈值                       | number | no       | iOS/Android | yes               |

### Swipe overlay labels

| Name                     | Description                  | Type   | Required | Platform    | HarmonyOS Support |
| ------------------------ | ---------------------------- | ------ | -------- | ----------- | ----------------- |
| overlayLabels            | 滑动标签的标题和样式 | object | no       | iOS/Android | yes               |
| overlayLabelStyle        | 滑动标签样式           | object | no       | iOS/Android | yes               |
| overlayLabelWrapperStyle | 覆盖标签包装器样式  | object | no       | iOS/Android | yes               |

### Swipe back to previous card props

| Name                              | Description                               | Type | Required | Platform    | HarmonyOS Support |
| --------------------------------- | ----------------------------------------- | ---- | -------- | ----------- | ----------------- |
| goBackToPreviousCardOnSwipeLeft   | 向左滑动时渲染上一张卡片   | bool | no       | iOS/Android | yes               |
| goBackToPreviousCardOnSwipeRight  | 向右滑动时渲染上一张卡片  | bool | no       | iOS/Android | yes               |
| goBackToPreviousCardOnSwipeTop    | 向上滑动时渲染上一张卡片    | bool | no       | iOS/Android | yes               |
| goBackToPreviousCardOnSwipeBottom | 向下滑动时渲染上一张卡片 | bool | no       | iOS/Android | yes               |

### Style props

| Name                 | Description                                               | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | --------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| backgroundColor      | 包含卡片的视图的背景颜色        | string | no       | iOS/Android | yes               |
| marginTop            | 滑动容器上边距                        | number | no       | iOS/Android | yes               |
| marginBottom         | 滑动容器下边距                     | number | no       | iOS/Android | yes               |
| cardVerticalMargin   | 卡片垂直边距                                      | number | no       | iOS/Android | yes               |
| cardHorizontalMargin | 卡片水平边距                                    | number | no       | iOS/Android | yes               |
| childrenOnTop        | 是否在顶部渲染子组件                             | bool   | no       | iOS/Android | yes               |
| cardStyle            | 重写可滑动卡片样式                              | node   | no       | iOS/Android | yes               |
| containerStyle       | 容器样式覆盖                        | node   | no       | iOS/Android | yes               |
| pointerEvents        | 容器的pointerEvents属性                     | string | no       | iOS/Android | yes               |
| useViewOverflow      | 对Swiper组件使用ViewOverflow而不是View | bool   | no       | iOS/Android | yes               |

### Swipe back Props

| Name                         | Description                                                 | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ----------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| previousCardDefaultPositionX | 卡片滑回牌堆时的动画起始位置X | number | no       | iOS/Android | yes               |
| previousCardDefaultPositionY | 卡片滑回牌堆时的动画起始位置Y | number | no       | iOS/Android | yes               |
| stackAnimationFriction       | 弹簧动画摩擦系数（弹性）                      | number | no       | iOS/Android | yes               |
| stackAnimationTension        | 弹簧动画张力（速度）                            | number | no       | iOS/Android | yes               |
| swipeBackCard                | 渲染滑动返回卡片，以便进行动画处理             | bool   | no       | iOS/Android | yes               |

## 事件回调

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                  | Type | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ---- | -------- | ----------- | ----------------- |
| onSwipedAll       | 所有卡片都被滑动后调用的函数        | func | no       | iOS/Android | yes               |
| onSwiped          | 卡片被滑动时调用的函数。接收被滑动卡片的索引 | func | no       | iOS/Android | yes               |
| onSwipedAborted   | 卡片在达到阈值前被释放时调用的函数 | func | no       | iOS/Android | yes               |
| onSwipedLeft      | 卡片向左滑动时调用的函数。接收被滑动卡片的索引 | func | no       | iOS/Android | yes               |
| onSwipedRight     | 卡片向右滑动时调用的函数。接收被滑动卡片的索引 | func | no       | iOS/Android | yes               |
| onSwipedTop       | 卡片向上滑动时调用的函数。接收被滑动卡片的索引 | func | no       | iOS/Android | yes               |
| onSwipedBottom    | 卡片向下滑动时调用的函数。接收被滑动卡片的索引 | func | no       | iOS/Android | yes               |
| onSwiping         | 卡片被移动时调用的函数。接收X和Y位置 | func | no       | iOS/Android | yes               |
| dragStart         | 拖动开始时调用的函数                        | func | no       | iOS/Android | yes               |
| dragEnd           | 拖动结束时调用的函数                          | func | no       | iOS/Android | yes               |
| onTapCard         | 点击卡片时调用的函数。接收被点击卡片的索引 | func | no       | iOS/Android | yes               |
| onTapCardDeadZone | 点击不再被识别为点击前的最大移动量 | func | no       | iOS/Android | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                           | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------- | -------- | -------- | ----------- | ----------------- |
| swipeBack       | 将最后滑出的卡片滑回牌堆 | callback | no       | iOS/Android | yes               |
| swipeLeft       | 向左滑动到下一张卡片           | callback | no       | iOS/Android | yes               |
| swipeRight      | 向右滑动到下一张卡片          | callback | no       | iOS/Android | yes               |
| swipeTop        | 向上滑动到下一张卡片            | callback | no       | iOS/Android | yes               |
| swipeBottom     | 向下滑动到下一张卡片         | callback | no       | iOS/Android | yes               |
| jumpToCardIndex | 设置当前卡片索引            | callback | no       | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/alexbrillant/react-native-deck-swiper/blob/master/LICENSE) ，请自由地享受和参与开源。

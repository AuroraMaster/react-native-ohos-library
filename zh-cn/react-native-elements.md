> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-elements</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-elements/react-native-elements">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-elements/react-native-elements/blob/next/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-elements/react-native-elements/tree/v4.0.0-rc.8)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 4.0.0-rc.8 | 0.72/0.77  |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @rneui/themed@4.0.0-rc.8
npm install @rneui/base@4.0.0-rc.7
```

#### **yarn**

```bash
yarn add @rneui/themed@4.0.0-rc.8
yarn add @rneui/base@4.0.0-rc.7
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React from 'react';
import { View, ScrollView, StyleSheet } from 'react-native';
import { Avatar } from '@rneui/themed';
import { Text } from '@rneui/base';

type AvatarData = {
  image_url: string;
};

const styles = StyleSheet.create({
  titleStyle: {
    fontWeight: 'bold',
    fontSize: 24,
  },
  subTitleStyle: {
    fontWeight: 'bold',
    fontSize: 18,
  },
  normalTitle: {
    fontWeight: 'bold',
    fontSize: 15,
  }
});

const dataList: AvatarData[][] = 
[
  [
    {
      image_url: 'https://api.uifaces.co/our-content/donated/xZ4wg2Xj.jpg',
    },
    {
      image_url: 'https://randomuser.me/api/portraits/men/36.jpg',
    },
    {
      image_url: 'https://cdn.pixabay.com/photo/2019/11/03/20/11/portrait-4599553__340.jpg',
    }
  ],
  [
    {
      image_url: 'https://cdn.pixabay.com/photo/2014/09/17/20/03/profile-449912__340.jpg',
    },
    {
      image_url: 'https://cdn.pixabay.com/photo/2020/09/18/05/58/lights-5580916__340.jpg',
    },
    {
      image_url: 'https://cdn.pixabay.com/photo/2016/11/21/12/42/beard-1845166_1280.jpg',
    }
  ]
];

type AvatarComponentProps = {};

const Avatars: React.FunctionComponent<AvatarComponentProps> = () => {
  return (
    <>
      <Text style={styles.titleStyle}>Avatars</Text>
      <ScrollView>
        <Text style={styles.subTitleStyle}>Photo Avatars</Text>
        {dataList.map((chunk, chunkIndex) => (
          <View
            style={{
              flexDirection: 'row',
              justifyContent: 'space-around',
              marginBottom: 30,
            }}
            key={chunkIndex}
          >
            {chunk.map((l, i) => (
              <Avatar
                size={64}
                rounded
                source={l.image_url ? { uri: l.image_url } : {}}
                key={`${chunkIndex}-${i}`}
              />
            ))}
          </View>
        ))}
        <Text style={styles.subTitleStyle}>Icon Avatars</Text>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 30,
          }}
        >
          <Avatar
            size={64}
            rounded
            icon={{ name: 'pencil', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: '#6733b9' }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'rocket', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: '#00a7f7' }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'heartbeat', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: '#eb1561' }}
          />
        </View>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 30,
          }}
        >
          <Avatar
            size={64}
            rounded
            icon={{
              name: 'users',
              type: 'font-awesome',
              color: '#cdde20',
            }}
            containerStyle={{
              borderColor: 'grey',
              borderStyle: 'solid',
              borderWidth: 1,
            }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'bank', type: 'font-awesome', color: '#009688' }}
            containerStyle={{
              borderColor: 'grey',
              borderStyle: 'solid',
              borderWidth: 1,
            }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'apple', type: 'font-awesome', color: '#ff5606' }}
            containerStyle={{
              borderColor: 'grey',
              borderStyle: 'solid',
              borderWidth: 1,
            }}
          />
        </View>

        <Text style={styles.subTitleStyle}>Letter Avatars</Text>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 30,
          }}
        >
          <Avatar
            size={64}
            rounded
            title="Fc"
            containerStyle={{ backgroundColor: '#3d4db7' }}
          />
          <Avatar
            size={64}
            rounded
            title="P"
            containerStyle={{ backgroundColor: 'coral' }}
          />
          <Avatar
            size={64}
            rounded
            title="Rd"
            containerStyle={{ backgroundColor: 'purple' }}
          />
        </View>

        <Text style={styles.subTitleStyle}>Badged Avatars</Text>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 40,
          }}
        >
          <Avatar
            size={64}
            rounded
            icon={{ name: 'pencil', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: 'orange' }}
          >
            <Avatar.Accessory size={24} />
          </Avatar>
          <Avatar
            size={64}
            rounded
            source={{ uri: 'https://randomuser.me/api/portraits/women/57.jpg' }}
            containerStyle={{ backgroundColor: 'grey' }}
          >
            <Avatar.Accessory size={23} />
          </Avatar>
        </View>
      </ScrollView>
    </>
  );
};

export default Avatars;
```

## Link

本库 HarmonyOS 侧实现依赖 @react-native-oh-tpl/react-native-safe-area-context ，@react-native-oh-tpl/react-native-linear-gradient的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-safe-area-context 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-safe-area-context.md#link)，[@react-native-oh-tpl/react-native-linear-gradient 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-linear-gradient.md#link)进行引入。

### 在 ArkTs 侧引入和注册字体文件

步骤一：
    复制字体文件到  `entry\src\main\resources\rawfile\fonts` 目录下(如使用了外部字体文件，需要将*.ttf文件复制过来)

步骤二：
    打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```ts
  build() {
    Column() {
      if (this.rnohCoreContext && this.shouldShow) {
        if (this.rnohCoreContext?.isDebugModeEnabled) {
          RNOHErrorDialog({ ctx: this.rnohCoreContext })
        }
        RNApp({
          rnInstanceConfig: {
              fontResourceByFontFamily: {
              'anticon': $rawfile('fonts/AntDesign.ttf'),
              'Entypo': $rawfile('fonts/Entypo.ttf'),
              'EvilIcons': $rawfile('fonts/EvilIcons.ttf'),
              'Feather': $rawfile('fonts/Feather.ttf'),
              'FontAwesome': $rawfile('fonts/FontAwesome.ttf'),
              'FontAwesome5Brands-Regular': $rawfile('fonts/FontAwesome5_Brands.ttf'),
              'FontAwesome5Free-Regular': $rawfile('fonts/FontAwesome5_Regular.ttf'),
              'FontAwesome5Free-Solid': $rawfile('fonts/FontAwesome5_Solid.ttf'),
              'FontAwesome6Brands-Regular': $rawfile('fonts/FontAwesome6_Brands.ttf'),
              'FontAwesome6Free-Regular': $rawfile('fonts/FontAwesome6_Regular.ttf'),
              'FontAwesome6Free-Solid': $rawfile('fonts/FontAwesome6_Solid.ttf'),
              'Fontisto': $rawfile('fonts/Fontisto.ttf'),
              'fontcustom': $rawfile('fonts/Foundation.ttf'),
              'Ionicons': $rawfile('fonts/Ionicons.ttf'),
              'Material Design Icons': $rawfile('fonts/MaterialCommunityIcons.ttf'),
              'Material Icons': $rawfile('fonts/MaterialIcons.ttf'),
              'Octicons': $rawfile('fonts/Octicons.ttf'),
              'simple-line-icons': $rawfile('fonts/SimpleLineIcons.ttf'),
              'zocial': $rawfile('fonts/Zocial.ttf'),
            }
        })
      }
    }
    .height('100%')
    .width('100%')
  }
```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.22;
2. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.700; ROM：3.0.0.60;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
4. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;
## 组件

详细请查看 [react-native-elements的文档介绍](https://reactnativeelements.com)

以下为目前已支持的组件属性：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**AirbnbRating**：爱彼迎风格的评级组件

|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        count         | 显示默认的评级总数是5        |        number         |    No    |   All    |        Yes        |
|    defaultRating     | 默认评分是3           |        number         |    No    |   All    |        Yes        |
|      isDisabled      | 用户是否可以修改评分 默认值为 false |        boolean        |    No    |   All    |        Yes        |
|    onFinishRating    | 用户完成评分时的回调方法。该方法会以整数形式返回最终评分值 | (number: any) => void |    No    |   All    |        Yes        |
| ratingContainerStyle | 容器评分样式默认为无           |      View Style       |    No    |   All    |        Yes        |
|     reviewColor      | 预览视图的颜色值。默认值为#f1c40f             |        string         |    No    |   All    |        Yes        |
|      reviewSize      | 预览视图的尺寸值。默认值为40                  |        number         |    No    |   All    |        Yes        |
|       reviews        | 显示每个值何时被点击的标签。例如，如果第一个星被点击，则索引0中的值将用作标签。默认值为 ['Terrible', 'Bad', 'Okay', 'Good', 'Great'] |       string[]        |    No    |   All    |        Yes        |
|    selectedColor     | 填充星星的颜色值。默认值为#004666         |        string         |    No    |   All    |        Yes        |
|      showRating      | 判断是否在评分上方显示评论 默认值为 true |        boolean        |    No    |   All    |        Yes        |
|         size         | 评分图片大小默认值为40                        |        number         |    No    |   All    |        Yes        |
|  starContainerStyle  | 星形容器的样式默认为无           |      View Style       |    No    |   All    |        Yes        |
|      starImage       | 传入自定义图像                |        string         |    No    |    No    |        No         |

**Avatar**：一个头像、Icon、字母渲染组件

|         Name          |                         Description                          |                        Type                         | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :-------------------------------------------------: | :------: | :------: | :---------------: |
|       Component       | 用于封闭元素的组件（例如：可触摸高亮显示、视图等）。 |                   React Component                   |    No    |   All    |        Yes        |
|    ImageComponent     | Avatar的自定义图像组件。               |               ComponentClass<{}, any>               |    No    |   All    |        Yes        |
|      avatarStyle      | Avatar图片的风格。                         |                     ImageStyle                      |    No    |   All    |        Yes        |
|    containerStyle     | 外部容器的样式                    |                     View Style                      |    No    |   All    |        Yes        |
|         icon          | 将图标作为头像的主要内容展示。**不能与标题同时使用**。当与`source`属性一起使用时，它将作为占位符。 |                     AvatarIcon                      |    No    |   All    |        Yes        |
|       iconStyle       | 为图标组件添加额外样式。                |                     Text Style                      |    No    |   All    |        Yes        |
|      imageProps       | 可传递给头像的可选属性，例如“resizeMode”。 |                 ImageProps(Object)                  |    No    |   All    |        Yes        |
|      onLongPress      | 组件长按时的回调函数。        |                      Function                       |    No    |   All    |        Yes        |
|        onPress        | 按下组件时的回调函数。         |                      Function                       |    No    |   All    |        Yes        |
|       onPressIn       | 在`onPress`之前，当触摸被触发时调用。       |            GestureResponderEventHandler             |    No    |   All    |        Yes        |
|      onPressOut       | 在`onPress`之前释放触摸时调用。       |            GestureResponderEventHandler             |    No    |   All    |        Yes        |
| overlayContainerStyle | 外部图像或图标的视图样式。           |                     Text Style                      |    No    |   All    |        Yes        |
|        rounded        | 使头像变成圆形。                   |                       boolean                       |    No    |   All    |        Yes        |
|         size          | 头像的大小。                       |     `number`,`small`,`medium`,`large`,`xlarge`      |    No    |   All    |        Yes        |
|        source         | 头像上显示的图片来源。            |                 ImageSourcePropType                 |    No    |   All    |        Yes        |
|      titleStyle       | 标题的风格。                           |                     Text Style                      |    No    |   All    |        Yes        |

**Avatar.Accessory**：Avatar组件的子组件，接收所有 [Icon](https://reactnativeelements.com/docs/components/icon#props), [Image](https://reactnativeelements.com/docs/components/image#props), [Text](https://reactnative.dev/docs/text#props) 的 props

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   |  当检测到长按手势时调用    | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     |  当检测到单点手势时调用。  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    |  在`onPress`之前，当触摸被触发时调用。 | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   |  在`onPress`之前释放触摸时调用。| GestureResponderEventHandler |    No    |   All    |        Yes        |

**Badge**：徽章组件，通常用于向用户传达数值或指示物品的状态

|      Name      |                        Description                        |                  Type                  | Required | Platform | HarmonyOS Support |
| :------------: | :-------------------------------------------------------: | :------------------------------------: | :------: | :------: | :---------------: |
|   Component    |   自定义组件以替换徽章外部组件。  |            React Component             |    No    |   All    |        Yes        |
|   badgeStyle   | 徽章（背景）视图组件的额外样式设计。 |               View Style               |    No    |   All    |        Yes        |
| containerStyle | 容器的样式。                     |               View Style               |    No    |   All    |        Yes        |
|  onLongPress   | 当检测到长按手势时调用。         |      GestureResponderEventHandler      |    No    |   All    |        Yes        |
|    onPress     | 当检测到单点手势时调用。       |                Function                |    No    |   All    |        Yes        |
|   onPressIn    | 在`onPress`之前，当触摸被触发时调用。      |      GestureResponderEventHandler      |    No    |   All    |        Yes        |
|   onPressOut   | 在`onPress`之前释放触摸时调用。     |      GestureResponderEventHandler      |    No    |   All    |        Yes        |
|     status     | 确定指示器的颜色。             | `primary`,`success`,`warning` ,`error` |    No    |   All    |        Yes        |
|   textProps    | 文本组件的额外属性。              |               TextProps                |    No    |   All    |        Yes        |
|   textStyle    | 文本组件的额外样式。             |               Text Style               |    No    |   All    |        Yes        |
|     value      | 徽章上显示的文本值，默认为空。  |               ReactNode                |    No    |   All    |        Yes        |

**BottomSheet**：从屏幕底部显示内容的组件，依赖react-native-safe-area-context三方库

|      Name       |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :-------------: | :----------------------------------------------------------: | :-------------: | :------: | :------: | :---------------: |
|  backdropStyle  | 背景容器的样式。                 |   View Style    |    No    |   All    |        Yes        |
| containerStyle  | 容器的样式。使用此选项可更改底纹的颜色。 |   View Style    |    No    |   All    |        Yes        |
|    isVisible    | 模态分量是否已显示。                   |     boolean     |    No    |   All    |        Yes        |
|   modalProps    | 向`Modal`组件传递了额外的道具。           |   ModalProps    |    No    |   All    |        Yes        |
| onBackdropPress | 背景板按压处理程序。                    |    Function     |    No    |   All    |        Yes        |
| scrollViewProps | 用于向滚动视图添加道具。                | ScrollViewProps |    No    |   All    |        Yes        |

**Button**：按钮组件，接收所有 [TouchableOpacityProps](https://reactnative.dev/docs/touchableopacity#props) 的 props

|        Name         |                         Description                          |                             Type                             | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------------: |
| TouchableComponent  | 用户交互组件。                |                       typeof Component                       |    No    |   All    |        Yes        |
|    ViewComponent    | 容器组件。                      |                       React Component                        |    No    |   All    |        Yes        |
|     buttonStyle     | 为按钮组件添加额外的样式。         |                          View Style                          |    No    |   All    |        Yes        |
|        color        | 按钮颜色                             | `string`,`primary`,`secondary`,`success` | No | All | Yes |
|   containerStyle    | 组件容器的样式设计。              |                          View Style                          |    No    |   All    |        Yes        |
|      disabled       | 禁用用户交互。                   |                           boolean                            |    No    |   All    |        Yes        |
| disabledTitleStyle  | 标题禁用时的样式。                |                      disabledTitleStyle                      |    No    |   All    |        Yes        |
|        icon         | 显示一个居中的图标（无标题时）或显示在左侧（有文本时）。（也可与iconRight一起使用）。可以是对象或自定义组件。 |                           IconNode                           |    No    |   All    |        Yes        |
| iconContainerStyle  | 图标组件容器的样式设计。              |                          View Style                          |    No    |   All    |        Yes        |
|    iconPosition     | 将图标显示到指定位置。需与`icon`属性一起使用。 | `left`,`right`,`top`,`bottom` | No | All | Yes           |
|      iconRight      | 在标题右侧显示图标。需与`icon`属性一起使用。 |                           boolean                            |    No    |   All    |        Yes        |
| linearGradientProps | 显示线性渐变。看 [usage](https://reactnativeelements.com/docs/components/button#linear-gradient). |                            object                            |    No    |   All    |        Yes        |
|       loading       | 显示加载指示器的道具。                 |                           boolean                            |    No    |   All    |        Yes        |
|    loadingProps     | 为ActivityIndicator组件添加额外的道具。     |                    ActivityIndicatorProps                    |    No    |   All    |        Yes        |
|    loadingStyle     | 加载样式                            |                          View Style                          |    No    |   All    |        Yes        |
|       radius        | 按钮圆角                    | `number`,`sm`,`md`,`lg` | No | All | Yes              |
|       raised        | 添加凸起按钮样式（可选）。如果`type="clear"`，则此设置无效。 |                           boolean                            |    No    |   All    |        Yes        |
|        size         | 按钮尺寸                         |            `sm`,`md`,`lg` |    No    |   All    |        Yes        |
|        title        | 添加按钮标题。             | `string`,`ReactElement<{}, string`,`JSXElementConstructor<any>>` | No |   All    |        Yes        |
|     titleProps      | 为文本组件添加额外的道具。            |                          TextProps                           |    No    |   All    |        Yes        |
|     titleStyle      | 为标题组件添加额外的样式。          |                          Text Style                          |    No    |   All    |        Yes        |
|        type         | 按钮类型。          | `solid`,`clear`,`outline` |    No    |   All    |        Yes        |
|      uppercase      | 大写按钮标题               |                           boolean                            |    No    |   All    |        Yes        |

**ButtonGroup**：按钮组组件

|           Name            |                         Description                          |                       Type                        | Required | Platform | HarmonyOS Support |
| :-----------------------: | :----------------------------------------------------------: | :-----------------------------------------------: | :------: | :------: | :---------------: |
|         Component         |  选择其他按钮组件，如TouchableOpacity   |                  React Component                  |    No    |   All    |        Yes        |
|       activeOpacity       |  为buttonGroup中的按钮添加页面不透明度。       |                      number                       |    No    |   No  |        No        |
|          button           |  组件的按钮                            |                      object                       |    No    |   No  |        No        |
|   buttonContainerStyle    |  为按钮容器指定样式                  |                    View Style                     |    No    |   All    |        Yes        |
|        buttonStyle        |  为按钮指定样式               |                    View Style                     |    No    |   All    |        Yes        |
|          buttons          |  组件的按钮数组（必填），如果返回的是组件，则必须是一个包含 { element: componentName } 的对象。| `(string`,`ButtonComponent`,`ButtonObject)[]` | No |   All    |        Yes        |
|      containerStyle       |  为主要按钮容器指定样式        |                    View Style                     |    No    |   All    |        Yes        |
|         disabled          |  控制按钮是否被禁用。设置为`true`会使所有按钮都禁用，而使用数组则只会禁用指定索引的按钮。 |    `boolean`,`number[]` |No               |   All    |        Yes        |
|   disabledSelectedStyle   |  为每个选定的禁用按钮设置样式         |                    View Style                     |    No    |   All    |        Yes        |
| disabledSelectedTextStyle |  为每个选定按钮在禁用状态下的文本设置样式。 |                    Text Style                     |    No    |   All    |        Yes        |
|       disabledStyle       |  为每个禁用状态的按钮设置样式               |                    View Style                     |    No    |   All    |        Yes        |
|     disabledTextStyle     |  为每个禁用状态的按钮文本设置样式        |                    Text Style                     |    No    |   All    |        Yes        |
|     innerBorderStyle      |  更新按钮列表内部边框的样式 |        { color?: string; width?: number; }        |    No    |   All    |        Yes        |
|      onHideUnderlay       |  在隐藏参考底图时调用了函数                    |                     Function                      |    No    |   No  |        No        |
|        onLongPress        |  当检测到长按手势时调用。              |           GestureResponderEventHandler            |    No    |   No  |        No        |
|          onPress          |  更新按钮组索引的方法              |             (...args: any[]) => void              |    No    |   All    |        Yes        |
|         onPressIn         |  当触摸在‘ onPress ’之前被占用时调用。      |           GestureResponderEventHandler            |    No    |   All    |        Yes        |
|        onPressOut         |  当触摸在‘ onPress ’之前被释放时调用。     |           GestureResponderEventHandler            |    No    |   All    |        Yes        |
|      onShowUnderlay       |  显示底层时调用的函数             |                     Function                      |    No    |   All    |        Yes        |
|      selectMultiple       |  允许用户选择多个按钮        |                      boolean                      |    No    |   All    |        Yes        |
|    selectedButtonStyle    |  指定所选按钮的样式             |                    View Style                     |    No    |   All    |        Yes        |
|       selectedIndex       |  当前选定的按钮数组索引。         |                      number                       |    No    |   All    |        Yes        |
|      selectedIndexes      |  中当前选定的按钮数组索引。     |                     number[]                      |    No    |   All    |        Yes        |
|     selectedTextStyle     |  为选定状态中的文本指定特定的样式 |                    Text Style                     |    No    |   All    |        Yes        |
|       setOpacityTo        |  设置不透明度             |              (value: number) => void              |    No    |   No  |        No        |
|         textStyle         |  为文本指定特定的样式                    |                    Text Style                     |    No    |   All    |        Yes        |
|       underlayColor       |  为TouchableHighlight指定underlayColor。      |                        ng                         |    No    |   No  |        No        |
|         vertical          |  垂直显示ButtonGroup               |                      boolean                      |    No    |   All    |        Yes        |

**Card**：卡片组件

|      Name      |      Description       |    Type    | Required | Platform | HarmonyOS Support |
| :------------: | :--------------------: | :--------: | :------: | :------: | :---------------: |
| containerStyle | 外部容器样式 | View Style |    No    |   All    |        Yes        |
|  wrapperStyle  | 内部容器样式 | View Style |    No    |   All    |        Yes        |

**Card.Divider**：卡片分割线组件，接收所有 [Divider](https://reactnativeelements.com/docs/components/divider#props) 组件的 Props

**Card.FeaturedSubtitle**：卡片功能字幕组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 组件的 Props

**Card.FeaturedTitle**：卡片功能标题组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 组件的 Props

**Card.Image**：卡片图片组件，接收所有 [Image](https://reactnativeelements.com/docs/components/image#props) 组件的 Props

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   |  当检测到长击手势时调用。    | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     |  当检测到单个点击手势时调用。   | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    |  当触摸在‘ onPress ’之前被占用时调用。 | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   |  当触摸在‘ onPress ’之前被释放时调用。 | GestureResponderEventHandler |    No    |   All    |        Yes        |

**Card.Title**：卡片标题组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 组件的 Props

**CheckBox**：选择框组件，接收所有[View](https://reactnative.dev/docs/view#props) 的 props.

|        Name        |                   Description                   |                             Type                             | Required | Platform | HarmonyOS Support |
| :----------------: | :---------------------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------------: |
|     Component      |  为主按钮指定 React Native 组件  |                       React Component                        |    No    |   All    |        Yes        |
|       center       |  将复选框居中对齐            |                           boolean                            |    No    |   All    |        Yes        |
|    checkedTitle    |  指定一个自定义的已勾选消息         |                            string                            |    No    |   All    |        Yes        |
|   containerStyle   |  主容器的样式            |                          View Style                          |    No    |   All    |        Yes        |
|      disabled      |  禁用用户交互            |                           boolean                            |    No    |   All    |        Yes        |
|   disabledStyle    |  禁用时复选框容器的样式 |                          View Style                          |    No    |   All    |        Yes        |
| disabledTitleStyle |  标题禁用时的样式       |                          Text Style                          |    No    |   All    |        Yes        |
|     fontFamily     |  指定不同的字体系列          |                            string                            |    No    |   All    |        Yes        |
|     iconRight      |  将图标移动到文本右侧              |                           boolean                            |    No    |   All    |        Yes        |
|       right        |  将复选框向右对齐            |                           boolean                            |    No    |   All    |        Yes        |
|     textStyle      |  文本风格                |                          Text Style                          |    No    |   All    |        Yes        |
|       title        |  复选框的标题              | `string` ，`ReactElement<{}, string` ，`JSXElementConstructor<any>>` |    No    |   All    |        Yes        |
|     titleProps     |  标题文本组件的附加属性 |                          TextProps                           |    No    |   All    |        Yes        |
|    wrapperStyle    |  复选框包装器的样式         |                          View Style                          |    No    |   All    |        Yes        |

**Chip**：显示触摸区组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props

| Name |      Description       |        Type        | Required | Platform | HarmonyOS Support |
| :--: | :--------------------: | :----------------: | :------: | :------: | :---------------: |
| type | 外部容器样式。 | `solid`，`outline` |    No    |   All    |        Yes        |

**Dialog**：对话框组件，接收所有 [Overlay](https://reactnativeelements.com/docs/components/overlay#props) 的props

|      Name      |                        Description                        |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|    children    |  添加封闭组件                       |          ReactNode           |    No    |   All    |        Yes        |
|  onLongPress   |  当检测到长按手势时调用         | GestureResponderEventHandler |    No    |    No    |        No         |
|   onPressIn    |  在`onPress`之前，当触摸被触发时调用     | GestureResponderEventHandler |    No    |    No    |        No         |
|   onPressOut   |  在`onPress`之前释放触摸时调用    | GestureResponderEventHandler |    No    |    No    |        No         |
|  overlayStyle  | 	为内部Overlay组件添加额外的样式 |          View Style          |    No    |   All    |        Yes        |

**Dialog.Actions**：定义对话框操作组件

|   Name   |                     Description                     |   Type    | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------------: | :-------: | :------: | :------: | :---------------: |
| children | 将“添加封闭组件”作为一项操作添加到对话框中。 | ReactNode |    No    |   All    |        Yes        |

**Dialog.Button**：定义对话框按钮组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props

**Dialog.Loading**：定义对话框加载组件

|     Name     |                     Description                      |          Type          | Required | Platform | HarmonyOS Support |
| :----------: | :--------------------------------------------------: | :--------------------: | :------: | :------: | :---------------: |
| loadingProps | 为ActivityIndicator组件添加额外的属性 | ActivityIndicatorProps |    No    |   All    |        Yes        |
| loadingStyle | 为加载组件添加额外的样式     |       View Style       |    No    |   All    |        Yes        |

**Dialog.Title**：定义对话框标题组件

|    Name    |                 Description                 |    Type    | Required | Platform | HarmonyOS Support |
| :--------: | :-----------------------------------------: | :--------: | :------: | :------: | :---------------: |
|   title    |              Add Dialog title.              |   string   |    No    |   All    |        Yes        |
| titleProps | 为文本组件添加额外的属性  | TextProps  |    No    |   All    |        Yes        |
| titleStyle | 为标题组件添加额外的样式 | Text Style |    No    |   All    |        Yes        |

**Divider**：分割线组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props.

|      Name      |                      Description                      |            Type             | Required | Platform | HarmonyOS Support |
| :------------: | :---------------------------------------------------: | :-------------------------: | :------: | :------: | :---------------: |
|     color      |  组件的颜色。                          |           string            |    No    |   All    |        Yes        |
|     inset      |  将inset应用于分割线         |           boolean           |    No    |   All    |        Yes        |
|   insetType    |  将insert应用于分隔符的特定方向 |  `middle`，`left`，`right`  |    No    |   All    |        Yes        |
|  orientation   |  对分割线应用方向           |  `vertical` ，`horizontal`  |    No    |   All    |        Yes        |
|     style      |  为分割线应用样式             |         View Style          |    No    |   All    |        Yes        |
|   subHeader    |  向分隔符添加子标题文本           |           string            |    No    |   All    |        Yes        |
| subHeaderStyle |  为分隔符的子标题文本添加样式    |         Text Style          |    No    |   All    |        Yes        |
|     width      |  宽度                     | Apply width to the divider. |    No    |   All    |        Yes        |

**FAB**：浮动操作按钮组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props.

|   Name    |                         Description                          |       Type        | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------------------------------------: | :---------------: | :------: | :------: | :---------------: |
|   color   | 更换FAB的颜色。                    |      string       |    No    |   All    |        Yes        |
| placement | FAB放置在底部，（可选）使用 [`style`](https://reactnativeelements.com/docs/components/fab#style) in case of custom placement. | `left`， `right`  |    No    |   All    |        Yes        |
|   size    | 更改FAB的大小                        | `small` ，`large` |    No    |   All    |        Yes        |
|   style   | FAB风格                        |    View Style     |    No    |   All    |        Yes        |
| upperCase | 将扩展标签文本转换为大写。        |      boolean      |    No    |   All    |        Yes        |
|  visible  | 决定FAB的可见度                 |      boolean      |    No    |   All    |        Yes        |

**Header**：头部组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|                       Name                        |                         Description                          |                 Type                 | Required | Platform | HarmonyOS Support |
| :-----------------------------------------------: | :----------------------------------------------------------: | :----------------------------------: | :------: | :------: | :---------------: |
|                   ViewComponent                   | 组件用于容器                        |           React Component            |    No    |   All    |        Yes        |
|                  backgroundColor                  | 设置父组件的背景色       |                string                |    No    |   All    |        Yes        |
|                  backgroundImage                  | 为父组件设置背景图像         |         ImageSourcePropType          |    No    |   All    |        Yes        |
|               backgroundImageStyle                | 主容器中backgrounimage的样式    |              ImageStyle              |    No    |   All    |        Yes        |
|                     barStyle                      | 设置状态栏文本的颜色             |            StatusBarStyle            |    No    |    No    |        No         |
|                  centerComponent                  | 在这里定义中心组件                |          HeaderSubComponent          |    No    |   All    |        Yes        |
|               centerContainerStyle                | 为中心组件周围的容器设置样式。   |              View Style              |    No    |   All    |        Yes        |
| Styling for container around the centerComponent. | 将子组件添加到头部             | `(Element`，`Element[]) & ReactNode` |    No    |   All    |        Yes        |
|                  containerStyle                   | 主容器周围的样式               |              View Style              |    No    |   All    |        Yes        |
|                     elevated                      | 页眉标高                         |               boolean                |    No    |    No    |        No         |
|                   leftComponent                   | 在此处定义您的左侧组件               |          HeaderSubComponent          |    No    |   All    |        Yes        |
|                leftContainerStyle                 | 为 leftComponent 周围的容器设置样式    |              View Style              |    No    |   All    |        Yes        |
|                linearGradientProps                | 显示线性渐变。看 [usage](https://reactnativeelements.com/docs/components/header#lineargradient-usage). |                Object                |    No    |    No    |        No         |
|                     placement                     | 标题的对齐方式                  |      `center`，`left`，`right`       |    No    |   All    |        Yes        |
|                  rightComponent                   | 在此处定义您的右侧组件                   |          HeaderSubComponent          |    No    |   All    |        Yes        |
|                rightContainerStyle                | 为rightComponent周围的容器设置样式     |              View Style              |    No    |   All    |        Yes        |
|                  statusBarProps                   | 接受StatusBar的所有属性            |            StatusBarProps            |    No    |   All    |        Yes        |

**Icon**：字体图标组件，接收所有 [Text](https://reactnative.dev/docs/text#props) 的props.

|      Name      |                         Description                          |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :----------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|   Component    | 更新 React Native 组件                   |       React Component        |    No    |   All    |        Yes        |
|     brand      | 使用品牌字体（仅限FontAwesome5         |           boolean            |    No    |   No    |        No        |
| containerStyle | 为包含图标的容器添加样式           |          View Style          |    No    |   All    |        Yes        |
|    disabled    | 禁用onPress事件。仅当`onPress`有处理程序时才有效。 |           boolean            |    No    |   All    |        Yes        |
| disabledStyle  | 按钮禁用时的样式。仅当`onPress`具有处理程序时有效。 |          View Style          |    No    |   All    |        Yes        |
|   iconProps    | 提供来自react-native Icon组件的所有属性      |          IconProps           |    No    |   All    |        Yes        |
|  onLongPress   | 当检测到长按手势时调用          | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     | 当检测到单次点击手势时调用        | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | 在`onPress`之前，当触摸被触发时调用       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | 在`onPress`之前，当触摸被触发时调用       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|     raised     | 为按钮添加框影效果                       |           boolean            |    No    |   All    |        Yes        |
|    reverse     | 改变配色方案                    |           boolean            |    No    |   All    |        Yes        |
|  reverseColor  | 指定反向图标颜色                |            string            |    No    |   All    |        Yes        |
|     solid      | 使用实心字体                     |           boolean            |    No    |   All    |        Yes        |
|     testID     | 图标的测试ID。                                   |            string            |    No    |   All    |        Yes        |
|      type      | 图标设置的类型 [Supported sets here](https://reactnativeelements.com/docs/components/icon#available-icon-sets). |            string            |    No    |   All    |        Yes        |

**Image**：图片组件，接收所有 [React Native Image](https://reactnative.dev/docs/image#props) 的props.

|          Name          |                      Description                      |                           Type                            | Required | Platform | HarmonyOS Support |
| :--------------------: | :---------------------------------------------------: | :-------------------------------------------------------: | :------: | :------: | :---------------: |
|       Component        | 定义传递给image的组件。             |                      React Component                      |    No    |   All    |        Yes        |
|     ImageComponent     | 指定另一个组件作为图像组件 |                     typeof Component                      |    No    |   All    |        Yes        |
|   PlaceholderContent   | 渲染图像时要加载的内容       | `ReactElement<any, string`，`JSXElementConstructor<any>>` |    No    |   All    |        Yes        |
| childrenContainerStyle | 子容器的附加样式   |                        View Style                         |    No    |   All    |        Yes        |
|     containerStyle     | 容器的附加样式        |                        View Style                         |    No    |   All    |        Yes        |
|      onLongPress       | 当检测到长按手势时调用       |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|        onPress         | 当检测到单个点击手势时调用      |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|       onPressIn        | 当触摸在‘ onPress ’之前被占用时调用。    |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|       onPressOut       | 当触摸在‘ onPress ’之前被释放时调用。    |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|    placeholderStyle    | 占位符容器的附加样式   |                        View Style                         |    No    |   All    |        Yes        |
|       transition       | 加载图像时执行淡入\淡出过渡         |                          boolean                          |    No    |   All    |        Yes        |
|   transitionDuration   | 加载图像时执行淡入\淡出过渡时长          |                          number                           |    No    |   All    |        Yes        |

**Input**：表单组件，接收所有 [React Native TextInput](https://reactnative.dev/docs/textinput#props), [View](https://reactnative.dev/docs/view#props) 的props.

|          Name           |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :---------------------: | :----------------------------------------------------------: | :-------------: | :------: | :------: | :---------------: |
|     InputComponent      | 组件将被渲染，以取代React Native的TextInput | React Component |    No    |   All    |        Yes        |
|     containerStyle      | 容器的样式                          |   View Style    |    No    |   All    |        Yes        |
|        disabled         | 禁用输入组件                          |     boolean     |    No    |   All    |        Yes        |
|   disabledInputStyle    | 禁用的样式将被传递给React Native TextInput的样式属性 |   Text Style    |    No    |   All    |        Yes        |
|      errorMessage       | 错误信息将显示在输入字段下      |     string      |    No    |   All    |        Yes        |
|       errorProps        | props传递给用于显示错误消息的React Native Text组件 |     object      |    No    |   All    |        Yes        |
|       errorStyle        | 向错误消息添加样式                 |   Text Style    |    No    |   All    |        Yes        |
|   inputContainerStyle   | 输入组件容器的样式            |   View Style    |    No    |   All    |        Yes        |
|       inputStyle        | 输入组件样式                     |   Text Style    |    No    |   All    |        Yes        |
|          label          | 在输入框顶部添加一个标签                         |    ReactNode    |    No    |   All    |        Yes        |
|       labelProps        | props传递给用于显示标签的React Native Text组件或使用的React组件，而不是标签prop中的简单字符串 |     object      |    No    |   All    |        Yes        |
|       labelStyle        | 标签的样式；只有当label是字符串时才能使用这个 |   Text Style    |    No    |   All    |        Yes        |
|        leftIcon         | 显示左侧的一个图标                    |    IconNode     |    No    |   All    |        Yes        |
| leftIconContainerStyle  | 左图标组件容器的样式           |   View Style    |    No    |   All    |        Yes        |
|   renderErrorMessage    | 错误消息容器是否需要渲染（占用垂直空间）。如果为false，当显示errorMessage时，布局将在那时移动并添加它。 |     boolean     |    No    |    No    |        No         |
|        rightIcon        | 右侧显示一个图标                    |    IconNode     |    No    |   All    |        Yes        |
| rightIconContainerStyle | 右侧图标组件容器样式          |   View Style    |    No    |   All    |        Yes        |
|          shake          | 震动的方法                                   |    Function     |    No    |   All    |        Yes        |

**LinearProgress**：加载条组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props.

|    Name    |                         Description                          |                 Type                 | Required | Platform | HarmonyOS Support |
| :--------: | :----------------------------------------------------------: | :----------------------------------: | :------: | :------: | :---------------: |
| animation  | 动画时长                   | `boolean` , `{ duration?: number; }` |    No    |   All    |        Yes        |
|   color    | 线性进度组件的颜色                      |                string                |    No    |   All    |        Yes        |
|   style    | 为线性进度组件添加额外的样式。    |              View Style              |    No    |   All    |        Yes        |
| trackColor | 线性进度的跟踪颜色。             |                string                |    No    |   All    |        Yes        |
|   value    | 确定变量的进度指示器的值。取值在0到1之间。 |                number                |    No    |   All    |        Yes        |
|  variant   | 按钮类型。                             |    `determinate`，`indeterminate`    |    No    |   All    |        Yes        |

**ListItem**：列表渲染组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props.

|                          Name                           |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------------------------------------------: | :----------------------------------------------------------: | :-------------: | :------: | :------: | :---------------: |
|                        Component                        | 将元素替换为自定义元素          | React Component |    No    |   All    |        Yes        |
|                      ViewComponent                      | 线性梯度容器                    | React Component |    No    |   All    |        Yes        |
|                      bottomDivider                      | 在列表项的底部添加分割线         |     boolean     |    No    |   All    |        Yes        |
|                        children                         | 添加封闭的子元素                      |       any       |    No    |   All    |        Yes        |
|                     containerStyle                      | 额外的主容器样式。              |   View Style    |    No    |   All    |        Yes        |
|                      disabledStyle                      | 当列表项被禁用时使用的特定样式。   |   View Style    |    No    |   All    |        Yes        |
| Specific styling to be used when list item is disabled. | 为线性渐变组件属性                |       any       |    No    |   All    |        Yes        |
|                           pad                           | 添加左组件，标题组件和右组件之间的间距。 |     number      |    No    |   All    |        Yes        |
|                       topDivider                        | 在列表项的顶部添加分割线。              |     boolean     |    No    |   All    |        Yes        |

**ListItem.Accordion**：列表渲染折叠组件，接收所有 [ListItem](https://reactnativeelements.com/docs/components/listitem#props) 的props.

|    Name    |                         Description                          |              Type              | Required | Platform | HarmonyOS Support |
| :--------: | :----------------------------------------------------------: | :----------------------------: | :------: | :------: | :---------------: |
| animation  | 决定是否显示动画              | Animated.TimingAnimationConfig |    No    |   All    |        Yes        |
|  content   | 类似于ListItem的子元素                      |           ReactNode            |    No    |   All    |        Yes        |
| expandIcon | 当折叠展开时，如果未提供` Icon `，则将旋转180度。 |            IconNode            |    No    |   All    |        Yes        |
|    icon    | 添加封闭的子元素                          |            IconNode            |    No    |   All    |        Yes        |
| isExpanded | 判断Accordion是否被展开                   |            boolean             |    No    |   All    |        Yes        |
| leftRotate | 左侧旋转图标                          |            boolean             |    No    |   All    |        Yes        |
|   noIcon   | 不要显示折叠图标。                         |            boolean             |    No    |   All    |        Yes        |
| noRotation | 展开Accordion时不要旋转             |            boolean             |    No    |   All    |        Yes        |

**ListItem.ButtonGroup**：列表渲染按钮组组件，接收所有 [ButtonGroup](https://reactnativeelements.com/docs/components/buttongroup#props) 的props.

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   | 当检测到长按手势时调用。      | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | 在`onPress`之前，当触摸被触发时调用。  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | 在`onPress`之前释放触摸时调用 | GestureResponderEventHandler |    No    |   All    |        Yes        |

**ListItem.CheckBox**：列表渲染选择框组件，接收所有 [CheckBox](https://reactnativeelements.com/docs/components/checkbox#props) 的props.

**ListItem.Chevron**：列表渲染字体图标组件，接收所有 [Icon](https://reactnativeelements.com/docs/components/icon#props) 的props.

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   | 当检测到单次点击手势时调用  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     | 当检测到单点触控手势时调用    | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | 在`onPress`之前，当触摸被触发时调用。 | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | 在`onPress`之前释放触摸时调用。 | GestureResponderEventHandler |    No    |   All    |        Yes        |

**ListItem.Content**：列表渲染内容组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 的props.

| Name  |          Description          |  Type   | Required | Platform | HarmonyOS Support |
| :---: | :---------------------------: | :-----: | :------: | :------: | :---------------: |
| right | 从右边开始内容. | boolean |    No    |   All    |        Yes        |

**ListItem.Input**：列表渲染表单组件，接收所有 [Input](https://reactnativeelements.com/docs/components/input#props) 的props.

**ListItem.Subtitle**：列表渲染字幕组件，接收所有 [Text](https://reactnative.dev/docs/text#props) 的props.

| Name  |          Description          |  Type   | Required | Platform | HarmonyOS Support |
| :---: | :---------------------------: | :-----: | :------: | :------: | :---------------: |
| right | 从右边开始内容. | boolean |    No    |   No    |        No        |

**ListItem.Swipeable**：列表渲染滑动框组件，接收所有 [ListItem](https://reactnativeelements.com/docs/components/listitem#props) 的props.

|     Name      |                 Description                 |                  Type                   | Required | Platform | HarmonyOS Support |
| :-----------: | :-----------------------------------------: | :-------------------------------------: | :------: | :------: | :---------------: |
|   animation   | 决定是否显示动画     |     Animated.TimingAnimationConfig      |    No    |   All    |        Yes        |
|  leftContent  | 左侧内容         | ReactNode or resetCallback => ReactNode |    No    |   All    |        Yes        |
|   leftStyle   | 左侧容器的样式。           |               View Style                |    No    |   All    |        Yes        |
|   leftWidth   | 左侧滑动容器的宽度。         |                 number                  |    No    |   All    |        Yes        |
| onSwipeBegin  | 用于处理向任意方向滑动的处理程序    | `(direction: left`,`right) => unknown`  |    No    |   All    |        Yes        |
|  onSwipeEnd   | 滑动结束的处理程序。           |              () => unknown              |    No    |   All    |        Yes        |
| rightContent  | 右侧内容           | ReactNode or resetCallback => ReactNode |    No    |   All    |        Yes        |
|  rightStyle   | 右侧容器的样式。          |               View Style                |    No    |   All    |        Yes        |
|  rightWidth   | 向右滑动容器的宽度。        |                 number                  |    No    |   All    |        Yes        |

**ListItem.Title**：列表渲染标题组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

| Name  |   Description    |  Type   | Required | Platform | HarmonyOS Support |
| :---: | :--------------: | :-----: | :------: | :------: | :---------------: |
| right | 添加正确的标题。 | boolean |    No    |    No    |        No         |

**Overlay**：弹窗组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|      Name       |                         Description                          |             Type             | Required | Platform | HarmonyOS Support |
| :-------------: | :----------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
| ModalComponent  | 重写 React Native 的 `Modal` 组件（适用于 Web 平台）。 |       typeof Component       |    No    |   No    |        No        |
|  backdropStyle  | 背景容器的样式。                      |          iew Style           |    No    |   No    |        No        |
|   fullScreen    | 如果设置为true，模态框将占据整个屏幕的宽度和高度。 |           boolean            |    No    |   No    |        No        |
|    isVisible    | 如果为True，则叠加层可见                    |           boolean            |    No    |   No    |        No        |
| onBackdropPress | 背景按压处理程序（仅当`fullscreen`为false时有效）。 |           Function           |    No    |   No    |        No        |
|   onLongPress   | 当检测到长按手势时调用。         | GestureResponderEventHandler |    No    |   No    |        No        |
|    onPressIn    | 在`onPress`之前，当触控被触发时调用。      | GestureResponderEventHandler |    No    |   No    |        No        |
|   onPressOut    | 在`onPress`之前释放触摸时调用。       | GestureResponderEventHandler |    No    |   No    |        No        |
|  overlayStyle   | 实际覆盖层的样式.                 |          View Style          |    No    |   No    |        No        |

**PricingCard**：价格卡组件

|      Name      |                Description                 |                Type                | Required | Platform | HarmonyOS Support |
| :------------: | :----------------------------------------: | :--------------------------------: | :------: | :------: | :---------------: |
|     button     | 按钮信息               | `ButtonProps`，`ButtonInformation` |    No    |   All    |        Yes        |
|     color      | 按钮和标题的配色方案。  |               string               |    No    |   All    |        Yes        |
| containerStyle | 外部组件样式。          |             View Style             |    No    |   All    |        Yes        |
|      info      | 定价信息。                  |              string[]              |    No    |   All    |        Yes        |
|   infoStyle    | 指定定价信息样式。      |             Text Style             |    No    |   All    |        Yes        |
| onButtonPress  | 按钮被按下时运行的函数。 |              Function              |    No    |   All    |        Yes        |
|     price      | 定价卡上提到的价格。  |         `string`，`number`         |    No    |   All    |        Yes        |
|  pricingStyle  | 文本风格                   |    Specify pricing text style.     |    No    |   All    |        Yes        |
|     title      | 在定价卡中添加标题。       |               string               |    No    |   All    |        Yes        |
|   titleStyle   | 指定标题文字样式。           |             Text Style             |    No    |   All    |        Yes        |
|  wrapperStyle  | 内包装组件样式。      |             View Style             |    No    |   All    |        Yes        |

**Ratings**：评分组件

|         Name          |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|       fractions       | 额定值的小数位数；必须介于0和20之间 |        anyany         |    No    |    No    |        No         |
|       imageSize       | 每个评级图像的大小默认为50          |        number         |    No    |    No    |        No         |
|       jumpValue       | 每次滑动跳转的数字默认为0（不跳转）     |        number         |    No    |    No    |        No         |
|       minValue        | 用户可以选择的最小值默认为0      |        number         |    No    |    No    |        No         |
|    onFinishRating     | 用户完成评级时的回调方法。以整数形式给出最终评级值 |       Function        |    No    |    No    |        No         |
|     onStartRating     | 用户开始评分时的回调方法。        |       Function        |    No    |    No    |        No         |
|     onSwipeRating     | 用户滑动时的回调方法      | (number: any) => void |    No    |    No    |        No         |
| ratingBackgroundColor | 为评级图标传递自定义背景填充颜色；与上面的type='custom'prop一起使用默认值为'white' |        string         |    No    |    No    |        No         |
|      ratingColor      | 为评级图标传递自定义填充颜色；将其与上面的type='custom'prop一起使用默认值为'#f1c40f' |        string         |    No    |    No    |        No         |
|      ratingCount      | 要显示的评级图像数量默认为5        |        number         |    No    |    No    |        No         |
|      ratingImage      | 传入自定义图像源；将其与上面的type=“custom”道具一起使用 |       ReactNode       |    No    |    No    |        No         |
|    ratingTextColor    | 文本标签使用的颜色               |        string         |    No    |    No    |        No         |
|       readonly        | 用户是否可以修改评级默认值为false |        boolean        |    No    |    No    |        No         |
|      showRating       | 显示内置评级UI以实时显示评级值默认值为false |        boolean        |    No    |    No    |        No         |
|   showReadOnlyText    | 文本是否为只读默认值为false         |        boolean        |    No    |    No    |        No         |
|     startingValue     | renderDefault的初始评级为ratingCount/2    |        number         |    No    |    No    |        No         |
|         style         | 显示样式道具，为容器视图添加其他样式 |      View Style       |    No    |    No    |        No         |
|       tintColor       | 背景颜色                |        string         |    No    |    No    |        No         |
|         type          | 用于表示评级的图形默认为“星形”     |        string         |    No    |    No    |        No         |

**SearchBar**：搜索框组件，接收所有 [Input](https://reactnativeelements.com/docs/components/input#props) 的 props

|          Name           |              Description               |            Type             | Required | Platform | HarmonyOS Support |
| :---------------------: | :------------------------------------: | :-------------------------: | :------: | :------: | :---------------: |
|    cancelButtonProps    | “取消”按钮的属性   |         Text Style          |    No    |    No    |        No         |
|    cancelButtonTitle    | 取消按钮的标题      |           string            |    No    |    No    |        No         |
|       cancelIcon        | 取消按钮图标      |          IconNode           |    No    |    No    |        No         |
|        clearIcon        | 清除图标               |          IconNode           |    No    |   All    |        Yes        |
|     containerStyle      | 容器样式         |         View Style          |    No    |   All    |        Yes        |
|   inputContainerStyle   | 输入容器样式     |         View Style          |    No    |   All    |        Yes        |
|       inputStyle        | 输入风格                |         Text Style          |    No    |   All    |        Yes        |
| leftIconContainerStyle  | 左侧图标容器样式       |         View Style          |    No    |   All    |        Yes        |
|       lightTheme        | 浅色主题               |           boolean           |    No    |    No    |        No         |
|      loadingProps       | 活跃度指示属性         |   ActivityIndicatorProps    |    No    |   All    |        Yes        |
|        onCancel         | 取消图标按下时的回调			|        `(() => any)`        |    No    |    No    |        No         |
|         onClear         | 按清除图标时的回调			 |          Function           |    No    |   All    |        Yes        |
|        platform         | 平台的判断           | `default`，`android`，`ios` |    No    |    No    |        No         |
| rightIconContainerStyle | 右图标容器样式      |   rightIconContainerStyle   |    No    |   All    |        Yes        |
|          round          | 是否为圆角		    |           boolean           |    No    |   All    |        Yes        |
|       searchIcon        | 搜索图标          |          IconNode           |    No    |   All    |        Yes        |
|       showCancel        | 显示取消               |           boolean           |    No    |    No    |        No         |
|       showLoading       | 显示加载              |           boolean           |    No    |   All    |        Yes        |

**Slider**：滑动条组件

|         Name          |                         Description                          |                       Type                       | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :----------------------------------------------: | :------: | :------: | :---------------: |
|    allowTouchTrack    | 如果为True，滑块将响应并跳跃到沿着轨迹的任何触摸。 |                     boolean                      |    No    |   All    |        Yes        |
|  animateTransitions   | 如果你想使用默认的“spring”动画，设置为true。 |                     boolean                      |    No    |   All    |        Yes        |
|    animationConfig    | 用于配置动画参数。这些是相同的参数[Animated library](https://reactnative.dev/docs/animations.html). | `TimingAnimationConfig`，`SpringAnimationConfig` |    No    |   All    |        Yes        |
|     animationType     | 设置为‘spring’或‘timing’，默认使用这两种类型的动画之一 [animation properties](https://reactnative.dev/docs/animations.html). |                `spring`，`timing`                |    No    |   All    |        Yes        |
|    containerStyle     | 为滑动条的容器应用样式。             |                      Style                       |    No    |   All    |        Yes        |
|    debugTouchArea     | 将此设置为true，可以在视觉上看到拇指触摸的橙色矩形。 |                     boolean                      |    No    |   All    |        Yes        |
|       disabled        | 如果为True，则用户将无法移动滑块。      |                     boolean                      |    No    |   All    |        Yes        |
| maximumTrackTintColor | 按钮右侧轨道使用的颜色。  |                      string                      |    No    |   All    |        Yes        |
|     maximumValue      | 滑块的初始最大值。                 |                      number                      |    No    |   All    |        Yes        |
| minimumTrackTintColor | 按钮左侧轨迹使用的颜色。    |                      string                      |    No    |   All    |        Yes        |
|     minimumValue      | 滑块的初始最小值。              |                      number                      |    No    |   All    |        Yes        |
|   onSlidingComplete   | 当用户完成值更改时（例如，当滑块被释放时）调用回调。 |             (value: number) => void              |    No    |   All    |        Yes        |
|    onSlidingStart     | 当用户开始更改值时（例如按下滑块时）调用回调。 |             (value: number) => void              |    No    |   All    |        Yes        |
|     onValueChange     | 当用户拖动滑块时，连续调用回调。|             (value: number) => void              |    No    |   All    |        Yes        |
|      orientation      | 设置滑块的方向。                  |             `vertical`,`horizontal`              |    No    |   All    |        Yes        |
|         step          | 滑块的步长值。该值应介于0和maximumValue-minimumValue之间）。 |                      number                      |    No    |   All    |        Yes        |
|         style         | 应用于滑块容器的样式。              |                    View Style                    |    No    |   All    |        Yes        |
|      thumbProps       | 适用于鼠标滑块。使用‘ Component ’道具，它可以接受‘ Animated ’组件。 |                       any                        |    No    |   All    |        Yes        |
|      thumbStyle       | 适用于鼠标滑块的样式。                |                    View Style                    |    No    |   All    |        Yes        |
|    thumbTintColor     | 鼠标滑块的颜色。                       |                      string                      |    No    |   All    |        Yes        |
|    thumbTouchSize     | 允许移动滑块的触摸区域的大小。触摸区域与可见滑块的中心相同。这允许有一个视觉上较小的拇指，同时仍然允许用户轻松移动它。 |                     Sizable                      |    No    |   All    |        Yes        |
|      trackStyle       | 适用于赛道的风格。                    |                    View Style                    |    No    |   All    |        Yes        |
|         value         | 滑块的初始值。                       |                      number                      |    No    |   All    |        Yes        |

**Skeleton**：骨架屏组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|          Name           |            Description             |           Type            | Required | Platform | HarmonyOS Support |
| :---------------------: | :--------------------------------: | :-----------------------: | :------: | :------: | :---------------: |
| LinearGradientComponent | 自定义线性渐变组件  |      React Component      |    No    |   All    |        Yes        |
|        animation        | 动画类型           | `none`|`wave`|`pulse` | No | No |    No    |
|         circle          | 显示圆形变体         |          boolean          |    No    |   All    |        Yes        |
|         height          | 骨架视图高度         |    `string`，`number`     |    No    |   All    |        Yes        |
|      skeletonStyle      | 骨架渐变的自定义样式 |        View Style         |    No    |   All    |        Yes        |
|          width          | 骨架视图的宽度      |     `string`,`number`     |    No    |   All    |        Yes        |

**SocialIcon**：社交字体图标组件

|          Name          |                         Description                          |             Type             | Required | Platform | HarmonyOS Support |
| :--------------------: | :----------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|       Component        | 按钮类型。              |       React Component        |    No    |   All    |        Yes        |
| activityIndicatorStyle | 加载状态下要渲染的样式。             |          View Style          |    No    |   All    |        Yes        |
|         button         | 创建带有社交图标的按钮。             |           boolean            |    No    |   All    |        Yes        |
|        disabled        | 如果为真，则禁用该按钮。                  |           boolean            |    No    |   All    |        Yes        |
|       fontFamily       | 指定不同的字体系列。          |            string            |    No    |    No    |        No         |
|       fontStyle        | 指定文本样式。        |          Text Style          |    No    |   All    |        Yes        |
|       fontWeight       | 如果设置为带标题的按钮，请指定标题的字体粗细。 |            string            |    No    |    No    |        No         |
|       iconColor        | 指定图标的颜色。                  |            string            |    No    |   All    |        Yes        |
|        iconSize        | 指定图标的大小。                        |            number            |    No    |   All    |        Yes        |
|       iconStyle        | 图标组件的额外样式。        |          View Style          |    No    |    No    |        No         |
|        iconType        | 图标集的类型。 [Supported sets here](https://reactnativeelements.com/docs/components/icon#available-icon-sets). |            string            |    No    |   All    |        Yes        |
|         light          | 反转图标配色方案，将背景设置为白色，图标设置为原色。 |           boolean            |    No    |    No    |        No         |
|        loading         | 显示加载指示器。                         |           boolean            |    No    |   All    |        Yes        |
|      onLongPress       | 当检测到长按手势时调用。           | GestureResponderEventHandler |    No    |   All    |        Yes        |
|        onPress         | 当检测到单次点击手势时调用。       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|       onPressIn        | 在“按下”之前进行触摸时调用。     | GestureResponderEventHandler |    No    |   All    |        Yes        |
|       onPressOut       | 在“按下”之前释放触摸时调用。      | GestureResponderEventHandler |    No    |   All    |        Yes        |
|         raised         | 凸起会添加一个阴影，设置为false可删除。  |           boolean            |    No    |    No    |        No         |
|         small          | 决定活动指标的大小。          |            string            |    No    |    No    |        No         |
|         style          | 为按钮添加样式。                     |          View Style          |    No    |   All    |        Yes        |
|         title          | 标题如果做成按钮。                 |            string            |    No    |   All    |        Yes        |
|          type          | 社交媒体类型。                          |       SocialMediaType        |    No    |   All    |        Yes        |
|     underlayColor      | 添加参考底图颜色。                           |            string            |    No    |    No    |        No         |

**SpeedDial**：浮动快速操作按钮组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props), [FAB](https://reactnativeelements.com/docs/components/fab#props)  的props

|          Name          |                       Description                        |       Type       | Required | Platform | HarmonyOS Support |
| :--------------------: | :------------------------------------------------------: | :--------------: | :------: | :------: | :---------------: |
| backdropPressableProps | 可按压背景道具        |  PressableProps  |    No    |    No    |        No         |
|        children        | 快速操作按钮子节点               | SpeedDial.Action |    No    |   All    |        Yes        |
|         isOpen         | 打开动作堆栈。       |     boolean      |    No    |   All    |        Yes        |
|     labelPressable     | 在所有操作中，按下标签上的“按下”按钮           |     boolean      |    No    |   All    |        Yes        |
|        onClose         | 当组件请求关闭时，会触发回调函数。 |     Function     |    No    |   All    |        Yes        |
|         onOpen         | 当组件请求打开时触发的回调。  |     Function     |    No    |   All    |        Yes        |
|        openIcon        | 当动作堆栈打开时，FAB上显示的图标。      |     IconNode     |    No    |   All    |        Yes        |
|      overlayColor      | 为快速操作按钮添加覆盖颜色。               |      string      |    No    |   All    |        Yes        |
|   transitionDuration   | 过渡的持续时间，以毫秒为单位。    |      number      |    No    |   All    |        Yes        |

**SpeedDial.Action**：浮动快速操作子按钮组件，接收所有 [FAB](https://reactnativeelements.com/docs/components/fab#props) 的props

|      Name      |      Description       |  Type   | Required | Platform | HarmonyOS Support |
| :------------: | :--------------------: | :-----: | :------: | :------: | :---------------: |
| labelPressable | 标签点击事件 | boolean |    No    |   All    |        Yes        |

**Switch**：滑动开关组件，接收所有[React Native Switch](https://reactnative.dev/docs/switch.html#props), [View](https://reactnative.dev/docs/view#props) 的props

| Name  |            Description             |  Type  | Required | Platform | HarmonyOS Support |
| :---: | :--------------------------------: | :----: | :------: | :------: | :---------------: |
| color | 附加按钮样式开关组件的颜色。 | string |    No    |   All    |        Yes        |

**Tab**：导航栏组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|       Name       |               Description                |                     Type                      | Required | Platform | HarmonyOS Support |
| :--------------: | :--------------------------------------: | :-------------------------------------------: | :------: | :------: | :---------------: |
|   buttonStyle    | 附加按钮样式         | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|  containerStyle  | 按钮容器的额外样式设计。 | `ViewStyle or (active: boolean) => ViewStyle` |    No    |    No    |        No         |
|      dense       | 紧凑标签项              |                    boolean                    |    No    |    No    |        No         |
| disableIndicator | 关闭下面的指示器。        |                    boolean                    |    No    |   All    |        Yes        |
|   iconPosition   | 图标位置        |       `left`，`right`，`top`，`bottom`        |    No    |   All    |        Yes        |
|  indicatorStyle  | 标签指示器的附加样式。  |                  View Style                   |    No    |   All    |        Yes        |
|     onChange     | 关于索引变更回调。         |            (value: number) => void            |    No    |   All    |        Yes        |
|    scrollable    | 使标签页滚动   |                    boolean                    |    No    |    No    |        No         |
|    titleStyle    | 附加按钮标题样式      | `ViewStyle or (active: boolean) => ViewStyle` |    No    |    No    |        No         |
|      value       | 子节点位置指标值。      |                    number                     |    No    |   All    |        Yes        |
|     variant      | 定义背景变量。      |             `primary`，`default`              |    No    |   All    |        Yes        |

**Tab.Item**：导航栏子组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props

|        Name        |                   Description                    |                     Type                      | Required | Platform | HarmonyOS Support |
| :----------------: | :----------------------------------------------: | :-------------------------------------------: | :------: | :------: | :---------------: |
|       active       | 允许定义TabItem是否处于活动状态      |                    boolean                    |    No    |    No    |        No         |
|    buttonStyle     | 附加按钮样式      | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|   containerStyle   | 按钮容器的附加样式。    | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|       dense        | 密集标签项            |                    boolean                    |    No    |    No    |        No         |
| iconContainerStyle | 为图标组件容器添加样式。 | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|     titleStyle     | 附加按钮标题样式          | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|      variant       | 定义背景变量。         |             `primary`，`default`              |    No    |    No    |        No         |

**TabView**：滑动开关内容组件

|         Name          |                         Description                          |          Type          | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :--------------------: | :------: | :------: | :---------------: |
|    animationConfig    | 定义动画配置。        |    AnimationConfig     |    No    |   All    |        Yes        |
|     animationType     | 在“弹簧”和“定时”中选择动画类型。当切换选项卡时，此选项可见。 |   `spring`，`timing`   |    No    |   All    |        Yes        |
|    containerStyle     | 组件容器的样式设计。       |       View Style       |    No    |   All    |        Yes        |
|     disableSwipe      | 滑动禁用与否             |        Boolean         |    No    |   All    |        Yes        |
|   disableTransition   | 禁用过渡         |        Boolean         |    No    |   All    |        Yes        |
|     minSwipeRatio     | 视图切换前所需的最小滑动距离。     |         number         |    No    |   All    |        Yes        |
|     minSwipeSpeed     | 视图切换前所需的最小滑动速度。        |         number         |    No    |   All    |        Yes        |
|       onChange        | 关于索引变更回调。           | (value: number) => any |    No    |   All    |        Yes        |
|     onSwipeStart      | 当用户滑动视图时，处理程序。           |  (direction) => void   |    No    |   All    |        Yes        |
| tabItemContainerStyle | TabView.Item组件容器的样式设计。         |       View Style       |    No    |   All    |        Yes        |
|         value         | 子节点位置指数值。                    |         number         |    No    |   All    |        Yes        |

**TabView.Item**：滑动开关内容子组件，接受所有 [View](https://reactnative.dev/docs/view#props) 的 props

**Text**：文本内容组件组件

|  Name   |           Description            |    Type    | Required | Platform | HarmonyOS Support |
| :-----: | :------------------------------: | :--------: | :------: | :------: | :---------------: |
|   h1    | 字体大小为40的文本。     |  boolean   |    No    |   All    |        Yes        |
| h1Style | 当h1标签被设置时的样式。      | Text Style |    No    |   All    |        Yes        |
|   h2    | 字体大小为34的文本。      |  boolean   |    No    |   All    |        Yes        |
| h2Style | 当h2标签被设置时的样式。      | Text Style |    No    |   All    |        Yes        |
|   h3    | 字体大小为28的文本。 |  boolean   |    No    |   All    |        Yes        |
| h3Style | 当h3标签被设置时的样式。      | Text Style |    No    |   All    |        Yes        |
|   h4    | 文本字体大小为22。     |  boolean   |    No    |   All    |        Yes        |
| h4Style | 当h4被设置时的样式。     | Text Style |    No    |   All    |        Yes        |
|  style  | 为文本添加额外的样式。 | Text Style |    No    |   All    |        Yes        |

**Tile**：卡片图块组件

|         Name          |                         Description                          |              Type              | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :----------------------------: | :------: | :------: | :---------------: |
|    ImageComponent     | 图块的自定义图像组件。                |        typeof Component        |    No    |   All    |        Yes        |
|     activeOpacity     | 按下时传递的数字用于控制不透明度。           |             number             |    No    |    No    |        No         |
|        caption        | 当卡片被突出显示时，文本位于倾斜区域内。          |           ReactNode            |    No    |   All    |        Yes        |
|     captionStyle      | 标题样式（可选）；仅当`caption`为字符串时使用此选项。 |           Text Style           |    No    |   All    |        Yes        |
|    containerStyle     | 外部卡片容器的样式设计。             |           View Style           |    No    |   All    |        Yes        |
| contentContainerStyle | 当容器未被用作特色卡片时，其样式设计。    |           View Style           |    No    |   All    |        Yes        |
|       featured        | 改变互动程序的外观。         |            boolean             |    No    |   All    |        Yes        |
|        height         | 卡片的高度。                     |             number             |    No    |   All    |        Yes        |
|         icon          | 图标组件属性。             |           IconObject           |    No    |   All    |        Yes        |
|  iconContainerStyle   | 外部图标容器的样式设计。             |           View Style           |    No    |   All    |        Yes        |
|  imageContainerStyle  | 为图片设计样式。                |           View Style           |    No    |   All    |        Yes        |
|      imageProps       | 如果提供了可选属性，例如“resizeMode”，则将其传递给图像。 |       ImageProps(Object)       |    No    |   All    |        Yes        |
|       imageSrc        | 图片来源。                         | `string`,`ImageSourcePropType` |    No    |   All    |        Yes        |
| overlayContainerStyle | 使用特色卡片时，对叠加容器进行样式设计。  |           View Style           |    No    |    No    |        No         |
|         title         | 互动程序内的文本。                         |             string             |    No    |   All    |        Yes        |
|  titleNumberOfLines   | 标题的行数。                      |             number             |    No    |   All    |        Yes        |
|      titleStyle       | 标题样式                   |           Text Style           |    No    |   All    |        Yes        |
|         width         | 卡片宽度                  |             number             |    No    |   All    |        Yes        |

**Tooltip**：文本提示组件

|           Name           |                         Description                          |                           Type                           | Required | Platform | HarmonyOS Support |
| :----------------------: | :----------------------------------------------------------: | :------------------------------------------------------: | :------: | :------: | :---------------: |
|      ModalComponent      | 重写 React Native 的 `Modal` 组件（适用于 Web 平台）。 |                     typeof Component                     |    No    |   All    |        Yes        |
|      animationType       | 动画类型                    |                      `none`,`fade`                       |    No    |   All    |        Yes        |
|     backgroundColor      | 设置工具提示和指针的背景颜色。    |                        ColorValue                        |    No    |   All    |        Yes        |
| closeOnlyOnBackdropPress | 一个标志，用于确定在活动工具提示弹出容器内任何位置触摸/滚动时，是否禁用工具提示的自动隐藏功能。当该标志为`true`时，仅当覆盖背景被按下（或）高亮显示的工具提示按钮被按下时，工具提示才会关闭。 |                         boolean                          |    No    |    No    |        No         |
|      containerStyle      | 将样式对象传递给工具提示容器        |                        View Style                        |    No    |   All    |        Yes        |
|          height          | 提示容器高度。为了在正确位置呈现容器，这是必要的。根据容器内呈现的内容大小来传递高度。 |                          number                          |    No    |   All    |        Yes        |
|      highlightColor      | 用于高亮显示工具提示所环绕的项目的颜色。   |                        ColorValue                        |    No    |   All    |        Yes        |
|         onClose          | 关闭工具提示时调用的函数。      |                         Function                         |    No    |   All    |        Yes        |
|          onOpen          | 在打开工具提示时调用的函数。      |                         Function                         |    No    |   All    |        Yes        |
|       overlayColor       | 工具提示打开时覆盖阴影的颜色。         |                        ColorValue                        |    No    |   All    |        Yes        |
|       pointerColor       | 工具提示指针的颜色，默认为 [`backgroundColor`](https://reactnativeelements.com/docs/components/tooltip#backgroundcolor) if none is passed. |                        ColorValue                        |    No    |   All    |        Yes        |
|       pointerStyle       | 指针上应用的样式。       |                        View Style                        |    No    |   All    |        Yes        |
|         popover          | 作为显示容器呈现的组件。       | `ReactElement<{}, string`，`JSXElementConstructor<any>>` |    No    |   All    |        Yes        |
|   skipAndroidStatusBar   | 在计算元素位置时，强制跳过StatusBar的高度。如果在react-native Modal组件内部使用了Tooltip，请传入`true`。 |                         boolean                          |    No    |   No    |        No        |
|       toggleAction       | 定义应触发工具提示的操作类型。可用选项包括 *onPress* 和 *onLongPress* |                          string                          |    No    |   All    |        Yes        |
|      toggleOnPress       | 一个标志，用于确定按下时是否切换工具提示。   |                         boolean                          |    No    |   All    |        Yes        |
|         visible          | 显示工具提示。                    |                         boolean                          |    No    |   All    |        Yes        |
|          width           | 提示容器宽度。为了在正确位置呈现容器，这是必要的。 |                          number                          |    No    |   All    |        Yes        |
|       withOverlay        | 一个标志，用于确定在工具提示打开时是否显示蒙层。 |                         boolean                          |    No    |   All    |        Yes        |
|       withPointer        | 一个标志，用于确定是否显示小尖角。   |                         boolean                          |    No    |   All    |        Yes        |

## 遗留问题
## 其他

-  Rating组件的readonly、onFinishRating等属性无法生效，与Android/iOS一致：[issue#1](https://github.com/react-native-elements/react-native-elements/issues/3736)、[issue#2](https://github.com/react-native-elements/react-native-elements/issues/3718)。
-  AirbnbRatings组件的startImage属性无法生效，与Android/iOS一致：[issue#3](https://github.com/react-native-elements/react-native-elements/issues/3718)。
-  ButtonGroups组件的activeOpacity、button等属性无法生效，与Android/iOS一致：[issue#4](https://github.com/react-native-elements/react-native-elements/issues/3938)。
-  Dialog组件的onLongPress、onpressIn等属性无法生效，与Android/iOS一致：[issue#5](https://github.com/react-native-elements/react-native-elements/issues/3931)。
-  Header组件的barStyle、elevated等属性无法生效，与Android、iOS一致：[issue#6](https://github.com/react-native-elements/react-native-elements/issues/3935)。
-  Input组件的renderErrorMessage属性无法生效，与Android、iOS一致：[issue#7](https://github.com/react-native-elements/react-native-elements/issues/3933)。
-  ListItem.Swipeable组件的minSlideWidth属性无法生效，与Android、iOS一致：[issue#8](https://github.com/react-native-elements/react-native-elements/issues/3825)。
-  ListItem.Title组件的right属性无法生效，与Android、iOS一致：[issue#9](https://github.com/react-native-elements/react-native-elements/issues/3934)。
-  SearchBar组件的cancelButtonProps、showCancel等属性无法生效，与Android、iOS一致：[issue#10](https://github.com/react-native-elements/react-native-elements/issues/3939)。
-  SocialIcon组件的fontFamily、fontWeight等属性无法生效，与Android、iOS一致：[issue#11](https://github.com/react-native-elements/react-native-elements/issues/3940)。
-  SpeedDial组件的backdropPressableProps属性无法生效，与Android、iOS一致：[issue#12](https://github.com/react-native-elements/react-native-elements/issues/3937)。
-  Tab组件的containerStyle、dense等属性无法生效，与Android、iOS一致：[issue#13](https://github.com/react-native-elements/react-native-elements/issues/3941)。
-  Tab.Item组件的active、dense等属性无法生效，与Android、iOS一致：[issue#14](https://github.com/react-native-elements/react-native-elements/issues/3936)。
-  Tile组件的activeOpacity等属性无法生效，与Android、iOS一致：[issue#15](https://github.com/react-native-elements/react-native-elements/issues/3932)。
-  Tooltip组件的closeOnlyOnBackdropPress属性无法生效，与Android、iOS一致：[issue#16](https://github.com/react-native-elements/react-native-elements/issues/3811)。
-  Overlay组件接收View的所有属性无效，与Android/iOS一致：[issue#17](https://github.com/react-native-elements/react-native-elements/issues/3950)。
-  Slider组件的属性animateTransitions单独设置为true报错：[issue#18](https://github.com/react-native-elements/react-native-elements/issues/3928)。
-  ListItem.Subtitle组件的right属性设置无效，与Android、iOS一致：[issue#19](https://github.com/react-native-elements/react-native-elements/issues/3951)。
-  Icon组件的brand属性设置无效，与Android、iOS一致：[issue#20](https://github.com/react-native-elements/react-native-elements/issues/3952)。
-  Header组件的centerComponent属性设置上下无法居中：[issue#21](https://github.com/react-native-elements/react-native-elements/issues/3953)。
-  ToolTip组件的skipAndroidStatusBar属性设置无效，与Android、iOS一致：[issue#22](https://github.com/react-native-elements/react-native-elements/issues/3954)。
-  Slider组件的当前进度条未完全覆盖总进度条，与Android、iOS一致：[issuse#23](https://github.com/react-native-elements/react-native-elements/issues/4010)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-elements/react-native-elements/blob/next/LICENSE)，请自由地享受和参与开源。
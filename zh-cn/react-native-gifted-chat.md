> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-gifted-chat</code> </h1>
</p>
<p align="center">
   <a href="https://github.com/FaridSafi/react-native-gifted-chat">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
   <a href="https://github.com/FaridSafi/react-native-gifted-chat/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/FaridSafi/react-native-gifted-chat)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 2.4.0      | 0.72       |
| 2.8.1      | 0.77       |

进入到工程目录并输入以下命令：

<!-- tabs:start -->


#### **npm**

```bash
#0.72
npm install react-native-gifted-chat@2.4.0
#0.77
npm install react-native-gifted-chat@2.8.1
```

#### **yarn**

```bash
#0.72
yarn add react-native-gifted-chat@2.4.0
#0.77
yarn add react-native-gifted-chat@2.8.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from 'react'
import { View } from 'react-native'

import { GiftedChat, IMessage } from 'react-native-gifted-chat'

export function App() {
  const [messages, setMessages] = useState([
    {
      _id: 1,
      text: 'My message111',
      createdAt: new Date(Date.UTC(2016, 5, 11, 17, 20, 0)),
      user: {
        _id: 2,
        name: 'React Native',
        avatar: 'https://facebook.github.io/react/img/logo_og.png',
      },
      quickReplies: {
        type: 'radio', // or 'checkbox',
        keepIt: true,
        values: [
          {
            title: '😋 Yes',
            value: 'yes',
          },
          {
            title: '📷 Yes, let me show you with a picture!',
            value: 'yes_picture',
          },
          {
            title: '😞 Nope. What?',
            value: 'no',
          },
        ],
      },
    },
  ])

  const onSend = (newMsg: IMessage[]) => setMessages([...messages, ...newMsg])

  return (
    <View style={{ flex: 1}}>
      <GiftedChat
        messages={messages}
        onSend={onSend}
        user={{_id: 1, name: 'Developer'}}
        messagesContainerStyle={{ flex: 1 }}
        isKeyboardInternallyHandled={false}
      />
    </View>
  )
}
```

Link
本库 HarmonyOS 侧2.8.1版本实现依赖react-native-keyboard-controller的代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-keyboard-controller 文档](/zh-cn/react-native-keyboard-controller.md#link)

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|              Name               |                         Description                          |      Type       | Required |  Platform   | HarmonyOS Support |
| :-----------------------------: | :----------------------------------------------------------: | :-------------: | :------: | :---------: | :---------------: |
|     **messageContainerRef**     |                    指向 FlatList 的引用 (Ref)                     | *FlatList ref*  |    No    | iOS/Android |        Yes        |
|        **textInputRef**         |                    指向 TextInput 的引用 (Ref)                     | *TextInput ref* |    No    | iOS/Android |        Yes        |
|          **messages**           |                     要显示的消息                      |     *Array*     |    No    | iOS/Android |        Yes        |
|          **isTyping**           | 输入指示器状态；如果使用了 `renderFooter`，将会覆盖此设置 |     Boolean     |    No    | iOS/Android |        Yes        |
|            **text**             |                          输入的文本                          |     String      |    No    | iOS/Android |        Yes        |
|         **placeholder**         | 当 `text` 为空时的占位符；默认为 `'Type a message...'` |     String      |    No    | iOS/Android |        Yes        |
|     **messageIdGenerator**      |     为新消息生成 ID。默认为 UUID v4     |   *Function*    |    No    | iOS/Android |        Yes        |
|            **user**             |                  发送消息的用户                   |    *Object*     |    No    | iOS/Android |        Yes        |
|           **onSend**            |               发送消息时的回调                |   *Function*    |    No    | iOS/Android |        Yes        |
|       **alwaysShowSend**        |        在文本输入编辑器中始终显示发送按钮        |     Boolean     |    No    | iOS/Android |        Yes        |
|           **locale**            | 用于本地化日期的语言环境 (Locale)。你需要先导入所需的语言环境（例如 `require('dayjs/locale/de')` 或 `import 'dayjs/locale/fr'`) |    *String*     |    No    | iOS/Android |        Yes        |
|         **timeFormat**          | *(String)* - 用于渲染时间的格式；默认为 `'LT'`（参见 [Day.js Format](https://day.js.org/docs/en/display/format)） |    *String*     |    No    | iOS/Android |        Yes        |
|         **dateFormatCalendar**<sup>2.8.1+</sup>          | 用于渲染相对时间的格式；例如 Today（参见 [Day.js Calendar](https://day.js.org/docs/en/plugin/calendar)） |    *String*     |    No    | iOS/Android |        Yes        |
|         **dateFormat**          | 用于渲染日期的格式；默认为 `'ll'`（参见 [Day.js Format](https://day.js.org/docs/en/display/format)） |    *String*     |    No    | iOS/Android |        Yes        |
|         **loadEarlier**         | 启用“加载更早消息”按钮，`infiniteScroll` 需要此项 |     Boolean     |    No    | iOS/Android |        Yes        |
| **isKeyboardInternallyHandled** | 决定是否在插件内部处理键盘感知。如果你在插件外部有自己的键盘处理逻辑，请将其设为 false；默认为 `true` |     Boolean     |    No    | iOS/Android |        Yes        |
| **disableKeyboardController**<sup>2.8.1+</sup> | 完全禁用 react-native-keyboard-controller。在使用 react-native-navigation 或其他冲突的键盘库时很有用；默认为 `false` |     Boolean     |    No    | iOS/Android |        Yes        |
|        **onLoadEarlier**        |            加载更早消息时的回调            |   *Function*    |    No    | iOS/Android |        Yes        |
|      **isLoadingEarlier**       | 加载更早消息时显示 `ActivityIndicator` |     Boolean     |    No    | iOS/Android |        Yes        |
|        **renderLoading**        |           初始化时渲染加载视图            |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderLoadEarlier**      |            自定义“加载更早消息”按钮             |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderAvatar**         | 自定义消息头像；设置为 `null` 则不渲染该消息的任何头像 |   *Function*    |    No    | iOS/Android |        Yes        |
|       **showUserAvatar**        | 是否渲染当前用户的头像；默认为 `false`，仅显示其他用户的头像 |     Boolean     |    No    | iOS/Android |        Yes        |
|  **showAvatarForEveryMessage**  | 即使是同一用户同一天的连续消息，也会显示头像 |     Boolean     |    No    | iOS/Android |        Yes        |
|        **onPressAvatar**        |           点击消息头像时的回调           |   *Function*    |    No    | iOS/Android |        Yes        |
|      **onLongPressAvatar**      |        长按消息头像时的回调        |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderAvatarOnTop**      | 在连续消息的顶部渲染消息头像 |     Boolean     |    No    | iOS/Android |        Yes        |
|        **renderBubble**         |                    自定义消息气泡                     |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderTicks**         |       自定义勾号指示器以显示消息状态       |    Function     |    No    | iOS/Android |        Yes        |
|     **renderSystemMessage**     |                    自定义系统消息                     |    Function     |    No    | iOS/Android |        Yes        |
|           **onPress**           |          点击消息气泡时的回调           |    Function     |    No    | iOS/Android |        Yes        |
|         **onLongPress**         | 长按消息气泡时的回调；默认显示带有“复制文本”的 ActionSheet（参见[使用 `showActionSheetWithOptions()` 的示例](https://github.com/FaridSafi/react-native-gifted-chat/blob/master@{2017-09-25}/src/Bubble.js#L96-L119)） |    Function     |    No    | iOS/Android |        Yes        |
|          **inverted**           |             反转 `messages` 的显示顺序             |     Boolean     |    No    | iOS/Android |        Yes        |
|   **renderUsernameOnMessage**   | 指示是否在消息气泡内显示用户名 |     Boolean     |    No    | iOS/Android |        Yes        |
|       **renderUsername**        |                  自定义用户名容器                   |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderMessage**        |                   自定义消息容器                   |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderMessageText**      |                     自定义消息文本                      |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderMessageImage**      |                     自定义消息图片                     |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderMessageVideo**      |                     自定义消息视频                     |   *Function*    |    No    | iOS/Android |        Yes        |
|         **imageProps**          | 传递给默认 `renderMessageImage` 创建的 `Image` 组件的额外属性 |    *Object*     |    No    | iOS/Android |        Yes        |
|         **videoProps**          | 传递给必需的 `renderMessageVideo` 创建的视频组件的额外属性 |    *Object*     |    No    | iOS/Android |        Yes        |
|         **imageSourceProps**<sup>2.8.1+</sup>          | 传递给 `MessageImage` 的额外属性 |    *Object*     |    No    | iOS/Android |        Yes        |
|        **lightboxProps**        | 传递给 `MessageImage` 的 [Lightbox](https://github.com/oblador/react-native-lightbox) 的额外属性 |    *Object*     |    No    | iOS/Android |        Yes        |
|     **isCustomViewBottom**      | 决定 `renderCustomView` 是显示在文本、图片和视频视图之前还是之后 |     Boolean     |    No    | iOS/Android |        Yes        |
|      **renderCustomView**       |                气泡内的自定义视图                 |   *Function*    |    No    | iOS/Android |        Yes        |
|          **renderDay**          |                  消息上方的自定义日期                  |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderTime**          |                 消息内的自定义时间                 |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderFooter**         | ListView 上的自定义页脚组件，例如 `'User is typing...'`；参见 [CustomizedFeaturesExample.tsx](https://github.com/FaridSafi/react-native-gifted-chat/blob/master/example/components/chat-examples/CustomizedFeaturesExample.tsx) 示例。覆盖 `isTyping` 为 true 时触发的默认输入指示器 |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderChatEmpty**       | 当消息为空时在 ListView 中渲染的自定义组件 |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderChatFooter**       | 渲染在 MessageContainer 下方的自定义组件（与 ListView 分离） |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderInputToolbar**      |              自定义消息编辑器容器               |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderComposer**        |              自定义文本输入消息编辑器              |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderActions**        |   消息编辑器左侧的自定义操作按钮   |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderSend**          | 自定义发送按钮；你可以很容易地将子元素传递给原始的 `Send` 组件，例如使用自定义图标（[示例](https://github.com/FaridSafi/react-native-gifted-chat/pull/487)） |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderAccessory**       |   消息编辑器下方的自定义第二行操作栏   |   *Function*    |    No    | iOS/Android |        Yes        |
|     **onPressActionButton**     | 点击操作按钮时的回调（如果设置，将不使用默认的 `actionSheet`） |   *Function*    |    No    | iOS/Android |        Yes        |
|        **bottomOffset**         | 聊天界面距离屏幕底部的距离（例如，如果你显示标签栏时很有用） |     Number      |    No    | iOS/Android |        No         |
|        **focusOnInputWhenOpeningKeyboard**<sup>2.8.1+</sup>         | 打开键盘时自动聚焦；默认为 true |     Bool      |    No    | iOS/Android |        No         |
|    **minInputToolbarHeight**    |     输入工具栏的最小高度；默认为 `44`     |     Number      |    No    | iOS/Android |        No         |
|        **listViewProps**        | 传递给消息列表 `ListView` 的额外属性；某些属性无法覆盖，详情请参阅 `MessageContainer.render()` 中的代码 |    *Object*     |    No    | iOS/Android |        Yes        |
|       **textInputProps**        | 传递给 `TextInput` 的额外属性 |    *Object*     |    No    | iOS/Android |        Yes        |
|       **textInputStyle**        | 传递给 `TextInput` 的自定义样式 |    *Object*     |    No    | iOS/Android |        Yes        |
|          **multiline**          | 指示是否允许 `TextInput` 多行输入 |     Boolean     |    No    | iOS/Android |        Yes        |
|  **keyboardShouldPersistTaps**  | 决定点击后键盘是否保持可见；参见 `ScrollView` 文档 |     String      |    No    | iOS/Android |        Yes        |
|     **onInputTextChanged**      |             输入文本改变时的回调             |   *Function*    |    No    | iOS/Android |        Yes        |
|       **maxInputLength**        |            消息编辑器 TextInput 的最大长度             |    *Number*     |    No    | iOS/Android |        Yes        |
|        **parsePatterns**        | 用于 [react-native-parsed-text](https://github.com/taskrabbit/react-native-parsed-text) 的自定义解析模式，用于链接消息内容（如 URL 和电话号码），例如： |   *Function*    |    No    | iOS/Android |        Yes        |
|          **extraData**          | 用于按需重新渲染 FlatList 的额外属性。这对渲染页脚等很有用。 |    *Object*     |    No    | iOS/Android |        Yes        |
|      **minComposerHeight**      |              编辑器的自定义最小高度               |    *Object*     |    No    | iOS/Android |        Yes        |
|      **maxComposerHeight**      |              编辑器的自定义最大高度               |    *Object*     |    No    | iOS/Android |        No         |
|       **scrollToBottom**        |  启用滚动到底部组件（默认为 false）   |     Boolean     |    No    | iOS/Android |        Yes        |
|   **scrollToBottomComponent**   |         自定义滚动到底部组件容器          |   *Function*    |    No    | iOS/Android |        Yes        |
|    **scrollToBottomOffset**     | 开始显示滚动到底部组件的自定义高度偏移量（默认为 200） |    *Number*     |    No    | iOS/Android |        Yes        |
|     **scrollToBottomStyle**     |         底部组件容器的自定义样式          |    *Object*     |    No    | iOS/Android |        Yes        |
|          **alignTop**           | 控制消息气泡是否出现在聊天界面的顶部（默认为 false - 气泡底部对齐） |    *Boolean*    |    No    | iOS/Android |        Yes        |
|        **onQuickReply**         |   发送快捷回复时的回调（发送到后端服务器）    |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderQuickReplies**      |                 自定义所有快捷回复视图                  |   *Function*    |    No    | iOS/Android |        Yes        |
|       **quickReplyStyle**       |                自定义快捷回复视图样式                 |    *Object*     |    No    | iOS/Android |        Yes        |
|       **quickReplyContainerStyle**<sup>2.8.1+</sup>       |                自定义快捷回复容器视图样式                 |    *Object*     |    No    | iOS/Android |        Yes        |
|    **renderQuickReplySend**     |                 自定义快捷回复发送视图                 |   *Function*    |    No    | iOS/Android |        Yes        |
|     **shouldUpdateMessage**     | 让消息组件知道何时在正常情况之外进行更新。 |   *Function*    |    No    | iOS/Android |        Yes        |
|       **infiniteScroll**        | 当到达消息容器顶部时无限向上滚动，如果存在 `onLoadEarlier` 函数则自动调用（暂不支持 Web）。你需要同时添加 `loadEarlier` 属性。 |    *Boolean*    |    No    | iOS/Android |        Yes        |
|       **isStatusBarTranslucentAndroid**<sup>2.8.1+</sup>        | 如果你在 Android 上使用半透明状态栏，请将此选项设置为 true。在 iOS 上被忽略。 |    *Boolean*    |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他
-  输入框最大高 maxComposerHeight 设置无效果 maxComposerHeight为复杂数据类型,设置后在HarmonyOS侧效果偶发
-  输入工具栏最小高 minInputToolbarHeight 设置无效,与iOS一致
-  聊天与屏幕底部的距离 bottomOffset 设置无效,与iOS一致

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/FaridSafi/react-native-gifted-chat/blob/master/LICENSE) ，请自由地享受和参与开源。
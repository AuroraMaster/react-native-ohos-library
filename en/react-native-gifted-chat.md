> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/FaridSafi/react-native-gifted-chat)

## Installation and Usage

| Library Version | Supported RN Version |
| :--- | :--- |
| 2.4.0 | 0.72 |
| 2.8.1 | 0.77 |

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

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
The HarmonyOS implementation (version 2.8.1) of this library depends on the code of `react-native-keyboard-controller`. If this library has already been integrated into your HarmonyOS project, there is no need to include it again. You can skip the steps in this section and proceed directly.

If it has not been included, please refer to the [react-native-keyboard-controller docs](/en/react-native-keyboard-controller.md#link).

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## Properties

>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|              Name               |                         Description                          |      Type       | Required |  Platform   | HarmonyOS Support |
| :-----------------------------: | :----------------------------------------------------------: | :-------------: | :------: | :---------: | :---------------: |
|     **messageContainerRef**     |                    Ref to the FlatList                     | *FlatList ref*  |    No    | iOS/Android |        Yes        |
|        **textInputRef**         |                    Ref to the TextInput                     | *TextInput ref* |    No    | iOS/Android |        Yes        |
|          **messages**           |                     Messages to display                      |     *Array*     |    No    | iOS/Android |        Yes        |
|          **isTyping**           | Typing Indicator state; If you use `renderFooter` it will override this |     Boolean     |    No    | iOS/Android |        Yes        |
|            **text**             |                          Input text                          |     String      |    No    | iOS/Android |        Yes        |
|         **placeholder**         | Placeholder when `text` is empty; default is `'Type a message...'` |     String      |    No    | iOS/Android |        Yes        |
|     **messageIdGenerator**      |     Generate an id for new messages. Defaults to UUID v4     |   *Function*    |    No    | iOS/Android |        Yes        |
|            **user**             |                  User sending the messages                   |    *Object*     |    No    | iOS/Android |        Yes        |
|           **onSend**            |               Callback when sending a message                |   *Function*    |    No    | iOS/Android |        Yes        |
|       **alwaysShowSend**        |        Always show send button in input text composer        |     Boolean     |    No    | iOS/Android |        Yes        |
|           **locale**            | Locale to localize the dates. You need first to import the locale you need (ie. `require('dayjs/locale/de')` or `import 'dayjs/locale/fr'`) |    *String*     |    No    | iOS/Android |        Yes        |
|         **timeFormat**          | *(String)* - Format to use for rendering times; default is `'LT'` (see [Day.js Format](https://day.js.org/docs/en/display/format)) |    *String*     |    No    | iOS/Android |        Yes        |
|         **dateFormatCalendar**<sup>2.8.1+</sup>          | Format to use for rendering relative times; Today - for now (see [Day.js Calendar](https://day.js.org/docs/en/plugin/calendar)) |    *String*     |    No    | iOS/Android |        Yes        |
|         **dateFormat**          | Format to use for rendering dates; default is `'ll'` (see [Day.js Format](https://day.js.org/docs/en/display/format)) |    *String*     |    No    | iOS/Android |        Yes        |
|         **loadEarlier**         | Enables the "load earlier messages" button, required for `infiniteScroll` |     Boolean     |    No    | iOS/Android |        Yes        |
| **isKeyboardInternallyHandled** | Determine whether to handle keyboard awareness inside the plugin. If you have your own keyboard handling outside the plugin set this to false; default is `true` |     Boolean     |    No    | iOS/Android |        Yes        |
| **disableKeyboardController**<sup>2.8.1+</sup> | Completely disable react-native-keyboard-controller. Useful when using react-native-navigation or other conflicting keyboard libraries; default is `false` |     Boolean     |    No    | iOS/Android |        Yes        |
|        **onLoadEarlier**        |            Callback when loading earlier messages            |   *Function*    |    No    | iOS/Android |        Yes        |
|      **isLoadingEarlier**       | Display an `ActivityIndicator` when loading earlier messages |     Boolean     |    No    | iOS/Android |        Yes        |
|        **renderLoading**        |           Render a loading view when initializing            |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderLoadEarlier**      |            Custom "Load earlier messages" button             |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderAvatar**         | Custom message avatar; set to `null` to not render any avatar for the message |   *Function*    |    No    | iOS/Android |        Yes        |
|       **showUserAvatar**        | Whether to render an avatar for the current user; default is `false`, only show avatars for other users |     Boolean     |    No    | iOS/Android |        Yes        |
|  **showAvatarForEveryMessage**  | avatars will only be displayed when a consecutive message is from the same user on the same day |     Boolean     |    No    | iOS/Android |        Yes        |
|        **onPressAvatar**        |           Callback when a message avatar is tapped           |   *Function*    |    No    | iOS/Android |        Yes        |
|      **onLongPressAvatar**      |        Callback when a message avatar is long-pressed        |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderAvatarOnTop**      | Render the message avatar at the top of consecutive messages |     Boolean     |    No    | iOS/Android |        Yes        |
|        **renderBubble**         |                    Custom message bubble                     |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderTicks**         |       Custom ticks indicator to display message status       |    Function     |    No    | iOS/Android |        Yes        |
|     **renderSystemMessage**     |                    Custom system message                     |    Function     |    No    | iOS/Android |        Yes        |
|           **onPress**           |          Callback when a message bubble is pressed           |    Function     |    No    | iOS/Android |        Yes        |
|         **onLongPress**         | Callback when a message bubble is long-pressed; default is to show an ActionSheet with "Copy Text" (see [example using `showActionSheetWithOptions()`](https://github.com/FaridSafi/react-native-gifted-chat/blob/master@{2017-09-25}/src/Bubble.js#L96-L119)) |    Function     |    No    | iOS/Android |        Yes        |
|          **inverted**           |             Reverses display order of `messages`             |     Boolean     |    No    | iOS/Android |        Yes        |
|   **renderUsernameOnMessage**   | Indicate whether to show the user's username inside the message bubble |     Boolean     |    No    | iOS/Android |        Yes        |
|       **renderUsername**        |                  Custom Username container                   |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderMessage**        |                   Custom message container                   |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderMessageText**      |                     Custom message text                      |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderMessageImage**      |                     Custom message image                     |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderMessageVideo**      |                     Custom message video                     |   *Function*    |    No    | iOS/Android |        Yes        |
|         **imageProps**          | Extra props to be passed to the `Image` component created by the default `renderMessageImage` |    *Object*     |    No    | iOS/Android |        Yes        |
|         **videoProps**          | Extra props to be passed to the video component created by the required `renderMessageVideo` |    *Object*     |    No    | iOS/Android |        Yes        |
|         **imageSourceProps**<sup>2.8.1+</sup>          | Extra props to be passed to the `MessageImage`'s |    *Object*     |    No    | iOS/Android |        Yes        |
|        **lightboxProps**        | Extra props to be passed to the `MessageImage`'s [Lightbox](https://github.com/oblador/react-native-lightbox) |    *Object*     |    No    | iOS/Android |        Yes        |
|     **isCustomViewBottom**      | Determine whether renderCustomView is displayed before or after the text, image and video views |     Boolean     |    No    | iOS/Android |        Yes        |
|      **renderCustomView**       |                Custom view inside the bubble                 |   *Function*    |    No    | iOS/Android |        Yes        |
|          **renderDay**          |                  Custom day above a message                  |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderTime**          |                 Custom time inside a message                 |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderFooter**         | Custom footer component on the ListView, e.g. `'User is typing...'`; see [CustomizedFeaturesExample.tsx](https://github.com/FaridSafi/react-native-gifted-chat/blob/master/example/components/chat-examples/CustomizedFeaturesExample.tsx) for an example. Overrides default typing indicator that triggers when `isTyping` is true |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderChatEmpty**       | Custom component to render in the ListView when messages are empty |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderChatFooter**       | Custom component to render below the MessageContainer (separate from the ListView) |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderInputToolbar**      |              Custom message composer container               |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderComposer**        |              Custom text input message composer              |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderActions**        |   Custom action button on the left of the message composer   |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderSend**          | Custom send button; you can pass children to the original `Send` component quite easily, for example, to use a custom icon ([example](https://github.com/FaridSafi/react-native-gifted-chat/pull/487)) |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderAccessory**       |   Custom second line of actions below the message composer   |   *Function*    |    No    | iOS/Android |        Yes        |
|     **onPressActionButton**     | Callback when the Action button is pressed (if set, the default `actionSheet` will not be used) |   *Function*    |    No    | iOS/Android |        Yes        |
|        **bottomOffset**         | Distance of the chat from the bottom of the screen (e.g. useful if you display a tab bar) |     Number      |    No    | iOS/Android |        No         |
|        **focusOnInputWhenOpeningKeyboard**<sup>2.8.1+</sup>         | Focus on automatically when opening the keyboard; default true |     Bool      |    No    | iOS/Android |        No         |
|    **minInputToolbarHeight**    |     Minimum height of the input toolbar; default is `44`     |     Number      |    No    | iOS/Android |        No         |
|        **listViewProps**        | Extra props to be passed to the messages `ListView`; some props can't be overridden, see the code in `MessageContainer.render()` for details |    *Object*     |    No    | iOS/Android |        Yes        |
|       **textInputProps**        | Extra props to be passed to the `TextInput` |    *Object*     |    No    | iOS/Android |        Yes        |
|       **textInputStyle**        | Custom style to be passed to the `TextInput` |    *Object*     |    No    | iOS/Android |        Yes        |
|          **multiline**          | Indicates whether to allow the `TextInput` to be multiple lines or not |     Boolean     |    No    | iOS/Android |        Yes        |
|  **keyboardShouldPersistTaps**  | Determines whether the keyboard should stay visible after a tap; see `ScrollView` docs |     String      |    No    | iOS/Android |        Yes        |
|     **onInputTextChanged**      |             Callback when the input text changes             |   *Function*    |    No    | iOS/Android |        Yes        |
|       **maxInputLength**        |            Max message composer TextInput length             |    *Number*     |    No    | iOS/Android |        Yes        |
|        **parsePatterns**        | Custom parse patterns for [react-native-parsed-text](https://github.com/taskrabbit/react-native-parsed-text) used to linking message content (like URLs and phone numbers), e.g.: |   *Function*    |    No    | iOS/Android |        Yes        |
|          **extraData**          | Extra props for re-rendering FlatList on demand. This will be useful for rendering footer etc. |    *Object*     |    No    | iOS/Android |        Yes        |
|      **minComposerHeight**      |              Custom min-height of the composer               |    *Object*     |    No    | iOS/Android |        Yes        |
|      **maxComposerHeight**      |              Custom max height of the composer               |    *Object*     |    No    | iOS/Android |        No         |
|       **scrollToBottom**        |  Enables the scroll to bottom Component (Default is false)   |     Boolean     |    No    | iOS/Android |        Yes        |
|   **scrollToBottomComponent**   |         Custom Scroll To Bottom Component container          |   *Function*    |    No    | iOS/Android |        Yes        |
|    **scrollToBottomOffset**     | Custom Height Offset upon which to begin showing Scroll To Bottom Component (Default is 200) |    *Number*     |    No    | iOS/Android |        Yes        |
|     **scrollToBottomStyle**     |         Custom style for Bottom Component container          |    *Object*     |    No    | iOS/Android |        Yes        |
|          **alignTop**           | Controls whether or not the message bubbles appear at the top of the chat (Default is false - bubbles align to bottom) |    *Boolean*    |    No    | iOS/Android |        Yes        |
|        **onQuickReply**         |   Callback when sending a quick reply (to backend server)    |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderQuickReplies**      |                 Custom all quick reply view                  |   *Function*    |    No    | iOS/Android |        Yes        |
|       **quickReplyStyle**       |                Custom quick reply view style                 |    *Object*     |    No    | iOS/Android |        Yes        |
|       **quickReplyContainerStyle**<sup>2.8.1+</sup>       |                Custom quick reply container view style                 |    *Object*     |    No    | iOS/Android |        Yes        |
|    **renderQuickReplySend**     |                 Custom quick reply send view                 |   *Function*    |    No    | iOS/Android |        Yes        |
|     **shouldUpdateMessage**     | Lets the message component know when to update outside of normal cases. |   *Function*    |    No    | iOS/Android |        Yes        |
|       **infiniteScroll**        | infinite scroll up when reach the top of messages container, automatically call onLoadEarlier function if exist (not yet supported for the web). You need to add `loadEarlier` prop too. |    *Boolean*    |    No    | iOS/Android |        Yes        |
|       **isStatusBarTranslucentAndroid**<sup>2.8.1+</sup>        | If you use translucent status bar on Android, set this option to true. Ignored on iOS. |    *Boolean*    |    No    | iOS/Android |        Yes        |


## Known Issues

## Others
-  The **maxComposerHeight** setting is invalid. **maxComposerHeight** is a complex data type, and its effect is sporadic on HarmonyOS.
-  The **minInputToolbarHeight** setting is invalid on HarmonyOS, which is consistent with that on iOS.
-  The **bottomOffset** setting is invalid on HarmonyOS, which is consistent with that on iOS.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/FaridSafi/react-native-gifted-chat/blob/master/LICENSE).
> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-offline</code> </h1>
</p>

> [!TIP] [GitHub address](https://github.com/rgommezz/react-native-offline)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 6.0.2     |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install  react-native-offline@6.0.2
```

#### **yarn**

```bash
yarn add react-native-offline@6.0.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Button } from 'react-native';
import { NetworkProvider, NetworkConsumer, useIsConnected, checkInternetConnection } from 'react-native-offline';

interface Context {
    pingUrl: string;
}

const DummyNetworkContext = React.createContext<Context>({
    pingUrl: 'https://www.huawei.com',
});

export const offlineDemoTest = () => {
    const isConnected = useIsConnected();
    const DEFAULT_TIMEOUT = 3000;
    const DEFAULT_PING_SERVER_URL = 'https://www.huawei.com/';
    const DEFAULT_HTTP_METHOD = 'HEAD';
    const DEFAULT_CUSTOM_HEADERS = {};
    return (
        <View>
            <View>
                {isConnected ? 'isConnected:YES' : 'isConnected:NO'}
            </View>
            <View>
                <DummyNetworkContext.Consumer>
                    {({ pingUrl }) => (
                        <NetworkProvider pingServerUrl={pingUrl}>
                            <NetworkConsumer >
                                {({ isConnected }) => (
                                    <View>
                                        {isConnected ? 'NetworkConsumer: YES' : 'NetworkConsumer :NO'}
                                    </View>
                                )}
                            </NetworkConsumer>
                        </NetworkProvider>
                    )}
                </DummyNetworkContext.Consumer>
            </View>
            <View>
                <Button
                    title='CheckInternetConnection'
                    onPress={async () => {
                        const isConnected = await checkInternetConnection(
                            DEFAULT_PING_SERVER_URL,
                            DEFAULT_TIMEOUT,
                            true,
                            DEFAULT_HTTP_METHOD,
                            DEFAULT_CUSTOM_HEADERS)
                        if (isConnected === true) {
                            <View>
                                CheckInternetConnection: yes
                            </View>
                        }
                    }}
                />
            </View>
        </View>
    );
};
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-community/netinfo 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-community/netinfo文档的 Link 章节](/zh-cn/react-native-community-netinfo.md#link)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                  | Type        | Required | Platform              | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------- | -------- | --------------------- | ----------------- |
| children              | 一个React元素。这是唯一必需的属性。             | React.Node  | yes      | Android、iOS、Windows | yes               |
| pingTimeout           | 组件应等待ping响应的时间（以毫秒为单位）。默认为10000毫秒。如果要使用不同的值，建议使用更高的值。 | number      | no       | Android、iOS、Windows | yes               |
| pingServerUrl         | 要ping的远程服务器。默认为https://www.google.com/，因为这可能是最稳定的服务器之一，但您可以根据需要提供自己的服务器。警告：www.google.com在中国是被屏蔽的域名，因此如果需要您的应用程序在那里可访问，您必须使用其他域名。 | string      | no       | Android、iOS、Windows | yes               |
| shouldPing            | 标志位，表示是否执行额外的ping检查。默认为true。 | boolean     | no       | Android、iOS、Windows | yes               |
| pingInterval          | 您想要ping服务器的时间间隔（以毫秒为单位）。默认为0，这意味着不会定期检查连接性。如果选择定期检查，建议不要选择很小的值，因为这可能会消耗电池。明智地选择。大约30000毫秒应该比较合适。 | number      | no       | Android、iOS、Windows | yes               |
| pingOnlyIfOffline     | 当设置为true且pingInterval > 0时，只有在离线时才会定期ping远程服务器。默认为false。 | boolean     | no       | Android、iOS、Windows | yes               |
| pingInBackground      | 当应用程序不在前台时是否检查连接性。默认为false。 | boolean     | no       | Android、iOS、Windows | yes               |
| httpMethod            | 用于ping服务器的http方法。支持HEAD或OPTIONS。默认为HEAD。 | HTTPMethod  | no       | Android、iOS、Windows | yes               |
| customHeaders         | 为ping请求添加的可选自定义标头。             | HTTPHeaders | no       | Android、iOS、Windows | yes               |
| regexActionType       | 正则表达式，用于指示在离线模式下要拦截的操作类型。默认情况下，它被配置为拦截遵循Redux约定的数据获取操作。这意味着它将拦截类型如FETCH_USER_ID_REQUEST、FETCH_PRODUCTS_REQUEST等的操作。 | RegExp      | no       | Android、iOS、Windows | yes               |
| actionTypes           | 不满足正则表达式条件的其他操作类型的数组。例如，对于携带刷新数据的操作（如REFRESH_LIST）很有用。 | Arrays      | no       | Android、iOS、Windows | yes               |
| queueReleaseThrottle  | 刷新离线队列时分发操作之间的等待时间（以毫秒为单位）。当重新连接时，有助于减少服务器压力。默认为50毫秒。 | number      | no       | Android、iOS、Windows | yes               |
| shouldDequeueSelector | 接收redux应用程序状态并返回布尔值的函数。每次分发操作时都会执行此函数，在操作到达reducer之前。这对于控制当重新连接且有操作排队时是否应释放队列很有用。返回true（默认行为）释放队列，而返回false则阻止队列释放。例如，您可能希望在释放队列之前执行一些身份验证检查。注意，如果shouldDequeueSelector的结果在队列释放过程中发生变化，队列不会停止。如果您希望在队列释放过程中停止队列，请参见相关的FAQ部分。 | boolean     | no       | Android、iOS、Windows | yes               |
| url                   | 要ping的远程服务器。默认为https://www.google.com/，因为这可能是最稳定的服务器之一，但您可以根据需要提供自己的服务器。警告：www.google.com在中国是被屏蔽的域名，因此如果需要您的应用程序在那里可访问，您必须使用其他域名。 | string      | no       | Android、iOS、Windows | yes               |
| method                | 用于ping服务器的http方法。支持HEAD或OPTIONS。默认为HEAD。 | HTTPMethod  | no       | Android、iOS、Windows | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                    | Description                                                  | Type | Required | Platform              | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ---- | -------- | --------------------- | ----------------- |
| NetworkProvider         | 提供程序组件，通过React Context将网络状态注入到子组件中。只需要children属性，其余都是可选的。应该在组件层次结构的顶部使用，理想情况下在（或接近）入口点。 | func | no       | Android、iOS、Windows | yes               |
| NetworkConsumer         | 订阅连接性变化的React组件。它需要一个函数作为子组件。该函数接收当前的连接状态并返回一个React节点。为了正常工作，此组件应在NetworkProvider内渲染。 | func | no       | Android、iOS、Windows | yes               |
| useIsConnected          | 返回一个布尔值，指示您是否连接到网络。 | func | no       | Android、iOS、Windows | yes               |
| ReduxNetworkProvider    | 使用提供程序组件机制。与`NetworkProvider`相同的属性适用。确保您的组件是react-redux `<Provider>`组件的后代，以便`ReduxNetworkProvider`可以访问store。 | func | no       | Android、iOS、Windows | yes               |
| networkSaga             | 只需从您的根saga中派生此saga。它接受与NetworkProvider和ReduxNetworkProvider相同的配置选项。如果您使用redux-saga，这是推荐的方式，因为它是一种非常优雅的处理全局连接性变化的方法，而无需用额外功能包装您的组件。 | func | no       | Android、iOS、Windows | yes               |
| createNetworkMiddleware | 返回一个Redux中间件的函数，该中间件监听针对在线/离线模式API调用的特定操作。 | func | no       | Android、iOS、Windows | yes               |
| OfflineQueue            | 一个队列系统，用于存储由于缺乏连接性而失败的操作。它适用于普通对象操作和thunks。 | func | no       | Android、iOS、Windows | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/rgommezz/react-native-offline/blob/master/LICENSE) ，请自由地享受和参与开源

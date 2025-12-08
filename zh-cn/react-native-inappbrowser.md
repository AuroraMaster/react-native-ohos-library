> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-inappbrowser-reborn</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/proyecto26/react-native-inappbrowser">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/proyecto26/react-native-inappbrowser/blob/develop/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-inappbrowser)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
|-------| ------------------------------------------------------------ | ---------- |
| <= 3.7.0-0.0.4@deprecated | [@react-native-oh-tpl/react-native-inappbrowser-reborn Releases(deprecated)](https://github.com/react-native-oh-library/react-native-inappbrowser/releases) | 0.72       |
| 3.7.1 | [@react-native-ohos/react-native-inappbrowser-reborn Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-inappbrowser/releases)                        | 0.72       |
| 3.8.0 | [@react-native-ohos/react-native-inappbrowser-reborn Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-inappbrowser/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```
npm install @react-native-ohos/react-native-inappbrowser-reborn
```

#### **yarn**

```
yarn add @react-native-ohos/react-native-inappbrowser-reborn
```

下面的代码展示了这个库的基本使用场景：

> [!TIP] 使用时 import 的库名不变。

```
import React, {useState } from 'react';
import {  StyleSheet, Text, Button ,ScrollView,View,StatusBarStyle,} from 'react-native';
import {InAppBrowser} from 'react-native-inappbrowser-reborn'
import {tryDeepLinking,openLink} from './utils'

export default function BrowserDemo() {
  const [text, setText] = useState('');
  const [url, setUrl] = useState('https://reactnative.dev');

  const onOpenLink = async() => {
    let resut = await openLink(url,{});
    setText(JSON.stringify(resut))
  }

  const onTryDeepLinking = async() => {
    let result = await tryDeepLinking();
    setText(JSON.stringify(result))
    return result;
  }

  const onIsAvailable = async () => {
    let isAvailable = await InAppBrowser.isAvailable();
    return isAvailable
  }

  const close =() => {
    openLink(url, {});
    setTimeout(function(){
      console.info('-----------------')
      InAppBrowser.close();
    },10000)
  }

  const closeAuth =() => {
    tryDeepLinking();
    setTimeout(function(){
      console.info('-----------------')
      InAppBrowser.closeAuth();
    },10000)
  }

  const warmup = () => {
    InAppBrowser.warmup();
  }

  const mayLaunchUrl = () => {
    InAppBrowser.mayLaunchUrl(url,[]);
  }
  
  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style = {styles.title}>BrowserDemo</Text>
      </View>
      <View style = {styles.inputArea}>
        <Text style={styles.baseText}>
          {text}
        </Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={ { flexDirection: 'column'}}>
          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>onOpenLink</Text>
             <Button title='运行' color='#841584' onPress={onOpenLink}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>onTryDeepLinking</Text>
             <Button title='运行' color='#841584' onPress={onTryDeepLinking}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>onIsAvailable</Text>
             <Button title='运行' color='#841584' onPress={onIsAvailable}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>close</Text>
             <Button title='运行' color='#841584' onPress={close}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>tryDeepLinking</Text>
             <Button title='运行' color='#841584' onPress={tryDeepLinking}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>closeAuth</Text>
             <Button title='运行' color='#841584' onPress={closeAuth}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>warmup</Text>
             <Button title='运行' color='#841584' onPress={warmup}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>mayLaunchUrl</Text>
             <Button title='运行' color='#841584' onPress={mayLaunchUrl}></Button>
          </View>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    flexDirection: 'column',
    alignItems: 'center',
    backgroundColor: '#F1F3F5',
  }, 
  baseText: {
    fontWeight: 'bold',
    textAlign:'center',
    fontSize:16
  },

  titleArea:{
    width:'90%',
    height:'8%',
    alignItems:'center',
    flexDirection:'row',
  },

  title: {
    width:'90%',
    color:'#000000',
    textAlign:'left',
    fontSize: 30,
  },

  scrollView: {
    width:'90%',
    marginHorizontal: 20,
  },

  inputArea: {
    width:'90%',
    height:'10%',
    borderWidth:2,
    borderColor:'#000000',
    marginTop:8,
    justifyContent:'center',
    alignItems:'center',
  },
  baseArea: {
    width:'100%',
    height:60,
    borderRadius:4,
    borderColor:'#000000',
    marginTop:8,
    backgroundColor:'#FFFFFF',
    flexDirection: 'row',
    alignItems:'center',
    paddingLeft:8,
    paddingRight:8
  }

});

import {Alert,Platform,} from 'react-native';
import {InAppBrowser} from 'react-native-inappbrowser-reborn'

export interface options {
  dismissButtonStyle?: 'done' | 'close' | 'cancel',
  preferredBarTintColor?:string,
  preferredControlTintColor?:string
}

export const openLink = async (
url: string,
statusBarStyle: options,
animated = true,
) => {
    let result  = await InAppBrowser.open(
        url,
        {
          dismissButtonStyle:statusBarStyle.dismissButtonStyle,
          preferredBarTintColor:statusBarStyle.preferredBarTintColor,
          preferredControlTintColor:statusBarStyle.preferredControlTintColor
        }
    );
    Alert.alert('Response', JSON.stringify(result));
    return result;
}

export const getDeepLink = (path = '') => {
    const scheme = 'my-demo';
    const prefix =
      Platform.OS === 'android' ? `${scheme}://demo/` : `${scheme}://`;
    return prefix + path;
};

export const tryDeepLinking = async () => {
    const loginUrl = 'https://proyecto26.github.io/react-native-inappbrowser/';
    const redirectUrl = getDeepLink();
    const url = `${loginUrl}?redirect_url=${encodeURIComponent(redirectUrl)}`;
    try {
      if (await InAppBrowser.isAvailable()) {
        const result = await InAppBrowser.openAuth(url, redirectUrl, {
          // iOS Properties
          ephemeralWebSession: false,
        });
        //await sleep(800);
        return result
      } else {
        return 'InAppBrowser is not supported :/'
      }
    } catch (error) {
      console.error(error);
    }
    return 'Something’s wrong with the app'
};
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-inappbrowser@3.7.1，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-localize@3.7.1，已支持 Autolink，无需手动配置（仍需手动配置的内容已在对应标题处标记），目前只支持72框架。 Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 harmony

```
在工程根目录的 oh-package.json 添加 overrides字段
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 1.配置Entry(该模块始终需要手动配置)

**1.在 entry/src/main/ets/entryability 下创建 BrowserManagerAbility.ets**

```
import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
import { window } from '@kit.ArkUI';

export default class BrowserManagerAbility extends UIAbility {

  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
  }

  onDestroy(): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onDestroy');
  }

  onWindowStageCreate(windowStage: window.WindowStage): void {
    // Main window is created, set main page for this ability
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');

    windowStage.loadContent('pages/BrowserManagerPage', (err) => {
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content.');
    });
  }

  onWindowStageDestroy(): void {
    // Main window is destroyed, release UI related resources
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageDestroy');
  }

  onForeground(): void {
    // Ability has brought to foreground
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onForeground');
  }

  onBackground(): void {
    // Ability has back to background
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onBackground');
  }
}

```

**2.在 entry/src/main/module.json5注册BrowserManagerAbility**

```
"abilities":[{
    "name": "BrowserManagerAbility",
    "srcEntry": "./ets/entryability/BrowserManagerAbility.ets",
    "description": "$string:EntryAbility_desc",
    "icon": "$media:icon",
    "startWindowIcon": "$media:startIcon",
    "startWindowBackground": "$color:start_window_background",
    "visible": true,
  }
...
]
```

**3.在 entry/src/main/ets/pages 下创建 BrowserManagerPage.ets**

```
import { BrowserPage } from '@react-native-ohos/react-native-inappbrowser-reborn/Index'

@Entry
@Component
struct ChromeTabsManagerPage {
  build() {
    Row(){
      Column(){
        BrowserPage();
      }
      .width('100%')
    }
    .height('100%')
  }

}
```

**4.在 entry/src/main/resources/base/profile/main_pages.json 添加配置**

```
{
 "src": [
  "pages/Index",
  "pages/BrowserManagerPage"
 ]
}
```

**5.如果需要预热应用内浏览器客户端，使其启动速度显著加快，可以将以下内容添加到BrowserManagerAbility**

```
import { RNInAppBrowserModule } from '@react-native-ohos/react-native-inappbrowser-reborn/ts';

export default class BrowserManagerAbility extends UIAbility {

  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
    RNInAppBrowserModule.start();
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入。
2. 直接链接源码。

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-inappbrowser-reborn": "file:../../node_modules/@react-native-ohos/react-native-inappbrowser-reborn/harmony/inappbrowser.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)

### 3.配置CMakeLists 和引入 InappbrowserRebornPackage

> 若使用的是 <= 3.7.0-0.0.4 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```cmake
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-inappbrowser-reborn/src/main/cpp" ./inappbrowser-reborn)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_inappbrowser_reborn)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "InappbrowserRebornPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<InappbrowserRebornPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNInAppBrowserPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNInAppBrowserPackage } from '@react-native-ohos/react-native-inappbrowser-reborn/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNInAppBrowserPackage(ctx),
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
## API

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| open  | 在 iOS 上使用 SFSafariViewController 以模态方式打开 Safari，在 Android 上使用新的自定义标签页打开 Chrome。在 iOS 上，模态 Safari 不会与系统 Safari 共享 Cookie。                      | function | no       | iOS/Android | yes               |
| close       | 关闭系统呈现的网页浏览器。 | function | no       | iOS/Android | yes               |
| openAuth |在 iOS 上使用 SFAuthenticationSession/ASWebAuthenticationSession 以模态方式打开 Safari，在 Android 上使用新的自定义标签页打开 Chrome。在 iOS 上，用户将被询问是否允许应用使用给定的 URL 进行身份验证（使用深度链接重定向的 OAuth 流程）。                                       | function | no       | iOS/Android | yes               |
| closeAuth | 关闭当前的身份验证会话。                                  | function | no       | iOS/Android | yes               |
| isAvailable  | 检测设备是否支持此插件。                                           | function | no       | iOS/Android | yes               |
| onStart  | 初始化绑定的后台服务，以便应用程序可以向浏览器传达其意图。服务连接后，客户端可用于预热浏览器以加快导航速度，并指示给定的 URL 可能会在将来加载。- 仅限 Android。                                           | function | no       | Android | yes               |
| warmup  | 预热浏览器进程 - 仅限 Android。                                           | function | no       | Android | yes               |
| mayLaunchUrl  | 告诉浏览器可能的未来导航到某个 URL。必须首先指定最可能的 URL。可选择提供其他可能 URL 的列表。它们被视为比第一个 URL 可能性小，并且必须按优先级递减的顺序排序。这些额外的 URL 可能会被忽略。之前对此方法的所有调用都将被降级 - 仅限 Android。                                        | function | no       | Android | yes               |

## 属性
**iOS Options**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| dismissButtonStyle  | 关闭按钮的样式。[done/close/cancel]     | String  | NO | iOS      | yes |
| preferredBarTintColor  | 用于导航栏和工具栏背景的着色颜色。[white/#FFFFFF]         | String  | NO | iOS      | yes |
| preferredControlTintColor  | 用于导航栏和工具栏上控制按钮的着色颜色。[gray/#808080]         | String  | NO | iOS      | yes |
| readerMode   | 指定 Safari 是否应进入阅读模式（如果可用）的值。[true/false]         | Boolean  | NO | iOS      | NO |
| animated    | 是否对呈现进行动画处理。[true/false]        | Boolean  | NO | iOS      | NO |
| modalPresentationStyle     | 模态呈现视图控制器的呈现样式。[automatic/none/fullScreen/pageSheet/formSheet/currentContext/custom/overFullScreen/overCurrentContext/popover]        | String  | NO | iOS      | NO |
| modalTransitionStyle      | 呈现视图控制器时使用的过渡样式。[coverVertical/flipHorizontal/crossDissolve/partialCurl]        | String  | NO | IOS      | NO |
| modalEnabled       | 以模态方式呈现 SafariViewController 或改为推送方式。[true/false]       | Boolean  | NO | iOS      | NO |
| enableBarCollapsing        | 确定浏览器的工具栏是否折叠。[true/false]       | Boolean  | NO | iOS      | NO |
| ephemeralWebSession         | 防止重用前一个会话的 cookie（仅限 openAuth）。[true/false]       | Boolean  | NO | iOS      | NO |
| formSheetPreferredContentSize          | iPad formSheet 模态框的自定义尺寸。[{width: 400, height: 500}]       | Boolean  | NO | iOS      | NO |

**Android  Options**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| showTitle   | 设置是否在自定义标签页中显示标题。[true/false]         | Boolean  | NO | Android      | NO |
| toolbarColor    | 设置工具栏颜色。[gray/#808080]         | String  | NO | Android      | NO |
| secondaryToolbarColor     | 设置辅助工具栏的颜色。[white/#FFFFFF]         | String  | NO | Android      | NO |
| navigationBarColor      | 设置导航栏颜色。[gray/#808080]         | String  | NO | Android      | NO |
| navigationBarDividerColor       | 设置导航栏分隔线颜色。[white/#FFFFFF]         | String  | NO | Android      | NO |
| enableUrlBarHiding        | 启用当用户向下滚动页面时隐藏 URL 栏。[true/false]         | String  | NO | Android      | NO |
| enableDefaultShare         | 在菜单中添加默认分享项。[true/false]         | String  | NO | Android      | NO |
| animations          | 设置启动和退出动画。[{ startEnter, startExit, endEnter, endExit }]         | Object  | NO | Android      | NO |
| headers           | 数据为键值对，将作为 HTTP 请求头发送到提供的 URL。[{ 'Authorization': 'Bearer ...' }]         | Object  | NO | Android      | NO |
| forceCloseOnRedirection            | 在新任务中打开自定义标签页，以避免重定向回应用 scheme 时出现问题。[true/false]         | Boolean  | NO | Android      | NO |
| hasBackButton             | 设置返回箭头而不是默认的 X 图标来关闭自定义标签页。[true/false]         | Boolean  | NO | Android      | NO |
| browserPackage              | 用于处理自定义标签页的浏览器包名。        | Boolean  | NO | Android      | NO |
| showInRecents               | 确定浏览的网站是否应显示为 Android 最近任务/多任务视图中的单独条目。[true/false]         | Boolean  | NO | Android      | NO |
| includeReferrer           | 确定是否将您的包名作为引荐来源包含在内以供网站跟踪。[true/false]       | Boolean  | NO | Android      | NO |


## 遗留问题

- [ ] 打开浏览器时，不能指定浏览器设置阅读模式 [#1](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/1)
- [ ] 打开浏览器，无法使文稿动起来 [#2](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/2)
- [ ] 无法设置浏览器的视图控制器的风格 [#3](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/3)
- [ ] 无法设置浏览器的过度风格 [#4](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/4)
- [ ] 无法设置浏览器的推送方式 [#5](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/5)
- [ ] 浏览器无法设置工具栏进行折叠  [#6](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/6)
- [ ] 浏览器设置是否重复使用前一次会话的cookie  [#7](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/7)
- [ ] 浏览器设置模态框的自定义尺寸  [#8](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/8)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/proyecto26/react-native-inappbrowser/blob/develop/LICENSE) ，请自由地享受和参与开源。

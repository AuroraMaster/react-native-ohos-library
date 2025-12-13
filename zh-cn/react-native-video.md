> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-video</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-video/react-native-video/tree/support/5.2.X">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-video/react-native-video/blob/support/5.2.X/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-video)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 6.13.1@deprecated  | [@react-native-oh-tpl/react-native-video Releases(deprecated)](https://github.com/react-native-oh-library/react-native-video/releases) | 0.72       |
| 6.13.2                | [@react-native-ohos/react-native-video Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-video/releases)   | 0.72       |
| 6.14.0                | [@react-native-ohos/react-native-video Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-video/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-video
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-video
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useRef } from "react";
import { Button, View, ScrollView, StyleSheet, Switch, Text, TextInput } from "react-native";
import RNCVideo from "react-native-video";

import {
  type OnPlaybackStateChangedData,
  OnSeekData,
} from 'react-native-video';

function RNCVideoDemo() {
  const [muted, setMuted] = useState(true);
  const [paused, setPaused] = useState(false);
  const [repeat, setRepeat] = useState(true);
  const [controls, setControls] = useState(false);
  const [disableFocus, setDisableFocus] = useState(false);
  const [uri, setUri] = useState(
    "https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4"
  );
  const [txt, setTxt] = useState("empty");
  const [resizeMode, setResizeMode] = useState("none");
  const [posterResizeMode, setPosterResizeMode] = useState("cover");
  const [seekSec, setSeekSec] = useState(5000);

  const [onVideoLoad, setOnVideoLoad] = useState("onVideoLoad");
  const [onVideoLoadStart, setOnVideoLoadStart] = useState("onVideoLoadStart");
  const [onVideoError, setOnVideoError] = useState("onVideoError");
  const [onVideoProgress, setOnVideoProgress] = useState("onVideoProgress");
  const [onVideoEnd, setOnVideoEnd] = useState("onVideoEnd");
  const [onVideoBuffer, setOnVideoBuffer] = useState("onVideoBuffer");

  const [onPlaybackStateChanged, setPlaybackStateChanged] = useState("onPlaybackStateChanged");
   
  const [onPlaybackResume, setOnPlaybackResume] = useState("onPlaybackResume");
  const [pictureInPicture, setPictureInPicture] = useState(false);
  const [enterPictureInPictureOnLeave, setEnterPictureInPictureOnLeave] = useState(false);

  const videoRef = React.useRef<typeof RNCVideo>();

  const toggleMuted = () => {
    setMuted((prevMuted) => !prevMuted);
  };

  const toggleControls = () => {
    setControls((prevControls) => !prevControls);
  };

  const togglePaused = () => {
    setPaused((prevPaused) => !prevPaused);
  };

  const toggleRepeat = () => {
    setRepeat((prevRepeat) => !prevRepeat);
  };

  const toggleDisableFocus = () => {
    setDisableFocus((prevDisableFocus) => !prevDisableFocus);
  };

  const firstVideo = () => {
    setUri((prevRepeat) => "https://vjs.zencdn.net/v/oceans.mp4");
  };

  const secondVideo = () => {
    // setUri((prevRepeat) => 'http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4');
    setUri(
      (prevRepeat) =>
        "https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4"
    );
  };

  const changeResizeMode = (resizeMode) => {
    setResizeMode((prevResizeMode) => resizeMode);
  };

  return (
    <ScrollView style={styles.container}>
      <View style={styles.container}>
        <Text style={styles.title}>网络视频demo</Text>
        <Text style={styles.labelB}>{onVideoLoad}</Text>
        <Text style={styles.label}>{onVideoError}</Text>
        <Text style={styles.label}>{onVideoLoadStart}</Text>
        <Text style={styles.labelB}>{onVideoProgress}</Text>
        <Text style={styles.label}>{onVideoEnd}</Text>
        <Text style={styles.label}>{onVideoBuffer}</Text>

        <Text style={styles.label}>{onPlaybackStateChanged}</Text>

        <Text style={styles.label}>{onPlaybackResume}</Text>
        <Text style={styles.title}>update source </Text>
        <View
          style={{
            flexDirection: "row",
            width: '100%',
            height: 40,
            justifyContent: 'space-between',
            alignItems: 'center',
          }}
        >
          <Text>应用返回桌面时是否自动启动画中画：</Text>
          <Switch
            trackColor={{ false: "#767577", true: "#81b0ff" }}
            thumbColor={enterPictureInPictureOnLeave ? "#f5dd4b" : "#f4f3f4"}
            ios_backgroundColor="#3e3e3e"
            onValueChange={setEnterPictureInPictureOnLeave}
            value={enterPictureInPictureOnLeave}
          />
        </View>
        <Button
          title="开启画中画"
          onPress={()=>{
            !pictureInPicture && setPictureInPicture(true);
          }}
        />
        <Button
          title="关闭画中画"
          onPress={()=>{
            pictureInPicture && setPictureInPicture(false);
          }}
        />
        <View
          style={{
            flexDirection: "row",
            height: 40,
            padding: 0,
          }}
        >
          <Text
            style={{ backgroundColor: "blue", flex: 0.25 }}
            onPress={() => {
              setUri(
                "https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4"
              );
              setPosterResizeMode("stretch");
            }}
          >
            切换net:vmallres
          </Text>
          <Text
            style={{ backgroundColor: "red", flex: 0.25 }}
            onPress={() => {
              setUri("https://vjs.zencdn.net/v/oceans.mp4");
              setPosterResizeMode("contain");
            }}
          >
            切换net:oceans
          </Text>
        </View>
        <Text style={styles.title}>set resizeMode </Text>
        <View
          style={{
            flexDirection: "row",
            height: 40,
            padding: 0,
          }}
        >
          <Text
            style={{ backgroundColor: "blue", flex: 0.25 }}
            onPress={() => {
              setResizeMode("none");
            }}
          >
            none
          </Text>
          <Text
            style={{ backgroundColor: "red", flex: 0.25 }}
            onPress={() => {
              setResizeMode("contain");
            }}
          >
            contain
          </Text>
          <Text
            style={{ backgroundColor: "yellow", flex: 0.25 }}
            onPress={() => {
              setResizeMode("stretch");
            }}
          >
            stretch
          </Text>
          <Text
            style={{ backgroundColor: "green", flex: 0.25 }}
            onPress={() => {
              setResizeMode("cover");
            }}
          >
            cover
          </Text>
        </View>
        <View
          style={{
            flexDirection: "row",
            flexWrap: "wrap",
            padding: 0,
          }}
        >
          <Text style={styles.title}>操作 </Text>
          <TextInput
            style={styles.prop_input}
            placeholder="input seek sec number:"
            multiline={false}
            maxLength={30}
            keyboardType="numeric"
            onChangeText={(text) => {
              const newText = text.replace(/[^\d]+/, "");
              setSeekSec(Number(newText));
            }}
            autoFocus={false}
          />
        </View>
        <View
          style={{
            flexDirection: "row",
            flexWrap: "wrap",
            padding: 0,
          }}
        >
          <Text
            style={styles.button_b}
            onPress={() => {
              videoRef.current?.seek(seekSec);
            }}
          >
            seek:{seekSec.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              togglePaused();
            }}
          >
            paused:{paused.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              toggleMuted();
            }}
          >
            muted:{muted.toString()}
          </Text>
         <Text style={styles.button_b} onPress={() => { toggleControls() }} >controls:{controls.toString()}</Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              toggleRepeat();
            }}
          >
            repeat:{repeat.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              toggleDisableFocus();
            }}
          >
            disableFocus:{disableFocus.toString()}
          </Text>
          <Text style={styles.button_b}>
            ReSizeMode:{resizeMode.toString()}
          </Text>
        </View>
        <RNCVideo
          style={styles.video}
          ref={videoRef}
          source={{ uri: uri, isNetwork: true }}
          paused={paused}
          muted={muted}
          pictureInPicture={pictureInPicture}
          enterPictureInPictureOnLeave={enterPictureInPictureOnLeave}
          onPictureInPictureStatusChanged={(e)=>{
            console.log('onPictureInPictureStatusChanged:',e);
            pictureInPicture !== e.isActive && setPictureInPicture(e.isActive || false)
          }}
          resizeMode={resizeMode}
          controls={controls}
          repeat={repeat}
          volume={1}
          disableFocus={disableFocus}
          poster={
            "https://res.vmallres.com/pimages/uomcdn/CN/pms/202304/sbom/4002010007801/group/800_800_9B1356F1330EADDCB20D35D2AE1F46E0.jpg"
          }
         posterResizeMode={posterResizeMode}
          onLoad={(e) => {
            setOnVideoLoad(
              "onVideoLoad currentTime =" +
                e.currentPosition +
                "s duration =" +
                e.duration +
                "s width =" +
                e.naturalSize.width +
                " orientation =" +
                e.naturalSize.orientation
            );
            setOnVideoError("onVideoError error = ok");
          }}
          onLoadStart={(e) => {
            setOnVideoLoadStart(
              "onVideoLoadStart isNetwork =" +
                e.isNetwork +
                " type=" +
                e.type +
                " uri=" +
                e.uri
            );
          }}
          onProgress={(e) => {
            setOnVideoProgress(
              "onVideoProgress currentTime =" +
                e.currentTime +
                " playableDuration=" +
                e.playableDuration +
                " seekableDuration=" +
                e.seekableDuration
            );
          }}
          
          onSeek = {(data: OnSeekData) => {
            console.log('onSeek');
          }}

          onError={(e) => {
            setOnVideoError("onVideoError error =" + e.error);
          }}
          onEnd={() => {
            setOnVideoEnd("onVideoEnd completed");
          }}
          onBuffer={(e) => {
            setOnVideoBuffer("onVideoBuffer :" + e.isBuffering);
          }}

          onPlaybackStateChanged={(data: OnPlaybackStateChangedData) => {
            console.log('onPlaybackStateChanged ' + JSON.stringify(data));
            setPlaybackStateChanged("onPlaybackStateChanged : " + JSON.stringify(data));
          }}

          onReadyForDisplay={() => {
            console.log(`onReadyForDisplay :setShowPoster(false)`);
          }}
        />
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  video: {
    width: "100%",
    height: 260,
  },
  container: {
    width: "100%",
    height: "100%",
    backgroundColor: "#f8f8f8",
  },
  title: {
    color: "white",
    width: "30%", // hack
    height: 30, // hack
  },
  label: {
    color: "gray",
    width: "100%", // hack
    minHeight: 20,
  },
  labelB: {
    color: "gray",
    width: "100%", // hack
    minHeight: 40,
  },
  button: {
    width: 160,
    height: 36,
    backgroundColor: "hsl(190, 50%, 70%)",
    paddingHorizontal: 16,
    paddingVertical: 8,
    borderRadius: 8,
  },
  buttonText: {
    width: "100%",
    height: "100%",
    fontWeight: "bold",
  },
  button_b: {
    paddingHorizontal: 8,
    paddingVertical: 6,
    borderRadius: 4,
    backgroundColor: "oldlace",
    alignSelf: "flex-start",
    marginHorizontal: "1%",
    marginBottom: 6,
    minWidth: "25%",
    minHeight: 20,
    textAlign: "center",
  },
  prop_input: {
    width: 160,
    height: 40,
    borderWidth: 1,
    backgroundColor: "white",
    color: "black",
    borderRadius: 8,
  },
});

export default RNCVideoDemo;
```

## Link

|                                     | 是否支持autolink | RN框架版本 |
|-------------------------------------|-----------------|------------|
| ~6.14.0                             |  No              |  0.77     |
| ~6.13.2                             |  Yes             |  0.72     |
| <= 6.13.1@deprecated                |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md。

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
   ...
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-video": "file:../../node_modules/@react-native-ohos/react-native-video/harmony/rn_video.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 RNCVideoPackage

> 若使用的是 <= 6.13.1 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-video/src/main/cpp" ./video)

# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_video)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNCVideoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNCVideoPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNCVideo 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNCVideo, RNC_VIDEO_TYPE } from "@react-native-ohos/react-native-video"


@Builder
function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNC_VIDEO_TYPE) {
+   RNCVideo({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
 ...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  ...
+ RNC_VIDEO_TYPE
  ];
```

### 5.在 ArkTs 侧引入 RNCVideoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNCVideoPackage } from '@react-native-ohos/react-native-video/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCVideoPackage(ctx)
  ];
}
```
</details>

## 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
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

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**VideoNativeProps**属性

| Name                                            | Description                                                   | Type                                                      | Required | Platform                                                 | HarmonyOS Support |
| ----------------------------------------------- | ------------------------------------------------------------ | :-------------------------------------------------------- | -------- | -------------------------------------------------------- | ----------------- |
| `source`                                        | 设置媒体源，可传入通过 require 加载的资源或带 uri 的对象。 | object                                                    | Yes      | All                                                      | yes               |
| `disableFocus`                                  | 决定视频音频在 Android 与 HarmonyOS 设备上是否覆盖后台音乐/音频。<br/>**false（默认）** | boolean                                                   | No       | Android Exoplayer                                        | yes               |
| `muted`                                         | 控制是否静音。<br/>**false（默认）** 表示不静音。 | boolean                                                   | No       | All                                                      | yes               |
| `paused`                                        | 控制媒体是否暂停。<br/>**false（默认）** 表示不中断播放。 | boolean                                                   | No       | All                                                      | yes               |
| `repeat`                                        | 决定播放到末尾时是否循环。<br/>**false（默认）** 表示不循环。 | boolean                                                   | No       | All                                                      | yes               |
| `resizeMode`                                    | 决定容器尺寸与原始视频尺寸不匹配时如何缩放。<br/>**"none"（默认）** 表示不缩放。 | string                                                    | No       | Android ExoPlayer, Android MediaPlayer, iOS, Windows UWP | yes               |
| `volume`                                        | 调节音量。<br/>**1.0（默认）** 表示全音量播放。 | number                                                    | No       | All                                                      | yes               |
| `poster`                                        | 视频加载时展示的图片，值为图片 URL，例如 "<https://baconmockup.com/300/200/>"。 | <br>V5.2.1：string<br>V6.13.0：string \| ReactVideoPoster | No       | All                                                      | yes               |
| `posterResizeMode`                              | 决定海报图在尺寸不匹配时如何缩放。<br/>**"contain"（默认）** 表示等比缩放以保证宽高不超过视图尺寸。 | string                                                    | No       | All                                                      | yes               |
| `allowsExternalPlayback`                        | 指示播放器是否允许切换到 AirPlay 或 HDMI 等外部播放模式。 | boolean                                                   | No       | iOS                                                      | No                |
| `audioOnly`                                     | 指示播放器是否只播放音轨并用海报替代视频画面。 | boolean                                                   | No       | All                                                      | No                |
| `automaticallyWaitsToMinimizeStalling`          | 布尔值，指示播放器是否自动延迟播放以尽量减少卡顿（适用于链接 iOS 10.0 及以上的客户端）。 | boolean                                                   | No       | iOS                                                      | No                |
| `bufferConfig`                                  | 调整缓冲配置，此属性接受包含下列任意字段的对象。 | object                                                    | No       | Android                                                  | No                |
| `controls`                                      | 决定是否显示播放控件。                                      | boolean                                                   | No       | All                                                      | Yes               |
| `currentPlaybackTime`                           | 播放带 EXT-X-PROGRAM-DATE-TIME 标签的 HLS 直播流时，该属性包含毫秒级纪元时间。 | string                                                    | No       | All                                                      | No                |
| `filter`                                        | 添加视频滤镜。                                               | string                                                    | No       | iOS                                                      | No                |
| `filterEnabled`                                 | 启用视频滤镜。                                               | string                                                    | No       | iOS                                                      | No                |
| `fullscreen`                                    | 控制播放时是否进入全屏。                                     | boolean                                                   | No       | iOS                                                      | No                |
| `fullscreenAutorotate`                          | 当设置了首选全屏方向时，使视频旋转到该方向，同时允许屏幕按用户持握方向旋转，默认为 TRUE。 | boolean                                                   | No       | iOS                                                      | No                |
| `fullscreenOrientation`                         | 设置全屏显示时的方向。                                       | string                                                    | No       | iOS                                                      | No                |
| `headers`                                       | 向 HTTP 客户端传递请求头（可用于鉴权），需作为 source 对象的一部分。 | object                                                    | No       | Android                                                  | No                |
| `hideShutterView`                               | 控制是否启用 ExoPlayer 的快门视图（加载时的黑屏）。         | boolean                                                   | No       | Android                                                  | No                |
| `id`                                            | 设置 DOM 元素 id，便于在 Web 平台通过 document.getElementById 获取。 | string                                                    | No       | All                                                      | No                |
| `ignoreSilentSwitch`                            | 控制 iOS 静音开关的行为。                                    | string                                                    | No       | iOS                                                      | No                |
| `maxBitRate`                                    | 在存在多个视频流的播放列表中设置网络带宽消耗的比特率上限。 | number                                                    | No       | All                                                      | No                |
| `minLoadRetryCount`                             | 设置在失败并上报错误前加载数据的最少重试次数，有助于恢复临时网络异常。 | number                                                    | No       | Android                                                  | No                |
| `mixWithOthers`                                 | 控制与其他应用的音频混音方式。                               | string                                                    | No       | iOS                                                      | No                |
| `pictureInPicture`                              | 决定媒体是否以画中画模式播放。                               | boolean                                                   | No       | iOS                                                      | No                |
| `playInBackground`                              | 决定应用处于后台时媒体是否继续播放，便于持续收听音频。       | boolean                                                   | No       | All                                                      | No                |
| `playWhenInactive`                              | 决定通知或控制中心浮于视频前时媒体是否继续播放。             | boolean                                                   | No       | iOS                                                      | No                |
| `preferredForwardBufferDuration`                | 设置播放器在播放头前从网络预缓冲的时长，对应 AVPlayerItem 的 preferredForwardBufferDuration。 | number                                                    | No       | iOS                                                      | No                |
| `preventsDisplaySleepDuringVideoPlayback`       | 控制播放视频时是否允许屏幕休眠，默认不允许。                 | boolean                                                   | No       | All                                                      | No                |
| `progressUpdateInterval`                        | 设置 onProgress 事件之间的间隔，单位为毫秒。                 | number                                                    | No       | iOS                                                      | No                |
| `rate`                                          | 控制媒体的播放速度。                                         | number                                                    | No       | All                                                      | Yes               |
| `reportBandwidth`                               | 决定是否生成 onBandwidthUpdate 事件（ExoPlayer 事件频率高需显式开启）。 | boolean                                                   | No       | Android                                                  | No                |
| `selectedAudioTrack`                            | 配置要播放的音频轨（若存在）。                                | object                                                    | No       | All                                                      | Yes               |
| `selectedTextTrack`                             | 配置要显示的文本轨（字幕或说明），若存在。                   | object                                                    | No       | All                                                      | No                |
| `selectedVideoTrack`                            | 配置要播放的视频轨，默认采用自适应码率根据带宽自动选择。     | object                                                    | No       | Android                                                  | No                |
| `stereoPan`                                     | 调节左右声道的平衡，取值范围为 -1.0 到 1.0。                 | number                                                    | No       | Android                                                  | No                |
| `textTracks`                                    | 加载一个或多个“外挂”文本轨，该属性接受描述各轨的对象数组。   | object                                                    | No       | All                                                      | No                |
| `trackId`                                       | 配置视频流的标识符，以便将播放上下文与事件关联。             | string                                                    | No       | Android                                                  | No                |
| `useTextureView`                                | 控制输出使用 TextureView 还是 SurfaceView。                 | boolean                                                   | No       | Android                                                  | No                |
| audioOutput<sup>6.13.0+</sup>                   | 切换音频输出设备。                                           | type AudioOutput = 'speaker' \| 'earpiece';               | No       | Andorid, iOS                                             | No                |
| bufferingStrategy<sup>6.13.0+</sup>             | 配置缓冲与数据加载策略。                                     | enum {DEFAULT, DISABLE_BUFFERING, DEPENDING_ON_MEMORY}    | No       | Android                                                  | No                |
| chapters<sup>6.13.0+</sup>                      | 为 tvOS 提供自定义章节源。                                   | Chapters[]                                                | No       | tvOS                                                     | No                |
| controlsStyles<sup>6.13.0+</sup>                | 调整控制栏样式，仅在 controls={true} 且传入对象时生效（hidePlayPause、hideSeekBar、hideDuration、hidePosition）。 | ControlsStyles                                            | No       | Android                                                  | partially         |
| disableDisconnectError<sup>6.13.0+</sup>        | 决定断网时播放器是否抛出错误。                               | boolean                                                   | No       | Android                                                  | Yes               |
| disableAudioSessionManagement<sup>6.13.0+</sup> | 禁用库内部的音频会话管理（作用于所有视图）。                 | boolean                                                   | No       | iOS                                                      | No                |
| enterPictureInPictureOnLeave<sup>6.13.0+</sup>  | 当用户离开应用时是否自动进入画中画模式。                     | boolean                                                   | No       | Android, iOS                                             | Yes               |
| focusable<sup>6.13.0+</sup>                     | 决定视频视图是否可被非触控输入设备（如硬件键盘）聚焦。       | boolean                                                   | No       | Android                                                  | No                |
| renderLoader<sup>6.13.0+</sup>                  | 允许自定义组件来展示视频加载状态。                           | ReactNode                                                 | No       | All                                                      | Yes               |
| resizeMode                                      | 当容器尺寸与原始视频尺寸不一致时决定如何缩放。               | V5.2.1: ResizeMode<br>V6.13.0: EnumValues\<ResizeMode\>   | No       | Android \| iOS \| Windows UWP                            | Yes               |
| shutterColor<sup>6.13.0+</sup>                  | 为快门视图应用指定颜色。                                     | string                                                    | No       | Android                                                  | No                |
| subtitleStyle<sup>6.13.0+</sup>                 | 字幕由第三个视图进行管理。                                   | SubtitleStyle                                             | No       | Android \| iOS                                           | No                |
| showNotificationControls<sup>6.13.0+</sup>      | 控制是否在通知区域显示媒体控件。                             | boolean                                                   | No       | Android \| iOS \| web                                    | No                |
| viewType<sup>6.13.0+</sup>                      | 允许显式指定视图类型（鸿蒙支持 TEXTURE、SURFACE）。         | enum {TEXTURE, SURFACE, SURFACE_SECURE}                   | No       | Android                                                  | partially         |



**VideoSrc** 属性

|              **Name**               | **Description**                                              | **Type**      | **Default** | **Required** | **Platform**                        | **HarmonyOS Support** |
| :---------------------------------: | ------------------------------------------------------------ | ------------- | ----------- | ------------ | ----------------------------------- | --------------------- |
|   bufferConfig<sup>6.13.0+</sup>    | “bufferingStrategy” 与 “bufferConfig” 属性密切相关但作用不同。 | BufferConfig  | -           | no           | Android                             | No                    |
| minLoadRetryCount<sup>6.13.0+</sup> | 仅说明设置该值可控制重试次数。                               | number        | -           | no           | Android                             | No                    |
| isLocalAssetFile<sup>6.13.0+</sup>  | 主要解决 Android 平台播放本地视频文件时的路径问题。          | boolean       | -           | no           | Android                             | No                    |
|   startPosition<sup>6.13.0+</sup>   | 提供可选的起始播放位置，单位毫秒。                           | number        | -           | no           | Android  \| iOS \| web              | Yes                   |
|     cropStart<sup>6.13.0+</sup>     | 为视频提供可选的 cropStart 和/或 cropEnd，单位毫秒。         | number        | -           | no           | Android  \| iOS                     | No                    |
|      cropEnd<sup>6.13.0+</sup>      | 为视频提供可选的 cropStart 和/或 cropEnd，单位毫秒。         | number        | -           | no           | Android  \| iOS                     | No                    |
| contentStartTime<sup>6.13.0+</sup>  | SSAI 内容的开始时间（毫秒），决定何时加载分辨率等视频信息。  | number        | -           | no           | Android                             | No                    |
|     metadata<sup>6.13.0+</sup>      | 为视频提供可选的 title、subtitle、artist、imageUri 和/或 description。 | VideoMetadata | -           | no           | Android  \| iOS \| tvOS             | No                    |
|        drm<sup>6.13.0+</sup>        | 用于配置 DRM。                                               | Drm           | -           | no           | Android  \| iOS \| visionOS \| tvOS | No                    |



## 事件回调

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                                 | Description                                                  | Type     | Required | Platform                       | HarmonyOS Support |
| ---------------------------------------------------- | ------------------------------------------------------------ | :------- | -------- | ------------------------------ | ----------------- |
| `onLoad`                                             | 媒体加载完成并可播放时触发的回调。                           | function | No       | All                            | yes               |
| `onLoadStart`                                        | 媒体开始加载时触发的回调。                                   | function | No       | All                            | yes               |
| `onProgress`                                         | 每隔 progressUpdateInterval 毫秒触发，提供当前播放进度信息。 | function | No       | All                            | yes               |
| `onEnd`                                              | 播放到媒体末尾时触发的回调。                                 | function | No       | All                            | yes               |
| `onError`                                            | 播放过程中发生错误时触发的回调。                             | function | No       | All                            | yes               |
| `onBuffer`                                           | 播放器进入缓冲状态时触发的回调。                             | function | No       | Android, iOS                   | yes               |
| `onPlaybackStalled`<sup>deprecated from 6.13.0</sup> | 对应 MediaPlayer 的 MEDIA_INFO_BUFFERING_START 事件。        | function | No       | Android MediaPlayer            | Yes               |
| `onPlaybackResume`<sup>deprecated from 6.13.0</sup>  | 对应 MediaPlayer 的 MEDIA_INFO_BUFFERING_END 事件。          | function | No       | Android MediaPlayer            | Yes               |
| `onAudioBecomingNoisy`                               | 音频输出因设备切换即将变得“嘈杂”时触发（如耳机拔出），建议在此暂停播放以避免扬声器突然响起。 | function | No       | All                            | No                |
| `onBandwidthUpdate`                                  | 可用带宽发生变化时触发。                                     | function | No       | Android                        | No                |
| `onExternalPlaybackChange`                           | 当前视频的外部播放模式变化时触发，常用于 Apple TV 连接或断开。 | function | No       | iOS                            | No                |
| `onFullscreenPlayerWillPresent`                      | 播放器即将进入全屏时触发。                                   | function | No       | All                            | Yes               |
| `onFullscreenPlayerDidPresent`                       | 播放器已进入全屏时触发。                                     | function | No       | All                            | Yes               |
| `onFullscreenPlayerWillDismiss`                      | 播放器即将退出全屏时触发。                                   | function | No       | All                            | Yes               |
| `onFullscreenPlayerDidDismiss`                       | 播放器退出全屏后触发。                                       | function | No       | All                            | Yes               |
| `onReadyForDisplay`                                  | 首帧准备好显示（海报被移除）时触发。                         | function | No       | All                            | Yes               |
| `onPictureInPictureStatusChanged`                    | 画中画激活或失效时触发。                                     | function | No       | IOS                            | Yes               |
| `onPlaybackRateChange`                               | 播放速率发生变化（例如暂停或恢复）时触发。                   | function | No       | All                            | Yes               |
| `onSeek`                                             | 完成一次 Seek 操作时触发。                                   | function | No       | All                            | partially         |
| `onRestoreUserInterfaceForPictureInPictureStop`      | 对应 Apple 的 restoreUserInterfaceForPictureInPictureStopWithCompletionHandler，恢复界面后需调用 restoreUserInterfaceForPictureInPictureStopCompleted。 | function | No       | iOS                            | No                |
| `onTimedMetadata`                                    | 定时元数据可用时触发。                                       | function | No       | All                            | No                |
| onIdle<sup>6.13.0+</sup>                             | 播放器进入空闲状态（无缓冲与播放任务）时触发。               | function | No       | Android                        | Yes               |
| onControlsVisibilityChange<sup>6.13.0+</sup>         | 播放器控件显示或隐藏时触发。                                 | function | No       | Android                        | Yes               |
| onVolumeChange<sup>6.13.0+</sup>                     | 播放器音量发生变化时触发。                                   | function | No       | Android， iOS, visionOS ,  web | Yes               |
| onReceiveAdEvent<sup>6.13.0+</sup>                   | IMA SDK 收到 AdEvent 时触发。                                | function | No       | Android, iOS                   | No                |
| onPlaybackStateChanged<sup>6.13.0+</sup>             | 播放状态变化时触发。                                         | function | No       | Android, iOS , visionOS, web   | Yes               |
| onAudioTracks<sup>6.13.0+</sup>                      | 可用音频轨道发生变化时触发。                                 | function | No       | Android， iOS                  | Yes               |
| onTextTracks<sup>6.13.0+</sup>                       | 可用文本（字幕）轨道发生变化时触发。                         | function | No       | Android， iOS                  | No                |
| onTextTrackDataChanged<sup>6.13.0+</sup>             | 新的字幕数据可用时触发。                                     | function | No       | Android， iOS                  | No                |
| onVideoTracks<sup>6.13.0+</sup>                      | 视频轨道发生变化时触发。                                     | function | No       | Android                        | Yes               |
| onAspectRatio<sup>6.13.0+</sup>                      | 视频宽高比发生变化时触发，便于同步 UI 布局。                 | function | No       | Android                        | Yes               |




## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                                         | Description                                                  | Type     | Required | Platform          | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- | ----------------- |
| `seek()`                                                     | 跳转到以秒为单位的指定位置，seconds 为浮点值。               | function | No       | All               | yes               |
| `dismissFullscreenPlayer()`                                  | 让播放器退出全屏模式。                                       | function | No       | All               | yes               |
| `presentFullscreenPlayer()`                                  | 让播放器进入全屏模式。                                       | function | No       | All               | yes               |
| `save()`                                                     | 将携带当前滤镜的视频保存到相册，返回 Promise。               | function | No       | iOS               | No                |
| `restoreUserInterfaceForPictureInPictureStop()`              | 对应 Apple 的 restoreUserInterfaceForPictureInPictureStop 完成处理器，必须在调用 onRestoreUserInterfaceForPictureInPictureStop 之后执行。 | function | No       | iOS               | No                |
| restoreUserInterfaceForPictureInPictureStopCompleted()<sup>6.13.0+</sup> | 必须在 onRestoreUserInterfaceForPictureInPictureStop 执行完毕后调用。 | function | No       | iOS               | No                |
| resume()<sup>6.13.0+</sup>                                   | 恢复视频播放。                                               | function | No       | Android, iOS, web | Yes               |
| pause()<sup>6.13.0+</sup>                                    | 暂停视频播放。                                               | function | No       | Android, iOS, web | Yes               |
| setVolume()<sup>6.13.0+</sup>                                | 调整音量，行为与 volume 属性一致。                           | function | No       | Android, iOS, web | Yes               |
| getCurrentPosition()<sup>6.13.0+</sup>                       | 返回当前播放位置（秒）。                                     | function | No       | Android, iOS, web | Yes               |
| setFullScreen()<sup>6.13.0+</sup>                            | 切换全屏模式。                                               | function | No       | Android, iOS, web | Yes               |
| setSource()<sup>6.13.0+</sup>                                | 动态更新媒体源。                                             | function | No       | Android, iOS      | Yes               |
| enterPictureInPicture()<sup>6.13.0+</sup>                    | 进入画中画（PiP）模式。                                       | function | No       | Android, iOS, web | Yes               |
| exitPictureInPicture()<sup>6.13.0+</sup>                     | 退出画中画（PiP）模式。                                      | function | No       | Android, iOS, web | Yes               |
| nativeHtmlVideoRef()<sup>6.13.0+</sup>                       | 返回原生 HTML `<video>` 元素引用，可用于集成 hls.js、shaka、video.js 等三方库。 | function | No       | web               | No                |
| getWidevineLevel()<sup>6.13.0+</sup>                         | 返回 Widevine DRM 级别。                                     | function | No       | Android           | No                |
| isCodecSupported()<sup>6.13.0+</sup>                         | 检查指定的视频编码是否受支持。                               | function | No       | Android, web      | No                |
| isHEVCSupported()<sup>6.13.0+</sup>                          | 检查是否支持 1920×1080 分辨率的 HEVC（H.265）。              | function | No       | Android           | No                |



## 遗留问题

- [ ] source 暂时只支持在线 URL 资源问题： [issue#34](https://github.com/react-native-oh-library/react-native-video/issues/34)。
- [ ] react-native-video 部分属性和方法未实现 HarmonyOS 化： [issue#60](https://github.com/react-native-oh-library/react-native-video/issues/60)。
- [ ] V6.13.0原库部分接口在HarmonyOS中没有对应属性或接口支持： [issue#153](https://github.com/react-native-oh-library/react-native-video/issues/153)。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TheWidlarzGroup/react-native-video/blob/master/LICENSE) ，请自由地享受和参与开源。
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-track-player</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/doublesymmetry/react-native-track-player">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/doublesymmetry/react-native-track-player/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-track-player)

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 4.1.2@deprecated      | [@react-native-oh-tpl/react-native-track-player Releases(deprecated)](https://github.com/react-native-oh-library/react-native-track-player/releases) | 0.72       |
| 4.1.3       | [@react-native-ohos/react-native-track-player Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-track-player/releases)                        | 0.72       |
| 4.2.0     | [@react-native-ohos/react-native-track-player Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-track-player/releases)                        | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-track-player
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-track-player
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect } from "react";
import { ScrollView, Text, Button, View, StyleSheet } from 'react-native';
import TrackPlayer from 'react-native-track-player';

const TrackPlayerDemo = () => {
    useEffect(() => {
        // Set up the player
        TrackPlayer.setupPlayer();
    }, []);

    const addExample = () => {
        TrackPlayer.add([
            {
                url: "https://ting8.yymp3.com/new27/chengxiang10/1.mp3",
                title: "世界这么大还是遇见你",
                artist: "程响",
                artwork: "https://rntp.dev/example/Longing.jpeg",
                duration: 237
            },
            {
                url: "https://ting8.yymp3.com/new18/fhzq4/8.mp3",
                title: "最炫民族风",
                artist: "凤凰传奇",
                artwork: "https://rntp.dev/example/Rhythm%20City%20(Demo).jpeg",
                duration: 283
            }, {
                url: "https://ting8.yymp3.com/new27/jinzhiwen3/1.mp3",
                title: "远走高飞",
                artist: "金志文",
                artwork: "https://rntp.dev/example/Rhythm%20City%20(Demo).jpeg",
                duration: 235
            }]);
    }

    // 开始播放歌曲
    const startExample = () => {
        // Start playing it
        TrackPlayer.play();
    }
    // 暂停播放歌曲
    const pauseExample = () => {
        TrackPlayer.pause();
    }
    return (
        <ScrollView>
            <View>
                <Text style={styles.text}>TrackPlayerDemo </Text>
                <View>
                    <Text style={styles.text}>添加Track</Text>
                    <Button
                        title="add"
                        color="#9a73ef"
                        onPress={addExample}
                    />
                </View>

                <View>
                    <Text style={styles.text}>播放Track</Text>
                    <Button
                        title="play"
                        color="#9a73ef"
                        onPress={startExample}
                    />
                </View>

                <View>
                    <Text style={styles.text}>暂停Track</Text>
                    <Button
                        title="pause"
                        color="#9a73ef"
                        onPress={pauseExample}
                    />
                </View>
            </View>
        </ScrollView>
    )
};

const styles = StyleSheet.create({
    text: {
        fontSize: 18,
        marginBottom: 10,
        color: 'red',
    },
});
export default TrackPlayerDemo;
```

## 使用 Codegen

Version >= @react-native-ohos/react-native-track-player@4.1.3，已适配codegen-lib生成桥接代码。

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

Version >= @react-native-ohos/react-native-track-player@4.1.3，已支持 Autolink，无需手动配置，目前只支持72框架。
Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-track-player": "file:../../node_modules/@react-native-ohos/react-native-track-player/harmony/track_player.har"
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

### 3.配置CMakeLists 和引入 TrackPlayerPackage

> [!TIP] 若使用的是 4.1.2 版本，请跳过本章

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-track-player/src/main/cpp" ./track-player)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_track_player)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "TrackPlayerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<TrackPlayerPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNTrackPlayerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNTrackPlayerPackage } from "@react-native-ohos/react-native-track-player/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTrackPlayerPackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

### 权限要求

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"abilities": [
+  {
+    "backgroundModes": [
+      "audioPlayback"
+    ]
+  }
]

"requestPermissions": [
+  {
+    "name": "ohos.permission.KEEP_BACKGROUND_RUNNING",
+    "reason": "$string:app_name",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when": "always"
+    }
+  },
]
```


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                     | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| setupPlayer              | 使用指定选项初始化播放器。           | promise | yes      | Android/iOS | partially               |
| isServiceRunning         | 不应使用此方法，大多数方法在服务未绑定时会拒绝。 | promise | no       | Android/iOS | yes               |
| add                      | 将曲目添加到队列中。                                   | promise | no       | Android/iOS | yes               |
| load                     | 替换当前曲目或将曲目加载为队列中的第一首。 | promise | no       | Android/iOS | yes               |
| move                     | 移动队列中的曲目。                              | promise | no       | Android/iOS | yes               |
| remove                   | 根据索引从队列中删除多个曲目。     | promise | no       | Android/iOS | yes               |
| removeUpcomingTracks     | 清除队列中即将到来的曲目。                   | promise | no       | Android/iOS | yes               |
| skip                     | 跳转到队列中的某个曲目。                               | promise | no       | Android/iOS | yes               |
| skipToNext               | 跳转到队列中的下一首曲目。                       | promise | no       | Android/iOS | yes               |
| skipToPrevious           | 跳转到队列中的上一首曲目。                    | promise | no       | Android/iOS | yes               |
| updateOptions            | 更新组件的配置。                | promise | no       | Android/iOS | no                |
| updateMetadataForTrack   | 更新队列中曲目的元数据。如果更新了当前曲目，则通知和正在播放中心将相应更新。 | promise | no       | Android/iOS | partially               |
| clearNowPlayingMetadata  | 清除正在播放中心中曲目的元数据。           | promise | no       | Android/iOS | partially               |
| updateNowPlayingMetadata | 更新正在播放中心的元数据内容，而不影响为当前曲目存储的数据。 | promise | no       | Android/iOS | partially               |
| reset                    | 重置播放器，停止当前曲目并清除队列。 | promise | no       | Android/iOS | yes               |
| play                     | 播放或恢复当前曲目。                         | promise | no       | Android/iOS | yes               |
| pause                    | 暂停当前曲目。                                    | promise | no       | Android/iOS | yes               |
| stop                     | 停止当前曲目。                                     | promise | no       | Android/iOS | yes               |
| setPlayWhenReady         | 设置播放器是否会在准备好时自动播放。 | promise | no       | Android/iOS | yes               |
| getPlayWhenReady         | 获取播放器是否会在准备好时自动播放。 | promise | no       | Android/iOS | yes               |
| seekTo                   | 寻找到当前曲目中的指定时间位置。     | promise | no       | Android/iOS | yes               |
| seekBy                   | 在当前曲目中按相对时间偏移进行寻址。       | promise | no       | Android/iOS | yes               |
| setVolume                | 设置播放器音量。                               | promise | no       | Android/iOS | yes               |
| setRate                  | 设置播放速度。                                      | promise | no       | Android/iOS | partially               |
| setQueue                 | 设置队列。                                              | promise | no       | Android/iOS | yes               |
| setRepeatMode            | 设置队列重复模式。                                  | promise | no       | Android/iOS | yes               |
| getVolume                | 获取播放器音量，范围为0到1之间的数字。   | promise | no       | Android/iOS | yes               |
| getRate                  | 获取播放速度，其中0.5为半速，1为正常速度，2为双倍速度等。 | promise | no       | Android/iOS | yes               |
| getTrack                 | 从队列中获取曲目对象。                          | promise | no       | Android/iOS | yes               |
| getQueue                 | 获取整个队列。                                        | promise | no       | Android/iOS | yes               |
| getActiveTrackIndex      | 获取队列中活动曲目的索引，如果没有当前曲目则返回undefined。 | promise | no       | Android/iOS | yes               |
| getCurrentTrack      | 获取队列中活动曲目的索引，如果没有当前曲目则返回undefined。（建议使用getActiveTrackIndex()获取。） | promise | no       | Android/iOS | yes               |
| getActiveTrack           | 获取活动曲目，如果没有当前曲目则返回undefined。 | promise | no       | Android/iOS | yes               |
| getDuration              | 获取当前曲目的持续时间（秒）。           | promise | no       | Android/iOS | yes               |
| getBufferedPosition      | 获取当前曲目的缓冲时间（秒）。  | promise | no       | Android/iOS | yes               |
| getPosition              | 获取当前曲目的播放时间（秒）。  | promise | no       | Android/iOS | yes               |
| getProgress              | 获取当前活动曲目的进度信息，包括当前播放位置（秒）、缓冲位置（秒）和持续时间（秒）。 | promise | no       | Android/iOS | yes               |
| getPlaybackState         | 获取播放器的播放状态。                      | promise | no       | Android/iOS | partially               |
| getState         | 获取播放器的播放状态。（建议使用getPlaybackState()获取。）                       | promise | no       | Android/iOS | partially               |
| getRepeatMode            | 获取队列重复模式。                                  | promise | no       | Android/iOS | yes               |
| retry                    | 当播放状态为State.Error时重新尝试播放当前项目。 | promise | no       | Android/iOS | yes               |

**setupPlayer方法参数**

| Name    | Description                                | Type          | Required | Platform    | HarmonyOS Support |
| ------- | ------------------------------------------ | ------------- | -------- | ----------- | ----------------- |
| options | 用于初始化播放器的选项。                     | PlayerOptions | no       | iOS/Android | no                |

**add方法参数**

| Name              | Description                           | Type               | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| track             | 要添加到队列中的曲目。                  | AddTrack\|ATrack[] | yes      | iOS/Android | yes               |
| insertBeforeIndex | 要在之前插入曲目的索引。                 | number             | no       | iOS/Android | yes               |

**load方法参数**

| Name  | Description        | Type  | Required | Platform    | HarmonyOS Support |
| ----- | ------------------ | ----- | -------- | ----------- | ----------------- |
| track | 要加载的曲目。 | Track | yes      | iOS/Android | yes               |

**move方法参数**

| Name      | Description                         | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ----------------------------------- | ------ | -------- | ----------- | ----------------- |
| fromIndex | 要移动的曲目索引。                    | number | yes      | iOS/Android | yes               |
| toIndex   | 曲目要移动到的目标索引。              | number | yes      | iOS/Android | yes               |

**remove方法参数**

| Name           | Description                           | Type             | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| indexOrIndexes | 要移除的曲目索引（可为单个索引或索引数组）。 | number\|number[] | yes      | iOS/Android | yes               |

**skip方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| index           | 要跳转到的曲目索引。                          | number | yes      | iOS/Android | yes               |
| initialPosition | 初始跳转位置，单位为秒。                       | number | no       | iOS/Android | yes               |

**skipToNext方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| initialPosition | 初始跳转位置，单位为秒。                       | number | no       | iOS/Android | yes               |

**skipToPrevious方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| initialPosition | 初始跳转位置，单位为秒。                      | number | no       | iOS/Android | yes               |

**updateOptions方法参数**

| Name                      | Description                 | Type          | Required | Platform    | HarmonyOS Support |
| ------------------------- | --------------------------- | ------------- | -------- | ----------- | ----------------- |
| alwaysPauseOnInterruption | 遇到音频中断时是否始终暂停。   | boolean       | no       | Android     | no                |
| options                   | 要更新的选项。               | UpdateOptions | no       | iOS/Android | no                |

**updateMetadataForTrack方法参数**

| Name       | Description                                            | Type              | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| trackIndex | 要更新元数据的曲目的索引。                                | number            | yes      | iOS/Android | yes               |
| metadata   | 要更新的元数据。                                         | TrackMetadataBase | yes      | iOS/Android | partially               |

**updateNowPlayingMetadata方法参数**

| Name     | Description             | Type               | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------- | ------------------ | -------- | ----------- | ----------------- |
| metadata | 要更新的元数据。         | NowPlayingMetadata | yes      | iOS/Android | partially               |

**setPlayWhenReady方法参数**

| Name          | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| playWhenReady | 当 playWhenReady = true 时，相当于调用 TrackPlayer.play()；当 playWhenReady = false 时，相当于调用 TrackPlayer.pause()。 | boolean | yes      | iOS/Android | yes               |

**seekTo方法参数**

| Name     | Description                         | Type   | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------------- | ------ | -------- | ----------- | ----------------- |
| position | 要跳转到的位置，单位为秒。             | number | yes      | iOS/Android | yes               |

**seekBy方法参数**

| Name   | Description                            | Type   | Required | Platform    | HarmonyOS Support |
| ------ | -------------------------------------- | ------ | -------- | ----------- | ----------------- |
| offset | 以秒为单位的时间偏移量，用于快进或快退。   | number | yes      | iOS/Android | yes               |

**setVolume方法参数**

| Name  | Description                             | Type   | Required | Platform    | HarmonyOS Support |
| ----- | --------------------------------------- | ------ | -------- | ----------- | ----------------- |
| level | 音量值，取值范围为 0 到 1 之间的数字。     | number | yes      | iOS/Android | yes               |

**setRate方法参数**

| Name | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| rate | 更改播放速度，其中0.5为半速，1为正常速度，2为双倍速度等。         | number | yes      | iOS/Android | partially              |

**setQueue方法参数**

| Name   | Description                     | Type    | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------- | ------- | -------- | ----------- | ----------------- |
| tracks | 要设置为队列的曲目。              | Track[] | yes      | iOS/Android | yes               |

**setRepeatMode方法参数**

| Name | Description             | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------------------- | ---------- | -------- | ----------- | ----------------- |
| mode | 要设置的重复模式。        | RepeatMode | yes      | iOS/Android | yes               |

**getTrack方法参数**

| Name  | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| index | 	曲目的索引。           | number | yes       | iOS/Android  | yes               |

## 遗留问题

- [ ] 目前harmonyOS设置metadata仅支持现有API中参数，对于genre、rating、isLiveStream、elapsedTime四个参数均未适配harmonyOS Next。[issue#3](https://github.com/react-native-oh-library/react-native-track-player/issues/3)
- [ ] 目前仅支持setupPlayer接口的调用，不支持该接口携带的参数对播放器进行相关的设置，该接口参数均未适配harmonyOS Next。[issue#4](https://github.com/react-native-oh-library/react-native-track-player/issues/4)
- [ ] 目前harmonyOS中不支持获取buffering状态。[issue#5](https://github.com/react-native-oh-library/react-native-track-player/issues/5)
- [ ] 目前harmonyOS中支持九种固定的播放速率，其他播放速率均未问题适配harmonyOS Next。[issue#6](https://github.com/react-native-oh-library/react-native-track-player/issues/6)
- [ ] 目前harmonyOS不支持对播控中心的更新设置，updateOptions接口未适配harmonyOS Next。[issue#7](https://github.com/react-native-oh-library/react-native-track-player/issues/7)

## 其他

## 开源协议

本项目基于 [The Apache License(Apache)](https://github.com/doublesymmetry/react-native-track-player/blob/main/LICENSE) ，请自由地享受和参与开源。


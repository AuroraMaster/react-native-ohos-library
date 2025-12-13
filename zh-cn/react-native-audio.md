> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-audio</code> </h1>
</p>

> [!TIP] [Github 地址](https://github.com/jsierles/react-native-audio)

## 1. 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本  | 发布信息                                                  | 支持RN版本 |
|--------| ------------------------------------------------------------ | ---------- |
| <= 4.3.1-0.1.0@deprecated  | [@react-native-oh-tpl/react-native-audio Releases(deprecated)](https://github.com/react-native-oh-library/react-native-audio/releases) | 0.72       |
| 4.2.4             | [@react-native-ohos/react-native-audio Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-audio/releases)   | 0.72       |
| 4.3.0             | [@react-native-ohos/react-native-audio Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-audio/releases)   | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-audio
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-audio
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState, useEffect } from 'react';
import { SafeAreaView, StatusBar, Text, Button, TextInput, View, Switch, StyleSheet, TouchableOpacity } from 'react-native';
import { AudioRecorder, AudioUtils } from 'react-native-audio';

type FileType = {
    [key: string]: any,
    base64: string;
    duration: number;
    status: string;
    audioFileSize: number;
    audioFileURL: string;
}

interface ObjectDataType {
  currentTime: number,
  duration: number,
  status: string,
  audioFileSize: number,
  audioFileURL: string,
  base64: string,
}

export default () => {
    const [second, setSecond] = useState<number>(0);
    const [file, setFile] = useState<FileType>();

    const initAudio = async () => {

        // request microphone premission
        await AudioRecorder.requestAuthorization()

        // you check premission any time
        await AudioRecorder.checkAuthorizationStatus();

        // Initialize recording parameters
        await AudioRecorder.prepareRecordingAtPath(
            `${AudioUtils.FilesDirectoryPath}/audio_demo.m4a`,
            {
                SampleRate: 48000,
                Channels: 2,
                AudioQuality: 'High',//only ios
                AudioEncoding: 'aac',
                AudioEncodingBitRate: 100000,
                AudioSource: 1,
                OutputFormat: 'm4a',
                MeteringEnabled: false,//only ios
                MeasurementMode: false,//only ios
                IncludeBase64: true
            })
        AudioRecorder.onProgress = (data: ObjectDataType) => {
            setSecond(data.currentTime);
        }
        AudioRecorder.onFinished = (data: ObjectDataType) => {
            const { duration, status, audioFileSize, audioFileURL } = data
            let str = data.base64.slice(0, 20);
            setFile({ base64: str + '...', duration, status, audioFileSize, audioFileURL })
        }
    }
    const resetRecording = () => {
        setFile({
            base64: "",
            duration: 0,
            status: "",
            audioFileSize: 0,
            audioFileURL: ""
        })
        setSecond(0)
        initAudio()
    }
    const renderFileLinesComp = () => {
        if (!file?.base64) return false
        return Object.keys(file).map(name => (
            <View key={name} style={{ display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center', marginTop: 10 }}>
                <Text style={{ fontSize: 12 }}>{name}:</Text>
                <Text >{`${file[name]}`}</Text>
            </View>))
    }

    useEffect(() => {
        initAudio()
        return () => { }
    }, [])

    return (
        <SafeAreaView>
            <View style={{ marginTop: 10, borderColor: '#aaa', borderWidth: 1, padding: 10 }}>
                <View>
                    <Text>{`currentTime: ${parseInt(`${second}`)}`}</Text>
                </View>
            </View>
            <View style={{ marginTop: 10, display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' }}>
                <View style={{ width: 80 }}>
                    <Button
                        title="start"
                        onPress={async () => {
                            await AudioRecorder.startRecording();
                        }}
                    />
                </View>
                <View style={{ width: 80 }}>
                    <Button
                        title="pause"
                        onPress={async () => {
                            await AudioRecorder.pauseRecording();
                        }}
                    />
                </View>
                <View style={{ width: 80 }}>
                    <Button
                        title="resume"
                        onPress={async () => {
                            await AudioRecorder.resumeRecording();
                        }}
                    />
                </View>
                <View style={{ width: 80 }}>
                    <Button
                        title="stop"
                        onPress={async () => {
                            await AudioRecorder.stopRecording();
                            !AudioRecorder.onFinished && resetRecording()
                        }}
                    />
                </View>
            </View>

            {!!file?.base64 && <View style={{ marginTop: 10, borderColor: '#aaa', borderWidth: 1, padding: 10 }}>
                <View style={{ marginTop: 10, display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' }}>
                    <Text>录音文件：</Text>
                    <Text style={{ fontSize: 12 }}>{`audio_demo.m4a`}</Text>
                </View>
                {renderFileLinesComp()}
                <View style={{ marginTop: 10, display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' }}>
                    <View style={{ width: 160 }}>
                        <Button
                            title="reset"
                            onPress={resetRecording}
                        />
                    </View>
                </View>
            </View>}

        </SafeAreaView >
    )
}    
```

## 2.Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~4.3.0                               |  No              |  0.77     |
| ~4.2.4                              |  Yes             |  0.72     |
| <= 4.3.1-0.1.0@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1 Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `harmony/oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-audio": "file:../../node_modules/@react-native-ohos/react-native-audio/harmony/audio.har"
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


### 2.3 配置 CMakeLists 和引入 AudioPackage

> 若使用的是 <= 4.3.1-0.1.0 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-audio/src/main/cpp" ./audio)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_audio)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "AudioPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<AudioPackage>(ctx)
    };
}
```

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {AudioPackage} from '@react-native-ohos/react-native-audio/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AudioPackage(ctx)
  ];
}
```
</details>

## 3. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 4. 约束与限制

### 4.1 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## 5. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| requestAuthorization  | Request microphone permission  | function  | no | Android/IOS | yes |
| checkAuthorizationStatus  | Check authorization status  | function  | no | Android/IOS | yes |
| prepareRecordingAtPath  | Initialize recording instance parameters  | function  | no | Android/IOS | yes |
| startRecording  | start recording   | function  | no | Android/IOS | yes |
| pauseRecording  | Pause recording  | function  | no | Android/IOS | yes |
| resumeRecording  | Resume recording  | function  | no | Android/IOS | yes |
| stopRecording  | stop recording   | function  | no | Android/IOS | yes |

## 6. 遗留问题

## 7. 其他
### 7.1 不同系统支持的编码格式

Encodings supported on iOS: lpcm, ima4, aac, MAC3, MAC6, ulaw, alaw, mp1, mp2, alac, amr.

Encodings supported on Android: aac, aac_eld, amr_nb, amr_wb, he_aac, vorbis.

Encodings supported on Harmony: aac.

AudioQuality、MeteringEnabled、MeasurementMode is only for ios now.

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-audio/blob/master/LICENSE) ，请自由地享受和参与开源。
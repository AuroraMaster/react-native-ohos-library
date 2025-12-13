> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ak1394/react-native-tts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20Windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ak1394/react-native-tts/blob/master/README.md#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-tts)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                     | Supported RN Version |
|-----------------------------| ------------------------------------------------------------ | ---------- |
| <= 4.1.1-0.0.3@deprecated   | [@react-native-oh-tpl/react-native-tts Releases(deprecated)](https://github.com/react-native-oh-library/react-native-tts/releases) | 0.72       |
| 4.1.3                       | [@react-native-ohos/react-native-tts Releases](https://github.com/react-native-oh-library/react-native-tts/releases)                        | 0.72       |
| 4.2.0                       | [@react-native-ohos/react-native-tts Releases](https://github.com/react-native-oh-library/react-native-tts/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-tts
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-tts
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { useState, useCallback } from "react";
import { Text, View, StyleSheet, SafeAreaView } from "react-native";
import Tts from "react-native-tts";

const cnText = `炎炎夏日，阳光如烈火般炙烤大地，空气中弥漫着热浪的气息。树荫下，蝉鸣声如同热浪中跳跃的音符，微风吹过，带来一丝清凉。远处的田野上，金黄的麦浪随风起伏，仿佛在舞动着夏天的节奏。天空湛蓝如洗，白云悠然飘过，似是一幅宁静而美丽的夏日画卷。`;

export function TTSDemo() {
  const [speakText, setSpeakText] = useState < string > cnText;

  const addEvent = useCallback(() => {
    Tts.addEventListener("tts-start", (res) => {
      console.log("tts-start", res);
    });
  }, []);

  const removeEvent = useCallback(() => {
    Tts.addEventListener("tts-start", (res) => {
      console.log("tts-start", res);
    });
  }, []);

  const stopSpeak = useCallback(() => {
    Tts.stop();
  }, []);

  const speakFc = useCallback(() => {
    Tts.speak(speakText);
  }, []);

  const getInitStatus = useCallback(() => {
    Tts.getInitStatus().then(() => {
      console.log("initialization completed");
    });
  }, []);

  const pauseFc = useCallback(() => {
    Tts.pause();
  }, []);

  const resumeFc = useCallback(() => {
    Tts.resume();
  }, []);

  const setSpeakRate = useCallback(() => {
    Tts.setDefaultRate(2);
  }, []);

  const setSpeakPitch = useCallback(() => {
    Tts.setDefaultPitch(2);
  }, []);

  const queryVoices = useCallback(() => {
    Tts.voices().then((res) => {
      const resTr = JSON.stringify(res);
      setSpeakText(resTr);
    });
  }, []);

  return (
    <>
      <SafeAreaView style={styles.constainer}>
        <Text style={styles.title}>react-native-tts functional verification</Text>
        <View style={styles.content}>
          <View style={styles.btnWrap}>
            <Text style={styles.button} onPress={getInitStatus}>
              getInitStatus
            </Text>
            <Text style={styles.button} onPress={speakFc}>
              speak（zh）
            </Text>
            <Text style={styles.button} onPress={stopSpeak}>
              stop
            </Text>
            <Text style={styles.button} onPress={pauseFc}>
              pause
            </Text>
            <Text style={styles.button} onPress={resumeFc}>
              resume
            </Text>
            <Text style={styles.button} onPress={setSpeakRate}>
              setDefaultRate
            </Text>
            <Text style={styles.button} onPress={setSpeakPitch}>
              setDefaultPitch
            </Text>
            <Text style={styles.button} onPress={queryVoices}>
              voices
            </Text>
            <Text style={styles.button} onPress={addEvent}>
              addEventListener
            </Text>
            <Text style={styles.button} onPress={removeEvent}>
              removeEventListener
            </Text>
          </View>
        </View>
      </SafeAreaView>
    </>
  );
}

const styles = StyleSheet.create({
  constainer: {
    flex: 1,
  },
  content: {
    flex: 1,
    display: "flex",
  },
  btnWrap: {
    width: "auto",
    backgroundColor: "gray",
    display: "flex",
    flexDirection: "row",
    flexWrap: "wrap",
    paddingLeft: 20,
  },
  text: {
    padding: 20,
    fontSize: 20,
  },
  title: {
    padding: 10,
    fontSize: 30,
    textAlign: "center",
  },
  button: {
    paddingVertical: 6,
    paddingHorizontal: 12,
    backgroundColor: "hsl(193, 95%, 68%)",
    borderWidth: 2,
    borderColor: "hsl(193, 95%, 30%)",
  },
});
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                           | is supporte autolink  | Supported RN Version |
|---------------------------|-----------------------|----------------------|
| ~4.2.0                    |  No                   |  0.77                |
| ~4.1.3                    |  Yes                  |  0.72                |
| <= 4.1.1-0.0.3@deprecated |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-tts": "file:../../node_modules/@react-native-ohos/react-native-tts/harmony/rn_tts.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing RNTTSPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+   import { RNTTSPackage } from '@react-native-ohos/react-native-tts/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTTSPackage(ctx)
  ];
}
```


### 4. Configuring CMakeLists and Introducing RNTTSPackage

> If you are using version <= 4.1.1-0.0.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-tts/src/main/cpp" ./rn_tts)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_tts)
# RNOH_BEGIN: manual_package_linking_2
```
Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
+ #include "RNTTSPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<RNTTSPackage>(ctx)
}
```
</details>





## Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                             | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ----------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| getInitStatus         | Returns a promise that resolves when the TTS engine is initialized.     | Function | no       | All      | yes               |
| requestInstallEngine  | Requests installation of the TTS engine if not already installed.       | Function | no       | Android  | no                |
| requestInstallData    | Requests installation of the TTS data if not already installed.         | Function | no       | Android  | no                |
| setDucking            | Sets whether the TTS engine should duck other audio when speaking.      | Function | no       | All      | no                |
| setDefaultEngine      | Sets the default TTS engine.                                            | Function | no       | Android  | no                |
| setDefaultVoice       | Sets the default voice for the TTS engine.                              | Function | no       | All      | no                |
| setDefaultRate        | Sets the default speech rate for the TTS engine.                        | Function | no       | All      | yes               |
| setDefaultPitch       | Sets the default pitch for the TTS engine.                              | Function | no       | All      | yes               |
| setDefaultLanguage    | Sets the default language for the TTS engine.                           | Function | no       | All      | no                |
| setIgnoreSilentSwitch | Sets whether to ignore the silent button.                               | Function | no       | iOS      | no                |
| voices                | Retrieves a list of available voices from the TTS engine.               | Function | no       | All      | yes               |
| engines               | Retrieves a list of available TTS engines.                              | Function | no       | Android  | no                |
| speak                 | Speaks the given utterance and returns a promise with the utterance ID. | Function | no       | All      | yes               |
| stop                  | Stops the current TTS utterance.                                        | Function | no       | All      | yes               |
| pause                 | Pause the current TTS utterance.                                        | Function | no       | All      | yes               |
| resume                | Resume the current TTS utterance.                                       | Function | no       | All      | yes               |
| addEventListener      | Adding an Event Listener                                                | Function | no       | All      | yes               |
| removeEventListener   | Remove Event Listener                                                   | Function | no       | All      | yes               |

## Known Issues

- [ ] 三方引擎相关功能无法实现的问题：[issue#2](https://github.com/react-native-oh-library/react-native-tts/issues/2)
- [ ] 语言类型只支持中文的问题：[issue#3](https://github.com/react-native-oh-library/react-native-tts/issues/3)
- [ ] setDucking 无法实现的问题：[issue#4](https://github.com/react-native-oh-library/react-native-tts/issues/4)
- [ ] setIgnoreSilentSwitch 无法实现的问题：[issue#5](https://github.com/react-native-oh-library/react-native-tts/issues/5)
- [ ] setDefaultVoice 无法实现的问题：[issue#6](https://github.com/react-native-oh-library/react-native-tts/issues/6)
- [ ] 边合成边播放的问题：[issue#7](https://github.com/react-native-oh-library/react-native-tts/issues/7)
- [ ] 参数 skipTransform、onWordBoundary 无效的问题：[issue#8](https://github.com/react-native-oh-library/react-native-tts/issues/8)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ak1394/react-native-tts/blob/master/README.md#license).

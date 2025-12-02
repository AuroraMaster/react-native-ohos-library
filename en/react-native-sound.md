> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sound</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zmxv/react-native-sound">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zmxv/react-native-sound/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-sound)

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-sound`, After introducing the new version of the third-party library, The version correspondence details are as follows:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | Support RN version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |------------------------------------------------------------ |
| <= 0.11.2-0.0.13@deprecated | @react-native-oh-tpl/react-native-sound | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-sound) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sound/releases) | 0.72 |
| >= 0.11.3                        | @react-native-ohos/react-native-sound       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-sound) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sound/releases) | 0.77 |

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-sound

# 0.77
npm install @react-native-ohos/react-native-sound
```

#### yarn

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-sound

# 0.77
yarn add @react-native-ohos/react-native-sound
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import type { PropsWithChildren } from "react";
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
  Button,
} from "react-native";

import {
  Colors,
  DebugInstructions,
  Header,
  LearnMoreLinks,
  ReloadInstructions,
} from "react-native/Libraries/NewAppScreen";

import Sound from "react-native-sound";

type SectionProps = PropsWithChildren<{
  title: string;
  func: () => void;
}>;

type SliderSectionProps = PropsWithChildren<{
  duration: number;
  value: number;
  func: () => void;
}>;

function Section({ title, func }: SectionProps): JSX.Element {
  const isDarkMode = useColorScheme() === "dark";
  return (
    <View style={styles.sectionContainer}>
      <Button
        onPress={func}
        title={title}
        color="#2196f3"
        accessibilityLabel="Learn more about this purple button"
      />
    </View>
  );
}

function SoundDemo(): JSX.Element {
  const isDarkMode = useColorScheme() === "dark";
  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };

  const navigationOptions = (props: {
    navigation: { state: { params: { title: any } } };
  }) => ({
    title: props.navigation.state.params.title,
  });

  let sound = new Sound("whoosh.mp3");

  const onPlay = () => {
    sound.play();
  };

  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={isDarkMode ? "light-content" : "dark-content"}
        backgroundColor={backgroundStyle.backgroundColor}
      />
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}
      >
        <Header />

        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
          }}
        >
          <Section title="play" func={onPlay}></Section>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 12,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: "600",
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: "400",
  },
  highlight: {
    fontWeight: "700",
  },
});

export default SoundDemo;
```

## Link

Version >= @react-native-ohos/react-native-sound@0.11.3 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

Currently, Version <= @react-native-oh-tpl/react-native-sound@0.11.2-0.0.13@deprecated does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

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

RN 72
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-sound": "file:../../node_modules/@react-native-oh-tpl/react-native-sound/harmony/sound.har"
  }
```
RN 77
```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-sound": "file:../../node_modules/@react-native-ohos/react-native-sound/harmony/sound.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing SoundPackge

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ # 0.72
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-sound/src/main/cpp" ./sound)

+ # 0.77
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-sound/src/main/cpp" ./sound)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_sound)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SoundPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SoundPackage>(ctx),
    };
}
```

### 4.Introducing SoundPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ // 0. 72  
+ import { SoundPackage } from '@react-native-oh-tpl/react-native-sound/ts';

+ // 0. 77
+ import { SoundPackage } from '@react-native-ohos/react-native-sound/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SoundPackage(ctx)
  ];
}
```

### 5.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

The content of this document has been verified based on the following version：

1. RNOH: 0.72.28; SDK: HarmonyOS-NEXT-DB1 5.0.0.31; IDE: DevEco Studio 5.0.3.500; ROM: 3.0.0.25;
2. RNOH: 0.77.18; SDK: HarmonyOS-5.1.1.208(API19); IDE: DevEco Studio 5.1.1.830; ROM: 6.0.0.112 SP12;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                               | Type   | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| setActive                | Set the device activation status           | function | No       | iOS       | no               |
| setCategory              | Set the device activation status            | function | No       | iOS、Android | no               |
| enable                   | Enable or disable audio playback           | function  | No       | iOS       | no               |
| enableInSilenceMode      | Whether to enable playback in silence mode | function  | No       | iOS       | no               |
| setMode                  | Set session mode                            | function  | No       | iOS       | no               |
| setSpeakerphoneOn       | Set up speakers                          | function  | No       | Android       | no               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                              | Type    | Required | Platform    | HarmonyOS Support |
| ------------------------| ---------------------------------------- | ------- | -------- | ----------- | ----------------- |
| play                    | Start playing audio.                     | function  | No       | iOS、Android | yes               |
| pause                   | Pause audio playback.                    | function  | No       | iOS、Android | yes               |
| stop                    | Stop playing audio.                      | function  | No       | iOS、Android | yes               |
| reset                   | Reset Audio Status.                      | function  | No       | Android      | yes               |
| release                 | Releasing audio resources.               | function  | No       | iOS、Android | yes               |
| getVolume               | Obtains the audio volume.                | function  | No       | iOS、Android | yes               |
| setVolume               | Setting the Relative Audio Volume.       | function  | No       | iOS、Android | yes               |
| getCurrentTime          | Obtains the current playback time point. | function  | No       | iOS、Android | yes               |
| setCurrentTime          | Sets the playback time point.            | function  | No       | iOS、Android | yes               |
| getSpeed                | Obtains the playback speed.              | function  | No       | iOS、Android | yes               |
| setSpeed                | Setting the Playback Speed               | function  | No       | iOS、Android | yes               |
| getFilename             | Obtains the audio file name              | function  | No       | iOS、Android | yes               |
| getDuration             | Obtains the audio duration               | function  | No       | iOS、Android | yes               |
| getNumberOfLoops        | Obtains whether the audio loops          | function | No       | iOS、Android | yes               |
| setNumberOfLoops        | Sets whether the audio loops             | function | No       | iOS、Android | yes               |
| isPlaying               | Whether the audio is being played        |function  | No       | iOS、Android | yes               |
| isLoaded                | Is loading completed                     | function  | No       | iOS、Android | yes               |
| getPitch                | get pitch                                | function  | No       | Android      | no               |
| setPitch                | Set pitch                                | function  | No       | Android      | no               |
| getPan                  | set left and right channel balance       | function  | No  | iOS、Android      | no               |
| setPan                  | set left and right channel balance       | function  | No  | iOS、Android      | no               |
| getSystemVolume         | set system volume                        | function  | No       | iOS、Android       | no               |
| setSystemVolume         | set system volume                        | function  | No       | iOS、Android       | no               |
| getNumberOfChannels      | get the number of channels              | function  | No       | iOS、Android       | no               |

## Known Issues

- [ ] The **getNumberOfChannels**, **setSystemVolume**, **getSystemVolume**, **setPan**, **getPan**, **setPitch**, **getPitch**, **setSpeakerphoneOn**, **setMode**, **enableInSilenceMode**, **enable**, **setCategory**, and **setActive** methods do not have corresponding APIs on HarmonyOS: [issue#1](https://github.com/react-native-oh-library/react-native-sound/issues/21).

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/zmxv/react-native-sound/blob/master/LICENSE).

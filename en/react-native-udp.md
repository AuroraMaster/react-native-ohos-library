> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-udp</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tradle/react-native-udp">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tradle/react-native-udp/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-udp)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=4.1.7-0.0.2@deprecated | [@react-native-oh-tpl/react-native-udp Releases(deprecated)](https://github.com/react-native-oh-library/react-native-udp/releases) | 0.72       |
| 4.1.8             | [@react-native-ohos/react-native-udp Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-udp/releases)   | 0.72       |
| 4.2.0             | [@react-native-ohos/react-native-udp Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-udp/releases)   | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



#### **npm**

```bash
npm install @react-native-ohos/react-native-udp
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-udp
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { ScrollView, StyleSheet, Text, View } from "react-native";

import dgram from "react-native-udp";

function randomPort() {
  return (Math.random() * 60536) | (0 + 5000); // 60536-65536
}

function toByteArray(obj) {
  var uint = new Uint8Array(obj.length);
  for (var i = 0, l = obj.length; i < l; i++) {
    uint[i] = obj.charCodeAt(i);
  }

  return new Uint8Array(uint);
}

class App extends Component {
  constructor(props) {
    super(props);

    this.updateChatter = this.updateChatter.bind(this);
    this.state = { chatter: [] };
  }

  updateChatter(msg) {
    this.setState({
      chatter: this.state.chatter.concat([msg]),
    });
  }

  componentDidMount() {
    let self = this;

    let a = dgram.createSocket("udp4");
    let aPort = randomPort();
    a.bind(aPort, function (err) {
      if (err) throw err;
      self.updateChatter("a bound to " + JSON.stringify(a.address()));
    });

    let b = dgram.createSocket("udp4");
    var bPort = randomPort();
    b.bind(bPort, function (err) {
      if (err) throw err;
      self.updateChatter("b bound to " + JSON.stringify(b.address()));
    });

    a.on("message", function (data, rinfo) {
      var str = String.fromCharCode.apply(null, new Uint8Array(data));
      self.updateChatter(
        "a received echo " + str + " " + JSON.stringify(rinfo)
      );
      a.close();
      b.close();
    });

    b.on("message", function (data, rinfo) {
      var str = String.fromCharCode.apply(null, new Uint8Array(data));
      self.updateChatter("b received " + str + " " + JSON.stringify(rinfo));

      // echo back
      b.send(data, 0, data.length, aPort, "127.0.0.1", function (err) {
        if (err) throw err;
        self.updateChatter("b echoed data");
      });
    });

    b.once("listening", function () {
      var msg = toByteArray("hello");
      a.send(msg, 0, msg.length, bPort, "127.0.0.1", function (err) {
        if (err) throw err;
        self.updateChatter("a sent data");
      });
    });
  }

  render() {
    return (
      <View style={styles.container}>
        <ScrollView>
          {this.state.chatter.map((msg, index) => {
            return (
              <Text key={index} style={styles.welcome}>
                {msg}
              </Text>
            );
          })}
        </ScrollView>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  instructions: {
    textAlign: "center",
    color: "#333333",
    marginBottom: 5,
  },
});

export default App;
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                           | is supporte autolink  | Supported RN Version |
|---------------------------|-----------------------|----------------------|
| ~4.2.0                    |  No                   |  0.77                |
| ~4.1.8                    |  Yes                  |  0.72                |
| <= 4.1.7-0.0.2@deprecated |  No                   |  0.72                |

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
    "@react-native-ohos/react-native-udp": "file:../../node_modules/@react-native-ohos/react-native-udp/harmony/react_native_udp.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configure CMakeLists and introduce UdpPackage

> [!TIP] If using version <=4.1.7-0.0.2, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add：

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-udp/src/main/cpp" ./rnoh_udp)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_udp)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "UdpPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<UdpPackage>(ctx),
    };
}
```

### 4.Introducing RNUdpPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import {RNUdpPackage} from '@react-native-ohos/react-native-udp/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNUdpPackage(ctx)
  ];
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

The following combinations have been verified:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                                                                                                      | Type     | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| createSocket   | Creates a Socket object.                                                                                                                         | Function | false    | Android/iOS | yes               |
| close          | Close the underlying socket and stop listening for data on it. If a callback is provided.                                                        | Function | false    | Android/iOS | yes               |
| bind           | For UDP sockets, causes the `UdpSocket` to listen for datagram messages on a named `port`.                                                       | Function | false    | Android/iOS | yes               |
| send           | Broadcasts a datagram on the socket.                                                                                                             | Function | false    | Android/iOS | yes               |
| address        | Returns an object containing the address information for a socket.                                                                               | Function | false    | Android/iOS | yes               |
| setBroadcast   | Sets or clears the `SO_BROADCAST` socket option.                                                                                                 | Function | false    | Android/iOS | yes               |
| addMembership  | Tells the kernel to join a multicast group at the given `multicastAddress` and `multicastInterface` using the `IP_ADD_MEMBERSHIP` socket option. | Function | false    | Android/iOS | yes               |
| dropMembership | Instructs the kernel to leave a multicast group at `multicastAddress` using the `IP_DROP_MEMBERSHIP` socket option.                              | Function | false    | Android/iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/tradle/react-native-udp/blob/master/LICENSE).
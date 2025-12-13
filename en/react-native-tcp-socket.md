> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tcp-socket</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Rapsssito/react-native-tcp-socket">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Rapsssito/react-native-tcp-socket/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github Address](https://github.com/react-native-oh-library/react-native-tcp-socket)

## Installation & Usage

Please check the corresponding version information in the third-party library's Releases:

| Third-party Version | Release Information | Supported RN Version |
| ------------------- | ------------------- | -------------------- |
| <= 6.2.0-0.0.3@deprecated | [@react-native-oh-tpl/react-native-tcp-socket Releases(deprecated)](https://github.com/react-native-oh-library/react-native-tcp-socket/releases) | 0.72 |
| 6.2.1 | [@react-native-ohos/react-native-tcp-socket Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-tcp-socket/releases) | 0.72 |
| 6.3.1 | [@react-native-ohos/react-native-tcp-socket Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-tcp-socket/releases) | 0.77 |

For older versions not published to npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Navigate to your project directory and run the following command:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-tcp-socket
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-tcp-socket
```

<!-- tabs:end -->

The following code demonstrates basic usage scenarios of this library:

> [!WARNING] The import library name remains unchanged during use.

```js
import React, {useState} from 'react';
import {StyleSheet, TouchableOpacity, FlatList, Text, View} from 'react-native';
import TcpSocket from 'react-native-tcp-socket';

const ca = `-----BEGIN CERTIFICATE-----
MIIFOTCCAyGgAwIBAgIUZiAx4QlvsVTwoSPJCW7oHBut1aEwDQYJKoZIhvcNAQEL
BQAwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgMClNvbWUtU3RhdGUxITAfBgNVBAoM
GEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDAeFw0yNDA4MjkxMTU5MzNaFw0yNDA5
MjgxMTU5MzNaMEUxCzAJBgNVBAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEw
HwYDVQQKDBhJbnRlcm5ldCBXaWRnaXRzIFB0eSBMdGQwggIiMA0GCSqGSIb3DQEB
AQUAA4ICDwAwggIKAoICAQC7zpsawfWsf0A4D+A2apWo87oleyYIEyi5nZo6Bo+8
Sp9dO0qFPBfVvRjDLW/E2ZRcb22I4KUNp6bXv8AvqDWRkiCsI19uuZ4CapLTLPvw
mJeJICr/ol6NIHNUMBHAW8LshojTOA9Tu5l1qw34kMVZokT/2b98FIk0z0xaPjpR
8YMYOIGHJO0J2zV3qQS60C8tvaJNvAwjhvu59J897I4putQsfnU5+xO7gsTYh4md
mzDxCMBbfxMnexwpnAXIpxvlUXpdoMZf2KV1qetEZ539qDKCvsj20ejpAHWJnbJs
uR4ZXroXer1413XzRmn9xISllq2Z3c4QX5OmCLusXwi5yrTDvs/M0PNjMsnMm1O/
OvjZznAQ8c6FnUYAGKf4K2q7HKSIn45kTrvPVeLNvb42xhQ3B5luuTraNr/oTRTK
nrteBSf3LYeK8YLCZlF9nm2ppJkV90xl7RCatU0MqmGx/VCe5b7EGgpxj8fnEm5V
GbyJ+8B5ruOLoPynejgp/2S2LdfS1oBvqdAZfjeu6sJDLS95vKUpPDoNFe4FZgFr
N3V2alzocX5D2vHacOGR2XBqZ33w53KwekPuq3hMnC9X+gCJCp/WfSBqArbcEUWF
2++Ps5cO8tJ2aq0AzD2N7epEbc6LXolXAfv1JyHszjcE5cF4CzOTMntd8BBiFxXl
YwIDAQABoyEwHzAdBgNVHQ4EFgQUtfcXe+EBtuSZNdHTxf/mFJickCswDQYJKoZI
hvcNAQELBQADggIBAI3DKyh/ylg4gzlIA5SYMlC0wFCv5rMyXAbfJHebLIs/iqEV
L+Gs9TvQnGXqcR2Rk86CgxA+4kpqOhhVOrzSO6t6YbLTZf3lxBME0p2kmbs65Llx
FFAXe5Lyg1mPWU5cgXdZ0sakf9uc16mtl6VpYnTw9aAGMdF0JSPYNbU/o734Ze+q
1GlEdsrBP3pOrmF04WVSgfdUCKqdksP8Gq1tU/pGDpT2UkzQGh+ZDz8VQePsKzAd
hgDMJbKapgEjE1cRyHAKU0JhmhRMoSXAz5svVpYm/q1dgvqi7TamoftJfXsMsOaW
eFlvUzOcS77eIE4hN2kL+fpBRwiAx8pli2RnKzd0yFnhb/LG32nwDmYhzGOMrHOO
JfpU4tWVVrIp9yY6IKRXGsj4XQ//5ofnAySTSpu4H9wOCY4o+UCv/OGx17PJT7E+
e2gyq9FGyUZg0j+GBxjlzhT32WIhpCuWqr5dTWnIlXQJSVk3RIY+zuGVOh+H6Nby
zAXyUbWUStdw8dj24PDJK89a9qCmswNTGhu7cOeOId0wxYqqkY5G6J0j57Wo1CUG
QBxQ0dpH79QAjXOAG0zE3E1ci/Sd8Nb99OSygn/Y6l0379PKkUMb6ic6G08snn00
Z3cbzglkWavGfLsNHv4r2tptJTn003Cvd8w1gYSViOA1wd3JN/e3qZPPraIM
-----END CERTIFICATE-----`;

const serverKey = `-----BEGIN PRIVATE KEY-----
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
06v4n5pCSJDPebsNaecm5HETSwAfsg==
-----END PRIVATE KEY-----`;

const keystore = require('./ca/server-keystore.p12');

interface Message {
  id: number;
  text: string;
  user: string;
}

const getNowTime = () => {
  let date = new Date();
  let hours = date.getHours();
  let minutes = date.getMinutes();
  let seconds = date.getSeconds();
  return `${hours}:${minutes}:${seconds}`;
};

let server: any = null;
let client: any = null;

let testCase = 1;

export const TcpSocketDemo = () => {
  const [messages, setMessages] = useState<Message[]>([]);

  const sendMessage = (msg: string, user: string) => {
    let newMessage = {
      id: Date.now(),
      text: msg,
      user: user,
    };
    setMessages([...messages, newMessage]);
  };

  const createTcpServer = () => {

    server = new TcpSocket.Server();

    server.listen({port: 0, host: '127.0.0.1', reuseAddress: true}, () => {
      const port = server.address()?.port;
      if (!port) throw new Error('Server port not found');
      console.log('TcpSocketDemo:tcpServer start listen success on:'+port);
    });

    server.on('connection', (socket: any) => {
      console.log('TcpSocketDemo:tcpServer on connection!');
      socket.on('data', (data: any) => {
        switch (testCase) {
          case 1:
            console.log(
              'TcpSocketDemo:tcpServer received data:' + JSON.stringify(data),
            );
            sendMessage(`received data: ${data}`, 'tcpServer');
            let time = getNowTime();
            socket.write(`${time} Hello, tcpClient!`);
            break;
          case 2:
            console.log(
              `TcpSocketDemo:tcpServer Received ${data.length} bytes of data.`,
            );
            socket.pause();
            console.log(
              'TcpSocketDemo:tcpServer There will be no additional data for 1 second.',
            );
            setTimeout(() => {
              console.log(
                'TcpSocketDemo:tcpServer Now data will start flowing again.',
              );
              socket.resume();
            }, 1000);
            break;
          case 3:
            let dataLen = data.length;
            let time1 = getNowTime();
            console.log(
              'TcpSocketDemo:tcpServer client received data: ' +
                dataLen +
                ' bytes',
            );
            sendMessage(
              `${time1} received data: ${dataLen} bytes`,
              'tcpServer',
            );
            break;
          default:
            console.log(
              'TcpSocketDemo:tcpServer socket received data:' +
                JSON.stringify(data),
            );
        }
      });
      socket.on('error', (error: any) => {
        let errorMsg = '';
        if (error) {
          errorMsg = JSON.stringify(error);
        }
        console.log('TcpSocketDemo:tcpServer socket on error ' + errorMsg);
      });

      socket.on('close', (error: any) => {
        let errorMsg = '';
        if (error) {
          errorMsg = JSON.stringify(error);
        }
        console.log('TcpSocketDemo:tcpServer socket on close ' + errorMsg);
      });
    });

    server.on('error', (error: any) => {
      console.log('TcpSocketDemo:tcpServer on error ' + JSON.stringify(error));
    });

    server.on('close', () => {
      console.log('TcpSocketDemo:tcpServer closed');
    });
  };

  const createTcpClient = () => {

    client = new TcpSocket.Socket();

    const port = server.address()?.port;
    if (!port) throw new Error('Server port not found');

    let options = {
      port: port,
      host: '127.0.0.1',
      localAddress: '127.0.0.1',
      reuseAddress: true,
      localPort: 20000,
      interface: 'wifi',
    };
    client.connect(options, () => {
      console.log('TcpSocketDemo:tcpClient connect success');
    });
    client.on('data', (data: any) => {
      console.log(
        'TcpSocketDemo:tcpClient received data: ' +
          (data.length < 500 ? data : data.length + ' bytes'),
      );
      sendMessage(`received data: ${data}`, 'tcpClient');
    });

    client.on('connect', () => {
      console.log(
        'TcpSocketDemo:tcpClient on connect:' +
          JSON.stringify(client.address()),
      );
    });

    client.on('drain', () => {
      console.log('TcpSocketDemo:tcpClient drained');
    });

    client.on('error', (error: any) => {
      if (error) {
        console.log('TcpSocketDemo:tcpClient error ' + JSON.stringify(error));
      }
    });

    client.on('close', (error: any) => {
      let errorMsg = '';
      if (error) {
        errorMsg = JSON.stringify(error);
      }
      console.log('TcpSocketDemo:tcpClient closed ' + errorMsg);
    });
  };

  const tcpSendData = () => {
    testCase = 1;
    let time = getNowTime();
    client.write(`${time} Hello, tcpServer!`);
  };

  const tcpClose = () => {
    client.destroy();
    server.close();
    client = null;
    server = null;
  };

  const tcpPauseResume = () => {
    testCase = 2;
    let i = 0;
    const MAX_ITER = 3000;
    write();
    async function write() {
      let ok = true;
      while (i <= MAX_ITER && ok) {
        i++;
        const buff = ' ->' + i + '<- ';
        ok = client.write(buff);
      }
      if (!ok) {
        client.once('drain', write);
      }
    }
  };

  const tcpLongData = () => {
    testCase = 3;
    const hugeData = 'x'.repeat(5 * 1024);
    client.end(hugeData, 'utf8');
    console.log('TcpSocketDemo:tcpClient end hugeData...');
  };

  const createTlsServer = () => {

    server = new TcpSocket.TLSServer();
    server.setSecureContext({
      key: serverKey,
      cert: ca,
      keystore: keystore,
    });
    server.on('secureConnection', (socket: any) => {
      console.log(
        'TcpSocketDemo:TlsServer on secureConnection:' +
          JSON.stringify(socket.address()),
      );
      socket.on('data', (data: any) => {

        switch (testCase) {
          case 1:
            console.log(
              'TcpSocketDemo:tlsServer received data:' + JSON.stringify(data),
            );
            sendMessage(`received data: ${data}`, 'tlsServer');
            let time = getNowTime();
            socket.write(`${time} Hello, tlsClient!`);
            break;
          case 2:
            console.log(
              `TcpSocketDemo:tlsServer Received ${data.length} bytes of data.`,
            );
            socket.pause();
            console.log(
              'TcpSocketDemo:tlsServer There will be no additional data for 1 second.',
            );
            setTimeout(() => {
              console.log(
                'TcpSocketDemo:tlsServer Now data will start flowing again.',
              );
              socket.resume();
            }, 1000);
            break;
          case 3:
            let dataLen = data.length;
            let time1 = getNowTime();
            console.log(
              'TcpSocketDemo:tlsServer client received data: ' +
                dataLen +
                ' bytes',
            );
            sendMessage(
              `${time1} received data: ${dataLen} bytes`,
              'tlsServer',
            );
            break;
          default:
            console.log(
              'TcpSocketDemo:tlsServer socket received data:' +
                JSON.stringify(data),
            );
        }
      });
      socket.on('error', (error: any) => {
        console.log(
          'TcpSocketDemo:TlsServer secureConnection socket error ' +
            JSON.stringify(error),
        );
      });

      socket.on('close', (error: any) => {
        console.log(
          'TcpSocketDemo:TlsServer secureConnection socket closed ' +
            (error ? JSON.stringify(error) : ''),
        );
      });
    });

    server.on('error', (error: any) => {
      console.log('TcpSocketDemo:TlsServer on error ' + JSON.stringify(error));
    });

    server.on('close', () => {
      console.log('TcpSocketDemo:TlsServer closed');
    });

    server.listen({port: 9999, host: '127.0.0.1', reuseAddress: true}, () => {
      console.log('TcpSocketDemo:tlsServer start listen success!');
    });
  };

  const createTlsClient = () => {

    let clientSocket = new TcpSocket.Socket();

    client = new TcpSocket.TLSSocket(clientSocket, {ca});
    clientSocket.on('error', error => {
      console.log(
        'TcpSocketDemo:TlsClient clientSocket error',
        error ? JSON.stringify(error) : '',
      );
    });

    clientSocket.on('close', hadError => {
      console.log(
        'TcpSocketDemo:TlsClient clientSocket close ' +
          (hadError ? JSON.stringify(hadError) : ''),
      );
    });

    clientSocket.connect(
      {
        port: 9999,
        host: '127.0.0.1',
        reuseAddress: true,
        localPort: 20000,
        interface: 'wifi',
      },
      () => {
        console.log('TcpSocketDemo:TlsClient clientSocket connect success.');
      },
    );
    client.on('secureConnect', () => {
      console.log(
        'TcpSocketDemo:TlsClient on secureConnect:' +
          JSON.stringify(client.address()),
      );
    });

    client.on('connect', () => {
      console.log(
        'TcpSocketDemo:TlsClient on connect:' +
          JSON.stringify(client.address()),
      );
    });

    client.on('drain', () => {
      console.log('TcpSocketDemo:TlsClient Client drained');
    });

    client.on('data', (data: any) => {
      console.log(
        'TcpSocketDemo:TlsClient received data: ' +
          (data.length < 500 ? data : data.length + ' bytes'),
      );
      sendMessage(
        `received data: ${data.length < 500 ? data : data.length + ' bytes'}`,
        'tlsClient',
      );
    });

    client.on('error', (error: any) => {
      console.log('TcpSocketDemo:TlsClient error ' + JSON.stringify(error));
    });

    client.on('close', (error: any) => {
      console.log(
        'cpSocketDemo:TlsClient closed ' + (error ? JSON.stringify(error) : ''),
      );
    });
  };

  return (
    <View style={styles.container}>
      <FlatList
        data={messages}
        renderItem={({item}) => (
          <View style={styles.message}>
            <Text style={styles.messageText}>
              {item?.user}: {item?.text}
            </Text>
          </View>
        )}
        keyExtractor={item => item.id.toString()}
      />
      <TouchableOpacity onPress={createTcpServer} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Create TCP Server</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={createTcpClient} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Create TCP Client</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={tcpSendData} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Client-Server Communication</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={tcpPauseResume} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Data Pause & Resume</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={tcpLongData} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Long Data Transfer</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={tcpClose} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Close Connection</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={createTlsServer} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Create TLS Server</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={createTlsClient} style={styles.moduleButton}>
        <Text style={styles.buttonText}>Create TLS Client</Text>
      </TouchableOpacity>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff',
  },
  message: {
    marginVertical: 10,
    padding: 10,
    backgroundColor: '#aaa',
  },
  messageText: {
    fontSize: 16,
  },
  moduleButton: {
    marginBottom: 5,
    backgroundColor: 'deepskyblue',
    height: 34,
    borderRadius: 10,
  },
  buttonText: {
    fontSize: 18,
    fontWeight: '400',
    color: '#fff',
    textAlign: 'center',
    lineHeight: 32,
    verticalAlign: 'middle',
  },
});
```

## Using Codegen

This library has been adapted for `Codegen`. Before use, you need to actively execute the command to generate the third-party library bridging code. Please refer to the [Codegen Usage Documentation](/zh-cn/codegen.md) for details.

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~6.3.1                               |  No              |  0.77     |
| ~6.2.1                               |  Yes             |  0.72     |
| <= 6.2.0-0.0.3@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 1. Add the overrides field to the root `oh-package.json5`

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Import Native Code

There are currently two methods:

1. Import via har package (Recommended until IDE functionality is improved);
2. Link source code directly.

Method 1: Import via har package (Recommended)

> [!TIP] The har package is located in the `harmony` folder of the installed third-party library path.

Open `entry/oh-package.json5` and add the following dependencies:

```JSON
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-ohos/react-native-tcp-socket": "file:../../node_modules/@react-native-ohos/react-native-tcp-socket/harmony/tcp_socket.har"
  }
```

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link Source Code Directly

> [!TIP] If you need to link source code directly, please refer to the [Direct Link Source Code Guide](/zh-cn/link-source-code.md).

### 3. Configure CMakeLists and Import TcpSocketPackage

> If you are using version <= 6.2.0-0.0.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-tcp-socket/src/main/cpp" ./tcp-socket)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_tcp_socket)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```c++
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "TcpSocketPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<TcpSocketPackage>(ctx)
    };
}
```

### 4. Import TcpSocketPackage on the ArkTS Side

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
+ import {TcpSocketPackage} from '@react-native-ohos/react-native-tcp-socket/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [new SamplePackage(ctx),
+   new TcpSocketPackage(ctx)
  ];
}
```
</details>

## Running

Click the `sync` button in the top right corner.

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## Constraints & Limitations

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements

Requires network information permission: "ohos.permission.GET_NETWORK_INFO" and internet usage permission: "ohos.permission.INTERNET". Configure as follows:

Open `entry/src/main/module.json5` and add:

```json
"requestPermissions": [
     ...
     {
        "name": "ohos.permission.INTERNET"
      },
      {
        "name": "ohos.permission.GET_NETWORK_INFO"
      }
]
```

## API

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for that property.

> [!TIP] The "HarmonyOS Support" column: 'Yes' means the property is supported on the HarmonyOS platform; 'No' means it is not supported; 'partially' means partial support. The usage method is consistent across platforms, with effects benchmarked against iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---------------------------------------------------------- | --------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| connect(options, callback) | Same as createConnection, Creating a TCP Socket | function | No | Android,iOS | Yes |
| createServer(connectionListener) | Creating a TCP Server | function | No | Android,iOS | Yes |
| createServer(options，connectionListener)<sup>6.3.1+</sup> | Creating a TCP Server | function | No | Android,iOS | Yes |
| createConnection(options, callback) | Creating a TCP Socket | function | No | Android,iOS | Yes |
| createTLSServer(options, connectionListener) | Creating a TLS-based TCP Server | function | No | Android,iOS | Yes |
| connectTLS | Creating a TLS-based encrypted connection | function | No | Android,iOS | Yes |
| isIP | Check whether a character string is an IP address | function | No | Android,iOS | Yes |
| isIPv4 | Check whether a character string is an IPv4 address | function | No | Android,iOS | Yes |
| isIPv6 | Check whether a character string is an IPv6 address | function | No | Android,iOS | Yes |
| Server | TCP Server Object | object | No | Android,iOS | Yes |
| Socket | TCP Socket Object | object | No | Android,iOS | Yes |
| TLSServer | TLS Server Object | object | No | Android,iOS | Yes |
| TLSSocket | TLS Socket Object | object | No | Android,iOS | Yes |

### Server

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ----------------- |
| address() | Returns the bound address, address family name, and port of the server | function | No | Android,iOS | Yes |
| listen(options, callback) | Start a server listening for connections | function | No | Android,iOS | Yes |
| close(callback) | Stops the server from accepting new connections and keeps existing connections | function | No | Android,iOS | Yes |
| getConnections(callback) | Asynchronously get the number of concurrent connections on the server | function | No | Android,iOS | Yes |
| listening | whether to enable the listening | boolean | No | Android,iOS | Yes |
| on('close') | Triggered when the server is shut down | event | No | Android,iOS | Yes |
| on('connection') | Triggered when the server receives a new connection | event | No | Android,iOS | Yes |
| on('error') | Triggered when an error occurs on the server | event | No | Android,iOS | Yes |
| on('listening') | Triggered when the server starts listening | event | No | Android,iOS | Yes |

### Socket
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ---- | ---- | -------- | ---- | -------- |
| address() | Returns the bound address, address family name and port of the socket | function | No | Android,iOS | Yes |
| destroy() | Ensures that no more I/O activity happens on this socket. Destroys the stream and closes the connection | function | No | Android,iOS | Yes |
| end() | Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data | function | No | Android,iOS | Yes |
| setEncoding(encoding) | Set the encoding for the socket as a Readable Stream. By default, no encoding is assigned and stream data will be returned as `Buffer` objects | function | No | Android,iOS | Yes |
| setNoDelay(noDelay) | Set no delay | function | No | Android,iOS | Yes |
| setTimeout() | Sets the socket to timeout after `timeout` milliseconds of inactivity on the socket. By default `TcpSocket` do not have a timeout | function | No | Android,iOS | Yes |
| write(buffer, encoding, cb) | Sends data on the socket. The second parameter specifies the encoding in the case of a string — it defaults to UTF8 encoding | function | No | Android,iOS | Yes |
| pause() | Pauses the reading of data. That is, `'data'` events will not be emitted. Useful to throttle back an upload | function | No | Android,iOS | Yes |
| resume() | Resumes reading after a call to `socket.pause()` | function | No | Android,iOS | Yes |
| writableNeedDrain | whether need to wait for data to be written to the socket | boolean | No | Android,iOS | Yes |
| bytesRead | Indicates the number of bytes of data that have been read from the socket | number | No | Android,iOS | Yes |
| bytesWritten | get the number of bytes last written to the socket | number | No | Android,iOS | Yes |
| connecting | whether the current socket is being connected | boolean | No | Android,iOS | Yes |
| destroyed | Whether the socket has been destroyed | boolean | No | Android,iOS | Yes |
| localAddress | Local ip address | string | No | Android,iOS | Yes |
| localPort | Local port | number | No | Android,iOS | Yes |
| remoteAddress | remote server IP address | string | No | Android,iOS | Yes |
| remoteFamily | remote server IP address type | string | No | Android,iOS | Yes |
| remotePort | remote server port | number | No | Android,iOS | Yes |
| pending | Whether has pending data to be sent to the remote server | boolean | No | Android,iOS | Yes |
| timeout | The timeout period for the socket, in milliseconds. The default timeout period is 30 seconds | number | No | Android,iOS | Yes |
| readyState | the state of socket,`0`: not connected,`1`:connected,2: closing,3:closed | number | No | Android,iOS | Yes |
| on('pause') | Triggered when pauses the reading of data | event | No | Android,iOS | Yes |
| on('resume') | Triggered when Resumes the reading of data | event | No | Android,iOS | Yes |
| on('close') | Triggered when socket is closed | event | No | Android,iOS | Yes |
| on('connect') | Triggered when socket is connected | event | No | Android,iOS | Yes |
| on('data') | Triggered when socket receives data | event | No | Android,iOS | Yes |
| on('drain') | Triggered when the buffer becomes empty, indicating that data can be written to the socket | event | No | Android,iOS | Yes |
| on('error') | Triggered when an error occurs on the socket | event | No | Android,iOS | Yes |
| on('timeout') | Triggered When the connection or data transmission times out | event | No | Android,iOS | Yes |

### TLSServer

[!TIP] TLSServer inherits from the Server object and has all properties, methods, and events of the Server object. Only its unique properties are listed below.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ---- | ---- | -------- | ---- | -------- |
| setSecureContext(options) | Set Security Context | function | No | Android,iOS | Yes |
| on('secureConnection') | Triggered When a secure TLS connection is established | event | No | Android,iOS | Yes |

### TLSSocket

[!TIP] TLSSocket inherits from the Socket object and has all properties, methods, and events of the Socket object. Only its unique properties are listed below.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ---- | ---- | -------- | ---- | -------- |
| getCertificate() | Get Local Certificate Information | function | No | Android | Yes |
| getPeerCertificate() | Get the Certificate Information of the Remote Server | function | No | Android | Yes |
| on('secureConnect') | Triggered When a secure connection is established | event | No | Android,iOS | Yes |

## Known Issues

- [ ] Currently unable to implement multithreading: [issue#3](https://github.com/react-native-oh-library/react-native-tcp-socket/issues/3)
- [ ] Certificate retrieval only has an async interface, currently returns a promise, inconsistent with the synchronous interface on Android: [issue#4](https://github.com/react-native-oh-library/react-native-tcp-socket/issues/4)

## Others

## License

This project is based on [The MIT License (MIT)](https://github.com/Rapsssito/react-native-tcp-socket/blob/master/LICENSE). Feel free to enjoy and contribute to open source.
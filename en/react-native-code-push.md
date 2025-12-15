> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-code-push</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/microsoft/react-native-code-push">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/microsoft/react-native-code-push/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-code-push)

The repository for this third-party library has been migrated to Gitcode, and it now supports direct download from npm. The new package name is: `@react-native-ohos/react-native-code-push`. The specific version relationships are as follows:

| Version                        | Package Name       | Repository          |  Release            |Supported RN Version  |
| ------------------------------ | ----------------   | ------------------- | ------------------- | -------------------- |
| <= 8.2.2-0.0.10@deprecated  |@react-native-oh-tpl/react-native-code-push|[Github](https://github.com/react-native-oh-library/react-native-code-push/releases) | [Github Releases](https://github.com/react-native-oh-library/react-native-code-push/releases) | 0.72       |
| 8.2.3             | @react-native-ohos/react-native-code-push|[GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-code-push) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-code-push/releases)   | 0.72       |
| 9.0.2             | @react-native-ohos/react-native-code-push|[GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-code-push) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-code-push/releases)   | 0.77       |

## Pre-preparation

### code-push-cli

1. Clone the [code-push-cli](https://github.com/react-native-oh-library/code-push-cli) to the local host.
2. Run the `npm install` command in the code-push-cli directory.
3. Run the `npm run start` command in the code-push-cli directory to generate the `bin` directory.
4. npm install -g <code-push-cli directory>
5. Restart a terminal and run the `code-push -v` command. If the version number is displayed, the installation is successful.

Common commands for code-push-cli are as follows:

```
code-push -v
code-push login
code-push app list //List all apps under the account.
code-push app add <apppname> harmony react-native // Creating an Application
code-push release <AppName> <bundle.harmony.js> "< version number > "--description "<v1.0.0 test update >" -m //Packet sending command. Add -m to forcibly update the version. The asterisk (*) indicates all versions, for example, code-push release CodePush_Local ./bundle.harmony.js "*" --description "v1.0.0 Test Update"
```
```
Execute the following commands in the project directory:

code-push login <server_address> // Prerequisite: Server must be started (public network accessible)
This will open a webpage. Enter account and password (default account: admin, password: 123456)
Click "Get token"
Copy the token to the command line window
Prompt shows login successful

# Ensure the bundle file has minor modifications
echo "// Force update for 1.0.0 pending fix - $(date)" >> ./bundles/bundle.harmony.js

Modify the characters in "// Force update for 1.0.0 pending fix - $(date)" as needed

# Publish a mandatory update for version 1.0.0
code-push release MyApp-Harmony ./bundles/bundle.harmony.js 1.0.0 -d Staging --description "Force fix for issues" --mandatory

# Publish a non-mandatory update for version 1.0.0
code-push release MyApp-Harmony ./bundles/bundle.harmony.js 1.0.0 -d Staging --description "Non-mandatory fix for issues"

```
### code-push-server

1. Clone the [code-push-server](https://github.com/react-native-oh-library/code-push-server) to the local host.
2. Run the `npm install` command in the code-push-server directory.
3. Install the MySQL and Redis.
4. Modifying the `code-push-server/src/core/config.ts` Configuration File
5. Run the `npm run dev` command in the code-push-server directory to generate the `bin` directory.
6. Run the `npm run start` command in the code-push-server directory to start the service.
```
Install MySQL
# Ubuntu/Debian
sudo apt update
sudo apt install mysql-server
# Start service
sudo systemctl start mysql
sudo mysql_secure_installation
# Follow the prompts to set up:
# 1. Set root password
# 2. Remove anonymous users
# 3. Disallow remote root login
# 4. Remove test database
# 5. Reload privilege tables
First enter y/yes for all

# First log in to MySQL (no password required)
sudo mysql
# Execute in MySQL command line:
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_strong_password';
FLUSH PRIVILEGES;
EXIT;

# Now log in with password
mysql -u root -p
Enter password
EXIT;

# Edit configuration file
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
# Find bind-address and modify
# bind-address = 0.0.0.0  
# Allow all IP access
# Ctrl+S to save and exit automatically
# Restart MySQL

sudo systemctl restart mysql

Install Redis
sudo apt update
sudo apt install redis-server -y

# Start and enable service
sudo systemctl start redis-server
# Test
redis-cli ping 
Should reply PONG
# Edit Redis configuration file
sudo nano /etc/redis/redis.conf

# Find and modify the following lines:
# bind 0.0.0.0  # If remote access is needed
# protected-mode no  # If bind is set to 0.0.0.0, need to turn off protected mode
# Ctrl+S to save and exit automatically
# Restart Redis
sudo systemctl restart redis-server
```

```
Modify document sections
In the code-push-server directory, modify code-push-server/src/core/config.ts  <127.0.0.1>  Change to server address

In code-push-server/src/db.ts, for example:
    .example(
        '$0 init --dbname codepush --dbhost localhost (replace with server address) --dbuser root --dbpassword <password> (replace with database password) --dbport 3306 --force',
        'Initialize code-push-server database',
    )
In this file, replace all occurrences of 'localhost' with server address

Create bin directory (might prompt that database codepush is not created)
npm run dev (prompts that database codepush doesn't exist) Ctrl+C to force exit
Execute
npm run init  Success returns "success" and creates database codepush
Execute
npm run dev
```

## Installation and Usage

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-code-push
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-code-push
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { View, Text, StyleSheet, TouchableOpacity } from "react-native";
import CodePush from "react-native-code-push";
class App extends Component<any, any> {
  constructor(props: any) {
    super(props);
    this.state = {
      syncMessage: "",
      progress: {},
    };
  }
  componentDidMount() {
    console.log("Begin checking for updates.");
    this.syncImmediate(); 
  }
  syncImmediate() {
    CodePush.sync(
      {
        updateDialog: {
          appendReleaseDescription: true, 
          descriptionPrefix: "Update content:", 
          mandatoryContinueButtonLabel: "Update immediately.", 
          mandatoryUpdateMessage: "", 
          optionalIgnoreButtonLabel: "later", 
          optionalInstallButtonLabel: "Background update.",
          optionalUpdateMessage: "There's a new version available. Would you like to update?", 
          title: "Update notification.",
        },
      },
      this.codePushStatusDidChange.bind(this),
      this.codePushDownloadDidProgress.bind(this)
    );
  }

  codePushStatusDidChange(syncStatus: string | number) {
    switch (syncStatus) {
      case CodePush.SyncStatus.CHECKING_FOR_UPDATE:
        this.setState({ syncMessage: "Checking for update." });
        break;
      case CodePush.SyncStatus.DOWNLOADING_PACKAGE:
        this.setState({
          syncMessage: "Downloading package.",
          progressModalVisible: true,
        });
        break;
      case CodePush.SyncStatus.AWAITING_USER_ACTION:
        this.setState({ syncMessage: "Awaiting user action." });
        break;
      case CodePush.SyncStatus.INSTALLING_UPDATE:
        this.setState({
          syncMessage: "Installing update.",
          progressModalVisible: true,
        });
        break;
      case CodePush.SyncStatus.UP_TO_DATE:
        this.setState({ syncMessage: "App up to date.", progress: false });
        break;
      case CodePush.SyncStatus.UPDATE_IGNORED:
        this.setState({
          syncMessage: "Update cancelled by user.",
          progress: false,
        });
        break;
      case CodePush.SyncStatus.UPDATE_INSTALLED:
        this.setState({
          syncMessage: "Update installed and will be applied on restart.",
          progress: false,
        });
        break;
      case CodePush.SyncStatus.UNKNOWN_ERROR:
        this.setState({
          syncMessage: "An unknown error occurred.",
          progress: false,
        });
        break;
    }
  }

  codePushDownloadDidProgress(progress: any) {
    this.setState({ progress });
  }

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>Welcome to the hot update--test!</Text>
        <Text>SyncStatus: {this.state.syncMessage}</Text>
        <Text>{this.state.progressModalVisible.toString()}</Text>
        <TouchableOpacity onPress={this.syncImmediate.bind(this)}>
          <Text style={styles.syncButton}>Press for dialog-driven sync</Text>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    backgroundColor: "#F5FCFF",
    paddingTop: 10,
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  syncButton: {
    color: "green",
    fontSize: 17,
  },
});

let codePushOptions = { checkFrequency: CodePush.CheckFrequency.MANUAL };

export default CodePush(codePushOptions)(App);
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~9.0.2                              |  No              |  0.77     |
| ~8.2.3                              |  Yes             |  0.72     |
| <= 8.2.2-0.0.10@deprecated            |  No              |  0.72     |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

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

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-code-push": "file:../../node_modules/@react-native-ohos/react-native-code-push/harmony/codePush.har"
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

### 3. Introducing CodePushPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { CodePushPackage } from "@react-native-ohos/react-native-code-push/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CodePushPackage(ctx)
  ];
}
```

### 4. Configuring CMakeLists and Introducing CodePushPackage

> If you are using version <= 8.2.2-0.0.10, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-code-push/src/main/cpp" ./codePush)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_code_push)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CodePushPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<CodePushPackage>(ctx)
    };
}
```

### 5. Introduce the comparingVersion method on the ArkTs side

Open `entry/src/main/ets/pages/index.ets` and invoke the comparingVersion method to compare the code-push version number to clear historical sandbox resources during installation.

```diff
+ import { comparingVersion } from "@react-native-ohos/react-native-code-push";

@Entry
@Component
struct Index {

  aboutToAppear() {
+     comparingVersion(context);
  }
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

Modifying the `entry\src\main\ets\pages\Index.ets` file.

```diff
...
+ import common from '@ohos.app.ability.common';
+ import BuildProfile from 'BuildProfile';
+ let context = getContext(this) as common.UIAbilityContext;
+ interface CodePushConfig{
+  Staging:String;
+  Production:String;
+  ServerUrl:String;
+  PublicKey:String;
+ }
struct Index {
  @StorageLink('RNOHCoreContext') private rnohCoreContext: RNOHCoreContext | undefined = undefined
  @State shouldShow: boolean = false
  private logger!: RNOHLogger
+ bundlePath:string = 'bundle.harmony.js'
aboutToAppear() {
     ...
+   this.setCodeConfig()
    this.shouldShow = true
    stopTracing()
  }
+ setCodeConfig(){
+    const CodePushConfig: CodePushConfig = {
+      Staging:BuildProfile.Staging,
+      Production:BuildProfile.Production,
+      ServerUrl:BuildProfile.ServerUrl,
+      PublicKey:BuildProfile.PublicKey
+    }
+    AppStorage.SetOrCreate('CodePushConfig',CodePushConfig)
+  }
build() {
   Column() {
    ...
    RNApp({
    jsBundleProvider:new TraceJSBundleProviderDecorator(
            new AnyJSBundleProvider([
              new MetroJSBundleProvider(),
              // NOTE: to load the bundle from file, place it in
              // `/data/app/el2/100/base/com.rnoh.tester/files/bundle.harmony.js`
              // on your device. The path mismatch is due to app sandboxing on HarmonyOS
+              new FileJSBundleProvider(context.filesDir + '/Bundles/' + this.bundlePath),
              new FileJSBundleProvider('/data/storage/el2/base/files/bundle.harmony.js'),
              new ResourceJSBundleProvider(this.rnohCoreContext.uiAbilityContext.resourceManager, 'hermes_bundle.hbc'),
              new ResourceJSBundleProvider(this.rnohCoreContext.uiAbilityContext.resourceManager, 'bundle.harmony.js')
            ]),
            this.rnohCoreContext.logger),
    })

   }

}
```

Open `entry/build-profile.json5` and add configuration

```diff
{
  "apiType": 'stageMode',
  "buildOption": {
    "externalNativeOptions": {
      "path": "./src/main/cpp/CMakeLists.txt",
      "arguments": "",
      "cppFlags": "-s",
    },
+    "arkOptions": {
+      "buildProfileFields": {
+        "Staging": "", //Test Environment Key
+        "Production": "",//Production Environment Key
+        "ServerUrl": "",//Server address
+        "PublicKey": "PublicKey"
      }
    }
  },
  "targets": [
    {
      "name": "default",
      "runtimeOS": "HarmonyOS"
    },
    {
      "name": "ohosTest",
    }
  ]
}
```

Then build and run the code.

## Constraints

### Compatibility


To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## API

| Name              | Description                                                                                                                                                                                                                                                                               | Type     | Required | Platform    | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| sync              | Sync method, automatic mode update                                                                                                                                                                                                                                                        | function | yes      | Android IOS | yes               |
| getUpdateMetadata | Retrieve the metadata of the currently installed updates (RemotePackage). When using the sync method, there is no need to call this method as sync will automatically call it                                                                                                             | function | no       | Android iOS | yes               |
| restartApp        | Restart the app. When using the sync method, there is no need to call this method because sync will automatically call it                                                                                                                                                                 | function | no       | Android iOS | yes               |
| getCurrentPackage | Get application version information. When using the sync method, there is no need to call this method because sync will automatically call it                                                                                                                                             | function | no       | Android iOS | yes               |
| getConfiguration  | Get application configuration information, appVersion (version number), deploymentKey (deploymentKey), serverless URL (server address), and client UniqueId (unique identifier). When using the sync method, there is no need to call this method because sync will automatically call it | function | no       | Android iOS | yes               |

**updateDialog**

When using the **CodePush.updateDialog** method, the following parameters are optional, representing the updated dialog box and default to null

| Name                         | Description                                                                                                 | Type    | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| appendReleaseDescription     | Whether to display update description, default is false                                                     | boolean | no       | Android iOS | yes               |
| descriptionPrefix            | Update the prefix of the description. The default is "Description:                                          | string  | no       | Android iOS | yes               |
| mandatoryContinueButtonLabel | The button text for forced updates defaults to continue                                                     | string  | no       | Android iOS | yes               |
| mandatoryUpdateMessage       | Update notifications when forced to update Defaults to “An update is available that must be installed.”     | string  | no       | Android iOS | yes               |
| optionalIgnoreButtonLabel    | When updateDialog is not forced to update, the cancel button text defaults to ignore                        | string  | no       | Android iOS | yes               |
| optionalInstallButtonLabel   | When non mandatory updates occur, confirm the text Defaults to “Install”                                    | string  | no       | Android iOS | yes               |
| optionalUpdateMessage        | Update notifications when not mandatory Defaults to “An update is available. Would you like to install it?” | string  | no       | Android iOS | yes               |
| title                        | The title of the update notification to be displayed Defaults to “Update available”.                        | string  | no       | Android iOS | yes               |

**SyncStatus**

When using **CodePush.SyncStatus**, the codePushStatus DidChange callback function retrieves the application status

| Name                 | Description                                                                                                                                                                                       | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| UP_TO_DATE           | A value of 0 indicates that the application has been fully updated to the configured deployment,                                                                                                  | number | no       | Android iOS | yes               |
| UPDATE_INSTALLED     | A value of 1 indicates that an available update has been installed and will run immediately after the syncStatus ChangedCallback function returns or during the next application recovery/restart | number | no       | Android iOS | yes               |
| UNKNOWN_ERROR        | Value 3, unknown error detected during synchronization operation                                                                                                                                  | number | no       | Android iOS | yes               |
| CHECKING_FOR_UPDATE  | Value is 5, checking if there are any updates to the CodePush server                                                                                                                              | number | no       | Android iOS | yes               |
| AWAITING_USER_ACTION | The value is 6, there are updates available, and a confirmation dialog box is displayed to the end user. (Applicable only when used with updateDialog)                                            | number | no       | Android iOS | yes               |
| DOWNLOADING_PACKAGE  | A value of 7, available updates downloaded from CodePush server                                                                                                                                   | number | no       | Android iOS | yes               |
| INSTALLING_UPDATE    | Value is 8, available updates have been downloaded and will be installed                                                                                                                          | number | no       | Android iOS | yes               |

**installMode**

When using **CodePush.InstallMode**, the following parameters are optional: installMode

| Name            | Description        | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------ | ------ | -------- | ----------- | ----------------- |
| IMMEDIATE       | Directly update    | number | no       | Android iOS | yes               |
| ON_NEXT_RESTART | Next update launch | number | no       | Android iOS | yes               |
| ON_NEXT_RESUME  | Next update launch | number | no       | Android iOS | yes               |
| ON_NEXT_SUSPEND | Next update launch | number | no       | Android iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/microsoft/react-native-code-push/blob/master/LICENSE.md).

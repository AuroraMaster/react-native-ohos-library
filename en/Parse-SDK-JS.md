> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>Parse-SDK-JS</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/parse-community/Parse-SDK-JS">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/parse-community/Parse-SDK-JS/blob/alpha/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/parse-community/Parse-SDK-JS)

## Installation and Usage

> [!TIP] It requires supporting services and third-party dependencies

The Parse JS SDK is compatible with the following versions of Parse Server. For the setup of the Parse Server server, please refer to[https://github.com/parse-community/parse-server/blob/alpha/README.md](https://github.com/parse-community/parse-server/blob/alpha/README.md)。

|   Parse JS SDK   |   Parse Server   |
| :--------------: | :--------------: |
| >= 4.0.0 < 5.0.0 | >= 6.0.0 < 7.0.0 |
|     >= 5.0.0     |     >= 7.0.0     |

> [!TIP] This library depends on[@react-native-oh-tpl/async-storage](/zh-cn/react-native-async-storage-async-storage.md)、[@react-native-oh-tpl/react-native-get-random-values](/zh-cn/react-native-get-random-values.md)

Please go to the Releases release address of the third-party library to view the supporting version information: @react-native-ohos/pull-to-refresh Releases.

|Version |Support RN version|
| --------|---------- |
| 5.3.0   | 0.72/0.77 |

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install parse@5.3.0
```

#### **yarn**

```bash
yarn add parse@5.3.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```jsx
import React, { useState } from "react";
import { View, Text, Button, Alert, StyleSheet } from "react-native";
import AsyncStorage from "@react-native-async-storage/async-storage";
import Parse from "parse/react-native";

Parse.setAsyncStorage(AsyncStorage);
Parse.initialize("your appId", "your javaScriptKey", "your masterKey");
Parse.serverURL = "your parse server url";
Parse.CoreManager.set("REQUEST_HEADERS", {
  "X-Parse-REST-API-Key": "your RESTAPIKEY",
});

const ParseExample = () => {
  const [data, setData] = useState < any > [];

  async function saveData() {
    const TestObject = Parse.Object.extend("TestObject");
    const testObject = new TestObject();
    testObject.set("name", "Zhang San");
    testObject.set(
      "description",
      "I am Zhang San, created by rn using the parse sdk js library!"
    );

    try {
      const result = await testObject.save();
      if (result) {
        Alert.alert("Added successfully");
      } else {
        Alert.alert("Add failed");
      }
      console.log("Object saved successfully:", result);
    } catch (error) {
      console.error("Error while saving object:", error);
    }
  }
  async function deleteData() {
    const TestObject = Parse.Object.extend("TestObject");
    const query = new Parse.Query(TestObject);
    query.equalTo("name", "Li Si");
    try {
      const results = await query.first();
      if (results) {
        Parse.Object.destroyAll(results).then((res) => {
          Alert.alert("Delete successfully");
        });
      } else {
        Alert.alert("Li Si not found");
      }
    } catch (error) {
      console.error("Error while fetching objects:", error);
    }
  }
  async function updateData() {
    const TestObject = Parse.Object.extend("TestObject");
    const query = new Parse.Query(TestObject);
    try {
      query.equalTo("name", "Zhang San");
      const results = await query.first();
      if (results) {
        console.log(results, 666);
        results.set("name", "Li Si");
        results.set("description", "My name has been changed to Li Si");
        results.save().then((update) => {
          Alert.alert("Modified successfully");
        });
      } else {
        Alert.alert("Modified filed");
      }
    } catch (error) {
      console.error("Error while fetching objects:", error);
    }
  }

  async function fetchData() {
    const TestObject = Parse.Object.extend("TestObject");
    const query = new Parse.Query(TestObject);

    try {
      const results = await query.find();
      const resultJson = results.map((item) => item.toJSON());
      console.log("query was successful:", resultJson);
      setData(resultJson);
    } catch (error) {
      console.error("Error while fetching objects:", error);
    }
  }

  return (
    <View style={style.mainBox}>
      <Text style={{ fontSize: 18, fontWeight: "bold" }}>
        Simulate data for adding, deleting, modifying, and querying
      </Text>
      <Text style={{ fontSize: 16, fontWeight: "bold" }}>
        TestObject Class (Table)
      </Text>
      <View style={{ marginTop: 10, marginBottom: 10 }}>
        <Button
          title="Add one piece of data for Zhang San"
          onPress={saveData}
        />
      </View>
      <View style={{ marginBottom: 10 }}>
        <Button
          title="Delete a data entry with the name Li Si"
          onPress={deleteData}
        />
      </View>
      <View style={{ marginBottom: 10 }}>
        <Button
          title="Modify, change one Zhang San data to Li Si"
          onPress={updateData}
        />
      </View>
      <Button title="Query all data" onPress={fetchData} />
      <View style={style.showBox}>
        {data?.map((item) => {
          return (
            <View style={{ marginTop: 10 }} key={item.objectId}>
              <Text>name: {item?.name}</Text>
              <Text>description: {item?.description}</Text>
            </View>
          );
        })}
      </View>
    </View>
  );
};

const style = StyleSheet.create({
  mainBox: {
    borderWidth: 1,
    borderColor: "#ebebeb",
    padding: 10,
    marginTop: 10,
  },
  showBox: {
    backgroundColor: "#f5f5f5",
    marginTop: 10,
    padding: 10,
    borderWidth: 1,
    borderColor: "#ebebeb",
  },
});

export default ParseExample;
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/async-storage、@react-native-oh-tpl/react-native-get-random-values. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/async-storage docs](/zh-cn/react-native-async-storage-async-storage.md)、[@react-native-oh-tpl/react-native-get-random-values docs](/zh-cn/react-native-get-random-values.md) to add it to your project.

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## API

The apis corresponding to different versions are also different. For details, please refer to the official documentation of [Parse-SDK-JS](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/index.html)。

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Parse**: Parse is the core object of Parse-SDK-JS, containing all Parse API classes and functions.

| Name            | Description                                                              | Type                                                                        | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| initialize      | Initialize the Parse SDK and set the ID and key of the application. It is usually called at the entrance of the application. | (applicationId: string, javaScriptKey?: string, masterKey?: string) => void | yes      | iOS/Android | yes               |
| setAsyncStorage | Set the AsyncStorage instance used by the Parse SDK to store session tokens and other information.        | (storage:AsyncStorage) => void                                              | yes      | iOS/Android | yes               |

**Parse.ACL**: Access permission object.

| Name                 | Description                                    | Type                                       | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------------------------------- | ------------------------------------------ | -------- | ----------- | ----------------- |
| setPublicReadAccess  | Set whether to allow public (unauthenticated users) to read the object.       | (allowed: boolean) => void                 | no       | iOS/Android | yes               |
| setPublicWriteAccess | Set whether to allow public (unauthenticated users) to write to the object.       | (allowed: boolean) => void                 | no       | iOS/Android | yes               |
| getPublicReadAccess  | Obtain whether public (unauthenticated users) are allowed to read the object.       | () => boolean                              | no       | iOS/Android | yes               |
| getPublicWriteAccess | Obtain the permission to allow public (unauthenticated users) to write to the object. | () => boolean                              | no       | iOS/Android | yes               |
| setReadAccess        | Set whether a specific user has the permission to read objects.             | (userId: string, allowed: boolean) => void | no       | iOS/Android | yes               |
| setWriteAccess       | Set whether a specific user has the permission to write objects.            | (userId: string, allowed: boolean) => void | no       | iOS/Android | yes               |
| getReadAccess        | Obtain whether a specific user has the permission to read objects.             | (userId: string) => boolean                | no       | iOS/Android | yes               |
| getWriteAccess       | Obtain whether a specific user has the permission to write objects.           | (userId: string) => boolean                | no       | iOS/Android | yes               |

**Parse.Object**: Under normal circumstances, you won't call this method directly. It is recommended that you use a subclass of Parse.Object and create a subclass object by calling the 'extend' method。

| Name             | Description                                                         | Type                                                                         | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| set              | Set the attribute values of the data object, where 'key' is the attribute name and 'value' is the corresponding attribute value. | (key: string\|object, value: string\|object, options: object) => ParseObject | no       | iOS/Android | yes               |
| get              | Obtain the specified attribute value of the data object and specify the attribute name through the 'key'.                   | (attr: string) => any                                                        | no       | iOS/Android | yes               |
| unset            | Remove the specified attribute value of the data object and specify the attribute name through the 'key'.                   | (attr: string) => ParseObject                                                | no       | iOS/Android | yes               |
| increment        | Increase the numeric type value of the specified attribute. 'amount' is the increased quantity.                  | (attr: String, amount: Number) => ParseObject                                | no       | iOS/Android | yes               |
| add              | Add a value to an array type property. 'value' is the value to be added.                | (attr: string, item) => ParseObject                                          | no       | iOS/Android | yes               |
| remove           | Remove a value from an array type property. 'value' is the value to be removed.            | (attr: string, item) => ParseObject                                          | no       | iOS/Android | yes               |
| save             | Save the data object to the Parse server. If the object does not exist, create it; if it exists, update it. | () => Promise                                                                | no       | iOS/Android | yes               |
| fetch            | Obtain the latest data object information from the Parse server.                           | (options: object) => Promise                                                 | no       | iOS/Android | yes               |
| destroy          | Delete the current data object from the Parse server.                                 | (options: object) => Promise                                                 | no       | iOS/Android | yes               |
| fetchWithInclude | When obtaining an object, include the associated object specified in the query.                        | (keys: string\|Array<string\|Array<string>>, options: object) => Promise     | no       | iOS/Android | yes               |
| saveAll          | Batch save a group of data objects to the Parse server.                              | (list: Array, options: object) => Array.<Parse.Object>                       | no       | iOS/Android | yes               |
| destroyAll       | Batch delete a group of data objects.                                             | (list: Array, options: object) => Promise                                    | no       | iOS/Android | yes               |

**Parse.Query**: Parse.Query defines a query used to obtain Parse.Object.

|         Name         | Description                                                                                                         | Type                                                                                                                                                    | Required | Platform    | HarmonyOS Support |
| :------------------: | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
|       equalTo        | Add an equality condition to make the value of the query field 'key' equal to 'value'.                                                                 | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|      notEqualTo      | Add an unequal condition, and the value of the query field 'key' is not equal to 'value'.                                                              | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|       lessThan       | Add a less than condition, and the value of the query field 'key' is less than 'value'.                                                               | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|     greaterThan      | Add a greater than condition to query that the value of the field 'key' is greater than that of 'value'.                                                               | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|  lessThanOrEqualTo   | Add a less than or equal to condition, and the value of the query field 'key' is less than or equal to 'value'.                                                  | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
| greaterThanOrEqualTo | Add a greater than or equal to condition, and the value of the query field 'key' is greater than or equal to 'value'.                                                    | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|     containedIn      | Add a condition that includes the value of the query field 'key' in the 'values' array.                                                     | (key: string, value: any[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                         | no       | iOS/Android | yes               |
|    notContainedIn    | Add a condition that does not include the value of the query field 'key' in the 'values' array.                                                 | (key: string, value: any[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                         | no       | iOS/Android | yes               |
|        exists        | Add a existence condition that the value of the query field 'key' exists (not 'null' or 'undefined').                                             | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|     doesNotExist     | Add a non-existence condition where the value of the query field 'key' does not exist (either 'null' or 'undefined').                                         | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|     containsAll      | Add a query field 'key' that contains all conditions. The value of the query field 'key' must include all elements in the 'values' array.                                      | (key: string, value: any[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                         | no       | iOS/Android | yes               |
|      startsWith      | Add a condition starting with the specified prefix. The value of the query field 'key' must start with the 'prefix' string.                                       | (key: string, prefix: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                       | no       | iOS/Android | yes               |
|       endsWith       | Add a condition that ends with the specified suffix. The value of the query field 'key' must end with the 'suffix' string.                                      | (key: string, suffix: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                       | no       | iOS/Android | yes               |
|         near         | Add a proximity condition to query that the value of the geographical location field 'key' is close to the specified geographical coordinate point 'point'.                                       | (key: string, point: Parse.GeoPoint) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                | no       | iOS/Android | yes               |
|    withinRadians     | Add a condition within the specified arc to query that the value of the geographical location field 'key' is within the circular range centered on 'point' with a radius of 'maxDistance'.     | (key: string, point: Parse.GeoPoint, maxDistance: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)           | no       | iOS/Android | yes               |
|     withinMiles      | Add a condition within the specified mile to query that the value of the geographical location field 'key' is within a circular range centered on 'point' with a radius of 'maxDistance' miles. | (key: string, point: Parse.GeoPoint, maxDistance: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)           | no       | iOS/Android | yes               |
|   withinKilometers   | Add a condition within the specified kilometers to query that the value of the geographical location field 'key' is within a circular range centered on 'point' with a radius of 'maxDistance' kilometers. | (key: string, point: Parse.GeoPoint, maxDistance: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)           | no       | iOS/Android | yes               |
|     withinGeoBox     | Add a condition within the specified rectangular area to query that the value of the geographical location field 'key' must be within the rectangle defined by 'southwest' and 'northeast'.       | (key: string, southwest: Parse.GeoPoint, northeast: Parse.GeoPoint) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html) | no       | iOS/Android | yes               |
|       include        | Add a condition containing the associated object                                                                                           | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|        select        | Only return the information of the specified fields in the query results.                                                                                    | (keys: string[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                    | no       | iOS/Android | yes               |
|        limit         | Limit the number of returned results.                                                                                                | (count: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                     | no       | iOS/Android | yes               |
|         skip         | Skip the specified number of query results.                                                                                           | (count: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                     | no       | iOS/Android | yes               |
|      ascending       | Sort the query results in ascending order according to the specified fields.                                                                                   | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|      descending      | Sort the query results in descending order according to the specified fields.                                                                                      | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|         find         | Sort the query results in descending order according to the specified fields.                                                                                     | (options?: Parse.Query.FindOptions) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                 | no       | iOS/Android | yes               |
|        first         | Execute the query and return the first object that meets the conditions.                                                                                | (options?: Parse.Query.FindOptions) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                 | no       | iOS/Android | yes               |
|        count         | Calculate the number of objects that meet the conditions.                                                                                          | (options?: Parse.Query.CountOptions) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                | no       | iOS/Android | yes               |

**Parse.Role**: Represents the role object on the Parse server.

| Name           | Description                     | Type                                          | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| getName        | Get the name of the character.                | () => String                                  | no       | iOS/Android | yes               |
| getUsers       | Obtain the list of users assigned to the role.      | () => Array<Parse.User>                       | no       | iOS/Android | yes               |
| getRoles       | Get the list of sub-roles assigned to the role.    | () => Array<Parse.Role>                       | no       | iOS/Android | yes               |
| getRolesByName | Obtain the list of role objects based on the role name.  | (Array<String>) => Promise<Array<Parse.Role>> | no       | iOS/Android | yes               |
| save           | Save the role object to the Parse server. | (obj: Object) => Promise<Array<Parse.Role>>   | no       | iOS/Android | yes               |
| destroy        | Delete the role object from the Parse server. | (obj: Object) => Promise<Array<Parse.Role>>   | no       | iOS/Android | yes               |

**Parse.User**: It represents the user object on the Parse server and can perform operations such as registration, login, and logout.

| Name    | Description                                               | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| signUp  | Register a new user to the Parse server.                            | ({username: string, password: string, email: string}) => Promise<Parse.User> | no       | iOS/Android | yes               |
| logIn   | Logged-in user.                                             | (username: string, password: string) => Promise<Parse.User>  | no       | iOS/Android | yes               |
| current | Get the currently logged-in user object. If no user is logged in, return 'null'. | () => Parse.User                                             | no       | iOS/Android | yes               |
| logOut  | Log out of the current user.                                            | () => Promise<void>                                          | no       | iOS/Android | yes               |
| become  | Authenticate users through session tokens.                    | (sessionToken: string) => Promise<Parse.User>                | no       | iOS/Android | yes               |
| save    | Save the user object to the Parse server.                           | (user: Object) => Promise<Parse.User>                        | no       | iOS/Android | yes               |
| destroy | Delete the user object from the Parse server.                           | (user: Object) => Promise<void>                              | no       | iOS/Android | yes               |

**Parse.Cloud**: Custom Cloud code can be executed through the Cloud API. The following are the main supported Cloud apis and their related information:

|     Name     | Description                                                                                                                                                                                      | Type                                                                                                 | Required | Platform    | HarmonyOS Support |
| :----------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
|     run      | Call the cloud function with the specified name and obtain its return value. 'functionName' is the name of the cloud function, 'data' is the parameter object passed to the cloud function, and 'options' is an optional configuration object used to set detailed options for cloud function calls, such as timeouts, etc.                     | (functionName: string, data?: object, options?: Parse.Cloud.HttpOptions) => Promise                  | no       | iOS/Android | yes               |
|  afterSave   | Register a cloud function that is triggered after saving the object. ` className ` is the name of the class of an object, ` func ` is an asynchronous function or return void function, receives a ` Parse. Cloud. AfterSaveRequest ` objects as parameters, can perform custom logic after save objects.      | (className: string, func: (request: Parse.Cloud.AfterSaveRequest) => Promise<void>\|void) => void    | no       | iOS/Android | yes               |
|  beforeSave  | Register a cloud function that is triggered before saving the object. ` className ` is the name of the class of an object, ` func ` is an asynchronous function or return void function, receives a ` Parse. Cloud. BeforeSaveRequest ` objects as parameters, can perform custom logic in front of the object.   | (className: string, func: (request: Parse.Cloud.BeforeSaveRequest) => Promise<void>\|void) => void   | no       | iOS/Android | yes               |
| afterDelete  | Register a cloud function that is triggered after deleting an object. ` className ` is the name of the class of an object, ` func ` is an asynchronous function or return void function, receives a ` Parse. Cloud. AfterDeleteRequest ` objects as parameters, can perform custom logic after delete the object.    | (className: string, func: (request: Parse.Cloud.AfterDeleteRequest) => Promise<void>\|void) => void  | no       | iOS/Android | yes               |
| beforeDelete | Register a cloud function that is triggered before deleting an object. ` className ` is the name of the class of an object, ` func ` is an asynchronous function or return void function, receives a ` Parse. Cloud. BeforeDeleteRequest ` objects as parameters, can perform custom logic before delete the object. | (className: string, func: (request: Parse.Cloud.BeforeDeleteRequest) => Promise<void>\|void) => void | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The Apache License (Apache)](https://github.com/parse-community/Parse-SDK-JS/blob/alpha/LICENSE).

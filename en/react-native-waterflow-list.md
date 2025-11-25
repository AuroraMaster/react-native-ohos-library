> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-waterflow-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ZakZheng/react-native-waterflow-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ZakZheng/react-native-waterflow-list/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/ZakZheng/react-native-waterflow-list)

## Installation and Usage

Please go to the Releases release address of the third-party library to view the supporting version information: [react-native-waterflow-list](https://github.com/ZakZheng/react-native-waterflow-list/releases). For older versions that are not published to npm, install the tgz package by referring to the [Installation Guide](/en/tgz-usage-en.md).

| Version |  Support RN version                                                   |
| ---------- | -------------- |
| 1.2.3      | 0.72/0.77 |

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-waterflow-list@1.2.3
```

#### **yarn**

```bash
yarn add react-native-waterflow-list@1.2.3
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import { Dimensions, Image, RefreshControl, Text, View } from 'react-native';
import { IColumnsHandles } from 'react-native-waterflow-list/src/Columns';
import WaterFlow from 'react-native-waterflow-list/src/';

const width = Math.round((Dimensions.get('screen').width - 30) / 2);

const getItemData = (() => {
  let id = 0;
  return () => {
    id++;
    const height = Math.ceil(Math.random() * 1000);
    return {
      id,
      text: Math.random(),
      image_path: `https://picsum.photos/${width}/${height}/?random`,
      height,
      width,
    };
  };
})();

const sleep = (ms: number) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

const itemDataFactory = () =>
  Array(10)
    .fill('')
    .map(() => getItemData());

interface IItem {
  id: number
  [index: string]: any
}

export default () => {
  const [data, setData] = React.useState<IItem[]>([]);
  const [loading, setLoading] = React.useState(false)

  const WaterFlowRef = React.useRef<IColumnsHandles>()
  const onLoadMore = React.useCallback(async () => {
    setLoading(true)
    await sleep(1000);
    setLoading(false)
    return setData(data.concat(itemDataFactory()));
  }, [data]);
  const loadData = React.useCallback(async () => {
    await sleep(1000);
    return setData(itemDataFactory());
  }, [data])

  React.useEffect(() => {
    setData(itemDataFactory());
  }, []);

  return (
    <WaterFlow
      ref={WaterFlowRef}
      data={data}
      keyForItem={item => item.id}
      numColumns={2}
      onEndReached={onLoadMore}
      //Custom Scroll Listener(if needed)
      onScroll={(e) => {console.log(e)}}
      columnFlatListProps={{
        style: { marginHorizontal: 5, },
      }}
      columnsFlatListProps={{
        ListHeaderComponent: () => <View><Text>Hello</Text></View>,
        refreshControl: <RefreshControl
          style={{ zIndex: 10 }}
          refreshing={loading}
          onRefresh={() => {
            WaterFlowRef.current?.clear()
            loadData()
          }}
          tintColor={'gray'}
        />
        ,
        style: { marginHorizontal: 10, },
      }}
      renderItem={({ item, index }) => {
        return renderItem(item);
      }}
    />
  );
};

```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH:0.72.29; SDK:HarmonyOS NEXT Developer Beta6 SDK; IDE:DevEco Studio 5.0.3.706; ROM:NEXT.0.0.60;
2. RNOH: 0.72.33; SDK: Openharmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH:0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> For details, see [react-native-waterflow-list Source library address](https://github.com/ZakZheng/react-native-waterflow-list)

| Name                      | Description                                                                                              | Type                                                         | Required | Platform                  | HarmonyOS Support |
| :-------------------------- | :------------------------------------------------------------------------------------------------ | :------------------------------------------------------------: | :--------: | :---------------------: |:--------------:|
| **data**           | List data, and the data type must be 'Object'             | Object[]                                              | Yes | All                   | Yes          |
| **numColumns**           | Number of columns                    | number                                              | No | All                   | Yes          |
| **keyForItem**                   | Used to check if the data is rendered                                                                      | string                                        | Yes    | All                   | Yes          |
| **heightForItem**                  | If the height of the renderItem is known, it is passed in to improve performance and loading speed | number                                                  | No       | All                   | Yes          |
| **asyncHeightForItem**                 | If the height of item is obtained asynchronously, this function returns the true height of item | Promise(number)                                      | No       | All | Yes           |
| **renderItem**                    | Render list entry | JSX.Element                        | Yes    | All  | Yes           |
| **onEndReached**       | Pull-up loading: If a Promise object is passed in, you must wait for the Promise event callback before triggering this event again. If otherwise, no action will be taken | function                                            | No       | All  | Yes           |
| **columnsFlatListProps** | The outer FlatList parameter           | FlatListProps                                      | No       | All  | Yes           |
| **columnFlatListProps**                 | Column the FlatList parameter | FlatListProps                                          | No       | All  | Yes           |

## Static Methods
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ----- | :-----------| :--: |:--------:| :------: |:-----------------:|
| **clear** | Clearing the render list is generally used to pull down and refresh to obtain the data and clear the previous data | function |    No    | All |        Yes        |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ZakZheng/react-native-waterflow-list/blob/master/LICENSE).
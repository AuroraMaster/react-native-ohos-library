> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>redux-toolkit</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reduxjs/redux-toolkit?tab=readme-ov-file">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/reduxjs/redux-toolkit?tab=MIT-1-ov-file">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/reduxjs/redux-toolkit/tree/v2.2.1)

## Installation and Usage

> [!TIP] This library depends on the react-redux library. For details about how to install this library, see [react-redux documentation](./react-redux.md).

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [redux-toolkit Releases](https://github.com/reduxjs/redux-toolkit/releases).

<!-- tabs:start -->

#### **npm**

```bash
npm install @reduxjs/toolkit@2.2.1
```

#### **yarn**

```bash
yarn add @reduxjs/toolkit@2.2.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

1. Introduce the **provider** component into the **index.js entry** file and add the **store** property.

```js
// index.js
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import { store } from "./app/store";
import { Provider } from "react-redux";

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root"),
);
```

2. Create a slice and export the **reducer** property.

```js
// features/counter/counterSlice.js
import { createSlice } from '@reduxjs/toolkit'
import type { PayloadAction } from '@reduxjs/toolkit'

export interface CounterState {
  value: number
}

const initialState: CounterState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action: PayloadAction<number>) => {
      state.value += action.payload
    },
  },
})

export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```

3. Create **store.js** and use **configurationStore** to import **reducer** exported above.

```js
// app/store.js
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from '../features/counter/counterSlice'

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
})

export type RootState = ReturnType<typeof store.getState>

export type AppDispatch = typeof store.dispatch
```

4. Write a **counter** component to implement simple counting increases and decreases.

```js
// features/counter/Counter.js
import React from 'react'
import {View, Button, Text} from 'react-native'
import type { RootState } from '../../app/store'
import { useSelector, useDispatch } from 'react-redux'
import { decrement, increment } from './counterSlice'

export function Counter() {
  const count = useSelector((state: RootState) => state.counter.value)
  const dispatch = useDispatch()

  return (
    <View>
      <View>
        <Button
          title="Increment value"
          onClick={() => dispatch(increment())}
        >
        </Button>
        <Text>{count}</Text>
        <Button
          title="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          Decrement
        </Button>
      </View>
    </View>
  )
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 5.0.3.200; ROM: 205.0.0.18;

## Properties and Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
>
> See details [redux-toolkit Source library address](https://github.com/reduxjs/redux-toolkit)

| Name                     | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| configureStore           | Method used to create **store**.                             | Function | NO      | All      | yes               |
| reducer                  | Parameter of **configureStore**.                             | Object   | NO      | All      | yes               |
| middleware               | Parameter of **configureStore**, which is used to store the array of middleware. | Array    | NO      | All      | yes               |
| devTools                 | Parameter of **configureStore**, which is used for browser debugging. | Boolean  | NO      | Web      | no                |
| preloadedState           | Parameter of **configureStore**, which is used to specify the default value of **state**. | Object   | NO      | All      | yes               |
| enhancers                | Parameter of **configureStore**, which is used to customize the enhancer array. | Array    | NO      | All      | yes               |
| getDefaultMiddleware     | Method used to obtain the default middleware list.           | Function | NO      | All      | yes               |
| immutableCheck           | Property of the object parameters in **getDefaultMiddleware**. | Boolean  | NO      | All      | yes               |
| serializableCheck        | Property of the object parameters in **getDefaultMiddleware**. | Boolean  | NO      | All      | yes               |
| actionCreatorCheck       | Property of the object parameters in **getDefaultMiddleware**. | Boolean  | NO      | All      | yes               |
| createListenerMiddleware | Method used to create a listener for the middleware.         | Function | NO      | All      | yes               |
| middleware               | Property of **createListenerMiddleware**, which indicates the middleware list. | Array    | NO      | All      | yes               |
| startListening           | Property of **createListenerMiddleware**, which is used to start a listening. | Function | NO      | All      | yes               |
| stopListening            | Property of **createListenerMiddleware**, which is used to stop a listening. | Function | NO      | All      | yes               |
| clearListeners           | Property of **createListenerMiddleware**, which is used to clear all listening events. | Function | NO      | All      | yes               |
| addListener              | Property of **createListenerMiddleware**, which is used to add a listener. | Function | NO      | All      | yes               |
| removeListener           | Property of **createListenerMiddleware**, which is used to remove a listener. | Function | NO      | All      | yes               |
| clearAllListeners        | Property of **createListenerMiddleware**, which is used to clear all listeners. | Function | NO      | All      | yes               |
| createDynamicMiddleware  | Method used to create a middleware.                          | Function | NO      | All      | yes               |
| getDefaultEnhancers      | Method used to obtain the default enhancers.                 | Function | NO      | All      | yes               |
| createReducer            | Method used to create a reducer.                             | Function | NO      | All      | yes               |
| addCase                  | Method for the **createReducer** function to return the object parameters, which is used to add an action. | Function | NO      | All      | yes               |
| addMatcher               | Method for the **createReducer** function to return the object parameters, which is used to add a matcher. | Function | NO      | All      | yes               |
| addDefaultCase           | Method for the **createReducer** function to return the object parameters, which is used to add a default action. | Function | NO      | All      | yes               |
| createAction             | Method used to create an action.                             | Function | NO      | All      | yes               |
| createSlice              | Method used to create a slice.                               | Function | NO      | All      | yes               |
| name                     | Property of **createSlice**, which indicates the name of **store**. | String   | NO      | All      | yes               |
| initialState             | Property of **createSlice**, which indicates the default value of **store**. | object   | NO      | All      | yes               |
| reducers                 | Property of **createSlice**, which is a **reducers** object. | Object   | NO      | All      | yes               |
| extraReducers            | Property of **createSlice**, which is an additional **reducers** object. | Object   | NO      | All      | yes               |
| createAsyncThunk         | Method used to create an asynchronous action.                | Function | NO      | All      | yes               |
| createEntityAdapter      | Method used to create an entity adapter.                     | Function | NO      | All      | yes               |
| selectId                 | Property of **createEntityAdapter**, which indicates a unique ID. | String   | NO      | All      | yes               |
| sortComparer             | Property of **createEntityAdapter**, which indicates the sorting method. | Function | NO      | All      | yes               |
| getInitialState          | Property of **createEntityAdapter**, which indicates the default state. | Object   | NO      | All      | yes               |
| combineSlices            | Method used to combine two slices.                           | Function | NO      | All      | yes               |
| createSelector           | Method used to create a selector.                            | Function | NO      | All      | yes               |
|                          |                                                              |          |          |          |                   |

## Utilities

| Name                | Description                                               | Type     | Required | Platform | HarmonyOS Support |
| ------------------- | --------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| isAllOf             | Checks whether all actions are passed.                    | Function | NO      | All      | yes               |
| isAnyOf             | Checks whether an action is passed.                       | Function | NO      | All      | yes               |
| isAsyncThunkAction  | Checks whether an action is asynchronous.                 | Function | NO      | All      | yes               |
| isPending           | Checks whether an action is pending.                      | Function | NO      | All      | yes               |
| isRejected          | Checks whether an action is fulfilled.                    | Function | NO      | All      | yes               |
| isFulfilled         | Checks whether an action is rejected.                     | Function | NO      | All      | yes               |
| isRejectedWithValue | Checks whether an action is rejected with a return value. | Function | NO      | All      | yes               |
| nanoid              | Method used to generate a random string.                  | Function | NO      | All      | yes               |
| miniSerializeError  | Method used to display error information.                 | Function | NO      | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/reduxjs/redux-toolkit/blob/master/LICENSE).
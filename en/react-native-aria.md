> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-aria</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gluestack/react-native-aria/tree/main">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gluestack/react-native-aria/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github Address](https://github.com/gluestack/react-native-aria/tree/main)

## Installation & Usage
> [!TIP] This library is no longer maintained. If you encounter missing modules when running the project after executing the general package command, you need to uninstall the old packages and add `--legacy-peer-deps` to the command, then download the package files again.

Please check the corresponding version information in the third-party library's Releases:

| Third-party Version | Release Information | Supported RN Version |
| ------------------- | ------------------- | -------------------- |
| 0.2.4 | [react-native-aria release](https://github.com/gluestack/react-native-aria/releases) | 0.72/0.77 |

For older versions not published to npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Navigate to your project directory and run the following command:

#### **yarn**

```bash
yarn add react-native-aria@0.2.4
```

#### **npm**

```bash
npm install react-native-aria@0.2.4
```

In addition to the main package, we also provide some separate packages, such as: @react-native-aria/button

#### **yarn**

```bash
yarn add @react-native-aria/button@0.2.7
```

#### **npm**

```bash
npm install @react-native-aria/button@0.2.7
```

The following code demonstrates the basic usage scenario of useToggleButton:

```js
import React from "react";
import { useToggleButton } from "@react-native-aria/button";
import { useToggleState } from "@react-stately/toggle";
import { Pressable, Text, View } from "react-native";
import { useRef } from "react";

export function ToggleButton(props: any) {
    const ref = useRef(null);
    let state = useToggleState(props);
    let { buttonProps, isPressed } = useToggleButton(props, state);

    return (
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <Text>ToggleButton：</Text>
            <Pressable ref={ref} {...buttonProps}
                style={{
                    backgroundColor: state.isSelected ? "rgb(9, 90, 186)" : "#e1e1e1", borderRadius: 15,
                    padding: 5, width: 100, height: 30, justifyContent: 'center', alignItems: 'center'
                }}
            >
                <Text style={{ color: state.isSelected ? "#f1f1f1" : "#000" }} >Click to toggle</Text>
            </Pressable>
        </View>
    );
}

export default ToggleButton

```

The following code demonstrates the basic usage scenario of useCheckbox and useCheckboxGroup:

```javascript
import React, { useContext, useRef } from 'react';
import { Pressable, View, Text } from 'react-native';
import { useCheckbox, useCheckboxGroupItem, useCheckboxGroup } from '@react-native-aria/checkbox';
import { useToggleState } from '@react-stately/toggle';
import { useCheckboxGroupState } from "@react-stately/checkbox";
import { useFocusRing } from '@react-native-aria/focus';

let CheckboxGroupContext = React.createContext<any>(null);

const CheckboxItems = [{ key: 'soccer', value: 'Football' }, { key: 'baseball', value: 'Baseball' }, { key: 'basketball', value: 'Basketball' }]
const findName = (value: string) => {
    const item = CheckboxItems.find(i => { return i.key === value; })
    return item && item.value
}

export function CheckboxGroup(props: any) {
    let { children, label } = props;
    let state = useCheckboxGroupState(props);
    let { groupProps, labelProps } = useCheckboxGroup(props, state);

    return (
        <View {...groupProps} style={{ flexDirection: 'row', alignItems: 'center' }}>
            {label && <Text {...labelProps}>{label}</Text>}
            <CheckboxGroupContext.Provider value={state}>
                {children}
            </CheckboxGroupContext.Provider>
            <View><Text>Selected：</Text>{props.value.map(i=>{
                return <Text>{findName(i)}</Text>
            })}</View> 
        </View>
    );
}


export function Checkbox(props: any) {
    let groupState = useContext(CheckboxGroupContext);
    let inputRef = useRef<HTMLInputElement>(null);

    let { isFocusVisible, focusProps } = useFocusRing();

    let { inputProps } = groupState ? useCheckboxGroupItem(
        {
            ...props,
            isRequired: props.isRequired,
            validationState: props.validationState,
        },
        groupState,
        inputRef
    ) : useCheckbox(props, useToggleState(props), inputRef);

    return (
        <View style={isFocusVisible ? { borderWidth: 2 } : {}}>
            <Pressable {...inputProps} {...focusProps} >
                <View style={{ flexDirection: 'row', alignItems: 'center', marginRight: 5 }}>
                    {props.children}
                </View>
            </Pressable>
        </View>
    );
}

export const CheckboxExample = () => {
    const [state, setCheckbox] = React.useState([]);

    return (
        <CheckboxGroup
            label="CheckboxGroup："
            value={state}
            onChange={(val: any) => {
                setCheckbox(val);
            }}
        >
            {CheckboxItems.map(i => {
                return <Checkbox key={i.key} value={i.key}>
                    <Text>{i.value}</Text>
                </Checkbox>;
            })}
        </CheckboxGroup>
    );
};
export default CheckboxExample

```

The following code demonstrates the basic usage scenario of useRadio and useRadioGroup:

```javascript
import React from "react";
import { useRadioGroupState } from "@react-stately/radio";
import { useRadio, useRadioGroup } from "@react-native-aria/radio";
import { Pressable, Text, View } from "react-native";
import { useFocusRing } from "@react-native-aria/focus";

let RadioContext = React.createContext<any>({});

const radioItems = [{ key: 'dogs', value: 'Dogs' }, { key: 'cats', value: 'Cats' }]
const findName = (value: string) => {
    const item = radioItems.find(i => { return i.key === value; })
    return item && item.value
}

export function RadioGroup(props: any) {
    let { children, label } = props;
    let state = useRadioGroupState(props);
    let { radioGroupProps, labelProps } = useRadioGroup(props, state);

    return (
        <View {...radioGroupProps} style={{ flexDirection: 'row', alignItems: 'center' }}>
            <Text {...labelProps}>{label}</Text>
            <RadioContext.Provider
                value={{
                    isDisabled: props.isDisabled,
                    isReadOnly: props.isReadOnly,
                    state,
                }}
            >
                {children}
            </RadioContext.Provider>
            <Text>Selected：{findName(state.selectedValue as string)}</Text>
        </View>
    );
}

export function Radio(props: any) {
    let { state, isReadOnly, isDisabled } = React.useContext(RadioContext);
    const inputRef = React.useRef(null);
    let { inputProps } = useRadio(
        { isReadOnly, isDisabled, ...props },
        state,
        inputRef
    );
    let { isFocusVisible, focusProps } = useFocusRing();

    return (
        <Pressable {...inputProps}{...focusProps} style={{ marginRight: 5 }}>
            <View style={[{ flexDirection: 'row', alignItems: 'center' }, isFocusVisible ? { borderWidth: 1 } : {},]}>
                <Text>{props.children}</Text>
            </View>
        </Pressable>
    );
}

export const RadioExample = () => {
    return (
        <View>
            <RadioGroup label="RadioGroup：">
                {radioItems.map(i => {
                    return <Radio key={i.key} value={i.key}>{i.value}</Radio>
                })}
            </RadioGroup>
        </View>
    );
};
export default RadioExample

```

The following code demonstrates the basic usage scenario of useSwitch:

```javascript
import { useToggleState } from "@react-stately/toggle";
import React, { useRef } from "react";
import { StyleSheet, Text, View, Animated, Pressable } from "react-native";
import { useSwitch } from "@react-native-aria/switch";
import { useFocusRing } from "@react-native-aria/focus";
import { VisuallyHidden } from "@react-aria/visually-hidden";

const calculateDimensions = (size: any) => {
    switch (size) {
        case "small":
            return {
                width: 40,
                padding: 10,
                circleWidth: 15,
                circleHeight: 15,
                translateX: 22,
            };
        case "large":
            return {
                width: 70,
                padding: 20,
                circleWidth: 30,
                circleHeight: 30,
                translateX: 38,
            };
        default:
            return {
                width: 46,
                padding: 12,
                circleWidth: 18,
                circleHeight: 18,
                translateX: 26,
            };
    }
};

const defaultProps = {
    isOn: false,
    onColor: "#4cd137",
    offColor: "#ecf0f1",
    size: "medium",
    labelStyle: {},
    thumbOnStyle: {},
    thumbOffStyle: {},
    trackOnStyle: {},
    trackOffStyle: {},
    icon: null,
    disabled: false,
    animationSpeed: 300,
    useNativeDriver: true,
    circleColor: "white",
};

export function Switch(origProps: any) {
    const props = {
        ...defaultProps,
        ...origProps,
    };

    const offsetX = useRef(new Animated.Value(0));
    const dimensions = useRef(calculateDimensions(props.size));

    const createToggleSwitchStyle = () => [
        {
            justifyContent: "center",
            width: dimensions.current.width,
            borderRadius: 20,
            padding: dimensions.current.padding,
            backgroundColor: props.isOn ? props.onColor : props.offColor,
        },
        props.isOn ? props.trackOnStyle : props.trackOffStyle,
    ];

    const createInsideCircleStyle = () => [
        {
            alignItems: "center",
            justifyContent: "center",
            margin: 4,
            left: 0,
            position: "absolute",
            backgroundColor: props.circleColor,
            transform: [{ translateX: offsetX.current }],
            width: dimensions.current.circleWidth,
            height: dimensions.current.circleHeight,
            borderRadius: dimensions.current.circleWidth / 2,
            shadowColor: "#000",
            shadowOffset: {
                width: 0,
                height: 2,
            },
            shadowOpacity: 0.2,
            shadowRadius: 2.5,
            elevation: 1.5,
        },
        props.isOn ? props.thumbOnStyle : props.thumbOffStyle,
    ];

    const { isOn, icon, label, labelStyle = {} } = props;

    const toValue = isOn
        ? dimensions.current.width - dimensions.current.translateX
        : 0;

    Animated.timing(offsetX.current, {
        toValue,
        duration: props.animationSpeed,
        useNativeDriver: props.useNativeDriver,
    }).start();

    return (
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            {label && <Text style={labelStyle}>{label}</Text>}
            <View style={[...createToggleSwitchStyle(), { marginBottom: 5 }]}>
                <Animated.View style={createInsideCircleStyle()}>{icon}</Animated.View>
            </View>
            <Text style={{ marginLeft: 5 }}>{isOn ? "On" : "Off"}</Text>
        </View>
    );
}

export function ControlledSwitch() {
    const state = useToggleState();
    const { isFocusVisible, focusProps } = useFocusRing();
    const inputRef = useRef(null);
    let { inputProps } = useSwitch(
        { "aria-label": "Example switch" },
        state,
        inputRef
    );

    return (
        <Pressable {...inputProps} {...focusProps} ref={inputRef}>
            <View style={isFocusVisible ? { borderWidth: 2 } : {}}>
                <Switch
                    isOn={state.isSelected}
                    onColor="green"
                    offColor="red"
                    label='Switch：'
                    size="large"
                    onToggle={state.toggle}
                />
            </View>
        </Pressable>
    );

}
export default ControlledSwitch

```

The following code demonstrates the basic usage scenario of useOverlayPosition:

```javascript
import React from "react";
import { useOverlayPosition, OverlayProvider, OverlayContainer } from "@react-native-aria/overlays";
import { useButton } from "@react-native-aria/button";
import { View, Text, Pressable, ScrollView, Modal } from "react-native";
import { useToggleState } from "@react-stately/toggle";

const positions = [
    "top",
    "left",
    "right",
    "bottom",
    "top left",
    "top right",
    "left top",
    "left bottom",
    "bottom right, bottom left",
    "right top",
    "right bottom",
];

export function TriggerWrapper() {
    const [placement, setPlacement] = React.useState<any>(-1);
    React.useEffect(() => {
        const id = setInterval(() => {
            setPlacement((prev) => (prev + 1) % positions.length);
        }, 2000);
        return () => clearInterval(id);
    }, []);

    return <Trigger placement={positions[placement]}></Trigger>;
}

const OverlayView = ({ targetRef, placement = 'top' }) => {
    let overlayRef = React.useRef();

    const { overlayProps } = useOverlayPosition({
        placement: placement as any,
        targetRef,
        overlayRef,
        offset: 10,
    });

    return (
        <ScrollView
            bounces={false}
            style={{
                position: "absolute",
                height: 400,
                backgroundColor: "lightgray",
                ...overlayProps.style,
            }}
            ref={(node) => overlayRef.current = node}
        >
            <View
                style={{
                    padding: 20,
                    height: 5000,
                }}
            >
                <Text>Hello world</Text>
            </View>
        </ScrollView>
    );
};

export function Trigger({ placement }: any) {
    let ref = React.useRef();
    const toggleState = useToggleState();

    let { buttonProps } = useButton({ onPress: toggleState.toggle }, ref);

    return (
        <View style={{ flexDirection: 'row', alignItems: "center" }} >
            <Text>useOverlayPosition：</Text>
            <Pressable
                {...buttonProps}
                ref={ref}
                role="button"
                aria-label="Click here to perform some actions"
            >
                <View
                    style={{
                        flexDirection: "row",
                        borderWidth: 1,
                        paddingHorizontal: 10,
                        paddingVertical: 10,
                    }}
                >
                    <Text>Click me</Text>
                </View>
            </Pressable>
            <Modal visible={toggleState.isSelected} onRequestClose={toggleState.toggle}>
                <OverlayProvider>
                    <OverlayContainer>
                        <OverlayView targetRef={ref} placement={placement} />
                    </OverlayContainer>
                </OverlayProvider>
            </Modal>
        </View>
    );
}
export default TriggerWrapper

```

For more hooks, please refer to the [react-native-aria official documentation](https://geekyants.github.io/react-native-aria/docs/)

## Constraints & Limitations

### Compatibility

To use this library, you need the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified in the following versions:

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## Hooks

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for that property.

> [!TIP] The "HarmonyOS Support" column: 'Yes' means the property is supported on the HarmonyOS platform; 'No' means it is not supported; 'partially' means partial support. The usage method is consistent across platforms, with effects benchmarked against iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|-------------|-------------------|
| useToggleButton    | Provides the behavior and accessibility implementation for a toggle button component. ToggleButtons allow users to toggle a selection on or off, for example switching between two states or modes.           | Function | No       | iOS,Android | Yes               |
| useCheckbox        | Provides the behavior and accessibility implementation for a checkbox component. Checkboxes allow users to select multiple items from a list of individual items, or to mark one individual item as selected. | Function | No       | iOS,Android | Yes               |
| useCheckboxGroup   | Provides the behavior and accessibility implementation for a checkbox group component. Checkbox groups allow users to select multiple items from a list of options.                                           | Function | No       | iOS,Android | Yes               |
| useRadioGroup      | Provides the behavior and accessibility implementation for a radio group component. Radio groups allow users to select a single item from a list of mutually exclusive options.                               | Function | No       | iOS,Android | Yes               |
| useSwitch          | Provides the behavior and accessibility implementation for a switch component. A switch is similar to a checkbox, but represents on/off values as opposed to selection.                                       | Function | No       | iOS,Android | Yes               |
| OverlayContainer   | Provides React Portal like functionality for React Native apps which can be useful for displaying absolutely positioned components like Menu, Tooltip, Popover.                                               | Function | No       | iOS,Android | Yes               |
| useOverlayPosition | Handles positioning overlays like popovers and menus relative to a trigger element, and updating the position when the window resizes.                                                                        | Function | No       | iOS,Android | Yes               |

## Known Issues
1. Immediate voice reading after toggling selection state is currently not supported.

## Others

## License

This project is based on [The MIT License (MIT)](https://github.com/gluestack/react-native-aria/blob/main/LICENSE). Feel free to enjoy and contribute to open source.
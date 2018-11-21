---
id: component-buttons
title: Buttons
sidebar_label: Buttons
---

<img src="assets/samplebutton.gif" width="280" />


Gesture handler library provides native components that can act as buttons. These can be treated as a replacement to `TouchableHighlight` or `TouchableOpacity` from RN core. Gesture handler's buttons recognize touches in native which makes the recognition process deterministic, allows for rendering ripples on Android in highly performant way (`TouchableNativeFeedback` requires that touch event does a roundtrip to JS before we can update ripple effect, which makes ripples lag a bit on older phones), and provides native and platform default interaction for buttons that are placed in a scrollable container (in which case the interaction is slightly delayed to prevent button from highlighting when you fling).

Currently Gesture handler library exposes three components that render native touchable elements under the hood:
 - `BaseButton`
 - `RectButton`
 - `BorderlessButton`

On top of that all the buttons are wrapped with `NativeViewGestureHandler` and therefore allow for all the [common gesture handler properties](#common-gesturehandler-properties) and `NativeViewGestureHandler`'s [extra properties](#nativeviewgesturehandler-extra-properties) to be applied to them.

## `BaseButton`

Can be used as a base class if you'd like to implement some custom interaction for when the button is pressed.

Below is a list of properties specific to `BaseButton` component:

### `onActiveStateChange`
function that gets triggered when button changes from inactive to active and vice versa. It passes active state as a boolean variable as a first parameter for that method.

---
### `onPress`
function that gets triggered when the button gets pressed (analogous to `onPress` in `TouchableHighlight` from RN core).


## `RectButton`

This type of button component should be used when you deal with a rectangular elements or blocks of content that can be pressed, for example table rows or buttons with text and icons. This component provides a platform specific interaction, rendering a rectangular ripple on Android or highlighting the background on iOS and on older versions of Android. In addition to the props of [`BaseButton`](#basebutton-component), it accepts the following:

Below is a list of properties specific to `RectButton` component:

---
### `underlayColor`
this is the background color that will be dimmed when button is in active state.

---
### `activeOpacity` (**iOS only**)
opacity applied to the underlay when button is in active state.

## `BorderlessButton`

This type of button component should be used with simple icon-only or text-only buttons. The interaction will be different depending on platform: on Android a borderless ripple will be rendered (it means that the ripple will animate into a circle that can span outside of the view bounds), whereas on iOS the button will be dimmed (similar to how `TouchableOpacity` works). In addition to the props of [`BaseButton`](#basebutton-component), it accepts the following:

Below is a list of properties specific to `BorderlessButton` component:

---
### `borderless` (**Android only**)
set this to `false` if you want the ripple animation to render only within view bounds.

---
### `activeOpacity` (**iOS only**)
opacity applied to the button when it is in an active state.

---

## Design patterns
Components listed here were not designed to behave and look in the same way on both platforms but rather to be used for handling similar behaviour on iOS and Android taking into consideration their's design concepts.

If you wish to get specific information about platforms design patters, visit [official Apple docs](https://developer.apple.com/design/human-interface-guidelines/ios/controls) and [Material.io guideline](https://material.io/design/components/buttons.html#text-button), which widely describe how to implement coherent design.

This library allows to use native components with native feedback in adequate situations.

If you do not wish to implement custom design approach, `RectButton` and `BorderlessButton` seem to be absolutely enough and there's no need to use anything else. In all the remaining cases you can always rely on `BaseButton` which is a superclass for the other button classes and can be used as a generic `Touchable` replacement that can be customized to your needs.

Below we list some of the common usecases for button components to be used along with the type of button that should be used according to the platform specific design guidelines.

### Lists and action buttons

If you have a list with clickable items or have an action button that need to display as a separate UI block (vs being inlined in a text) you should use `RectButton`. It changes opacity on click and additionally supports a ripple effect on Android.


<img src="assets/androidsettings.gif" width="280" />


<img src="assets/iossettings.gif" width="280" />


To determine emphasis of button it's vital to use fill color or leave it transparent especially on Android.
For medium emphasis you may consider outlined buttons which are used for lower impact than fill buttons.
 
<img src="assets/androidbutton.gif" width="280" />

### Icon or text only buttons

Use `BorderlessButton` for simple icon-only or text-only buttons. The interaction will be different depending on platform: on Android a borderless ripple will be rendered, whereas on iOS the button will be dimmed.
It should be used if you wish to handle non-crucial actions and supportive behaviour.


<img src="assets/androidmail.gif" width="280" />


<img src="assets/iosmail.gif" width="280" />

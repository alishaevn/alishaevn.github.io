---
title: Large Text Scrolling
categories: [JavaScript, React Native]
layout: post
excerpt: "Allowing your mobile app to maintain a positive user experience when a user sets their phone to use a larger font size can be tricky."
---

Hola. 👋🏾

Allowing your mobile app to maintain a positive user experience when a user sets their phone to use a larger font size can be tricky. The content that used to fit neatly on their screen, may now flow off screen. If your app isn't set up properly, that may now mean that the user can't see some of the content you'd like them to see.

The way I fixed this problem was by making a custom component using a `KeyboardAvoidingView` and `ScrollView`. This component then wraps your root screen so that all of its capabilities can be passed down.

``` jsx
import React from 'react'
import { KeyboardAvoidingView, ScrollView, Text } from 'react-native'
const KAV_BEHAVIOR = 'padding'
const KAV_OFFSET = 40
const KAV_STYLE = { flex: 1 }
const SV_INSET = { bottom: 50 }

const KeyboardAvoidingWrapper = ({ behavior, contentInset, keyboardVerticalOffset, style }, props) => (
    <KeyboardAvoidingView
        behavior={behavior || KAV_BEHAVIOR}
        keyboardVerticalOffset={keyboardVerticalOffset || KAV_OFFSET}
        style={style || KAV_STYLE}
		{...props}
    >
		<ScrollView contentInset={SV_INSET}>
			{children}
		</ScrollView>
    </KeyboardAvoidingView>
)

const App = () => (
	<KeyboardAvoidingWrapper>
		<Text>
			{`This is my app!`}
		</Text>
	</KeyboardAvoidingWrapper>
)

export default App
```

See you next time. 🙃
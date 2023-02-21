---
title: React Class to Function Pt. 4
categories: [JavaScript, React]
layout: post
---

Hola. 👋🏾

Lifecycle methods are a pretty big deal in class components. There are so many because each one is called at a different point in the life of the component. They're basically broken into 3 categories though: before the component mounts, after the component mounts and when the component is going to unmount.

The "render" method is the most used lifecycle method and the only required one in every class component. I'd assume that `componentDidMount` is second to render. It's where you put your code that you'd like to be set when the component has mounted. In our case, we were setting up a keyboard listener. We only want the app to pay attention to this listener while our component is on screen though, so we remove the listener in the "componentWillUnmount" method.

```js
import React, { Component } from 'react'
import { View } from 'react-native'

class Form extends Component {
    componentDidMount() {
        this.keyboardDidHide = Keyboard.addListener(
            'keyboardDidHide',
            this._keyboardDidHide
        )
    }

    componentWillUnmount() {
        this.keyboardDidHide.remove()
    }

    _keyboardDidHide = () => this.props.scrollDown()

    render() {
        return <View></View>
    }
}

export default Form
```

In our functional component, the "componentDidMount" and "componentWillUnmount" methods can be written using the same hook: "useEffect". You can have multiple "useEffect's" in a single component and they also can take a value in the square brackets at the end. For our conversion, we don't need either of those things. We move whatever was in the "componentDidMount" into the body of the "useEffect". Then we move whatever was in the "componentWillUnmount" into a return function at the end of the "useEffect".

```js
import React, { useEffect } from 'react'
import { View } from 'react-native'

const Form = ({ scrollDown }) => {
    useEffect(() => {
        const keyboardDidHide = Keyboard.addListener(
            'keyboardDidHide',
            _keyboardDidHide
        )

        return () => {
            keyboardDidHide.remove()
        }
    }, [])

    const _keyboardDidHide = () => scrollDown()

    return <View></View>
}

export default Form
```

See you next time. 🙃
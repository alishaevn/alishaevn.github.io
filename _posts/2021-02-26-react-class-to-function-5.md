---
title: React Class to Function Pt. 5
categories: [JavaScript, React]
layout: post
---

Hola. 👋🏾

What I'm calling "helper functions" are simply the functions written outside of the "render" method, that are called inside the "return" statement. In the class component our Button is calling the "onSubmitRequest" method which sets up the "resetTextFields" function.

```js
import React, { Component } from 'react'
import { Alert, Button } from 'react-native'

class Form extends Component {
    constructor(props) {
        super(props)
        this.state = {
            email: '',
            name: '',
        }
    }

    onSubmitRequest = async () => {
        Alert.alert(
            `Got it!`,
            [{ text: 'OK', onPress: () => resetTextFields() }],
            { cancelable: false }
        )
    }

    resetTextFields = () => {
        this.setState({
            name: '',
            email: '',
        })
    }

    render() {
        return <Button onPress={() => onSubmitRequest()} />
    }
}

export default Form
```

In the functional component the only real difference, besides changes we've already discussed, is that the helper functions are declared as a const.

```js
import React, { useState } from 'react'
import { Alert, Button } from 'react-native'

const Form = () => {
    const [name, setName] = useState('')
    const [email, setEmail] = useState('')

    const onSubmitRequest = async () => {
        Alert.alert(
            `Got it!`,
            [{ text: 'OK', onPress: () => resetTextFields() }],
            { cancelable: false }
        )
    }

    const resetTextFields = () => {
        setName('')
        setEmail('')
    }

    return <Button onPress={() => onSubmitRequest()} />
}

export default Form
```

See you next time. 🙃
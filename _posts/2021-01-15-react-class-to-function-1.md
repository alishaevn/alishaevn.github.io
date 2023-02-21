---
title: React Class to Function Pt. 1
categories: [JavaScript, React]
layout: post
---

Hola. 👋🏾

Below is a condensed example of a class component that I converted into a functional component in a React Native app a few weeks ago. Whether it's a React app or React Native app though, the principles would have been the same.

For some the below may be enough to go off and convert classes yourself. For anyone who would appreciate a more guided approach, I'll be breaking down a few pieces over the next few posts.
- Declaring the function and props
- Removing the constructor
- Converting common lifecycle methods
- Converting helper functions

### Class
```js
import React, { Component } from 'react'
import { Alert, Button, TextInput, View } from 'react-native'

class Form extends Component {
    constructor(props) {
        super(props)
        this.state = {
            email: '',
            name: '',
        }
        this.emailRef = React.createRef()
        this.nameRef = React.createRef()
    }

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

	onChange = field => value => this.setState({ [field]: value })

    onSubmitRequest = async () => {
        const { email, name } = this.state

        if (!name || !email || name.length === 0 || email.length === 0) {
            return Alert.alert('Please fill in all the fields')
        }

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
		const { submitText } = this.props

        return (
            <View>
                <TextInput
                    value={name}
                    ref={this.nameRef}
                    onChangeText={this.onChange('name')}
                />
                <TextInput
                    value={email}
                    ref={this.emailRef}
                    onChangeText={this.onChange('email')}
                />
                <Button
                    text={submitText}
                    onPress={() => onSubmitRequest()}
                />
            </View>
        )
    }
}

export default Form
```

### Function

```js
import React, { useEffect, useRef, useState } from 'react'
import { Alert, Button, TextInput, View } from 'react-native'

const Form = ({ scrollDown, submitText }) => {
    const [email, setEmail] = useState('')
    const [name, setName] = useState('')
    const emailRef = useRef()
    const nameRef = useRef()

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

    const onSubmitRequest = async () => {
        if (!name || !email || name.length === 0 || email.length === 0) {
            return Alert.alert('Please fill in all the fields')
        }

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

    return (
        <View>
            <TextInput
                value={email}
                ref={emailRef}
                onChangeText={email => setEmail(email)}
            />
            <TextInput
                value={name}
                ref={nameRef}
                onChangeText={name => setName(name)}
            />
			<Button
                text={submitText}
                onPress={() => onSubmitRequest()}
            />
        </View>
    )
}

export default Form
```

See you next time. 🙃

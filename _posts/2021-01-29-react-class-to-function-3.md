---
title: React Class to Function Pt. 3
categories: [JavaScript, React]
layout: post
excerpt: "A constructor in a React component is used for 1 of 2 reasons: 1. When setting up local state. 2. When binding a value."
---

Hola. 👋🏾

A constructor in a React component is used for 1 of 2 reasons:
- When setting up local state
- When binding a value

The constructor isn't mandatory, but React function components have ways of still allowing us to perform both of the above actions if we need to. I've commented in the example below how we were using the constructor for two reasons.

```js
import React, { Component } from 'react'
import { View } from 'react-native'

class Form extends Component {
    constructor(props) {
        super(props)
        // setting up local state
        this.state = {
            name: '',
            email: '',
        }

        // binding ref's
        this.nameRef = React.createRef()
        this.emailRef = React.createRef()
    }

    render() {
        return <View></View>
   }
}

export default Form
```

Function components allow us to use React Hooks. Since we've created our component with fat arrow syntax, we also don't need to reference "this" anymore because our variables are already bound. :100:

Instead of having a single object that holds our local state, we will use the "useState" React hook. The setup is pretty straightforward. `const [<stateName>, <setStateName>] = useState(<initial state value>)`. While naming your "setter" the same as the actual state variable name isn't required, I find it easier to reason about what's going on.

Next, we replace "React.createRef". There's a "createRef" hook, but we'll be using the "useRef" hook instead. The difference between the two is that "createRef" will create a new ref every time the component renders. "useRef", as its name suggests, uses the same ref every time the component renders. In short, "useRef" is more useful. :smile:

```js
import React, { useRef, useState } from 'react'
import { View } from 'react-native'

const Form = () => {
    // setting up local state
    const [name, setName] = useState('')
    const [email, setEmail] = useState('')

    // binding ref's
    const nameRef = useRef()
    const emailRef = useRef()

    return <View></View>
}

export default Form
```

See you next time. 🙃

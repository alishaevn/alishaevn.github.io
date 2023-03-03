---
title: React Class to Function Pt. 2
categories: [JavaScript, React]
layout: post
excerpt: "Below is a simplified version of the React class component from part 1 of this series."
---

Hola. 👋🏾

Below is a simplified version of the React class component from part 1 of this series. Today we'll be going over how to handle the component declaration and using props. Take a look at the class and then continue below.

```js
import React, { Component } from 'react'
import { Button, View } from 'react-native'

class Form extends Component {
    render() {
        const { submitText } = this.props

        return (
            <View>
                <Button text={submitText} />
            </View>
        )
    }
}

export default Form
```

When converting a class component into a functional one, the first thing I like to do is actually declare the component as a function. Brilliant, I know. :grin:

As a class component we needed to import the "Component" class so React knew how to render what we were writing. As a function, that's no longer necessary. We simply declare a function, just like any other function we would write in JavaScript. I typically write my functions, component or otherwise, as anonymous functions using ES6 syntax. For the purposes of this post though, I'll show an example using function declaration as well.
For now we change lines 1 and 4 from above.

### Anonymous
```js
import React from 'react'

const Form = () => {
    ...
}
```

### Declaration
```js
import React from 'react'

function Form() {
    ...
}
```

That part was pretty straightforward. Next, we update our props importing. "Props" is shorthand for "properties". It's how we pass data from one component to another. In our example, it means that wherever we are rendering the Form component, we passed it a prop of "submitText". It would look something like `<Form submitText='this is some text!' />`.

Something I'm also a fan of is object destructuring. On line 3 below, I've chosen to destructure my prop of "submitText" instead of importing "props" and having to reference "submitText" later in the component. (Although we'll see how to do that too in case that's anyone's preference.) We'll also see on lines 3 and 5 that parenthesis are used instead of curly brackets after the function is declared. Functional components don't require a "render" statement and we've just destructured our props as an argument to the function. With that being the case, we can directly return the contents of our function instead of using a return statement inside of curly braces.

```js
import React from 'react'

const Form = ({ submitText }) => (
    ...
)
```

If anyone prefers not to destructure the props, the syntax below also works. It looks nearly identical to how it did in the class except there is no "this" being referenced. Using the ES6 fat arrow removes the need to use the "this" keyword. I'm also not wrapping the word "props" in parenthesis. It's just a preferential decision since there's only one argument. Parenthesis can of course be used and if we had multiple arguments, they would be required.

```js
import React from 'react'

const Form = props => {
    const { submitText } = props
    ...
}
```

That's it for today! In the next post we'll go over what happened to the constructor.

See you next time. 🙃

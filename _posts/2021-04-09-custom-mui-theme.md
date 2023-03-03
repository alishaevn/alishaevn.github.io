---
title: Create A Custom MUI Theme
categories: [JavaScript]
layout: post
excerpt: "The default Material UI (MUI) theme comes with a lot of features right out of the box."
---

Hola. 👋🏾

The default Material UI (MUI) theme comes with a lot of features [right out of the box](https://material-ui.com/customization/default-theme/). However, I highly recommend that you customize it for your own brand purposes. In the colors, typography and index "files" below are examples (some more complex than others) of how I've created a custom theme before.

`theme/colors.js`
``` js
export const black = '#000000'
export const white = '#FFFFFF'
export const disabled = 'rgba(0,0,0,0.5)'

export const blue = '#0000FF'
export const red = '#F22A07'
export const yellow = '#FDF30B'

export const success = {
    main: '#66FF33',
    dark: '#009933',
    light: 'rgba(102,255,51,0.5)',
}
```

`theme/typography.js`
``` js
import * as colors from './colors'

export const h1 = {
    fontFamily: 'Open Sans, sans-serif',
    fontWeight: 600,
    fontSize: 36,
    color: colors.blue,
    textTransform: 'initial',
}

const p = ({ inverse = false, color = colors.black }) => ({
    fontFamily: 'Open Sans, sans-serif',
    fontWeight: inverse ? 400 : 300,
    fontSize: 12,
    color: inverse ? colors.text.white : color,
    transform: 'sentence',
})
```

`theme/index.js`
``` js
import { createMuiTheme, responsiveFontSizes } from '@material-ui/core/styles'

let theme = createMuiTheme({
    palette: {
        primary: { main: colors.blue },
        success: {
            main: colors.success.main,
            dark: colors.success.dark,
            light: colors.success.light,
        },
        error: { main: colors.red },
        info: { main: colors.yellow },
        text: {
            primary: colors.black,
            secondary: colors.white,
            disabled: colors.disabled,
        },
    },
    typography: {
        h1: typography.h1,
        body1: typography.p(),
    },
})
theme = responsiveFontSizes(theme)

export {
    colors,
    theme,
    typography,
}

```

See you next time. 🙃

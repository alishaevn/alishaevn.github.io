---
title: How To Write A Jest Test For Nested Props
categories: [JavaScript]
layout: post
excerpt: "When writing a jest test, sometimes we'd like to check for a value to be present somewhere in the file tree (aka, the array)."
---

Hola. 👋🏾
When writing a jest test, sometimes we'd like to check for a value to be present _somewhere_ in the file tree (aka, the array). There isn't a way to "fuzzy find" something, but if you know the nesting pattern, there's still an (UGLY) of finding what you're looking for.


### Component
``` js
import React from 'react'
import { Text, View } from 'react-native'
import { observer } from 'mobx-react-lite'
import Activities from '../../stores/activitiesStore'
import Flame from './assets/Flame'
import styles from './styles'

const Activity = () => {
    const { count } = Activities.jumping_jacks

    return (
        <View>
            <View>
                <View>
                    <Text>{count}</Text>
                </View>
                <Text>{`jumping jacks today!`}</Text>
            </View>
        </View>
    )
}

export default observer(Activity)
```

# Test
``` js
import React from 'react'
import { act, create } from 'react-test-renderer'
import Activity from '..'

describe('with access to Activities values', () => {
    const randomNumberGenerator = () => Math.floor(Math.random() * 8) + 1

    beforeAll(() => {
        Activities.jumping_jacks = {
            count: randomNumberGenerator(),
        }
    })

    it('renders the amount of jumping jacks to do today', () => {
        let component

        act(() => {
            component = create(<Activity />)
        })

        const rendered = component.toTree()
        // you may need to do a console log of "rendered" to find how your values are nested
        const children = rendered.rendered.props.children[1].props.children

        expect(rendered).toBeTruthy()
        expect(children.length).toBe(2)
        expect(children).toEqual(
            expect.arrayContaining([
                expect.objectContaining({
                    props: expect.objectContaining({
                        children: 'jumping jacks today!',
                    })
                }),
                expect.objectContaining({
                    props: expect.objectContaining({
                        children: expect.objectContaining({
                            props: expect.objectContaining({
                                children: Activities.jumping_jacks.count,
                            }),
                        }),
                    })
                }),
            ])
        )
    })
})
```

See you next time. 🙃

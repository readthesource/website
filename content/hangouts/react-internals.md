---
title: "React.js Internals with Nick Niemeir"
description: "In JavaScript you create a virtual DOM, react diffs changes between the last virtual DOM and the next, mutating the real DOM only as necessary to reflect the changes. This has huge implications for cognitive overhead as well as performance. We are going to enter the source where that virtual DOM gets created using calls to `React.DOM[element](attributes, contents)`"
date: 2014-09-04T16:00:00Z
tense: ["past"]
youtube: "FAgSdSikSCc"
googleplus: "https://plus.google.com/b/105627089988168968277/events/cpuemsgmdltri201f25ud3fsnn8"
repository: "https://github.com/facebook/react"
hackernews: "8274133"
participants:
  0:
    name: Nick Niemeir
    avatar: https://pbs.twimg.com/profile_images/496528143008542720/ayPM6CHw.jpeg
  1:
    name: Christian Smith
    avatar: https://pbs.twimg.com/profile_images/2824302893/c2711652fb0e430b86c801d46f739638.png
  2:
    name: Erik Isaksen
    avatar: https://pbs.twimg.com/profile_images/477429289151787009/iGNukk9x.jpeg
---

React: a robust functional view layer.

View code and templating are combined as JavaScript.

In JavaScript you create a virtual DOM, react diffs
changes between the last virtual DOM and the next,
mutating the real DOM only as necessary to reflect
the changes. This has huge implications for cognitive
overhead as well as performance.

We are going to enter the source where that virtual
DOM gets created using calls to
`React.DOM[element](attributes, contents)`

Example usage

```JavaScript

var React = require('react')
  , d = React.DOM // Alias React.DOM for easier typing

var vDom =
  d.div({className: 'conainer'}
    , d.div({className: 'contents'},
      { start: d.p({}, 'Foo, bar, baz')
      , middle: d.a({href: 'http://github.com'}, 'github')
      , end: d.p({}, ['Weee', 'eeeeeee', 'eeee'])
      }
    )
  )

console.log(JSON.stringify(vDom, null, 2))

```

Creating the template interface-
https://github.com/facebook/react/blob/master/src/browser/ReactDOM.js#L45

The actual function called for a tag (eg. React.DOM.div)-
https://github.com/facebook/react/blob/master/src/core/ReactDescriptor.js#L136-188

Mixed in component pieces-
https://github.com/facebook/react/blob/master/src/core/ReactComponent.js#L217

https://github.com/facebook/react/blob/master/src/core/ReactMultiChild.js#L178
  Util to traverse all children-
  https://github.com/facebook/react/blob/master/src/utils/traverseAllChildren.js#L185

https://github.com/facebook/react/blob/master/src/browser/ui/ReactBrowserComponentMixin.js

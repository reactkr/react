---
id: special-non-dom-attributes
title: Special Non-DOM Attributes
permalink: special-non-dom-attributes.html
prev: dom-differences.html
next: reconciliation.html
---

Beside [DOM differences](/docs/docs/ref-06-dom-differences.ko-KR.md), React offers some attributes that simply don't exist in DOM.

- `key`: an optional, unique identifier. When your component shuffles around during `render` passes, it might be destroyed and recreated due to the diff algorithm. Assigning it a key that persists makes sure the component stays. See more [here](/react/docs/multiple-components.html#dynamic-children).
- `ref`: see [here](/docs/docs/08.1-more-about-refs.md).
- `dangerouslySetInnerHTML`: Provides the ability to insert raw HTML, mainly for cooperating with DOM string manipulation libraries. See more [here](/docs/tips/dangerously-set-inner-html.html).

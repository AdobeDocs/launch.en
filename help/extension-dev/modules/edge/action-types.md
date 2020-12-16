---
title: Action types
seo-title: Action types
description: Action types
seo-description: Action types
---

# Action types in edge extensions

>[!IMPORTANT]
>
>This document covers action types for edge extensions. If you are developing a web extension, see the guide on [action types for web extensions](../web/action-types.md) instead.
>
>This document also assumes you are familiar with library modules and how they are integrated in Platform Launch extensions. If you require an introduction, see the overview on [library module formatting](./format.md) before returning to this guide.

An action-type library module is intended to take an action--any action. What this action does is entirely up to you. Would you like to send a beacon or perhaps transform some data from the event?

For example, if you wanted to forward some data to a third-party party endpoint, your module may look like this:

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Now, consider a situation where you want to make the endpoint configurable by the Adobe Experience Platform Launch user. You could allow the user to input an endpoint and then save the endpoint to the settings object, with the object looking something like this:

```json
{
  "endpoint": "http://someendpoint.com"
}
```

In order to operate on the user-defined endpoint, your module would need to change to this:

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Action result

The result returned by an action module can be anything. If the action needs to execute an asynchronous task, you can return a [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that returns the result you want once it resolves.

The action result is stored inside a `ruleStash` key that is made available to all modules through the `context` parameter (`context.arc.ruleStash`). You can learn more about `ruleStash` [here](./context.md#rulestash).

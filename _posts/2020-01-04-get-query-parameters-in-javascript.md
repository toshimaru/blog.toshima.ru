---
layout: post
title: Get Query Parameters in JavaScript
tag: javascript
---

## Get current URI query params

You can get query parameters from current URL using [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams).

```js
const params = new URLSearchParams(window.location.search);
```

## Iterate query params

Let's say your access URL is `http://example.com/query_param?a=1&b=2`.

You can iterate the query parameters with `URLSearchParams` and [for...of statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of).

```js
const params = new URLSearchParams(window.location.search);
for (const [key, value] of params) { console.log(`key: ${key}, value: ${value}`) }
```

The output:

```
key: a, value: 1
key: b, value: 2
```

## Get value from key

You can get the value from the key.

```js
const params = new URLSearchParams(window.location.search);
console.log(params.get("a"))
console.log(params.get("b"))
```

The output:

```
1
2
```

## Reference

[URLSearchParams - Web APIs \| MDN](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)

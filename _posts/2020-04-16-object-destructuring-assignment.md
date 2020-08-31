---
layout: post
title: Object Destructuring Assignment in JavaScript
tags: javascript
last_modified_at: 2020-08-31
---

TIL: Object destructuring assignment in JavaScript.

## Basic usage

```js
const { one, two } = { zero: 0, one: 1, two: 2 }
one // 1
two // 2
```

## Assign with default value

```js
const { zero, three = 3 } = { zero: 0, one: 1, two: 2 }
zero // 0
three // 3
```

## Assign another variable name

```js
const { one: foo, two: bar } = { zero: 0, one: 1, two: 2 }
foo // 1
bar // 2
```

## Assign another variable name with default value

```js
const { three: t = 3 } = { zero: 0, one: 1, two: 2 }
console.log(t) // 3
```


## Nested object

```js
const {
  one,
  two: { number, ordinal: two }
} = {
  one: { number: 1, ordinal: "first" },
  two: { number: 2, ordinal: "second" }
}
one // { number: 1, ordinal: 'first' }
number // 2
two // 'second'
```

## Reference

- [Destructuring assignment - JavaScript \| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Object_destructuring)

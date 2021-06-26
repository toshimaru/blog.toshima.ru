---
layout: post
title: "[JavaScript]Shorthand Property Name and Shorthand Method Name"
tags: javascript
---

## ES6 Shorthand Property Name

You can simplify the following code with ES6 shorthand property.

```js
let id = 1, name = 'Toshimaru'
let obj = {
  id: id,
  name: name
}
//  { id: 1, name: 'Toshimaru' }
```

```js
let id = 1, name = 'Toshimaru'
let obj = {
  id,
  name
}
//  { id: 1, name: 'Toshimaru' }
```

## ES6 Shorthand Method Name

ES2015 introduces shorthand method names as well as shorthand property name.


You can simplify the following code with ES6 shorthand method name.

```js
let obj = {
  say: function(msg) {
    console.log(msg)
  }
}
obj.say("hello")
// hello
```

```js
let obj = {
  say(msg) {
    console.log(msg)
  }
}
obj.say("hello")
```

## See Also

[Merge arrays in ES6 way \| Toshimaru’s Blog](/2017/03/24/es6-array-merge.html)

## Reference

- [Shorthand Property and Method Names in JavaScript \| ES6 - ui.dev](https://ui.dev/shorthand-properties/)
- [Object initializer - JavaScript \| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)

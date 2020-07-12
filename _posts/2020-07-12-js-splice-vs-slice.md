---
layout: post
title: JavaScript splice vs slice
tags: javascript
---

Let's look into the difference between `splice` and `slice`, which are JavaScript Array methods.

## splice

### Syntax

```js
let arrDeletedItems = array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
```

### Sample Code

```js
const ary = [1, 2, 3, 4, 5]
const deletedAry = ary.splice(1)
ary // [ 1 ]
deletedAry // [ 2, 3, 4, 5 ]
```

```js
const ary = [1, 2, 3, 4, 5]
const deletedAry = ary.splice(0, 1)
ary // [ 2, 3, 4, 5 ]
deletedAry // [ 1 ]
```

## slice

### Syntax

```js
arr.slice([start[, end]])
```

### Sample Code

```js
const ary = [1, 2, 3, 4, 5]
ary.slice(1) // [ 2, 3, 4, 5 ]
ary // [ 1, 2, 3, 4, 5 ]

ary.slice(0, 1) // [1]
ary // [ 1, 2, 3, 4, 5 ]
```

## Conclusion

|  | `splice()` | `slice()`|
| --- | --- | --- |
| Return value  | Array  |  Array |
| Change receiver?  | Yes | No |
| Use case  | Get and remove value from array  | Get value from array  |

## Reference

- [Array.prototype.splice() - JavaScript \| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- [Array.prototype.slice() - JavaScript \| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

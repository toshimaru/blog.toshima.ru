---
layout: post
title: Merge arrays in ES6 way
tags: javascript
---

How can we merge some arrays in JavaScript?

## Old Way

### Merge 2 Arrays

You can use [concat](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) to merge arrays.

```js
ary1 = [1, 2]
ary2 = [2, 3]
ary1.concat(ary2)
// [ 1, 2, 2, 3 ]
```

### Merge Multiple Arrays

`concat` can take multiple arrays as arguments.

```js
ary1.concat(ary2, [5, 6, 7])
// [ 1, 2, 2, 3, 5, 6, 7 ]
```

## ES6 way

You can use [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator) to merge arrays in ES6(ES2015). This way is easier and more readable.

```js
ary1 = [1, 2]
ary2 = [2, 3]
[...ary1, ...ary2]
// [ 1, 2, 2, 3 ]
```

You can merge multiple arrays as much as you want.

```js
[...ary1, ...ary2, ...ary3]
```

Also, you can use combination of [push](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/push) and spread syntax.

```js
ary1.push(...ary2)
console.log(ary1)
// [ 1, 2, 2, 3 ]
```

This changes `ary1` value, so you should use this way when you want to merge another array into an array. In this case, `ary2` is merged into `ary1`.

## Reference

- [Merge Arrays in one with ES6 Array spread](https://gist.github.com/yesvods/51af798dd1e7058625f4)

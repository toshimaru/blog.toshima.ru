---
layout: post
title: Add/Remove/Toggle class with Element.classList
tags: javascript
---

```js
const div = document.createElement('div');
div.outerHTML // "<div></div>"
```

## Add class

```js
div.classList.add("x")
div.classList.add("y")
div.classList.add("z")

div.outerHTML // "<div class="x y z"></div>"
div.className // "x y z"
```

You can add multiple classes

```js
const div = document.createElement('div');
div.classList.add("x", "y", "z")
div.outerHTML // "<div class="x y z"></div>"
```

## Remove class

```js
div.outerHTML // "<div class="x y z"></div>"
div.classList.remove("y")
div.outerHTML // "<div class="x z"></div>"
```

## Toggle class

```js
div.className // "x z y"
div.classList.toggle("y")
div.className // "x z"
div.classList.toggle("y")
div.className // "x z y"
```

### Conditional toggle

```js
div.classList.toggle("y", false) // = div.classList.remove("y")

div.className // "x z y"
div.classList.toggle("y", false)
div.className // "x z"
div.classList.toggle("y", false)
div.className // "x z"
```

```js
div.classList.toggle("y", true) // = div.classList.add("y")

div.classList.toggle("y", true)
div.className // "x z y"
div.classList.toggle("y", true)
div.className // "x z y"
```

## Reference

- [Element.classList - Web APIs \| MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

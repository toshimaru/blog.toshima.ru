---
layout: post
title: Remove element from Array in Ruby
tags: ruby
---

## delete(obj)

Remove elements from Array.

```rb
ary = [1, 2, 3, 4, 5, 3]
ary.delete(3)
ary #=> [1, 2, 4, 5]
```

## delete_at(index)

Remove element at index position from Array.

```rb
ary = [1, 2, 3, 4, 5, 3]
ary.delete_at(2)
ary #=> [1, 2, 4, 5, 3]
```

## pop & shift

- **pop**: Remove the last element from Array
- **shift**: Remove the first element from Array

```rb
ary = [1, 2, 3, 4, 5]
ary.pop
ary #=> [1, 2, 3, 4]

ary.shift
ary #=> [2, 3, 4]
```

## Reference

- [Class: Array (Ruby 3.1.1)](https://ruby-doc.org/core-3.1.1/Array.html#method-i-delete)
- [Japanese] [Rubyで配列の要素を削除する：delete, delete_at, shift, slice! \| UX MILK](https://uxmilk.jp/24060)

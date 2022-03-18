---
title: "[Ruby]How to call Proc"
tags: ruby
---

## Create Proc

Let's create Proc in Ruby.

```rb
square = Proc.new { |x| x**2 }
# or 
square = lambda { |x| x**2 }
# or 
square = ->(x) { x**2 }
```

`->(x) { ... }` looks good to me.

## Call Proc

How to call Proc?

```rb
square.call(3)  #=> 9
# shorthands:
square.(3)      #=> 9
square[3]       #=> 9
```

`proc.call()` is orthodox.

## Reference

- [Class: Proc (Ruby 3.1.1)](https://ruby-doc.org/core-3.1.1/Proc.html)

---
layout: post
title: Factorial function in Ruby
tags: ruby
---

```rb
def factorial(num)
  (1..num).inject(:*)
end
```

## 3!

```rb
factorial 3 #=> 6
```

## 10!

```rb
factorial 10 #=> 3628800
```

## 15!

```rb
factorial 15 #=> 1307674368000
```

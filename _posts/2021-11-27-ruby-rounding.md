---
layout: post
title: Rounding in Ruby
tags: ruby
---

## Rounding off

```rb
1.4.round
# => 1
1.5.round
# => 2
-1.5.round
# => -2
-1.4.round
# => -1
```

## Rounding up

```rb
1.4.ceil
# => 2
1.5.ceil
# => 2
-1.4.ceil
# => -1
-1.5.ceil
# => -1
```

## Rounding down

```rb
1.4.floor
# => 1
1.5.floor
# => 1
-1.5.floor
# => -2
-1.4.floor
# => -2
```

## Rounding down (truncate)

```rb
1.4.truncate
# => 1
1.5.truncate
# => 1
-1.5.truncate
# => -1
-1.4.truncate
# => -1
```

## Reference

- [Class: Float (Ruby 3.0.0)](https://ruby-doc.org/core-3.0.0/Float.html)

---
layout: post
title: Array to Hash in Ruby
tags: ruby
---

You can convert from Array to Hash in Ruby using `Array#to_h`.

```rb
["a", "b", "c"].to_h { |str| [str, str] }
# => {"a"=>"a", "b"=>"b", "c"=>"c"}
```

```rb
[1, 2, 3].to_h { |num| [num, num * num] }
# => {1=>1, 2=>4, 3=>9}
```

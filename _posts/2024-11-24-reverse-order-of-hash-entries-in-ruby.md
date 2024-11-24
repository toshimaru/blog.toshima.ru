---
layout: post
title: "Reversing the Order of Hash Entries in Ruby"
tags: ruby
---

## What I want to do

I'd like to convert the Hash from

```rb
{1=>:a, 2=>:b, 3=>:c}
```

to:

```rb
{3=>:c, 2=>:b, 1=>:a}
```

## How to reverse the order of Hash

`reverse_each.to_h` is the way to reverse the order of Hash entries.

```rb
{ 1 => :a, 2 => :b, 3 => :c }.reverse_each.to_h #=> {3=>:c, 2=>:b, 1=>:a}
```

Or you could use `to_a.reverse.to_h` as well.

```rb
{ 1 => :a, 2 => :b, 3 => :c }.to_a.reverse.to_h #=> {3=>:c, 2=>:b, 1=>:a}
```

## Just sort by the key

FYI, if you just want to sort the Hash by the key, `sort.to_h` can be used.

```rb
{b: 2, a: 1, x: -1, c: 3}.sort.to_h #=> {:a=>1, :b=>2, :c=>3, :x=>-1}
```

## References

- [hashmap - Reverse a hash in Ruby - Stack Overflow](https://stackoverflow.com/questions/10874356/reverse-a-hash-in-ruby)

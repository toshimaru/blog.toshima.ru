---
layout: post
title: Create an Array of n items in Ruby
tags: ruby
---

- toc
{:toc}

## Create array of items

How can we create an array of 10 items in Ruby?

```rb
ary = []
10.times { |i| ary << i }
p ary # => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

This code can be refactored with `Array.new`:

```rb
Array.new(10) { |i| i }
# => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Create array with Array.new

The initial value is `nil`.

```rb
Array.new(3) #=> [nil, nil, nil]
```

## SymbolProc

```rb
Array.new(10, &:to_s)
# => ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
```

## Array of Array

```rb
Array.new(3) {Array.new(3)}
#=> [[nil, nil, nil], [nil, nil, nil], [nil, nil, nil]]
```

## Array of Hash

```rb
Array.new(4) {Hash.new}
#=> [{}, {}, {}, {}]
```

## Array of Object

```rb
Array.new(5, User.new)
=> [#<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>, #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>, #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>, #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>, #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>]
```

## Reference

[class Array - Documentation for Ruby 2.7.0](https://docs.ruby-lang.org/en/2.7.0/Array.html#class-Array-label-Creating+Arrays)

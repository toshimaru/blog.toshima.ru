---
layout: post
title: Convet lowercase to uppercase in Ruby
tags: ruby rails
---

## lowercase → uppercase

### upcase

Convert all letters to uppercase.

```rb
'hello'.upcase
#=> "HELLO"
```

### capitalize

Convert first letter to uppercase.

```rb
'hello'.capitalize
#=> "Hello"
```

### camelize

Convert snake case to camel case.

This method is provided by ActiveSupport.

```rb
'snake_case'.camelize
#=> "SnakeCase"
```

### lower camelize

Convert snake case to lower camel case.

This method is provided by ActiveSupport.

```rb
'snake_case'.camelize(:lower)
#=> "snakeCase"
```

## uppercase → lowercase

### downcase

Convert uppercase to lowercase.

```rb
'ABC'.downcase
#=> "abc"
```

### underscore

Conver camel case to snake case.

This method is provided by ActiveSupport.

```rb
'HelloWorld'.underscore
#=> "hello_world"
```

## swapcase

Swap letters.

```rb
'AbC'.swapcase
#=> "aBc"
```

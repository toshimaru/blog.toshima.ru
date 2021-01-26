---
layout: post
title: Remove line breaks from String in Ruby
tags: ruby rails
---

How do you remove line break from string in Ruby?

```rb
> puts "a\nb\nc"
a
b
c
```

## In Ruby

### delete

Just delete line breaks.

```rb
> "a\nb\nc".delete("\n")
=> "abc"
```

ref. (Japanese) [Array#delete](https://docs.ruby-lang.org/ja/latest/method/Array/i/delete.html)

### tr

Replace line breaks with tabs.

```rb
> "a\nb\nc".tr("\n", "\t")
=> "abc"
```

ref. (Japanese) [String#tr](https://docs.ruby-lang.org/ja/latest/method/String/i/tr.html)

## In Rails

### squish

In Rails, `squish` can be used. line breaks are replaced with white spaces.

```rb
> "a\nb\nc".squish
=> "a b c"
```

All whitespace characters are replaced with one white spaces.

```rb
> "   a\nb\tc   ".squish
=> "a b c"
```

ref. [String squish()](https://api.rubyonrails.org/classes/String.html#method-i-squish)

---
layout: post
title: Enable Ruby YJIT
tags: ruby
---

## Prerequisite

- Ruby 3.2
- Use `ruby:3.2` docker image

## Enable YJIT

You can enable Ruby YJIT by adding `RUBY_YJIT_ENABLE` environment variable.

```console
$ docker run ruby:3.2 bash -c "RUBY_YJIT_ENABLE=1 ruby -e 'p RubyVM::YJIT.enabled?'"
true

$ docker run ruby:3.2 bash -c "ruby -e 'p RubyVM::YJIT.enabled?'"
false
```

## Benchmark

Let's benchmark simple Ruby script to check how fast YJIT is.

Here is a simple recursive fibonacchi in Ruby:

```rb
def fibonacci(n)
  return n if n == 0 || n == 1

  fibonacci(n-2) + fibonacci(n-1)
end

puts fibonacci(45)
```

### Disable YJIT

```console
$ time ruby fibo.rb
1134903170

real	2m28.208s
user	2m28.174s
sys	0m0.029s
$ time ruby fibo.rb
1134903170

real	2m28.895s
user	2m28.853s
sys	0m0.034s
$ time ruby fibo.rb
1134903170

real	2m29.092s
user	2m29.051s
sys	0m0.034s
```

### Enable YJIT

```console
$ time RUBY_YJIT_ENABLE=1 ruby fibo.rb
1134903170

real	0m20.768s
user	0m20.738s
sys	0m0.029s
$ time RUBY_YJIT_ENABLE=1 ruby fibo.rb
1134903170

real	0m20.769s
user	0m20.737s
sys	0m0.031s
$ time RUBY_YJIT_ENABLE=1 ruby fibo.rb
1134903170

real	0m20.818s
user	0m20.785s
sys	0m0.030s
```

### Comparison

| Ruby 3.2 without YJIT | Ruby 3.2 with YJIT | Result |
| --- | --- | --- |
| 2m30s | 20s | **YJIT is 7x faster** |

## References

- [Install rust and enable yjit by eileencodes · Pull Request #40 · ruby/ruby-docker-images](https://github.com/ruby/ruby-docker-images/pull/40)

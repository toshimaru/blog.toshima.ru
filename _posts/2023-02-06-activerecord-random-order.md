---
layout: post
title: Get random records in Rails
tags: rails activerecord
---

## MySQL

```rb
User.order("RAND()").limit(10)
```

## PostgreSQL

```rb
User.order("RANDOM()").limit(10)
```

## Ruby Array#sample

```rb
User.where(id: User.ids.sample(10))
```

## Reference

- [What's the 'Rails 4 Way' of finding some number of random records? - Stack Overflow](https://stackoverflow.com/questions/17372886/whats-the-rails-4-way-of-finding-some-number-of-random-records)

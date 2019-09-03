---
layout: post
title: Explain SQL on Rails Console
tags: rails
---

Lets's say you'd like to explain the following SQL.

```ruby
> User.all
  User Load (0.9ms)  SELECT `users`.* FROM `users`
=> [#<User: ...snip...

> User.all.to_sql
=> "SELECT `users`.* FROM `users`"
```

All you need to do is adding `.explain` to the method.

```ruby
> User.all.explain
  User Load (0.6ms)  SELECT `users`.* FROM `users`
=> EXPLAIN for: SELECT `users`.* FROM `users`
+----+-------------+-------+------+---------------+------+---------+------+------+-------+
| id | select_type | table | type | possible_keys | key  | key_len | ref  | rows | Extra |
+----+-------------+-------+------+---------------+------+---------+------+------+-------+
|  1 | SIMPLE      | users | ALL  | NULL          | NULL | NULL    | NULL | xxxx |       |
+----+-------------+-------+------+---------------+------+---------+------+------+-------+
1 row in set (0.00 sec)
```

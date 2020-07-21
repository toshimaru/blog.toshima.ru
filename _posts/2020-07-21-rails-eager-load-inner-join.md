---
layout: post
title: "Rails eager_load with inner join"
tags: rails activerecord
---

* Table Of Contents
{:toc}

## `eager_load`

`eager_load` works with `LEFT OUTER JOIN`.

> Forces eager loading by performing a LEFT OUTER JOIN on args:
>
> ```rb
> User.eager_load(:posts)
> # SELECT "users"."id" AS t0_r0, "users"."name" AS t0_r1, ...
> # FROM "users" LEFT OUTER JOIN "posts" ON "posts"."user_id" =
> # "users"."id"
> ```

<https://railsdoc.github.io/classes/ActiveRecord/QueryMethods.html#method-i-eager_load>

But what about `inner join`?

## `eager_load` + `INNER JOIN`

### Model

Let's say you have the following Models.

```rb
class Tweet < ApplicationRecord
  belongs_to :user
end

class User < ApplicationRecord
  has_many :tweets
end
```

### Default `eager_load`

```rb
Tweet.eager_load(:user).to_sql
```

The output:

```sql
SELECT "tweets"."id" AS t0_r0, /*...snip...*/
FROM "tweets"
LEFT OUTER JOIN "users" ON "users"."id" = "tweets"."user_id"
```

### `eager_load` with `INNER JOIN`

Add `joins` before `eager_load`.

```rb
Tweet.joins(:user).eager_load(:user).to_sql
```

The output:

```sql
SELECT "tweets"."id" , /*...snip...*/
FROM "tweets"
INNER JOIN "users" ON "users"."id" = "tweets"."user_id"
```

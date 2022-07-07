---
layout: post
title: "Rails eager_load with inner join"
tags: rails activerecord
last_modified_at: 2022-07-08
---

* Table Of Contents
{:toc}

## Rails eager_load

Rails `eager_load` works with `LEFT OUTER JOIN` query.

> Forces eager loading by performing a LEFT OUTER JOIN on args:
>
> ```rb
> User.eager_load(:posts)
> # SELECT "users"."id" AS t0_r0, "users"."name" AS t0_r1, ...
> # FROM "users" LEFT OUTER JOIN "posts" ON "posts"."user_id" =
> # "users"."id"
> ```

[ActiveRecord::QueryMethods eager_load \| RailsDoc(β)](https://railsdoc.github.io/classes/ActiveRecord/QueryMethods.html#method-i-eager_load)

But what about `INNER JOIN`?

## eager_load + INNER JOIN

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

### Default eager_load

```rb
Tweet.eager_load(:user).to_sql
```

The SQL:

```sql
SELECT "tweets"."id" AS t0_r0, /*...snip...*/
FROM "tweets"
LEFT OUTER JOIN "users" ON "users"."id" = "tweets"."user_id"
```

`LEFT OUTER JOIN` is used.

### eager_load with INNER JOIN

Add `joins` before `eager_load`.

```rb
Tweet.joins(:user).eager_load(:user).to_sql
```

The SQL:

```sql
SELECT "tweets"."id" , /*...snip...*/
FROM "tweets"
INNER JOIN "users" ON "users"."id" = "tweets"."user_id"
```

`INNER JOIN` is used.

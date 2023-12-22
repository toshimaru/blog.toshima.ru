---
layout: post
title: Select Unique Values from a Column in ActiveRecord
tags: activerecord rails
last_modified_at: 2023-12-22
---

To retrieve unique values from a column in ActiveRecord, the `distinct` method combined with `pluck` can be utilized.

```rb
Model.distinct.pluck(:column)
```

For instance:

```rb
User.distinct.pluck(:id)
#    (0.1ms)  SELECT DISTINCT "users"."id" FROM "users"
```

This approach can also be extended to obtain unique values from multiple columns.

```rb
User.distinct.pluck(:id, :name)
#    (0.1ms)  SELECT DISTINCT "users"."id", "users"."name" FROM "users"
```

## API Document

[ActiveRecord::Calculations \| RailsDoc(β)](https://railsdoc.github.io/classes/ActiveRecord/Calculations.html#method-i-pluck)

> ```rb
> Person.distinct.pluck(:role)
> # SELECT DISTINCT role FROM people
> # => ['admin', 'member', 'guest']
> ```


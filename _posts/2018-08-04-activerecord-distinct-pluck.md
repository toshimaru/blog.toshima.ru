---
layout: post
title: Select Unique Values from a Column in ActiveRecord
tags: activerecord rails
---

IF you want to select unique values from a column in ActiveRecord, you can use `distinct` + `pluck`.

```rb
Model.distinct.pluck(:column)
```

For example:

```rb
User.distinct.pluck(:id)
#    (0.1ms)  SELECT DISTINCT "users"."id" FROM "users"
```

You can also get unique values from multiple columns.

```rb
User.distinct.pluck(:id, :name)
#    (0.1ms)  SELECT DISTINCT "users"."id", "users"."name" FROM "users"
```

## See also

- [activerecord - Rails: select unique values from a column - Stack Overflow](https://stackoverflow.com/questions/9658881/rails-select-unique-values-from-a-column)

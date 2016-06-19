---
layout: post
title: Show Active Record Model column names
tags: activerecord rails
---

Active Record provides a `column_names` method to show column names of a Model.


```rb
User.column_names
# => ["id", "name", "email", "password_digest", "created_at", "updated_at"]
```

## See also
* [sql - ActiveRecord: List columns in table from console - Stack Overflow](http://stackoverflow.com/questions/5575970/activerecord-list-columns-in-table-from-console)

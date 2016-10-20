---
layout: post
title: Build group_by and having query with ActiveRecord
tags: activerecord
---

Want to build query which has `group by` and `having`(like below) with ActiveRecord?

```sql
SELECT bar, count(*)  
FROM tables
GROUP BY foo, bar
HAVING count(*) > 1;
```

You can build it by using `group` and `having` which are `ActiveRecord::QueryMethods`.

```rb
ActiveRecordModel.group(:foo, :bar).having("count(*) > 1").count
```

## See also

- [ActiveRecord::QueryMethods - APIdock](http://apidock.com/rails/ActiveRecord/QueryMethods)

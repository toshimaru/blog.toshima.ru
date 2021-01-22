---
title: Filter MySQL processlist
tags: mysql
last_modified_at: 2021-01-22
---

You can see MySQL processes by querying `show processlist`.

```sql
show processlist;
-- or
show full processlist;
```

However, it can't be filtered. If you'd like to retrieve processes like usual SQL syntax, it can be replaced with:

```sql
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST;
```

Now, you can filter process with `WHERE` clause.

```sql
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST
WHERE
    DB = 'your_database_name' AND
    USER = 'username_runnning_query';
```

## Order by Time

```sql
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST
WHERE
    DB = 'development' AND
    USER = 'myuser'
ORDER BY TIME DESC;
```

## See also

* [how to customize `show processlist` in mysql? - Stack Overflow](https://stackoverflow.com/questions/929612/how-to-customize-show-processlist-in-mysql)
* [MySQL :: MySQL 8.0 Reference Manual :: 13.7.7.29 SHOW PROCESSLIST Statement](https://dev.mysql.com/doc/refman/8.0/en/show-processlist.html)

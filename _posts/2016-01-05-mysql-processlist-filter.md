---
title: Filter MySQL processlist
tags: mysql
---

You can see MySQL processes by `show processlist`.

```sql
show processlist;
-- Or
show full processlist;
```

But, it can't be filtered. If you'd like to retrieve processes like usual SQL syntax, it can be replaced with:

```sql
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST;
```

Now, you can filter process with `WHERE` clause.

```sql
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST
WHERE 
    DB = 'development' AND 
    USER = 'myuser';
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

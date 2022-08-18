---
layout: post
title: MySQL GROUP_CONCAT() Function
tags: mysql
---

## Create Data

Create a table named `tags`:

```
mysql> create table tags(
    ->   id bigint not null auto_increment primary key,
    ->   group_id integer not null,
    ->   name varchar(255) not null
    -> );
Query OK, 0 rows affected (0.01 sec)
```

Show data:

```
mysql> select * from tags;
+----+----------+------+
| id | group_id | name |
+----+----------+------+
|  1 |        1 | tag1 |
|  2 |        1 | tag2 |
|  3 |        1 | tag3 |
|  4 |        2 | TAG1 |
|  5 |        2 | TAG2 |
+----+----------+------+
5 rows in set (0.01 sec)
```

## GROUP_CONCAT()

A SQL with `group_concat`:

```sql
select group_id,
       count(*) as tag_count,
       group_concat(name)
from tags
group by group_id;
```

The result:

```
+----------+-----------+--------------------+
| group_id | tag_count | group_concat(name) |
+----------+-----------+--------------------+
|        1 |         3 | tag1,tag2,tag3     |
|        2 |         2 | TAG1,TAG2          |
+----------+-----------+--------------------+
2 rows in set (0.01 sec)
```

### Customize Separator

```sql
select group_id,
       count(*) as tag_count,
       group_concat(name SEPARATOR '/')
from tags
group by group_id;
```

```
+----------+-----------+--------------------+
| group_id | tag_count | group_concat(name) |
+----------+-----------+--------------------+
|        1 |         3 | tag1/tag2/tag3     |
|        2 |         2 | TAG1/TAG2          |
+----------+-----------+--------------------+
```

## Reference

- [MySQL :: MySQL 8.0 Reference Manual :: 12.20.1 Aggregate Function Descriptions](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_group-concat)

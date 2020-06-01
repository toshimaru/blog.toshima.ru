---
layout: post
title: MySQL ADD COLUMN statements
tags: mysql
---

## MySQL Version

MySQL 8.0

## Table Schema

```sql
CREATE TABLE users(
    id INTEGER NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);
-- Query OK, 0 rows affected
```

The result is:

```
> desc users
+-------+--------------+------+-----+---------+----------------+
| Field | Type         | Null | Key | Default | Extra          |
+-------+--------------+------+-----+---------+----------------+
| id    | int(11)      | NO   | PRI | <null>  | auto_increment |
| name  | varchar(255) | NO   |     | <null>  |                |
+-------+--------------+------+-----+---------+----------------+
```

## Add a column to the last field

```sql
ALTER TABLE users ADD COLUMN new_column1 VARCHAR(255);
```

The result is:

```
> desc users;
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| id          | int(11)      | NO   | PRI | <null>  | auto_increment |
| name        | varchar(255) | NO   |     | <null>  |                |
| new_column1 | varchar(255) | YES  |     | <null>  |                |
+-------------+--------------+------+-----+---------+----------------+
```

## Add a column to the first field

```sql
ALTER TABLE users ADD COLUMN new_column1 VARCHAR(255) FIRST;
```

The result is:

```
> desc users
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| new_column1 | varchar(255) | YES  |     | <null>  |                |
| id          | int(11)      | NO   | PRI | <null>  | auto_increment |
| name        | varchar(255) | NO   |     | <null>  |                |
+-------------+--------------+------+-----+---------+----------------+
```

## Add a column after another column


```sql
ALTER TABLE users ADD COLUMN new_column1 VARCHAR(255) AFTER id;
```

The result is:

```
> desc users
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| id          | int(11)      | NO   | PRI | <null>  | auto_increment |
| new_column1 | varchar(255) | YES  |     | <null>  |                |
| name        | varchar(255) | NO   |     | <null>  |                |
+-------------+--------------+------+-----+---------+----------------+
```

### What about "before"?

Let's use `BEFORE` instead of `AFTER`.

```sql
ALTER TABLE users ADD COLUMN new_column1 VARCHAR(255) BEFORE id;
-- (1064, "You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'BEFORE id' at line 1")
```

It causes syntax error!

**We can't use `BEFORE` for `ADD COLUMN` statement.**

## Reference

- [MySQL :: MySQL 8.0 Reference Manual :: 13.1.9 ALTER TABLE Statement](https://dev.mysql.com/doc/refman/8.0/en/alter-table.html)

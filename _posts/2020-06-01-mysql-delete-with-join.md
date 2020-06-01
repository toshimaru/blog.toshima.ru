---
layout: post
title: "[MySQL] Delete with join query"
tags: mysql
---

- toc
{:toc}

## Preparation

### Create Table

Create 2 tables.

```sql
CREATE TABLE users(
    id INTEGER NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

CREATE TABLE user_types(
    user_id INTEGER NOT NULL PRIMARY KEY,
    type INTEGER NOT NULL
);
```

### Create Data

Insert data to the tables.

```sql
-- users data
INSERT INTO users(name) values('name1');
INSERT INTO users(name) values('name2');
INSERT INTO users(name) values('name3');

-- user_types data
INSERT INTO user_types values(1, 1);
INSERT INTO user_types values(2, 2);
INSERT INTO user_types values(3, 3);
```

## Select data with join

```sql
select * from users join user_types on id = user_id where type = 2;
```

```
+----+-------+---------+------+
| id | name  | user_id | type |
+----+-------+---------+------+
|  2 | name2 |       2 |    2 |
+----+-------+---------+------+
```

## Delete data with join

### Error case

Just changing from `select` to `delete` doesn't work.

```sql
delete * from users join user_types on id = user_id where type = 2;
-- ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '* from users join user_types on id = user_id where type = 2' at line 1
```

### Success case

You need to add alias like `users u`.

```sql
delete u from users u join user_types on id = user_id where type = 2;
-- Query OK, 1 row affected (0.02 sec)
```

Make sure the data is deleted from `users` table.

```
mysql> select * from users join user_types on id = user_id;
+----+-------+---------+------+
| id | name  | user_id | type |
+----+-------+---------+------+
|  1 | name1 |       1 |    1 |
|  3 | name3 |       3 |    3 |
+----+-------+---------+------+
2 rows in set (0.00 sec)

mysql> select * from user_types;
+---------+------+
| user_id | type |
+---------+------+
|       1 |    1 |
|       2 |    2 |
|       3 |    3 |
+---------+------+
3 rows in set (0.00 sec)
```

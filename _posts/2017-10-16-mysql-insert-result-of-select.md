---
layout: post
title: "MySQL: Insert Result of Select query"
tags: mysql
last_modified_at: 2021-01-26
---

* toc
{:toc}

## Normal Insert

Use `INSERT INTO ~ VALUES ~` for normal insert query.

```sql
INSERT INTO
  table_name(col1, col2, ...)
VALUES
  (val1, val2, ...)
```

## Insert Result of Select query

Then, how can you insert result of select query?

You don't need to add `VALUES` after `INSERT INTO`.

Just add `SELECT` after `INSERT INTO`.

```sql
INSERT INTO
  table_name(col1, col2, ...)
SELECT
  col1, col2, ...
  FROM another_table_name;
```

## Reference

- [MySQL :: MySQL 8.0 Reference Manual :: 13.2.6 INSERT Statement](https://dev.mysql.com/doc/refman/8.0/en/insert.html)
- [MySQL :: MySQL 8.0 Reference Manual :: 13.2.6.1 INSERT ... SELECT Statement](https://dev.mysql.com/doc/refman/8.0/en/insert-select.html)

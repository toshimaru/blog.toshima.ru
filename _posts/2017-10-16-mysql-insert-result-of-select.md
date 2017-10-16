---
layout: post
title: "MySQL: Insert Result of Select query"
tags: mysql
---

You don't need to use `VALUES` after `INSERT INTO`. Just use `SELECT` after `INSERT INTO`.

```sql
INSERT INTO
  table_name(col1, col2, ...)
SELECT
  col1, col2, ...
  FROM another_table_name;
```

## Reference

- [MySQL :: MySQL 5.7 Reference Manual :: 13.2.5.1 INSERT ... SELECT Syntax](https://dev.mysql.com/doc/refman/5.7/en/insert-select.html)

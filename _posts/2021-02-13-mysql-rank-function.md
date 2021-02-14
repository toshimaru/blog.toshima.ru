---
layout: post
title: MySQL rank() function
tags: mysql
---

Since MySQL 8.0, `rank()` window function is available.

* Table Of Contents
{:toc}

## Table

```sql
CREATE TABLE scores (score INT)
```

```
select * from scores;
+-------+
| score |
+-------+
| 1     |
| 2     |
| 100   |
| 5     |
| 3     |
| 100   |
+-------+
```

## rank()

> Rank of current row within its partition, with gaps

```sql
select score, rank() over (order by score desc)
from scores
order by score desc;
```

```
+-------+-----------------------------------+
| score | rank() over (order by score desc) |
+-------+-----------------------------------+
| 100   | 1                                 |
| 100   | 1                                 |
| 5     | 3                                 |
| 3     | 4                                 |
| 2     | 5                                 |
| 1     | 6                                 |
+-------+-----------------------------------+
```

## dense_rank()

> Rank of current row within its partition, without gaps

```sql
select score, dense_rank() over (order by score desc)
from scores
order by score desc;
```

```
+-------+-----------------------------------------+
| score | dense_rank() over (order by score desc) |
+-------+-----------------------------------------+
| 100   | 1                                       |
| 100   | 1                                       |
| 5     | 2                                       |
| 3     | 3                                       |
| 2     | 4                                       |
| 1     | 5                                       |
+-------+-----------------------------------------+
```

## Reference

- [MySQL :: MySQL 8.0 Reference Manual :: 12.21.1 Window Function Descriptions](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html)

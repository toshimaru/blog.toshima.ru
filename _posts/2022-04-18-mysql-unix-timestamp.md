---
layout: post
title: "[mysql] Unix timestamp ⇔ datetime conversion"
tags: mysql
---


## Environment

- MySQL 8.0



## datetime → Unix timestamp

Get current datetime.

```console
mysql> select NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2022-04-18 06:15:07 |
+---------------------+
1 row in set (0.01 sec)
```

Convert from datetime to Unix timestamp.

```console
mysql> select UNIX_TIMESTAMP(NOW());
+-----------------------+
| UNIX_TIMESTAMP(NOW()) |
+-----------------------+
|            1650262556 |
+-----------------------+
1 row in set (0.01 sec)
```

## Unix timestamp → datetime

Convert from Unix timestamp to datetime.

```console
mysql> select FROM_UNIXTIME(1650262556);
+---------------------------+
| FROM_UNIXTIME(1650262556) |
+---------------------------+
| 2022-04-18 06:15:56       |
+---------------------------+
1 row in set (0.00 sec)
```

## Reference

- [MySQL :: MySQL 8.0 Reference Manual :: 12.7 Date and Time Functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)

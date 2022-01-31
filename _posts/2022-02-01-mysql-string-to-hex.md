---
layout: post
title: "Convert String to Hex in MySQL"
tags: mysql
---

## Environment

- mysql 5.7

## String to Hex

Use `HEX` to convert string to hex.

```sql
 select 'cat', HEX('cat');
```

	+-----+------------+
	| cat | HEX('cat') |
	+-----+------------+
	| cat | 636174     |
	+-----+------------+

## Hex to String


Use `X''` or `UNHEX()` to convert hex to string.

```sql
select 'cat', X'636174', UNHEX(636174);
```

	+-----+-----------+---------------+
	| cat | X'636174' | unhex(636174) |
	+-----+-----------+---------------+
	| cat | cat       | cat           |
	+-----+-----------+---------------+

## Reference

- [MySQL :: MySQL 5.7 Reference Manual :: 9.1.4 Hexadecimal Literals](https://dev.mysql.com/doc/refman/5.7/en/hexadecimal-literals.html)

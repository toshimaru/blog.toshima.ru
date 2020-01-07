---
layout: post
title: Run MySQL query from command line
tags: mysql bash
---

## MySQL Version

```console
$ mysql --version
mysql  Ver 8.0.18 for Linux on x86_64 (MySQL Community Server - GPL)
```

## Table output from command line

```console
$ mysql -u root -p -e "select User from mysql.user"
Enter password:
+------------------+
| User             |
+------------------+
| root             |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
+------------------+
```

## Table output without header from command line

```console
$ mysql -u root -p -N -e "select User from mysql.user"
Enter password:
+------------------+
| root             |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
+------------------+
```

## TSV output from command line

```console
$ mmysql -u root -p -B -e "select User, Host from mysql.user"
Enter password:
User	Host
root	%
mysql.infoschema	localhost
mysql.session	localhost
mysql.sys	localhost
root	localhost
```

## Reference

- [Japanese] [MySQLをコマンドラインから直接実行&出力形式の変更方法 - tkuchikiの日記](https://tkuchiki.hatenablog.com/entry/2012/11/30/114946)

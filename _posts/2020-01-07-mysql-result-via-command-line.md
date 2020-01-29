---
layout: post
title: Run MySQL query from command line
tags: mysql bash
---

* Table of Contents
{:toc}

## MySQL Version

```console
$ mysql --version
mysql  Ver 8.0.18 for Linux on x86_64 (MySQL Community Server - GPL)
```

**Use MySQL on Docker?**

See my another post: [Run and Connect to MySQL on Docker](/2018/09/16/docker-run-mysql.html)

## Table output from command line

Add `-e "SELECT QUERY ..."` to the mysql command.

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

Add `-N`.

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

Add `-B`.

```console
$ mysql -u root -p -B -e "select User, Host from mysql.user"
Enter password:
User	Host
root	%
mysql.infoschema	localhost
mysql.session	localhost
mysql.sys	localhost
root	localhost
```

## TSV output without header from command line

Add `-B` and `-N`.

```console
$  mysql -u root -p -B -N -e "select User, Host from mysql.user"
Enter password:
root	%
mysql.infoschema	localhost
mysql.session	localhost
mysql.sys	localhost
root	localhost
```

## Reference

- [Japanese] [MySQLをコマンドラインから直接実行&出力形式の変更方法 - tkuchikiの日記](https://tkuchiki.hatenablog.com/entry/2012/11/30/114946)

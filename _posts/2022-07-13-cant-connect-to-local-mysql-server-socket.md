---
layout: post
title: Can't connect to local MySQL server through socket
tags: mysql
---

## Connect to localhost

I was trying to connect to mysql on docker using `localhost`, but got an error.

```console
$ mysql -u root -h localhost
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```

## Connect to 127.0.0.1

Using `127.0.0.1` instead of `localhost` solves the issue.

```console
$ mysql -u root -h 127.0.0.1
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 8.0.28 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

## Why?

> when you connect to "localhost" the socket connector is used, but when you connect to "127.0.0.1" the TCP/IP connector is used.

[Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2) - Stack Overflow](https://stackoverflow.com/questions/4448467/cant-connect-to-local-mysql-server-through-socket-var-lib-mysql-mysql-sock)

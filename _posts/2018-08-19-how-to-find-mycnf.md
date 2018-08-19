---
layout: post
title: How to Find MySQL my.cnf file
tags: mysql
---

## MySQL Version

- MySQL 5.7

```console
$ mysql --version
mysql  Ver 14.14 Distrib 5.7.22, for osx10.13 (x86_64) using  EditLine wrapper
```

## How to find my.cnf

`mysql --help` outputs your possible `my.cnf` path. So, what you need to do is `grep my.cnf`.

```console
$ mysql --help | grep my.cnf
 order of preference, my.cnf, $MYSQL_TCP_PORT,
/etc/my.cnf /etc/mysql/my.cnf /usr/local/etc/my.cnf ~/.my.cnf
```

One of which is your MySQL configuration file(in this case, `/usr/local/etc/my.cnf`). 

```console
$ cat /usr/local/etc/my.cnf
# Default Homebrew MySQL server config
[mysqld]
# Only allow connections from localhost
bind-address = 127.0.0.1
```


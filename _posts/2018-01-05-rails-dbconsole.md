---
layout: post
title: Run Rails Database Console
tags: rails
---

## rails dbconsole

`rails dbconsole` opens database console for you based on your application `database.yml`.

```console
$ rails dbconsole
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 6
Server version: 5.6.x MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.00 sec)
```

This is useful to validate your `database.yml` configuration.


## rails db

You can also use `rails db` command.

```console
$ rails db
SQLite version 3.19.3 2017-06-27 16:48:08
Enter ".help" for usage hints.
sqlite>
```

## Reference

- [The Rails Command Line — Ruby on Rails Guides](http://guides.rubyonrails.org/command_line.html#rails-dbconsole)

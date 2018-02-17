---
layout: post
title: MySQL Load CSV Data into Table
tags: mysql
description: "If you want to import CSV data into MySQL table, it'd be good to use MySQL LOAD DATA INFILE. ref. MySQL :: MySQL 5.7 Reference Manual :: 13.2.6 LOAD DATA INFILE Syntax"
---

## Environment

- MySQL 5.7

## LOAD DATA INFILE

If you want to import CSV data into MySQL table, it'd be good to use MySQL `LOAD DATA INFILE`.

ref. [MySQL :: MySQL 5.7 Reference Manual :: 13.2.6 LOAD DATA INFILE Syntax](https://dev.mysql.com/doc/refman/5.7/en/load-data.html)

Let's use it on the command line.

```console
$ mysql -u root -e "LOAD DATA INFILE './data.csv' INTO TABLE db_development.users(email, password);"
ERROR 1290 (HY000) at line 1: The MySQL server is running with the --secure-file-priv option so it cannot execute this statement
```

But I've got an error, which says *The MySQL server is running with the --secure-file-priv option*.

## LOAD DATA LOCAL INFILE

[A stackoverflow answer](https://stackoverflow.com/a/40630313) says it's good to use `LOAD DATA LOCAL`.

```console
$ mysql -u root -e "LOAD DATA LOCAL INFILE './data.csv' INTO TABLE db_development.users(email, password);"
ERROR 1148 (42000) at line 1: The used command is not allowed with this MySQL version
```

Hmm, we've got another error, which says *The used command is not allowed with this MySQL version*.

## local-infile option

[Another answer](https://stackoverflow.com/a/10762399) says it should be used with `--local-infile` option.

```console
$ mysql -u root --local-infile -e "LOAD DATA LOCAL INFILE './data.csv' INTO TABLE db_development.users(email, password);"
```

It worked, but imported data was a bit wrong because I didn't specify fields separator. The CSV data was separated by comma(`,`), so let's specify comma.

```console
$ mysql -u root --local-infile -e "LOAD DATA LOCAL INFILE './data.csv' INTO TABLE db_development.users FIELDS TERMINATED BY ',' (email, password);"
```

It properly worked!

## Other Reference

- [MySQL :: MySQL 5.7 Reference Manual :: 4.2.4 Using Options on the Command Line](https://dev.mysql.com/doc/refman/5.7/en/command-line-options.html)

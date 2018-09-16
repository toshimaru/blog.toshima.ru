---
layout: post
title: Run MySQL on Docker and Connect to MySQL
tags: mysql docker 
---

I wanted to run MySQL 8.0.x on docker aside from MySQL 5.7 running on localhost, so I'll give a instruction for it.

## docker pull

First of all, let's run `docker pull`.

```
$ docker pull mysql:8.0
```

(`8.0` means a tag. if it's not specified, latest mysql docker image is used.)

## docker run

```
$ docker run --name mysql -e MYSQL_ROOT_PASSWORD=xxxx -p 3306:3306 mysql:8.0
```

`MYSQL_ROOT_PASSWORD` is required, you can set whatever password you like.

## Connect to MySQL

Let's conect to MySQL run by docker.

```console
$ mysql -h 127.0.0.1 -u root -p
Enter password:
ERROR 2059 (HY000): Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/Cellar/mysql/5.7.22/lib/plugin/caching_sha2_password.so, 2): image not found
```
But we've got an error. This is because mysql server version and client version are differenct and those encryption methods are differenct.

Let's connect to mysql on docker.

```console
# from localhost
$ docker exec -it mysql bash 

# inside docker
# mysql -uroot -p 
Enter password:

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

It works!


## Reference

- [mysql - Authentication plugin 'caching_sha2_password' cannot be loaded - Stack Overflow](https://stackoverflow.com/questions/49194719/authentication-plugin-caching-sha2-password-cannot-be-loaded)

---
layout: post
title: Run and Connect to MySQL on Docker
last_modified_at: 2019-07-26
tags: mysql docker
---

I wanted to run MySQL v8.0.x on docker aside from MySQL 5.7 running on my localhost, so I'll give a instruction for it.

## docker pull

First of all, let's run `docker pull` and pull MySQL v8.0 image.

```console
$ docker pull mysql:8.0
```

(`8.0` means a tag. if it's not specified, latest MySQL docker image is used.)

## docker run

Then, run `docker run`.

```console
$ docker run --name mysql -e MYSQL_ROOT_PASSWORD=xxxx -p 3306:3306 mysql:8.0
```

- `MYSQL_ROOT_PASSWORD` is required, you can set whatever password you like.
- `--name mysql` option assigns a name(`mysql`) to the container
- `-p 3306:3306` option publishes a container's `3306` port to the host

## Connect to MySQL

Finally, let's conect to MySQL running on the docker.

```console
$ mysql -h 127.0.0.1 -u root -p
Enter password:
ERROR 2059 (HY000): Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/Cellar/mysql/5.7.22/lib/plugin/caching_sha2_password.so, 2): image not found
```

But we've got an error. This is because **MySQL server version and client version are different** and those encryption methods are different.

Let's connect to mysql using mysql client on the docker.

```console
$ docker exec -it mysql bash
```

The folloing commands are run inside the docker.

```console
root@xxx:/# mysql --version
mysql  Ver 8.0.17 for Linux on x86_64 (MySQL Community Server - GPL)
root@xxx:/# mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.17 MySQL Community Server - GPL

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

It works!

## Reference

- [mysql - Authentication plugin 'caching_sha2_password' cannot be loaded - Stack Overflow](https://stackoverflow.com/questions/49194719/authentication-plugin-caching-sha2-password-cannot-be-loaded)
- [docker exec \| Docker Documentation](https://docs.docker.com/engine/reference/commandline/exec/)

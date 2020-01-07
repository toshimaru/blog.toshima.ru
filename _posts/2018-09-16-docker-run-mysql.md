---
layout: post
title: Run and Connect to MySQL on Docker
last_modified_at: 2020-01-08
tags: mysql docker
---

I wanted to run MySQL v8.0.x on Docker aside from MySQL v5.7 running on my localhost, so I'll give a instruction for it.

## docker pull

First of all, let's run `docker pull` and get MySQL v8.0 image.

```console
$ docker pull mysql:8.0
```

`8.0` means a tag. if it's not specified, latest MySQL docker image well be used.

## docker run

Then, run `docker run`.

```console
$ docker run --name mysql8 -e MYSQL_ROOT_PASSWORD={your_password} -p 3306:3306 mysql:8.0
```

- `MYSQL_ROOT_PASSWORD` is required, you can set whatever password you like
- `--name mysql` option assigns a name(`mysql`) to the container
- `-p 3306:3306` option publishes a container's `3306` port to the host
  - If you want to change port, change it to `-p 3307:3306`. Then, `3307` port is used

### Simple docker run

Just setting `MYSQL_ROOT_PASSWORD` is enough. :)

```console
$ docker run -e MYSQL_ROOT_PASSWORD={your_password} mysql:8.0
2020-01-07 16:06:52+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.18-1debian9 started.
2020-01-07 16:06:52+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2020-01-07 16:06:52+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.18-1debian9 started.
2020-01-07 16:06:52+00:00 [Note] [Entrypoint]: Initializing database files
```

## docker ps

```console
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
77ecf2eb0b98        mysql:8.0           "docker-entrypoint.s…"   8 seconds ago       Up 6 seconds        0.0.0.0:3306->3306/tcp, 33060/tcp   mysql8
```

You can see:

- image is `mysql:8.0`
- Name is `mysql8`
- Port setting is `0.0.0.0:3306->3306/`

## Connect to MySQL

Finally, let's connect to MySQL running on the docker.

```console
$ mysql -h 127.0.0.1 -u root -p
Enter password: {your_password}
ERROR 2059 (HY000): Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/Cellar/mysql/5.7.22/lib/plugin/caching_sha2_password.so, 2): image not found
```

But we've got an error. This is because **MySQL server version and client version are different** and those encryption methods are different.

Let's connect to mysql using mysql client on the docker.

```console
$ docker exec -it mysql8 bash
```

The following commands are run inside the docker.

```console
root@xxx:/# mysql --version
mysql  Ver 8.0.17 for Linux on x86_64 (MySQL Community Server - GPL)
root@xxx:/# mysql -uroot -p
Enter password: {your_password}
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

## Stop MySQL container

```console
$ docker stop mysql8
mysql8
```

## Remove created container

```console
$ docker rm mysql8
mysql8
```

## Reference

- [mysql - Authentication plugin 'caching_sha2_password' cannot be loaded - Stack Overflow](https://stackoverflow.com/questions/49194719/authentication-plugin-caching-sha2-password-cannot-be-loaded)
- [docker exec \| Docker Documentation](https://docs.docker.com/engine/reference/commandline/exec/)

---
layout: post
title: Connection Check with netcat(nc) command
tags: network bash
---

To test TCP connection with `nc` command, add `-v` and `-z` option.

```
$ nc -vz hostname port
```

- `-v`: verbose output
- `-z`: do not send data

```console
$  nc -vz blog.toshima.ru 80
Connection to blog.toshima.ru port 80 [tcp/http] succeeded!
```

```console
$ nc -vz blog.toshima.ru 443
Connection to blog.toshima.ru port 443 [tcp/https] succeeded!
```

```console
$ nc -vz blog.toshima.ru 443  
Connection to blog.toshima.ru port 443 [tcp/https] succeeded!
```

```console
$ nc -vzu 1.1.1.1 53
Connection to 1.1.1.1 port 53 [udp/domain] succeeded!
```

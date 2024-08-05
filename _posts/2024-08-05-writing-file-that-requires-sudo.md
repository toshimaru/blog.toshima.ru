---
layout: post
title: Writing to a file that requires sudo in one line
tags: linux bash
---

## The error

The following command does not work:

```console
$ sudo echo test >> /file/thare/requires/sudo
bash: /file/thare/requires/sudo: Permission denied
```

## The fixed command

Use `sudo tee -a` instead.

```console
$ echo test | sudo tee -a /file/thare/requires/sudo
```

For example:

```console
$ echo '127.0.0.1 localhost.example.com' | sudo tee -a /etc/hosts
```

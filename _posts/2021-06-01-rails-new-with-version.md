---
layout: post
title: Creating Rails project with a specific version
tags: rails
---

If you have some Rails versions installed, you may create new Rails project with a specific version.


## `rails new` command with version

You can do it with the following command.

```console
$ rails _x.y.z_ new appname
```

For example:


```console
$ gem list | grep rails
...
rails (6.1.3, 6.0.3, 5.2.3 ...)
...
```

```bash
# Create Rails 6.1 project
$ rails _6.1.3_ new rails6_1

# Create Rails 6.0 project
$ rails _6.0.3_ new rails6_0

# Create Rails 5.2 project
$ rails _5.2.3_ new rails5.2
```
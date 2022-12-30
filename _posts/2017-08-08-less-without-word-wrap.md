---
layout: post
title: Using less without word-wrap
tags: less linux
---

When you open up a file with less, word-wrap is sometimes annoying.

```console
$ less longtext.txt
```

![less1](/images/less1.png)

You can open it without word-wrap by passing `-S` option.

```console
$ less -S longtext.txt
```

![less2](/images/less2.png)

## Reference

- [linux - How to turn off word-wrap in less - Super User](https://superuser.com/questions/272818/how-to-turn-off-word-wrap-in-less)

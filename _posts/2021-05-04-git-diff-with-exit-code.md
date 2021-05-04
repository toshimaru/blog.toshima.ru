---
layout: post
title: git diff with exit code 1
tags: git
---

If there's a diff in `git diff`, I want the command to exit with an error.

That's when to use `--exit-code`.

> `--exit-code`
>
>    Make the program exit with codes similar to diff(1). That is, it exits with 1 if there were differences and 0 means no differences.

Let's try it.

```console
$ git diff --exit-code
diff --git a/_config.yml b/_config.yml
index e5c6d1aa..a2b7826c 100644
--- a/_config.yml
+++ b/_config.yml
@@ -1,3 +1,4 @@
+
 title: "Toshimaru's Blog"
 url: "https://blog.toshima.ru"
 description: >

$ echo $?
1
```

The exit code is `1` (error).

If no diff in `git diff`:

```console
$ git diff --exit-code

$ echo $?
0
```

The exit code is `0` (no error).

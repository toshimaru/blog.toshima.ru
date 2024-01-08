---
layout: post
title: Using git without a pager
tags: git
last_modified_at: 2024-01-08
---

Git employs a pager when you run commands like `git diff`, `git show`, `git grep`, etc.

If you prefer to view the results without a pager, simply add `--no-pager` or `-P`.

## `--no-pager` option

```console
$ git --no-pager diff
diff --git a/Gemfile b/Gemfile
index b413366f..9d9b8837 100644
--- a/Gemfile
+++ b/Gemfile
@@ -1,3 +1,5 @@
+# This is test diff
+
 source 'https://rubygems.org'

 gem 'jekyll', '~> 4.2'
...snip...
```

## `-P` option

```console
$ git -P grep Toshimaru
_config.yml:title: "Toshimaru's Blog"
_layouts/default.html:      <link type="application/atom+xml" rel="alternate" href="{{ site.url }}/feed/by_tag/{{ page.title }}.xml" title="Tag: {{ page.title }} - Toshimaru's Blog" />
_layouts/default.html:      © Toshimaru
...snip...
```

## Reference

[How do I prevent 'git diff' from using a pager? - Stack Overflow](https://stackoverflow.com/questions/2183900/how-do-i-prevent-git-diff-from-using-a-pager)

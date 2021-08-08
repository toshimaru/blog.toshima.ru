---
layout: post
title: "[rbenv] List installed/stable/available versions"
tags: ruby
---

* Table Of Contents
{:toc}

## Show current using Ruby version

```console
$ rbenv version
3.0.2 (set by /Users/toshimaru/.rbenv/version)
```

## List installed versions

```console
$ rbenv versions
  system
  2.6.5
  2.7.4
* 3.0.2 (set by /Users/toshimaru/.rbenv/version)
```

## List latest stable versions

```console
$ rbenv install -l
2.6.8
2.7.4
3.0.2
jruby-9.2.19.0
mruby-3.0.0
rbx-5.0
truffleruby-21.2.0
truffleruby+graalvm-21.2.0

Only latest stable releases for each Ruby implementation are shown.
Use 'rbenv install --list-all / -L' to show all local versions.
```

## List available versions

```console
$ rbenv install -L
1.8.5-p52
1.8.5-p113
1.8.5-p114
1.8.5-p115
1.8.5-p231
1.8.6
(...snip...)
2.7.4
3.0.0-dev
3.0.0-preview1
3.0.0-preview2
3.0.0-rc1
3.0.0
3.0.1
3.0.2
3.1.0-dev
(...snip...)
```

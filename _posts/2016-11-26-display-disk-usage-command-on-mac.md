---
layout: post
title: Display disk usage on macOS with du command
tags: mac bash
---

You can get disk usage on MacOS by using `du` command.

```
$ du -d 1 -h
200M  ./Amazon Music.app
6.1M  ./Android File Transfer.app
1.9M  ./App Store.app
...
```

`-d` option means depth. `du` outputs result for all files which is too much, so `-d 1` option is needed.

`-h` option means human-readable. This option add unit suffixes such as Byte, Kilobyte, Megabyte, Gigabyte.

## Filter by unit

If you want to filter result by unit:

```
du -d 1 -h | grep -e "\dG"
2.0G  ./iMovie.app
1.3G  ./iPhoto.app
8.2G  .
```

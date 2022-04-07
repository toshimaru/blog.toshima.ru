---
layout: post
title: Grep text recursively
tags: bash
---

## Grep text recursively in a current directory

The folloing command greps `grep_text` in a current directory.

```console
$ grep -r "grep_text" .
```

## Grep text recursively in a specific directory

The folloing command greps `grep_text` in `grep_directory` directory.

```console
$ grep -r grep_text grep_directory
```

## Grep text recursively and list only file names

The folloing command greps `grep_text` and list files which includes the text.

```console
$ grep -rl grep_text .
```

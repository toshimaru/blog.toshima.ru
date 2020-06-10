---
layout: post
title: Linux man Section Numbers
tags: linux unix mac bash
---

When you use \*nux `man` command, you'll see number after commands or system calls. e.g. `LS(1)`, `FORK(2)`.

What's this number? It's called **section number**.

The next question is, what does the section number actually mean?

## Section numbers

| section number | description |
| --- | --- |
| 1  | **Executable programs or shell commands**. |
| 2  | **System calls**. This functions are provided by the kernel. |
| 3  | **Library calls**. This functions are used as program libraries. |
| 4  | **Special files**. This is usually found in `/dev`.  |
| 5  | **File formats and conventions**, e.g. `/etc/passwd`.  |
| 6  | **Games**. |
| 7  | **Miscellaneous** (including macro packages and conventions), e.g. `man(7)`, `groff(7)` |
| 8  | **System administration commands**. This is usually only for root.  |
| 9  | **Kernel routines** [Non standard]  |

* This list is based on Linux `man` command (You can see it by runnning `man man`).

## See also

- [man page - Wikipedia](https://en.wikipedia.org/wiki/Man_page#Manual_sections)

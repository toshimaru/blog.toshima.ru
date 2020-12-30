---
layout: post
title: "Fix macOS Kernel Panic with Disabling auto graphic switching"
tags: mac
---

## Prerequisites

- macOS Catalina
- MacBook Pro 15-inch
- Graphics: Intel UHD Graphics

## Error

MacOS suddenly restarts with the following error:

```
Kernel Extensions in backtrace:
   com.apple.iokit.IOPCIFamily ...
```

## Solution

According to Apple Community, this seems an issue related "energy saver".

> Go to system preferences>energy saver and do the following for both battery and power adapter:
>
> 1) Disable auto graphic switching
> 2) Turn off Power Nap

ref. [Your computer was restarted because of a … - Apple Community](https://discussions.apple.com/thread/251233423?answerId=252366191022#252366191022)

Disabling auto graphic switching solves the issue.

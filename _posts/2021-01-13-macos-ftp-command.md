---
layout: post
title: Install ftp command on macOS with brew
tags: ftp macos
---

`ftp` command is removed since macOS High Sierra [for a security reason](https://discussions.apple.com/thread/8093031). `ftp` command can be installed with brew.

## Prerequisites

- macOS Catalina (v10.15)
- MacBook Pro
- brew

## Install

Just install `tnftp` with `brew`.

```console
$ brew Install tnftp
```

## Command Sample

```console
$ ftp -a 127.0.0.1 4481
```

`-a` means "Causes ftp to bypass normal login proce-dure, and use an anonymous login instead".

```console
$ ftp
ftp> help
Commands may be abbreviated.  Commands are:

!		edit		lpage		nlist		rcvbuf		struct
$		epsv		lpwd		nmap		recv		sunique
account		epsv4		ls		ntrans		reget		system
append		epsv6		macdef		open		remopts		tenex
ascii		exit		mdelete		page		rename		throttle
bell		features	mdir		passive		reset		trace
binary		fget		mget		pdir		restart		type
bye		form		mkdir		pls		rhelp		umask
case		ftp		mls		pmlsd		rmdir		unset
cd		gate		mlsd		preserve	rstatus		usage
cdup		get		mlst		progress	runique		user
chmod		glob		mode		prompt		send		verbose
close		hash		modtime		proxy		sendport	xferbuf
cr		help		more		put		set		?
debug		idle		mput		pwd		site
delete		image		mreget		quit		size
dir		lcd		msend		quote		sndbuf
disconnect	less		newer		rate		status
```

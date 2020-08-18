---
layout: post
title: DNS lookup with dig command
tags: network linux bash
---

`dig` is a DNS lookup command which can be used both Linux and macOS.

- toc
{:toc}

## dig domain

`dig` returns `A` record by default. Let's `dig` this blog.

```console
$ dig blog.toshima.ru

; <<>> DiG 9.10.6 <<>> blog.toshima.ru
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60414
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;blog.toshima.ru.		IN	A

;; ANSWER SECTION:
blog.toshima.ru.	299	IN	CNAME	toshimaru.github.io.
toshimaru.github.io.	2996	IN	A	185.199.108.153
toshimaru.github.io.	2996	IN	A	185.199.109.153
toshimaru.github.io.	2996	IN	A	185.199.110.153
toshimaru.github.io.	2996	IN	A	185.199.111.153

;; Query time: 42 msec
;; SERVER: 192.168.86.1#53(192.168.86.1)
;; WHEN: Tue Aug 18 09:53:40 JST 2020
;; MSG SIZE  rcvd: 141
```

`dig` answers `CNAME` record at first, then answers `A` record for `CNAME`.

### Answer Section Only

You can get only the answer section by using options:

```console
$ dig +noall +answer blog.toshima.ru
blog.toshima.ru.	284	IN	CNAME	toshimaru.github.io.
toshimaru.github.io.	3584	IN	A	185.199.111.153
toshimaru.github.io.	3584	IN	A	185.199.109.153
toshimaru.github.io.	3584	IN	A	185.199.108.153
toshimaru.github.io.	3584	IN	A	185.199.110.153
```

### Short Answer

Adding `+short` option returns shorter answer.

```console
$ dig +short blog.toshima.ru
toshimaru.github.io.
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

## Get another record with dig

Adding type allows you to get another record.

### MX record

```console
$ dig github.com mx

; <<>> DiG 9.10.6 <<>> github.com mx
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21563
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;github.com.			IN	MX

;; ANSWER SECTION:
github.com.		3476	IN	MX	1 aspmx.l.google.com.
github.com.		3476	IN	MX	10 alt3.aspmx.l.google.com.
github.com.		3476	IN	MX	10 alt4.aspmx.l.google.com.
github.com.		3476	IN	MX	5 alt1.aspmx.l.google.com.
github.com.		3476	IN	MX	5 alt2.aspmx.l.google.com.

;; Query time: 51 msec
;; SERVER: 192.168.86.1#53(192.168.86.1)
;; WHEN: Tue Aug 18 09:48:21 JST 2020
;; MSG SIZE  rcvd: 154
```

### TXT record

```console
$ dig github.com txt

; <<>> DiG 9.10.6 <<>> github.com txt
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 61063
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;github.com.			IN	TXT

;; ANSWER SECTION:
github.com.		3599	IN	TXT	"MS=6BF03E6AF5CB689E315FB6199603BABF2C88D805"
github.com.		3599	IN	TXT	"MS=ms44452932"
github.com.		3599	IN	TXT	"MS=ms58704441"
github.com.		3599	IN	TXT	"docusign=087098e3-3d46-47b7-9b4e-8a23028154cd"
github.com.		3599	IN	TXT	"v=spf1 ip4:192.30.252.0/22 ip4:208.74.204.0/22 ip4:46.19.168.0/23 include:_spf.google.com include:esp.github.com include:_spf.createsend.com include:servers.mcsv.net ~all"

;; Query time: 39 msec
;; SERVER: 192.168.86.1#53(192.168.86.1)
;; WHEN: Tue Aug 18 09:50:10 JST 2020
;; MSG SIZE  rcvd: 388
```

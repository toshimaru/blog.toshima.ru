---
layout: post
title: Generate Ed25519 SSH key
tags: ssh security
---

Using Ed25519 as SSH key is recommended because it has:

> High security level. This system has a 2^128 security target; breaking it has similar difficulty to breaking NIST P-256, RSA with ~3000-bit keys, strong 128-bit block ciphers, etc.

via. [Ed25519: high-speed high-security signatures](http://ed25519.cr.yp.to/)

## Environment

Mac OS X El Capitan

## SSH version

```
$ ssh -V
OpenSSH_6.9p1, LibreSSL 2.1.8
```

## Generate Ed25519 SSH

```
$ ssh-keygen -t ed25519
```

Output:

```
$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/toshi/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/toshi/.ssh/id_ed25519.
Your public key has been saved in /Users/toshi/.ssh/id_ed25519.pub.
The key fingerprint is:
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
The key's randomart image is:
+--[ED25519 256]--+
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
| xxx xxx xxx xxx |
+----[SHA256]-----+
```

Then, your private key should be at `~/.ssh/id_ed25519` and your public key should be at `~/.ssh/id_ed25519.pub`

## See also

- [EdDSA - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/EdDSA)

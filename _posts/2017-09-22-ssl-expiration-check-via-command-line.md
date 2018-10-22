---
layout: post
title: Check SSL Certificate Expiration Date via Command Line
description: If you wanna check SSL certificate expiration date for specific domain via command line, you can use openssl command. Let’s check google.com:443 certificate expiration date using openssl.
tags: ssl bash
---

If you wanna check SSL certificate expiration date for specific domain via command line, you can use `openssl` command.

Let's check `google.com:443` certificate expiration date using `openssl`.

```console
$ openssl s_client -connect google.com:443 -servername google.com < /dev/null 2> /dev/null | openssl x509 -text | grep "After"
            Not After : Dec  6 17:09:00 2017 GMT
```

`Dec  6 17:09:00 2017 GMT` is expiration date.

## Reference

- [OpenSSL: Check SSL Certificate Expiration Date and More - ShellHacks](https://www.shellhacks.com/openssl-check-ssl-certificate-expiration-date/)
- [Japanese] [Lambda を使って SSL サーバ証明書の有効期限をチェックする](https://blog.manabusakai.com/2016/07/lambda-cert-expire/)

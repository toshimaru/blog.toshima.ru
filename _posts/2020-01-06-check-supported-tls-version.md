---
layout: post
title: Check supported TLS version with openssl command
tags: tls ssl
---

1. Table of Contents
{:toc}

## Web TLS Checker

You can check if a specific version of TLS is supported with the following TLS Checker.

- [TLS Checker - Instant Results \| CDN77.com](https://www.cdn77.com/tls-test)
- [SSL Server Test (Powered by Qualys SSL Labs)](https://www.ssllabs.com/ssltest/)

## openssl command

You can also check supported TLS version by using `openssl s_client`.

```
$ openssl s_client -connect {domain}:443 -servername {domain} -tls{version}
```

If supported, valid SSL Certificate is shown.

```console
$ openssl s_client -connect google.com:443 -servername google.com -tls1
CONNECTED(00000005)
depth=2 OU = GlobalSign Root CA - R2, O = GlobalSign, CN = GlobalSign
verify return:1
depth=1 C = US, O = Google Trust Services, CN = GTS CA 1O1
verify return:1
depth=0 C = US, ST = California, L = Mountain View, O = Google LLC, CN = *.google.com
verify return:1
---
Certificate chain
 0 s:/C=US/ST=California/L=Mountain View/O=Google LLC/CN=*.google.com
   i:/C=US/O=Google Trust Services/CN=GTS CA 1O1
 1 s:/C=US/O=Google Trust Services/CN=GTS CA 1O1
   i:/OU=GlobalSign Root CA - R2/O=GlobalSign/CN=GlobalSign
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIJRDCCCCygAwIBAgIRAOXiH3ntcKfZAwAAAABmVK4wDQYJKoZIhvcNAQELBQAw
...(snip)...
rRUF99NVPWhf8+q+LIkUf60Gr2V3ZfVf
-----END CERTIFICATE-----
subject=/C=US/ST=California/L=Mountain View/O=Google LLC/CN=*.google.com
issuer=/C=US/O=Google Trust Services/CN=GTS CA 1O1
---
No client certificate CA names sent
Server Temp Key: ECDH, X25519, 253 bits
---
SSL handshake has read 3973 bytes and written 242 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-ECDSA-AES128-SHA
Server public key is 256 bit
Secure Renegotiation IS supported
```

If not supported, the following messages are shown.

```console
$ openssl s_client -connect yahoo.co.jp:443 -servername yahoo.co.jp -tls1
CONNECTED(00000006)
...
---
no peer certificate available
---
No client certificate CA names sent
---
SSL handshake has read 7 bytes and written 0 bytes
---
New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1
    Cipher    : 0000
    Session-ID:
    Session-ID-ctx:
    Master-Key:
    Start Time: 1578292633
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
---
```

### Check TLS v1 is supported

```console
$ openssl s_client -connect google.com:443 -servername google.com -tls1
```

### Check TLS v1.1 is supported

```console
$ openssl s_client -connect google.com:443 -servername google.com -tls1_1
```

### Check TLS v1.2 is supported

```console
$ openssl s_client -connect google.com:443 -servername google.com -tls1_2
```

## Related Post

- [Check SSL Certificate Expiration Date via Command Line \| Toshimaru’s Blog](/2017/09/22/ssl-expiration-check-via-command-line.html)

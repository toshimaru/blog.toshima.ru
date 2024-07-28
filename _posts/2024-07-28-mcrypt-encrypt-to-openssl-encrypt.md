---
layout: post
title: Convert mcrypt_encrypt to openssl_encrypt in PHP
tags: php
---

## `mcrypt_encrypt` is deprecated

The PHP function `mcrypt_encrypt` has been DEPRECATED as of PHP 7.1.0 and REMOVED as of PHP 7.2.0.

see. [PHP: mcrypt_encrypt - Manual](https://www.php.net/manual/en/function.mcrypt-encrypt.php)

## Use `openssl_encrypt` instead

> If you're writing code to encrypt/encrypt data in 2015, you should use openssl_encrypt() and openssl_decrypt(). The underlying library (libmcrypt) has been abandoned since 2007, and performs far worse than OpenSSL (which leverages AES-NI on modern processors and is cache-timing safe).
>
> <https://www.php.net/manual/en/function.mcrypt-encrypt.php#117667>

see. [PHP: openssl_decrypt - Manual](https://www.php.net/manual/en/function.openssl-decrypt.php)

##  `mcrypt_encrypt` with `MCRYPT_RIJNDAEL_128` and `MCRYPT_MODE_CBC`

```php
function my_mcrypt_encrypt($data) {
  $key = "my-crypt-key-123my-crypt-key-123";
  $iv = 'initial-vector-1';
  $encrypted_data = mcrypt_encrypt(MCRYPT_RIJNDAEL_128, $key, $data, MCRYPT_MODE_CBC, $iv);
  return base64_encode($encrypted_data);
}

function my_mcrypt_decrypt($encrypted_data) {
  $key = "my-crypt-key-123my-crypt-key-123";
  $iv = 'initial-vector-1';
  $encrypted_data = base64_decode($encrypted_data);
  $decrypted_data = mcrypt_decrypt(MCRYPT_RIJNDAEL_128, $key, $encrypted_data, MCRYPT_MODE_CBC, $iv);
  return rtrim($decrypted_data, "\0");
}

echo my_mcrypt_encrypt("test"); //eGjPLeYwcMiaaqAo8/zl3w==
echo my_mcrypt_decrypt("eGjPLeYwcMiaaqAo8/zl3w=="); //test
```

##  `openssl_encrypt` with `aes-256-cbc`

```php
function pad_zero($data) {
  $block_size = mcrypt_get_block_size(MCRYPT_RIJNDAEL_128, MCRYPT_MODE_CBC);
  $padding = $block_size - (strlen($data) % $block_size);
  return $data . str_repeat("\0", $padding);
}

function my_openssl_encrypt($data) {
  $key = "my-crypt-key-123my-crypt-key-123";
  $iv = 'initial-vector-1';
  $method = "aes-256-cbc";
  $encrypted_data = openssl_encrypt(pad_zero($data), $method, $key, OPENSSL_RAW_DATA|OPENSSL_ZERO_PADDING , $iv);
  return base64_encode($encrypted_data);
}

function my_openssl_decrypt($encrypted_data) {
  $key = "my-crypt-key-123my-crypt-key-123";
  $iv = 'initial-vector-1';
  $method = "aes-256-cbc";
  $encrypted_data = base64_decode($encrypted_data);
  $decrypted_data = openssl_decrypt($encrypted_data, $method, $key, OPENSSL_RAW_DATA | OPENSSL_ZERO_PADDING, $iv);
  return rtrim($decrypted_data, "\0"); // Remove padding
}

echo my_openssl_encrypt("test"); //eGjPLeYwcMiaaqAo8/zl3w==
echo my_openssl_decrypt("eGjPLeYwcMiaaqAo8/zl3w=="); //test
```

### 128? 256?

You may notice that the numbers of `RIJNDAEL_128` and `aes-256` are different, but they have different meanings.

- `128` is the block size (16 bytes = 128 bits)
- `256` is the key length (32 bytes = 256 bits)

### options

Available options are:

[PHP: Other Constants - Manual](https://www.php.net/manual/en/openssl.constants.other.php#constant.openssl-raw-data)

You can specify bitwise OR (`|`) of the flags.

## Function Tests

```php
php > echo my_mcrypt_encrypt("a");
0MiZj8BfOTSdHzVP4v6Wig==
php > echo my_openssl_encrypt("a");
0MiZj8BfOTSdHzVP4v6Wig==

php > echo my_mcrypt_encrypt("my encription string");
8D9rFmhRY3XtcP6j0aC+sGF5dK8GAHYbWnusgRdMxks=
php > echo my_openssl_encrypt("my encription string");
8D9rFmhRY3XtcP6j0aC+sGF5dK8GAHYbWnusgRdMxks=
```

## References

- [php AES-128-CBC mcrypt & openssl](https://gist.github.com/srsbiz/8373451ed3450c0548c3)
- [Convert PHP `mcrypt_encrypt` fucntion to `openssl_encrypt` function.](https://gist.github.com/toshimaru/255dd68850efdf2f7363667e1207d856)
- [Japanese][PHP 7.2で消えるMcryptの対処法を徹底解説！代替手段やOpenSLLへの移行方法は？インストール方法も再確認](https://freelance.shiftinc.jp/column/php--with-mcrypt)

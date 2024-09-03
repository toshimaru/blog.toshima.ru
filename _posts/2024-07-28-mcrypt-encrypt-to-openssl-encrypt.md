---
layout: post
title: Convert mcrypt_encrypt to openssl_encrypt in PHP
tags: php
last_modified_at: 2024-09-03
---

## `mcrypt_encrypt` is deprecated

The PHP function `mcrypt_encrypt` has been DEPRECATED as of PHP 7.1.0 and REMOVED as of PHP 7.2.0.

> **Warning**
This function has been DEPRECATED as of PHP 7.1.0 and REMOVED as of PHP 7.2.0. Relying on this function is highly discouraged.

ref. [PHP: mcrypt_encrypt - Manual](https://www.php.net/manual/en/function.mcrypt-encrypt.php)

## Use `openssl_encrypt` instead

> If you're writing code to encrypt/encrypt data in 2015, you should use `openssl_encrypt()` and `openssl_decrypt()`.
>
> <https://www.php.net/manual/en/function.mcrypt-encrypt.php#117667>

ref. [PHP: openssl_decrypt - Manual](https://www.php.net/manual/en/function.openssl-decrypt.php)

##  `mcrypt_encrypt` with `MCRYPT_RIJNDAEL_128` and `MCRYPT_MODE_CBC`

```php
<?php
function pad_zero($data) {
  $block_size = mcrypt_get_block_size(MCRYPT_RIJNDAEL_128, MCRYPT_MODE_CBC);
  $padding = $block_size - (strlen($data) % $block_size);
  return $data . str_repeat("\0", $padding);
}

function my_mcrypt_encrypt($data) {
  $key = pad_zero("my-key");
  $iv = pad_zero('my-iv');
  $encrypted_data = mcrypt_encrypt(MCRYPT_RIJNDAEL_128, $key, $data, MCRYPT_MODE_CBC, $iv);
  return base64_encode($encrypted_data);
}

function my_mcrypt_decrypt($encrypted_data) {
  $key = pad_zero("my-key");
  $iv = pad_zero('my-iv');
  $encrypted_data = base64_decode($encrypted_data);
  $decrypted_data = mcrypt_decrypt(MCRYPT_RIJNDAEL_128, $key, $encrypted_data, MCRYPT_MODE_CBC, $iv);
  return rtrim($decrypted_data, "\0");
}

echo my_mcrypt_encrypt("test"); //YcBFq1jPeN7rKB1WWLeZOA==
echo my_mcrypt_decrypt("YcBFq1jPeN7rKB1WWLeZOA=="); //test
```

##  `openssl_encrypt` with `aes-128-cbc`

```php
<?php
function pad_zero($data) {
  $block_size = openssl_cipher_iv_length("aes-128-cbc");
  $padding = $block_size - (strlen($data) % $block_size);
  return $data . str_repeat("\0", $padding);
}

function my_openssl_encrypt($data) {
  $key = pad_zero("my-key");
  $iv = pad_zero('my-iv');
  $method = "aes-128-cbc";
  $encrypted_data = openssl_encrypt(pad_zero($data), $method, $key, OPENSSL_RAW_DATA|OPENSSL_ZERO_PADDING , $iv);
  return base64_encode($encrypted_data);
}

function my_openssl_decrypt($encrypted_data) {
  $key = pad_zero("my-key");
  $iv = pad_zero('my-iv');
  $method = "aes-128-cbc";
  $encrypted_data = base64_decode($encrypted_data);
  $decrypted_data = openssl_decrypt($encrypted_data, $method, $key, OPENSSL_RAW_DATA | OPENSSL_ZERO_PADDING, $iv);
  return rtrim($decrypted_data, "\0"); // Remove padding
}

echo my_openssl_encrypt("test"); //YcBFq1jPeN7rKB1WWLeZOA==
echo my_openssl_decrypt("YcBFq1jPeN7rKB1WWLeZOA=="); //test
```

## AES vs RIJNDAEL


| Algorithm | Key Length (bytes) | IV Length (bytes) | Block Length (bytes) |
|---------- |------- |------------- | --- |
| **AES-128**         | 16  | 16 | 16 |
| **AES-192**         | 24  | 16 | 16 |
| **AES-256**         | 32  | 16 | 16 |
| **Rijndael-128**    | 16/24/32  | 16 | 16 |
| **Rijndael-192**    | 16/24/32  | 24 | 24 |
| **Rijndael-256**    | 16/24/32  | 32 | 32 |

ref. [Japanese (My Japanese Blog)] [2024-08-27 AES vs Rijndael \| TTIL](https://til.toshimaru.net/2024-08-27)

### options

Available options are:

1. `OPENSSL_RAW_DATA` (int)
2. `OPENSSL_DONT_ZERO_PAD_KEY` (int)
3. `OPENSSL_ZERO_PADDING` (int)
4. `OPENSSL_ENCODING_SMIME` (int)
5. `OPENSSL_ENCODING_DER` (int)
6. `OPENSSL_ENCODING_PEM` (int)

ref. [PHP: Other Constants - Manual](https://www.php.net/manual/en/openssl.constants.other.php#constant.openssl-raw-data)

You can specify bitwise OR (`|`) of the flags.

## Function Tests

The results are the same.

```php
php > echo my_mcrypt_encrypt("a");
hxHEroQFXNwHMXeCaO8Oyw==
php > echo my_openssl_encrypt("a");
hxHEroQFXNwHMXeCaO8Oyw==
```

```php
php > echo my_mcrypt_encrypt("my encription string");
xYsMYUYqNXe7MKJWKUHseEp/SShKk48idzhTC43cYK4=
php > echo my_openssl_encrypt("my encription string");
xYsMYUYqNXe7MKJWKUHseEp/SShKk48idzhTC43cYK4=
```

## References

- [php AES-128-CBC mcrypt & openssl](https://gist.github.com/srsbiz/8373451ed3450c0548c3)
- [Convert PHP `mcrypt_encrypt` fucntion to `openssl_encrypt` function.](https://gist.github.com/toshimaru/255dd68850efdf2f7363667e1207d856)
- [Japanese][PHP 7.2で消えるMcryptの対処法を徹底解説！代替手段やOpenSLLへの移行方法は？インストール方法も再確認](https://freelance.shiftinc.jp/column/php--with-mcrypt)

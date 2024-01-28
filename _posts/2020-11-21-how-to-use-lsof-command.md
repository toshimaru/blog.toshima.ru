---
layout: post
title: How to use lsof command
tags: linux
last_modified_at: 2024-01-28
redirect_from: /2020/11/21/new-lsof-command.html
---

## What is lsof command?

`lsof` command is used to list open files. The word `lsof` is a combination of list (`ls`) and open files (`of`).

## list open files by pid

```console
$ lsof -p {pid}
```

Let's list files after runnning `irb`((Interactive Ruby) as an example.

```console
$ irb
irb(main):001:0> Process.pid
=> 16340
```

```console
$ lsof -p 16340
COMMAND   PID      USER   FD   TYPE             DEVICE SIZE/OFF                NODE NAME
ruby    16340 toshimaru  cwd    DIR                1,4     2720              633342 /Users/toshimaru
ruby    16340 toshimaru  txt    REG                1,4    13320          8621866282 /Users/toshimaru/.rbenv/versions/2.7.1/bin/ruby
ruby    16340 toshimaru  txt    REG                1,4  4258012          8621866283 /Users/toshimaru/.rbenv/versions/2.7.1/lib/libruby.2.7.dylib
ruby    16340 toshimaru  txt    REG                1,4   419040          8619930286 /usr/local/Cellar/gmp/6.2.0/lib/libgmp.10.dylib
ruby    16340 toshimaru  txt    REG                1,4    17388          8621866350 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/enc/encdb.bundle
ruby    16340 toshimaru  txt    REG                1,4    17020          8621866365 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/enc/trans/transdb.bundle
ruby    16340 toshimaru  txt    REG                1,4    16416          8621866400 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/monitor.bundle
ruby    16340 toshimaru  txt    REG                1,4   273648          8621866311 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/ripper.bundle
ruby    16340 toshimaru  txt    REG                1,4    45420          8621866414 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/readline.bundle
ruby    16340 toshimaru  txt    REG                1,4   239260          8620006484 /usr/local/Cellar/readline/8.0.4/lib/libreadline.8.0.dylib
ruby    16340 toshimaru  txt    REG                1,4    36552          8621866309 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/io/console.bundle
ruby    16340 toshimaru  txt    REG                1,4    50512          8621866306 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/pathname.bundle
ruby    16340 toshimaru  txt    REG                1,4    33124          8621866295 /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0/x86_64-darwin19/etc.bundle
ruby    16340 toshimaru  txt    REG                1,4  1568368 1152921500312682291 /usr/lib/dyld
ruby    16340 toshimaru    0u   CHR               16,6   0t1027                5123 /dev/ttys006
ruby    16340 toshimaru    1u   CHR               16,6   0t1027                5123 /dev/ttys006
ruby    16340 toshimaru    2u   CHR               16,6   0t1027                5123 /dev/ttys006
ruby    16340 toshimaru    3   PIPE 0xe9b98e34a50c0958    16384                     ->0x5234dd6eed3ba038
ruby    16340 toshimaru    4   PIPE 0x5234dd6eed3ba038    16384                     ->0xe9b98e34a50c0958
ruby    16340 toshimaru    5   PIPE 0x25bac2bfb3b4d94d    16384                     ->0x33b50c39b0670301
ruby    16340 toshimaru    6   PIPE 0x33b50c39b0670301    16384                     ->0x25bac2bfb3b4d94d
ruby    16340 toshimaru    7   PIPE 0xbe80cf7b978688af    16384                     ->0x5fac99197a7632cb
ruby    16340 toshimaru    8   PIPE 0x5fac99197a7632cb    16384                     ->0xbe80cf7b978688af
```

- `FD`
  - `cwd`: current working directory
  - `txt`: text
  - `0`, `1`, `2`: stdin, stdout, stderr respectively (and `u` means read/write access)
- `TYPE`
  - `DIR`: directory
  - `REG`: regular file
  - `CHR`: character special file

## lsof by port

```console
$ lsof -i:{port}
```

Let's see the result after runnning `rails server` (which uses port 3000 by default) as an example.

```console
$ lsof -i:3000
COMMAND   PID      USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ruby    18077 toshimaru   14u  IPv4 0xc33ab1611224e4b5      0t0  TCP localhost:hbci (LISTEN)
ruby    18077 toshimaru   15u  IPv6 0xc33ab160fc2911e5      0t0  TCP localhost:hbci (LISTEN)
```

I prefer port number to port name, so add `-P` option.

```console
$ lsof -Pi:3000
COMMAND   PID      USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ruby    18077 toshimaru   14u  IPv4 0xc33ab1611224e4b5      0t0  TCP localhost:3000 (LISTEN)
ruby    18077 toshimaru   15u  IPv6 0xc33ab160fc2911e5      0t0  TCP localhost:3000 (LISTEN)
```

## lsof by file

```console
$ lsof {filepath}
```

```console
$ lsof log/development.log
COMMAND   PID      USER   FD   TYPE DEVICE SIZE/OFF       NODE NAME
ruby    18077 toshimaru   10w   REG    1,4 20287686 8591532843 log/development.log
```

## lsof by process name

```console
$ lsof -c {process_name}
```

```console
$ lsof -c ruby
COMMAND   PID      USER   FD     TYPE             DEVICE SIZE/OFF                NODE NAME
ruby    18077 toshimaru  cwd      DIR                1,4      992          8591531532 /Users/toshimaru/src/github.com/toshimaru/RailsTwitterClone
ruby    18077 toshimaru  txt      REG                1,4    13320          8621866282 /Users/toshimaru/.rbenv/versions/2.7.1/bin/ruby
(...snip...)
```

## See Also

- [lsof command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/#:~:text=lsof%20command%20stands%20for%20List,open%20files%20in%20output%20console.)
- [Lsof – A Unix Utility You Should Know About](https://catonmat.net/unix-utilities-lsof)
- [macos - Who is listening on a given TCP port on Mac OS X? - Stack Overflow](https://stackoverflow.com/questions/4421633/who-is-listening-on-a-given-tcp-port-on-mac-os-x?rq=1)

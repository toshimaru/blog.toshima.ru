---
layout: post
title: Installing MySQL 5.7 on CircleCI
tags: circleci mysql
---

CircleCI doesn't support MySQL 5.7 by default.

[kimh](https://discuss.circleci.com/users/kimh/activity), CircleCI employee, created a script to install MySQL 5.7 on CircleCI.

To use this script, add below configuration to your `circle.yml`:

```yml
dependencies:
  pre:
    - curl -sSL https://s3.amazonaws.com/circle-downloads/install-mysql5.7-circleci.sh | sh
```

The output on CircleCI is:

```
(snip)
..
 * MySQL Community Server 5.7.8-rc is started
Setting up mysql-server (5.7.8-rc-1ubuntu12.04) ...
+ echo Checking installed version.....
Checking installed version.....
+ mysql -D mysql -e SELECT version()
version()
5.7.8-rc
+ echo Done!!
Done!!
```

Then, you can use MySQL 5.7 on CircleCI container.

See also
---
- [Installing MySQL 5.7 - Build Environment - CircleCI Community Discussion](https://discuss.circleci.com/t/installing-mysql-5-7/1021)

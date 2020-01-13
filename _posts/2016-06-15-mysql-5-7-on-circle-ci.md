---
layout: post
title: Installing MySQL 5.7 on CircleCI
description: CircleCI doesn’t support MySQL 5.7 by default. To install MySQL 5.7, add below configuration to your circle.yml.
tags: circleci mysql
---

## [UPDATE 2]

Current best approach is changing CircleCI **Build Environment** to the latest version which is `Ubuntu 14.04`.

[Ubuntu 14.04 (Trusty) - CircleCI](https://circleci.com/docs/build-image-trusty/)

This build image has MySQL 5.7.x by default.

## [UPDATE]

[Original script](https://s3.amazonaws.com/circle-downloads/install-mysql5.7-circleci.sh) currently doesn't work because it refers to `mysql-5.7-dmr`[^1] which is outdated.

Please use [my forked script](https://gist.github.com/toshimaru/06ffbf2e8ad7d4e3dab889fa27681835/).

The raw source is: <https://gist.githubusercontent.com/toshimaru/06ffbf2e8ad7d4e3dab889fa27681835/raw/install-mysql5.7-circleci.sh>

---

CircleCI doesn't support MySQL 5.7 by default.

[kimh](https://discuss.circleci.com/users/kimh/activity), CircleCI employee, created a script to install MySQL 5.7 on CircleCI.

To use this script, add below configuration to your `circle.yml`:

```yml
dependencies:
  pre:
    - curl -sSL https://gist.githubusercontent.com/toshimaru/06ffbf2e8ad7d4e3dab889fa27681835/raw/install-mysql5.7-circleci.sh | sh
```

The output on CircleCI is:

```
(snip)
..
* MySQL Community Server 5.7.14 is started
Setting up mysql-server (5.7.14-1ubuntu12.04) ...
Setting up libmysqlclient20 (5.7.14-1ubuntu12.04) ...
Setting up libmysqlclient-dev (5.7.14-1ubuntu12.04) ...
Processing triggers for libc-bin ...
ldconfig deferred processing now taking place
+ echo Checking installed version.....
Checking installed version.....
+ mysql -D mysql -e SELECT version()
version()
5.7.14
+ echo Done!!
Done!!
```

Then, you can use MySQL 5.7 on CircleCI container.

See also
---

- [Installing MySQL 5.7 - Build Environment - CircleCI Community Discussion](https://discuss.circleci.com/t/installing-mysql-5-7/1021)

[^1]: DMR means development milestone release. ref. [MySQL :: MySQL Development Cycle :: 6 Development Milestone Releases](https://dev.mysql.com/doc/mysql-development-cycle/en/development-milestone-releases.html)

---
layout: post
title: How to rollback migration in Rails
tags: rails activerecord
---

* table of contents
{:toc}

## Rollback last migration

```console
$ rails db:rollback STEP=1
```

If you specify `STEP=2`, the last two migrations are rollbacked.

## Rollback specific migration

You can rollback a specific migration with `db:migrate:down` and `VERSION=xxxx`.

```console
$ rails db:migrate:down VERSION=20200905201547
```

if you want to run the migration again:

```console
$ rails db:migrate:up VERSION=20200905201547
```

## Check migration status

You can check your migrations are up or down with `db:migrate:status`.

```console
$ rails db:migrate:status
Status   Migration ID    Migration Name
--------------------------------------------------
  up     20190307124026  Create users
  up     20190315090930  Add index to users email
 down    20190315xxxxxx  xxxx
```

## Migration down and up

You can run `db:migrate:down` and `db:migrate:up` with one command, which is `db:migrate:redo`.

```console
$ rails db:migrate:redo VERSION=20200905201547
```

You can check if a specific migration is reversible. If not, [ActiveRecord::IrreversibleMigration](https://railsdoc.github.io/classes/ActiveRecord/IrreversibleMigration.html) error will be raised.

## Reference

[ruby on rails - How to rollback a specific migration? - Stack Overflow](https://stackoverflow.com/questions/3647685/how-to-rollback-a-specific-migration)

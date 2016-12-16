---
layout: post
title: mysqldump command for existing Rails app
tags: mysql rails
---

## Environment

- Rails 5.0.0.1

## How to export dump.sql using mysqldump

The following command generates `dump.sql` for existing Rails app.

```bash
mysqldump -u {USER_NAME} -h {HOST_NAME} -p --no-create-info --ignore-table=DATABASE_NAME.schema_migrations --ignore-table=DATABASE_NAME.ar_internal_metadata {DATABASE_NAME} > dump.sql
```

### Variables

Change following variables depending on your environment.

- `USER_NAME`: database user name
- `HOST_NAME`: MySQL host name
- `DATABASE_NAME`: your rails app database name

### Command explanation

`--no-create-info` flag means do not include `CREATE TABLE` information. It's needed because we already have create table information file in Rails `schema.rb`.

`--ignore-table` is needed to ignore those two tables.

- `schema_migrations`: This table has version information(e.g. `20161205083433`)
- `ar_internal_metadata`: This table has your Rails app environment information

These are automatically created by Rails, so you don't need it.

## How to import dump.sql

```
$ bundle exec rails db:reset
$ mysql -u root DATABASE_NAME < ./dump.sql
```

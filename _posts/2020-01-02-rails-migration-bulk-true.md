---
layout: post
title: Rails Bulk Migration
tags: rails activerecord
---

Schema change on RDB might be a dangerous operation.

That's the same as Rails, so it's important to run migrations with `bulk` option.

This article explains how `bulk` option changes the schema change operation.

## User table schema

This is `users` table for a sample.

```
mysql> desc users;
+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| id         | bigint(20)   | NO   | PRI | NULL    | auto_increment |
| name       | varchar(255) | YES  |     | NULL    |                |
| created_at | datetime(6)  | NO   |     | NULL    |                |
| updated_at | datetime(6)  | NO   |     | NULL    |                |
+------------+--------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)
```

## Migration without bulk option

Let's add three columns named `new_column1`, `new_column2` and `new_column3`.

```console
$ bundle exec rails g migration addColumnsToUser new_column1:integer new_column2:string new_column3:boolean
Running via Spring preloader in process 408
      invoke  active_record
      create    db/migrate/20200101164105_add_columns_to_user.rb
```

The migration file is the following:

```rb
class AddColumnsToUser < ActiveRecord::Migration[6.0]
  def change
    add_column :users, :new_column1, :integer
    add_column :users, :new_column2, :string
    add_column :users, :new_column3, :boolean
  end
end
```

Run `db:migrate`.

```console
$ bundle exec rails db:migrate
== 20200101164105 AddColumnsToUser: migrating =================================
-- add_column(:users, :new_column1, :integer)
   -> 0.2708s
-- add_column(:users, :new_column2, :string)
   -> 0.0496s
-- add_column(:users, :new_column3, :boolean)
   -> 0.0347s
== 20200101164105 AddColumnsToUser: migrated (0.3771s) ========================
```

As you can see, `add_column`, which may be a dangerous operation, is invoked three times.

## Migration with bulk option

Let't create a migration with `bulk` option.

Modify the migration file like below:

```rb
class AddColumnsToUser < ActiveRecord::Migration[6.0]
  def change
    change_table :users, bulk: true do |t|
      t.integer :new_column1
      t.string  :new_column2
      t.boolean :new_column3
    end
  end
end
```

`bulk: true` means the schema change will be squashed into one.

Run `db:migrate`.

```console
$ bundle exec rails db:migrate
== 20200101164105 AddColumnsToUser: migrating =================================
-- change_table(:users, {:bulk=>true})
   -> 0.1296s
== 20200101164105 AddColumnsToUser: migrated (0.1300s) ========================
```

Yes! `change_table` is invoked just one time!

---
layout: post
title: Rails Bulk Migration
tags: rails activerecord
last_modified_at: 2023-09-20
---

Schema changes in RDB can be dangerous operations.

The same is true for Rails, so it's important to run migrations with the `bulk` option.

This article explains how the `bulk` option affects Rails migrations.

* Table Of Contents
{:toc}

## Prerequisites

- Rails 6.0
- MySQL 8.0

## User table schema

Here is the `users` table schema for reference:

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

## Migration without the `bulk` option

Let's add three columns named `new_column1`, `new_column2` and `new_column3`.

```console
$ bundle exec rails g migration addColumnsToUser new_column1:integer new_column2:string new_column3:boolean
      invoke  active_record
      create    db/migrate/20200101164105_add_columns_to_user.rb
```

The generated migration file is as follows:

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

As you can see, `add_column`, which can be a dangerous operation, is invoked three times. This is not ideal.

## Migration with `bulk` option

Let's modify the migration to include the `bulk` option.

Edit the migration file as follows:

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

Using `bulk: true` means that all the schema changes will be batched into one operation.

Run `db:migrate`.

```console
$ bundle exec rails db:migrate
== 20200101164105 AddColumnsToUser: migrating =================================
-- change_table(:users, {:bulk=>true})
   -> 0.1296s
== 20200101164105 AddColumnsToUser: migrated (0.1300s) ========================
```

Great! `change_table` is invoked only once!

### The `after` Option Is Available

Tip: `after` option is also available in bulk migration.

```rb
class AddColumnsToUser < ActiveRecord::Migration[6.0]
  def change
    change_table :users, bulk: true do |t|
      t.integer :new_column1, after: existing_column1
      t.string  :new_column2, after: existing_column2
    end
  end
end
```

## Add indexes with the `bulk` option

You can also add indexes with the `bulk` option.

```rb
class AddIndexesToUsers < ActiveRecord::Migration[7.1]
  def change
    # Good migration
    change_table :users, bulk: true do |t|
      t.index :first_name
      t.index :last_name
    end

    # Bad migration
    # add_index :users, :first_name
    # add_index :users, :last_name
  end
end
```

Run `db:migrate`.

```
== 20230920001834 AddIndexesToUsers: migrating ================================
-- change_table(:users, {:bulk=>true})
   -> 0.0068s
== 20230920001834 AddIndexesToUsers: migrated (0.0069s) =======================
```

---
layout: post
title: Rails can create a table having composite primary key
tags: rails
---

Rails is able to create a table which has composite primary key without a gem.

This is documented in Rails like below:

```rb
create_table(:orders, primary_key: [:product_id, :client_id]) do |t|
  t.belongs_to :product
  t.belongs_to :client
end
```

ref. [Document support for composite primary keys by Nerian · Pull Request #29135 · rails/rails](https://github.com/rails/rails/pull/29135)

## Create composite primary key

Let's create a table having composite primary key step by step.

First, generate migration file which has two types of `id` columns.

```console
$ rails generate migration createRelationship follower_id:bigint followed_id:bigint
      invoke  active_record
      create    db/migrate/20190905xxxxxx_create_relationship.rb
```

The created file is like this:

```rb
#  db/migrate/20190905xxxxxx_create_relationship.rb
class CreateRelationship < ActiveRecord::Migration[5.2]
  def change
    create_table :relationships do |t|
      t.bigint :follower_id
      t.bigint :followed_id
    end
  end
end
```

What we'd like to do is creating a composite primary key of `follower_id` and `followed_id`.

So, add `primary_key` option and pass Array of composite primary key as a value.

```rb
#  db/migrate/20190905xxxxxx_create_relationship.rb
class CreateRelationship < ActiveRecord::Migration[5.2]
  def change
    create_table :relationships, primary_key: [:follower_id, :followed_id] do |t|
      t.bigint :follower_id
      t.bigint :followed_id
    end
  end
end
```

After running `rails db:migrate`, you can see composite primary key in the table. This is a created schema on my local MySQL.

```
mysql> desc relationships;
+-------------+------------+------+-----+---------+-------+
| Field       | Type       | Null | Key | Default | Extra |
+-------------+------------+------+-----+---------+-------+
| follower_id | bigint(20) | NO   | PRI | NULL    |       |
| followed_id | bigint(20) | NO   | PRI | NULL    |       |
+-------------+------------+------+-----+---------+-------+
```

This is composite primary key, so:

- You can't insert `null`
- You can't insert same record 

```
insert relationships values  (null, null);
ERROR 1048 (23000): Column 'follower_id' cannot be null
mysql> insert relationships values  (1, 1);
Query OK, 1 row affected (0.01 sec)
mysql> insert relationships values  (1, 1);
ERROR 1062 (23000): Duplicate entry '1-1' for key 'PRIMARY'
```

## Heads-up

ActiveRecord can't find composite primary key record since it does not support.

```
irb> Relationship.find(1)
WARNING: Active Record does not support composite primary key.

relationships has composite primary key. Composite primary key is ignored.
Traceback (most recent call last):
        1: from (irb):2
ActiveRecord::UnknownPrimaryKey (Unknown primary key for table relationships in model Relationship.)
```

If you want to get composite primary key support, use [composite_primary_keys](https://github.com/composite-primary-keys/composite_primary_keys) gem.

## Reference

- [ActiveRecord::ConnectionAdapters::SchemaStatements - Create a composite primary key \| RailsDoc(β)](https://railsdoc.github.io/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-create_table-label-Create+a+composite+primary+key)

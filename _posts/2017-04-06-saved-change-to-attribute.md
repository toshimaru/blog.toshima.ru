---
layout: post
title: Use saved_change_to_attribute? instead of attribute_changed? as of Rails 5.1
tags: rails activerecord
last_modified_at: 2021-08-09
---

- toc
{:toc}

**As of [Ruby on Rails 5.1](http://edgeguides.rubyonrails.org/5_1_release_notes.html), `attribute_changed?` ActiveRecord method have been deprecated.**

The deprecation message:

```
DEPRECATION WARNING: The behavior of `attribute_changed?` inside of after callbacks will be changing in the next version of Rails. The new return value will reflect the behavior of calling the method after `save` returned (e.g. the opposite of what it returns now). To maintain the current behavior, use `saved_change_to_attribute?` instead.
```

As the messages says, using `saved_change_to_attribute?` instead of `attribute_changed?` is recommended.

## Use `saved_change_to_attribute?` instead of `attribute_changed?`

Let's say you write code like this:

```rb
class Post < ApplicationRecord
  after_update :deprecation_after_update

  def deprecation_after_update
    # Post has title column
    if title_changed?
      # ...
    end
  end
end
```

Then, you need to rewrite it like this:

```rb
class Post < ApplicationRecord
  after_update :deprecation_after_update

  def deprecation_after_update
    if saved_change_to_attribute?(:title)
      # ...
    end
  end
end
```

## Use `attribute_before_last_save` instead of `attribute_was`

Also, `attribute_was` is deprecated in Rails 5.1. which is one of methods in [ActiveModel::Dirty](https://api.rubyonrails.org/v5.1.0/classes/ActiveModel/Dirty.html).

The deprecation message is:

```
DEPRECATION WARNING: The behavior of `attribute_was` inside of after callbacks will be changing in the next version of Rails. The new return value will reflect the behavior of calling the method after `save` returned (e.g. the opposite of what it returns now). To maintain the current behavior, use `attribute_before_last_save` instead.
```

As message says, we need to replace `attribute_was` with `attribute_before_last_save`.

For example:

```diff
-title_was
+attribute_before_last_save(:title)
```

## Why this change needed?

[sgrif](https://github.com/sgrif) explains why on GitHub issue: [Deprecate the behavior of AR::Dirty inside of after_(create\|update\|save) callbacks by sgrif · Pull Request #25337 · rails/rails](https://github.com/rails/rails/pull/25337)

## Conversion Table (before_update/after_update)

| Rails 5.0- | Rails 5.1+<br>(before_update) | Rails 5.1+<br>(after_update) |
|-------|-------|
| `attribute_changed?` | `will_save_change_to_attribute?` | `saved_change_to_attribute?` |
| `attribute_change` | `attribute_change_to_be_saved` | `saved_change_to_attribute` |
| `attribute_was` | `attribute_in_database` | `attribute_before_last_save` |
| `changes` | `changes_to_save` | `saved_changes` |
| `changed?` | `has_changes_to_save?` | `saved_changes?` |
| `changed` | `changed_attribute_names_to_save` | `saved_changes.keys` |
| `changed_attributes` | `attributes_in_database` | `saved_changes.transform_values(&:first)` |

ref. [Japanese] [Rails 5.1 で attribute_was, attribute_change, attribute_changed?, changed?, changed 等が DEPRECATION WARNING - Qiita](https://qiita.com/htz/items/56798d53ec5988733fc6#%E5%A4%89%E6%8F%9B%E8%A1%A8)

## Reference

- [ActiveRecord::AttributeMethods::Dirty \| RailsDoc](https://railsdoc.github.io/classes/ActiveRecord/AttributeMethods/Dirty.html)

---
layout: post
title: Use saved_change_to_attribute? instead of attribute_changed? as of Rails 5.1
tags: rails activerecord
---

As of [Ruby on Rails 5.1](http://edgeguides.rubyonrails.org/5_1_release_notes.html), `attribute_changed?` ActiveRecord method will be deprecated.

The deprecation message:

```
DEPRECATION WARNING: The behavior of `attribute_changed?` inside of after callbacks will be changing in the next version of Rails. The new return value will reflect the behavior of calling the method after `save` returned (e.g. the opposite of what it returns now). To maintain the current behavior, use `saved_change_to_attribute?` instead.
```

As the messages says, using `saved_change_to_attribute?` instead of `attribute_changed?` is recommended.

## Example

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

Then you need to rewrite it like this:

```rb
if saved_change_to_title?
  # ...
end
```

or

```rb
if saved_change_to_attribute?(:title)
  # ...
end
```

## Use `attribute_before_last_save` instead of `attribute_was`

Also, `attribute_was` is deprecated in Rails 5.1. which is one of methods in [ActiveModel::Dirty](http://api.rubyonrails.org/classes/ActiveModel/Dirty.html).

The deprecation message is:

```
DEPRECATION WARNING: The behavior of `attribute_was` inside of after callbacks will be changing in the next version of Rails. The new return value will reflect the behavior of calling the method after `save` returned (e.g. the opposite of what it returns now). To maintain the current behavior, use `attribute_before_last_save` instead.
```

As message says, we need to replace `attribute_was` with `attribute_before_last_save`.

For example:

```diff
-title_was
+title_before_last_save
```

## Why this change needed?

[sgrif](https://github.com/sgrif) explains why on GitHub issue: [Deprecate the behavior of AR::Dirty inside of after_(create\|update\|save) callbacks by sgrif · Pull Request #25337 · rails/rails](https://github.com/rails/rails/pull/25337)

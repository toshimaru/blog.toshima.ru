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

## Why this change needed?

[sgrif](https://github.com/sgrif) explains why on GitHub issue: [Deprecate the behavior of AR::Dirty inside of after_(create\|update\|save) callbacks by sgrif · Pull Request #25337 · rails/rails](https://github.com/rails/rails/pull/25337)

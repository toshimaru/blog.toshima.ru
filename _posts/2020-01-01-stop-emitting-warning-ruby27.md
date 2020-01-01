---
layout: post
title: Stop emitting warnings in Ruby 2.7
tags: ruby
---

Ruby 2.7 emits many warnings.

For example:

```console
$ bundle exec rails db:migrate
/usr/local/bundle/ruby/2.7.0/gems/actionpack-6.0.2.1/lib/action_dispatch/middleware/stack.rb:37: warning: Using the last argument as keyword parameters is deprecated; maybe ** should be added to the call
/usr/local/bundle/ruby/2.7.0/gems/actionpack-6.0.2.1/lib/action_dispatch/middleware/static.rb:110: warning: The called method `initialize' is defined here
/usr/local/bundle/ruby/2.7.0/gems/activerecord-6.0.2.1/lib/active_record/connection_adapters/mysql/database_statements.rb:12: warning: Using the last argument as keyword parameters is deprecated; maybe ** should be added to the call
/usr/local/bundle/ruby/2.7.0/gems/activerecord-6.0.2.1/lib/active_record/connection_adapters/abstract/query_cache.rb:96: warning: The called method `select_all' is defined here
/usr/local/bundle/ruby/2.7.0/gems/activerecord-6.0.2.1/lib/active_record/transactions.rb:212: warning: Using the last argument as keyword parameters is deprecated; maybe ** should be added to the call
/usr/local/bundle/ruby/2.7.0/gems/activerecord-6.0.2.1/lib/active_record/connection_adapters/abstract/database_statements.rb:274: warning: The called method `transaction' is defined here
/usr/local/bundle/ruby/2.7.0/gems/activerecord-6.0.2.1/lib/active_record/persistence.rb:503: warning: Using the last argument as keyword parameters is deprecated; maybe ** should be added to the call
/usr/local/bundle/ruby/2.7.0/gems/activerecord-6.0.2.1/lib/active_record/timestamp.rb:127: warning: The called method `create_or_update' is defined here
/usr/local/bundle/ruby/2.7.0/gems/activemodel-6.0.2.1/lib/active_model/type/integer.rb:13: warning: Using the last argument as keyword parameters is deprecated; maybe ** should be added to the call
/usr/local/bundle/ruby/2.7.0/gems/activemodel-6.0.2.1/lib/active_model/type/value.rb:8: warning: The called method `initialize' is defined here
```

To stop emitting the warnings, just add `RUBYOPT=-W:no-deprecated`.

```console
$ RUBYOPT=-W:no-deprecated bundle exec rails db:migrate
# no Ruby warnings
```

---
layout: post
title: How to clear file cache in Rails
tags: rails
---

## Rails clear cache task

`rails tmp:clear` task clears the file cache.

```console
$ rails tmp:clear # Clear cache, socket and screenshot files from tmp/ (narrow w/ tmp:cache:clear, tmp:sockets:clear, tmp:screenshots:clear)
```

### The implementation

```rb
namespace :tmp do
  desc "Clear cache, socket and screenshot files from tmp/ (narrow w/ tmp:cache:clear, tmp:sockets:clear, tmp:screenshots:clear)"
  task clear: ["tmp:cache:clear", "tmp:sockets:clear", "tmp:screenshots:clear", "tmp:storage:clear"]
  ...
end
```

ref. <https://github.com/rails/rails/blob/ac1d5f09e6d12679b80774872d9919cab6c34c3a/railties/lib/rails/tasks/tmp.rake#L4-L5>

The each task just deletes directories inside `tmp`.

```rb
  namespace :cache do
    # desc "Clears all files and directories in tmp/cache"
    task :clear do
      rm_rf Dir["tmp/cache/[^.]*"], verbose: false
    end
  end
```

ref. <https://github.com/rails/rails/blob/ac1d5f09e6d12679b80774872d9919cab6c34c3a/railties/lib/rails/tasks/tmp.rake#L17-L22>

## The difference between `Rails.cache.clear` and rails `tmp:cache:clear`

> If you are using `config.cache_store = :file_store` then `Rails.cache.clear` will be functionally identical to `rake tmp:cache:clear`. However, if you're using some other cache_store, like `:memory_store` or `:mem_cache_store`, then only `Rails.cache.clear` will clear your app cache.

ref. [What is the difference between Rails.cache.clear and rake tmp:cache:clear? - Stack Overflow](https://stackoverflow.com/questions/19017983/what-is-the-difference-between-rails-cache-clear-and-rake-tmpcacheclear#19018365)

---
title: Bundler Github/Gist shorthand
tags: bundler gist gem
last_modified_at: 2019-09-10
---

## Bundler for git source

You may know how to `bundle install` from `git` source.

```rb
gem 'page_number', git: "https://gist.github.com/123456789"
```

## Bundler for GitHub/Gist source

How about GitHub/Gist source? Bundler has shorthands for GitHub/Gist.


```rb
gem "page_number", github: "user_name/repo_name"
```

```rb
gem "page_number", gist: "gist_id_123456789"
```

## See also

- [Gems from git repositories](https://bundler.io/v1.12/git.html#gems-from-git-repositories)

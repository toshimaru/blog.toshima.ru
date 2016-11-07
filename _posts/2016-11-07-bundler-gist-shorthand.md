---
layout: post
title: Bundler Github/Gist shorthand
tags: bundler gist gem
---

## Bundler for git source

You may know how to `bundle install` from `git` source.

```rb
gem 'page_number', git: "https://gist.github.com/123456789"
```

## Bundler for GitHub/Gist source

How about GitHub/Gist source?

Bundler has shorthands for GitHub/Gist.


```rb
gem "page_number", github: "user_name/repo_name"
```

```rb
gem "page_number", gist: "gist_id_123456789"
```

## See also

- [Bundler: Custom git sources](http://bundler.io/git.html#custom-git-sources)

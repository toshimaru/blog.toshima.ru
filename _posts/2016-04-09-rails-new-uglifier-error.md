---
title: how to fix uglifier Bundler::GemRequireError
tags: rails
---

I got an error below when I tried to run `rails server` after running `rails new`.

```
web_1 | /usr/local/lib/ruby/gems/2.3.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:80:in `rescue in block (2 levels) in require': There was an error while trying to load the gem 'uglifier'. (Bundler::GemRequireError)
```

All you need to do is the uncomment `# gem 'therubyracer', platforms: :ruby` in your `Gemfile`.

```ruby
# See https://github.com/rails/execjs#readme for more supported runtimes
gem 'therubyracer', platforms: :ruby
```

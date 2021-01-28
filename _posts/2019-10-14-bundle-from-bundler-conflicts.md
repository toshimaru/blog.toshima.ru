---
layout: post
title: "Bundler Error: bundle from bundler conflicts"
tags: bundler ruby
last_modified_at: 2021-01-28
---

One day, I tyied to install `bundler` and got an error.

```console
$ gem install bundler
ERROR:  Error installing bundler:
	"bundle" from bundler conflicts with ...../bin/bundle
```

Adding `--force` option resolves this error.

```console
$ gem install bundler --force
Parsing documentation for bundler-2.0.2
Installing ri documentation for bundler-2.0.2
Done installing documentation for bundler after 5 seconds
1 gem installed
```

## Tips

Adding `--no-document` option is a good practice if you don't need doc.

```console
$ gem install bundler --no-document --force
```

## Reference

- [Bundler fails to install after RubyGems update · Issue #2058 · rubygems/rubygems](https://github.com/rubygems/rubygems/issues/2058)

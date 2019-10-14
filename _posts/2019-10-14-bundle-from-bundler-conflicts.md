---
layout: post
title: "Bundler Error: bundle from bundler conflicts"
tags: bundler ruby
---

One day I installed `bundler` and got an error.

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

Adding `--no-document` option is good practice if you don't need it.

```console
$ gem install bundler --no-document --force
```

## Reference

- [Bundler fails to install after RubyGems update · Issue #2058 · rubygems/rubygems](https://github.com/rubygems/rubygems/issues/2058)

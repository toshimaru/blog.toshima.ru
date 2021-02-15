---
layout: post
title: How to install multiple gems with specific version
tags: gem ruby
---

I'll explain how to install multiple gems with the specific version.

## Install gem normally

First of all, how to install a gem normally.

Just run `gem install gem_name`.

In the following example, install `rubocop` gem.

```console
$ gem i rubocop
Fetching regexp_parser-2.0.3.gem
Fetching ast-2.4.2.gem
Fetching unicode-display_width-2.0.0.gem
Fetching ruby-progressbar-1.11.0.gem
Fetching parser-3.0.0.0.gem
Fetching rubocop-ast-1.4.1.gem
Fetching rainbow-3.0.0.gem
Fetching rubocop-1.9.1.gem
Fetching parallel-1.20.1.gem
Successfully installed unicode-display_width-2.0.0
Successfully installed ruby-progressbar-1.11.0
Successfully installed ast-2.4.2
Successfully installed parser-3.0.0.0
Successfully installed rubocop-ast-1.4.1
Successfully installed regexp_parser-2.0.3
Successfully installed rainbow-3.0.0
Successfully installed parallel-1.20.1
Successfully installed rubocop-1.9.1
9 gems installed
```

The latest version of the gem will be installed. In this example, rubocop 1.9 was installed.

##  Install gem with version

Let's specify the version of gem with `-v` option.

```console
$ gem i rubocop -v 1.0.0
```

Or, you can use `gem_name:version`

```console
$ gem i rubocop:1.0
Fetching parser-3.0.0.0.gem
Fetching rainbow-3.0.0.gem
Fetching ast-2.4.2.gem
Fetching ruby-progressbar-1.11.0.gem
Fetching rubocop-1.0.0.gem
Fetching unicode-display_width-1.7.0.gem
Fetching regexp_parser-2.0.3.gem
Fetching rubocop-ast-1.4.1.gem
Fetching parallel-1.20.1.gem
Successfully installed unicode-display_width-1.7.0
Successfully installed ruby-progressbar-1.11.0
Successfully installed ast-2.4.2
Successfully installed parser-3.0.0.0
Successfully installed rubocop-ast-1.4.1
Successfully installed regexp_parser-2.0.3
Successfully installed rainbow-3.0.0
Successfully installed parallel-1.20.1
Successfully installed rubocop-1.0.0
9 gems installed
```

##  Install multiple gems with version

How about installing multiple gems with version?

Let's install `rubocop` v1.0.0 and `rubocop-ast` v1.0.0.

```console
$ gem i rubocop-ast:1.0 rubocop:1.0
Fetching parser-3.0.0.0.gem
Fetching ast-2.4.2.gem
Fetching rubocop-ast-1.0.0.gem
Successfully installed ast-2.4.2
Successfully installed parser-3.0.0.0
Successfully installed rubocop-ast-1.0.0
Fetching ruby-progressbar-1.11.0.gem
Fetching rubocop-1.0.0.gem
Fetching regexp_parser-2.0.3.gem
Fetching rainbow-3.0.0.gem
Fetching parallel-1.20.1.gem
Fetching unicode-display_width-1.7.0.gem
Successfully installed unicode-display_width-1.7.0
Successfully installed ruby-progressbar-1.11.0
Successfully installed regexp_parser-2.0.3
Successfully installed rainbow-3.0.0
Successfully installed parallel-1.20.1
Successfully installed rubocop-1.0.0
9 gems installed
```

Check the versions.

```console
$ gem list | grep rubocop
rubocop (1.0.0)
rubocop-ast (1.0.0)
```

### Install child dependency first

**Heads up**: install child dependency first, otherwise other version will also be installed.

```
$ gem i rubocop:1.0 rubocop-ast:1.0
Fetching rainbow-3.0.0.gem
Fetching regexp_parser-2.0.3.gem
Fetching parser-3.0.0.0.gem
Fetching ruby-progressbar-1.11.0.gem
Fetching parallel-1.20.1.gem
Fetching rubocop-1.0.0.gem
Fetching ast-2.4.2.gem
Fetching rubocop-ast-1.4.1.gem
Fetching unicode-display_width-1.7.0.gem
Successfully installed unicode-display_width-1.7.0
Successfully installed ruby-progressbar-1.11.0
Successfully installed ast-2.4.2
Successfully installed parser-3.0.0.0
Successfully installed rubocop-ast-1.4.1
Successfully installed regexp_parser-2.0.3
Successfully installed rainbow-3.0.0
Successfully installed parallel-1.20.1
Successfully installed rubocop-1.0.0
Fetching rubocop-ast-1.0.0.gem
Successfully installed rubocop-ast-1.0.0
10 gems installed
```

In this example, `rubocop-ast` v1.4 has been installed as well as v1.0.

```
$ gem list | grep rubocop
rubocop (1.0.0)
rubocop-ast (1.4.1, 1.0.0)
```

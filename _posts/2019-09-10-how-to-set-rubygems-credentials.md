---
title: How to set your rubygems credentials
tags: ruby gem
---

One day, I tried to publish [my gem](https://github.com/toshimaru/rubocop-rails_config), but it failed.

```console
$ rake release
rubocop-rails_config 0.7.2 built to pkg/rubocop-rails_config-0.7.2.gem.
Tagged v0.7.2.
Pushed git commits and tags.
rake aborted!
Your rubygems.org credentials aren't set. Run `gem push` to set them.
```

To resolve this, you need to put gem credential on `~/.gem/credentials`.

```console
$ curl -u {your_gem_account_name} https://rubygems.org/api/v1/api_key.yaml > ~/.gem/credentials
Enter host password for user '{your_gem_account_name}': {your_password}
```

Then, let's run `rake release` command again.

```console
$ rake release
rubocop-rails_config 0.7.2 built to pkg/rubocop-rails_config-0.7.2.gem.
Tag v0.7.2 has already been created.
rake aborted!
ERROR:  Your gem push credentials file located at:

	~/.gem/credentials

has file permissions of 0644 but 0600 is required.

To fix this error run:

	chmod 0600 ~/.gem/credentials
```

Okay, let's fix the permission.

```console
$ chmod 0600 ~/.gem/credentials
```

Re-try:

```console
$ rake release
rubocop-rails_config 0.7.2 built to pkg/rubocop-rails_config-0.7.2.gem.
Tag v0.7.2 has already been created.
Pushed rubocop-rails_config 0.7.2 to rubygems.org
```

Success! That's it! :)

## Reference

- [Easily publish your ruby gems](https://michaelrigart.be/easily-publish-ruby-gems/)

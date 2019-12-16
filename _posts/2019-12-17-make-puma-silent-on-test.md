---
layout: post
title: Make Puma test output silent
tags: ruby
---

When you run RSpec, you might see the following output:

```console
$ bundle exec rspec
Randomized with seed 59799
............................................................................................Capybara starting Puma...
* Version 4.3.1 , codename: Mysterious Traveller
* Min threads: 0, max threads: 4
* Listening on tcp://127.0.0.1:42837
...................................................................
```

`Capybara starting Puma` is shown in the RSpec output.

```
Capybara starting Puma...
* Version 4.3.1 , codename: Mysterious Traveller
* Min threads: 0, max threads: 4
* Listening on tcp://127.0.0.1:42837
```

This is because Puma is started by Capybara when system test is invoked.

You can make it silent by setting. In your test helper, add the line:

```
Capybara.server = :puma, { Silent: true }
```

It means run puma server silently.

After this setting:

```console
$ bundle exec rspec

Randomized with seed 45766
...............................................................................................................................................................

Finished in 11.6 seconds (files took 5.29 seconds to load)
159 examples, 0 failures
```

Test output is now clean!

## Reference

[teamcapybara/capybara: Acceptance test framework for web applications](https://github.com/teamcapybara/capybara#setup)

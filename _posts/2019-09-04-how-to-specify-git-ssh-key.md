---
layout: post
title: How to specify Git SSH key for different hosts
tags: git ssh
---

When you run `git push`, you might specify which SSH key to use. It's not possible to add option to specify which SSH key to use, but it's possible to tell git which SSH key to use with `.ssh/config`.

Here is the example:

```
# .ssh/config
Host github.com
  Hostname github.com
  User git
  IdentityFile ~/.ssh/your_private_key

Host github.yourcompany.com
  Hostname github.yourcompany.com
  User git
  IdentityFile ~/.ssh/your_another_private_key
```

This means that `git` uses `~/.ssh/your_private_key` SSH key for host `github.com` and `~/.ssh/your_another_private_key` SSH key for host `github.yourcompany.com`.

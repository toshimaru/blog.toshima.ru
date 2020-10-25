---
title: Get current branch name in Git
tags: git
---

You can get current branch name in git as follows:

```bash
$ git rev-parse --abbrev-ref HEAD
```

For example,

```bash
$ git branch
* gh-pages
  master

$ git rev-parse --abbrev-ref HEAD
gh-pages

$ echo "Your current branch is $(git rev-parse --abbrev-ref HEAD)."
Your current branch is gh-pages.
```

See also
---
* [How to get current branch name in Git? - Stack Overflow](https://stackoverflow.com/questions/6245570/how-to-get-current-branch-name-in-git)

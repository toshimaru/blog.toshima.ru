---
layout: post
title: Go Release Automation with goreleaser + GitHub Actions
tags: go
image: /images/goreleaser.jpg
---

I created a workflow to automate [my go CLI tool](https://github.com/toshimaru/nyan) with goreleaser + GitHub actions.

## Tools I used

- [GoReleaser](https://goreleaser.com/) ([GitHub Source](https://github.com/goreleaser/goreleaser))
- [GitHub Actions](https://github.com/features/actions)
- [goreleaser/goreleaser-action](https://github.com/goreleaser/goreleaser-action)

## What I want to do

When a new tag is pushed, I'd like to release new go binary with goreleaser.

```console
$ git tag -a v0.1.0 -m "First release"
$ git push origin v0.1.0 # => want to release v0.1.0
```

## Trigger TagCreated-Event

I want to trigger an event - _\<A new tag is pushed\>_. How can I do this on GitHub Actions?

The example:

```yml
name: Release with goreleaser
on:
  push:
    branches:
      - "!*"
    tags:
      - "v*.*.*"
```

The points are:

- Disabling an event - _\<A new branch is pushed\>_
- Enabling an event - _\<A new tag named `v*.*.*` is pushed\>_

## Release Workflow Definition

Release Workflow is:

1. Set up Go
1. Check out Code
1. Run `goreleaser` command using [goreleaser/goreleaser-action](https://github.com/goreleaser/goreleaser-action)

The workflow definition sample is:

```yml
jobs:
  build:
    runs-on: ubuntu-latest
    name: goreleaser
    steps:
    - name: Set up Go
      uses: actions/setup-go@v1
      with:
        go-version: 1.13
      id: go
    - name: Check out code into the Go module directory
      uses: actions/checkout@v1
    - name: goreleaser
      uses: goreleaser/goreleaser-action@master
      with:
        args: release
      env:
        GITHUB_TOKEN: ${% raw %}{{ secrets.CUSTOM_GITHUB_TOKEN }}{% endraw %}
```

I use `CUSTOM_GITHUB_TOKEN` because I need to update [another repository for homebrew](https://github.com/toshimaru/homebrew-nyan) in release process.

If you don't need an additional permission for another repository, you can use default `GITHUB_TOKEN`.

> GitHub automatically creates a GITHUB_TOKEN secret to use in your workflow.

ref. [Virtual environments for GitHub Actions - GitHub Help](https://help.github.com/en/articles/virtual-environments-for-github-actions#github_token-secret)

### Tips: No tag found. Snapshot forced

If no tag is found, snapshot option is forced.

```ts
console.log(`⚠️ No tag found. Snapshot forced`);
if (!args.includes('--snapshot')) {
  snapshot = ' --snapshot';
}
```

ref. <https://github.com/goreleaser/goreleaser-action/blob/7550dd03404a4d4f35fc4ebf1bc8442767cc4545/src/main.ts#L18-L21>

## Whole Sample

You can watch whole sample on my repository:

- Repository: [toshimaru/nyan: Colored cat command.](https://github.com/toshimaru/nyan)
- GitHub Actions configuration: [nyan/release.yml at master · toshimaru/nyan](https://github.com/toshimaru/nyan/blob/master/.github/workflows/release.yml)

## Reference

- [GitHub Actions · GoReleaser](https://goreleaser.com/actions/)
- [Virtual environments for GitHub Actions - GitHub Help](https://help.github.com/en/articles/virtual-environments-for-github-actions)

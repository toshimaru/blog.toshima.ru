---
layout: post
title: Bump version with npm-version
tags: npm
---

## What is semantic versioning?

See the video below (npm official video):

<p><amp-youtube data-videoid="kK4Meix58R4" layout="responsive" width="480" height="270" ></amp-youtube></p>

## Bump version with npm-version

`package.json`:

```json
{
  "name": "test",
  "version": "0.0.1",
  "description": "test package",
  "main": "index.js",
  ...
}
```

### Bump major version

```console
$ npm version major
v1.0.0
```

The result:

```console
$ git tag
v1.0.0

$ git show -q
commit a1e9473677f10b863eacf3289b9c34e759f47b1b (HEAD -> master, tag: v1.0.0)
Author: toshimaru <me@toshimaru.net>
Date:   Thu Apr 15 03:18:09 2020

    1.0.0
```

```json
{
  "name": "test",
  "version": "1.0.0",
  "description": "test package",
  "main": "index.js",
  ...
}
```

### Bump minor/patch version

```
$ npm version minor
v1.1.0

$ npm version patch
v1.1.1
```

### another version option

```
$ npm version [major | minor | patch | premajor | preminor | prepatch | prerelease]
```

## Reference

- [npm-version \| npm Documentation](https://docs.npmjs.com/cli/version)
- [npm-semver \| npm Documentation](https://docs.npmjs.com/misc/semver)
- [Semantic Versioning 2.0.0 \| Semantic Versioning](https://semver.org/)

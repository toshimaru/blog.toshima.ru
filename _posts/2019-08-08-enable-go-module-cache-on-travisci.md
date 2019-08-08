---
layout: post
title: Enable Go Module Cache on TravisCI
tags: go
---

![Go Mod Cache before/after](/images/go-mod-cache.png)
 
## Enbale Go Module Cache on TravisCI

To enbale Go module cache, set `$GOPATH/pkg/mod` as TravisCI cache directory.

`.travis.yml`:

```yaml
cache:
  directories:
    - $GOPATH/pkg/mod
```

## Whole `.travis.yml` Sample

`.travis.yml`:

```yaml
language: go
go:
  - "1.12.x"
cache:
  directories:
    - $GOPATH/pkg/mod
env:
  global:
    - GO111MODULE=on
install:
  - go mod download
script:
  - go test ./...
```

## Reference

- [Add `$GOPATH/pkg/mod` to Travis CI cache by yongtang · Pull Request #2686 · coredns/coredns](https://github.com/coredns/coredns/pull/2686/files)

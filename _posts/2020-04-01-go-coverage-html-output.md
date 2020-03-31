---
layout: post
title: How to output HTML for Go code coverage
tags: go
---

## Normal test in Go

Let's run tests normally for [my go repository](https://github.com/toshimaru/nyan):

```console
$ go test ./...
ok  	github.com/toshimaru/nyan	0.432s
ok  	github.com/toshimaru/nyan/styles	0.253s
```

## Test with coverage profile output

```console
$ go test ./... -coverprofile coverage.out
```

### Coverage profile content

```console
$ cat coverage.out
mode: set
github.com/toshimaru/nyan/styles/api.go:16.50,19.2 2 1
github.com/toshimaru/nyan/styles/api.go:22.23,24.29 2 1
github.com/toshimaru/nyan/styles/api.go:27.2,28.12 2 1
github.com/toshimaru/nyan/styles/api.go:24.29,26.3 1 1
github.com/toshimaru/nyan/styles/api.go:32.37,33.37 1 1
github.com/toshimaru/nyan/styles/api.go:36.2,36.17 1 1
github.com/toshimaru/nyan/styles/api.go:33.37,35.3 1 1
github.com/toshimaru/nyan/main.go:39.13,47.2 6 1
github.com/toshimaru/nyan/main.go:49.13,50.42 1 1
github.com/toshimaru/nyan/main.go:50.42,52.3 1 0
github.com/toshimaru/nyan/main.go:55.61,56.17 1 1
github.com/toshimaru/nyan/main.go:64.2,67.37 3 1
...
```

## Coverage output as HTML

```console
$ go tool cover -html coverage.out -o coverage.html
```

### Screenshot

![coverage.html](/images/gocoverage.png)

## Related post

- [How to measure code coverage on CodeClimate in Go](/2019/08/11/go-codeclimate-coverage.html)

## Reference

- [The cover story - The Go Blog](https://blog.golang.org/cover)

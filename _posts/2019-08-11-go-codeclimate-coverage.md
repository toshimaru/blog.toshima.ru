---
layout: post
title: How to measure code coverage on CodeClimate in Go
image: /images/coverage.png
tags: go
last_modified_at: 2020-01-10
---

Would you like to measure code coverage on [Code Climate](https://codeclimate.com/) in Go?

* Table of Contents
{:toc}

![coverage](/images/coverage.png)

## Viewing Coverage Result

All you need to is adding `-coverprofile c.out` option to `go test` command.

```
$ go test ./... -coverprofile c.out
```

`c.out` is a test coverage result file.

## Sending Coverage Result

This is a sample to send coverage result on TravisCI.

```bash
# Install test-reporter
curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-latest-linux-amd64 > ./cc-test-reporter
chmod +x ./cc-test-reporter

# before build step
./cc-test-reporter before-build

# RUN TEST HERE
go test ./... -coverprofile c.out

# after build step
./cc-test-reporter after-build --exit-code $TRAVIS_TEST_RESULT
```

## Sample Setting for TravisCI

Whole sample for TravisCI:

```yaml
language: go
before_script:
  - curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-latest-linux-amd64 > ./cc-test-reporter
  - chmod +x ./cc-test-reporter
  - ./cc-test-reporter before-build
script:
  - go test ./... -coverprofile c.out
after_script:
  - ./cc-test-reporter after-build --exit-code $TRAVIS_TEST_RESULT
```

## Reference

- [test-reporter/go_examples.md at master · codeclimate/test-reporter](https://github.com/codeclimate/test-reporter/blob/master/examples/go_examples.md)
- [The cover story - The Go Blog](https://blog.golang.org/cover)
- [Configuring Test Coverage](https://docs.codeclimate.com/docs/configuring-test-coverage)

## See Also

- [Enable Go Module Cache on TravisCI]({% post_url 2019-08-08-enable-go-module-cache-on-travisci %})

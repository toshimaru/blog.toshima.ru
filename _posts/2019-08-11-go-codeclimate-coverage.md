---
layout: post
title: How to Measure Code Coverage on CodeClimate in Go
tags: go
---

Would you like to measure code coverage on [Code Climate](https://codeclimate.com/) in Go?

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
curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-latest-linux-amd64 > ./cc-test-reporter
chmod +x ./cc-test-reporter
./cc-test-reporter before-build
# RUN TEST HERE
# go test ./... -coverprofile c.out
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

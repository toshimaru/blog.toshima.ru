---
layout: post
title: CircleCI 2 speeds up your CI build time drastically
tags: circleci
---

[CircleCI 2 has been released](https://circleci.com/blog/launching-today-circleci-2-0-reaches-general-availability/), which makes your CI faster and flexible.

I've accomplished 3 times faster CI build time on [my public project](https://github.com/toshimaru/RailsTwitterClone).

![faster build time](/images/circleci2.png)

Here is how I configured my `circle.yml`.

## Before: Circle 1.0 configuration

Circle 1.0 configuration is very simple.

```yml
# circle.yml
machine:
  ruby:
    version: 2.4.1
general:
  artifacts:
    - coverage
    - tmp/capybara
```

## After: Circle 2.0 configuration

Circle 2.0 configuration becomes a bit overwhelming, but I'll explain it one by one.

```yml
# .circleci/config.yml
{%- raw %}
jobs:
  build:
    working_directory: ~/app
    docker:
      - image: circleci/ruby:2.5-node-browsers
        environment:
          RAILS_ENV: test
    steps:
      - checkout
      # Restore bundle cache
      - type: cache-restore
        key: bundle-{{ checksum "Gemfile.lock" }}
      # Bundle install dependencies
      - run: bundle install --path vendor/bundle
      # Store bundle cache
      - type: cache-save
        key: bundle-{{ checksum "Gemfile.lock" }}
        paths:
          - vendor/bundle
      # Database setup
      - run: bundle exec rails db:create db:schema:load
      # RSpec
      - run: bundle exec rspec
      - store_artifacts:
          path: coverage
      - store_artifacts:
          path: tmp/capybara
{% endraw %}
```

### Working Directory

First of all, set your `working_directory`, any name is okay.

```yml
working_directory: ~/app
```

### docker image

Then, you need to specify base docker image on CircleCI 2. In this case, I used CircleCI official docker image listed [here](https://hub.docker.com/r/circleci/ruby/tags/)(All available images are listed [here](https://hub.docker.com/u/circleci/)).

```yml
docker:
  - image: circleci/ruby:2.5-node-browsers
    environment:
      RAILS_ENV: test
```

In `environment` section, I configured environment variables for the base image.

### Repository checkout

This line means checkout your code base from the repository.

```yml
- checkout
```

### Bundle cache configuration

As of CircleCI 2, you need to configured cache setting by yourself. In my Rails project, bundler is used, so I configured bundle install cache as the following.

```yml
# Restore bundle cache
{%- raw %}
- type: cache-restore
  key: bundle-{{ checksum "Gemfile.lock" }}

# Bundle install dependencies
- run: bundle install --path vendor/bundle

# Store bundle cache
- type: cache-save
  key: bundle-{{ checksum "Gemfile.lock" }}
  paths:
    - vendor/bundle
{% endraw %}
```

### Rails testing

Rails database setup and runnning RSpec:

```yml
# Database setup
- run: bundle exec rails db:create db:schema:load
# RSpec
- run: bundle exec rspec
```

### PhantomJS

**Update: If you use `circleci/ruby:2.5-node-browsers` docker image, PhantomJS is bundled in the image. Therefore, you don't have to follow the following step.**

~~I used [poltergeist](https://github.com/teampoltergeist/poltergeist) as a Capybara javascript driver. It requires PhantomJS as a dependency but official Ruby docker image doesn't include PhantomJS, so I needed to install PhantomJS by myself.~~

```yml
- run:
    name: Install PhantomJS
    command: |
      mkdir -p ~/.phantomjs/${PHANTOM_JS_VERSION}
      curl -L --output ~/.phantomjs/${PHANTOM_JS_VERSION}/phantomjs.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-${PHANTOM_JS_VERSION}-linux-x86_64.tar.bz2
      tar xfvj ~/.phantomjs/${PHANTOM_JS_VERSION}/phantomjs.tar.bz2 -C ~/.phantomjs/${PHANTOM_JS_VERSION}/
      chmod ugo+x ~/.phantomjs/${PHANTOM_JS_VERSION}/phantomjs-${PHANTOM_JS_VERSION}-linux-x86_64/bin/phantomjs
      sudo ln -sf ~/.phantomjs/${PHANTOM_JS_VERSION}/phantomjs-${PHANTOM_JS_VERSION}-linux-x86_64/bin/phantomjs /usr/local/bin/phantomjs
```

~~I created environment variable of PhantomJS version(`PHANTOM_JS_VERSION`) so that we can upgrade PhantomJS version easily.~~

### Artifacts

You can upload artifacts by specifying `store_artifacts` and the `path`.

```yml
- store_artifacts:
    path: coverage
- store_artifacts:
    path: tmp/capybara
```

## Comparison

![circleci 1 to 2](/images/circleci2-2.png)

| CircleCI 1.0 Phase | [CircleCI 1.0](https://circleci.com/gh/toshimaru/RailsTwitterClone/197) |  [CircleCI 2.0](https://circleci.com/gh/toshimaru/RailsTwitterClone/264) | improvement |
| --- | --- | --- | --- |
| INFRASTRUCTURE | 25 sec | 1 sec | **25x faster**{:.green} |
| CHECKOUT | 10 sec | 1 sec | **10x faster**{:.green} |
| MACHINE(cache restore) | 15 sec | 3 sec | **5x faster**{:.green} |
| DEPENDENCIES(bundle install) | 6 sec | 1 sec | **6x faster**{:.green} |
| DATABASE | 11 sec | 6 sec | **2x faseter**{:.green} |
| TEST(RSpec) | 20 sec | 22 sec | - |
| TEARDOWN(artifacts) | 26 sec | 1 sec | **26x fasetr**{:.green} |
| **Total build time on CircleCI** | **02:02** | **00:40** | **3x faster**{:.green} |

\* 0 sec is rounded to 1 sec

## Conclusion

CircleCI 2.0 is much faster than CircleCI 1.0. Although CircleCI 2 configuration looks complex, it gives you flexibility and better CI experience. It'll be worth it.

## Resources

- [CircleCI 2 by toshimaru · Pull Request #80 · toshimaru/RailsTwitterClone](https://github.com/toshimaru/RailsTwitterClone/pull/80)
- [CircleCI: master branch CI build time](https://circleci.com/gh/toshimaru/RailsTwitterClone/tree/master)
- [My latest config.yml for CircleCI](https://github.com/toshimaru/RailsTwitterClone/blob/master/.circleci/config.yml)
- [2.0 Docs - CircleCI](https://circleci.com/docs/2.0/)

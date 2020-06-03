---
layout: post
title: How to fix "This version of ChromeDriver only supports Chrome version xx" on Ubuntu
description: "When I was running CI on GitHub Actions, CI for Ubuntu suddenly gets an error. The error message is: Selenium::WebDriver::Error::SessionNotCreatedError: "
tags: ci chrome
last_modified_at: 2020-06-04
---

- toc
{:toc}

## Issue

When I was running CI on [GitHub Actions](https://github.com/features/actions), CI for Ubuntu suddenly gets an error.

The error says:

```
Failures:

  1) ...
     Got 0 failures and 2 other errors:

     1.1) Failure/Error: visit login_path

          Selenium::WebDriver::Error::SessionNotCreatedError:
            session not created: This version of ChromeDriver only supports Chrome version 79

     1.2) Failure/Error: Unable to infer file and line number from backtrace

          Selenium::WebDriver::Error::SessionNotCreatedError:
            session not created: This version of ChromeDriver only supports Chrome version 79
```

The error message is:

```
Selenium::WebDriver::Error::SessionNotCreatedError:
  session not created: This version of ChromeDriver only supports Chrome version 79
```

## Solution 1: Install latest Chrome

The error message basically says "your Chrome version is outdated", so install the latest chrome with chromedriver.

```diff
- sudo apt-get install libsqlite3-dev chromium-driver
+ sudo apt-get update
+ sudo apt-get install libsqlite3-dev chromium-driver google-chrome-stable
```

## Solution: Remove outdated Chrome

Another solution is removing outdated Google Chrome (`google-chrome-stable`) on the machine. By doing so, CI uses chromium instead of google-chrome as the browser.

```diff
+ sudo apt-get remove google-chrome-stable
  sudo apt-get install libsqlite3-dev chromium-driver
```

## See also

- Pull Request examples
  - Solution 1: [Bump faker from 2.8.1 to 2.9.0](https://github.com/toshimaru/RailsTwitterClone/pull/619)
  - Solution 2: [Use chromium-browser instead of google-chrome-stable](https://github.com/toshimaru/RailsTwitterClone/pull/625)
- [Install Chromium on Ubuntu 18.04 LTS & Linux Mint](https://www.omgubuntu.co.uk/2019/08/install-chromium-browser-ubuntu)

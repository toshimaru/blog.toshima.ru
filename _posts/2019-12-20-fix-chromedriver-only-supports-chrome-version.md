---
layout: post
title: How to fix "This version of ChromeDriver only supports Chrome version xx" on Ubuntu
tags: ci chrome
---

## Issue

When I was running CI on [GitHub Actions](https://github.com/features/actions), CI on Ubuntu suddenly gets an error.

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

## Solution 1

The error message basically says "your Chrome version is outdated", so install the latest chrome with chromedriver (`chromium-driver`).

```diff
- sudo apt-get install libsqlite3-dev chromium-driver
+ sudo apt-get install libsqlite3-dev chromium-driver google-chrome-stable
```

## Solution 2

Another solution is removing outdated Google Chrome (`google-chrome-stable`) on the machine. By doing so, CI uses chromium as a browser instead of google-chrome.

```diff
+ sudo apt-get remove google-chrome-stable
  sudo apt-get install libsqlite3-dev chromium-driver
```

## See also

- The Pull Request where I encountered the issue (First Solution): [Bump faker from 2.8.1 to 2.9.0](https://github.com/toshimaru/RailsTwitterClone/pull/619)
  - Another solution: [Use chromium-browser instead of google-chrome-stable](https://github.com/toshimaru/RailsTwitterClone/pull/625)
- [Install Chromium on Ubuntu 18.04 LTS & Linux Mint](https://www.omgubuntu.co.uk/2019/08/install-chromium-browser-ubuntu)

---
layout: post
title: Publish Jekyll without gh-pages branch
description: Github releases supports variety of sources of Github Pages in Github blog, which allows developer to publish Github Pages without gh-pages branch. Since this feature, you can publish your Jekyll site without using gh-pages branch and Github deployment can be more simpler now. Build page on docs directory First step: Configure build destination.
tags: jekyll github
---

Github releases supports [variety of sources of Github Pages](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/) in [Github blog](https://github.com/blog/2233-publish-your-project-documentation-with-github-pages), which allows developer to publish Github Pages without `gh-pages` branch. Since this feature, you can publish your Jekyll site without using `gh-pages` branch and Github deployment can be more simpler now.

## Build page on docs directory

First step: Configure build destination.

```yml
# _config.yml
destination: ./docs
```

Now Jekyll pages are built on `./docs` directory.

```
$ jekyll build
Configuration file: /Users/toshimaru/blog.toshima.ru/_config.yml
            Source: /Users/toshimaru/blog.toshima.ru
       Destination: ./docs
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 4.078 seconds.
 Auto-regeneration: disabled. Use --watch to enable.
```

Yay, you are almost ready to publish the pages.

## Use docs instead of gh-pages branch

Last step: Change Github Pages source from your repository setting.

![change Github Pages source](/images/doc-gh-pages.png)

You will see your Github Pages on your own published pages. Happy Jekylling :heart:

## See also

- [Configuration - Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/configuration/)

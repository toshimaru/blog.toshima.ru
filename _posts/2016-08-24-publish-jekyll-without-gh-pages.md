---
layout: post
title: Publish Jekyll site without gh-pages branch
description: "Github releases supports variety of sources of Github Pages in Github blog, which allows developer to publish Github Pages without gh-pages branch. Since this feature, you can publish your Jekyll site without using gh-pages branch and Github deployment can be more simpler now. Build page on docs directory First step: Configure build destination."
tags: jekyll github
---

Github announced [variety of sources of Github Pages](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/) is supported in [their official blog](https://github.com/blog/2233-publish-your-project-documentation-with-github-pages). It allows developers to publish Github Pages with master branch instead of `gh-pages` branch. Since this feature, you can publish your Jekyll site without using `gh-pages` branch and Github Pages deployment now can be much simpler.

## Build page on docs directory

**First step**: Configure build destination.

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

**Last step**: Change Github Pages source in your repository setting.

![change Github Pages source](/images/doc-gh-pages.png)

You will see your Github Pages on your own published pages. Happy Jekylling <3

## Pro Tip

By using [rake](https://github.com/ruby/rake), you can deploy your Jekyll site with one command, `rake deploy`.

```rb
# Rakefile
desc 'deploy Jekyll site to Github Pages'
task :deploy do
  sh 'bundle exec jekyll clean'
  sh 'bundle exec jekyll build'
  sh 'git add ./docs'
  sh 'git commit -m \'Update\''
  sh 'git push origin master'
end
```

In this task, `rake deploy` builds Jekyll site and push it to Github for you. This is useful if you'd like to release your site on CI such as TravisCI, CircleCi.

## See also

- [Configuration - Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/configuration/)

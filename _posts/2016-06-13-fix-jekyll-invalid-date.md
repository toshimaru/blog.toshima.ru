---
layout: post
title: "Fix Jekyll build error: Invalid date error"
tags: jekyll
---

When I ran `jekyll build`, I got an error:

```
Configuration file: blog.toshima.ru/_config.yml
            Source: blog.toshima.ru
       Destination: blog.toshima.ru/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
             ERROR: YOUR SITE COULD NOT BE BUILT:
                    ------------------------------------
                    Invalid date '<%= Time.now.strftime('%Y-%m-%d %H:%M:%S %z') %>': Document 'gems/jekyll-3.1.6/lib/site_template/_posts/0000-00-00-welcome-to-jekyll.markdown.erb' does not have a valid date in the YAML front matter.
```

This is because I didn't exclude `vendor` directory in `_config.yml`, so I added the following Configuration:

```yml
exclude:
  - ...
  - vendor
```

This fixes Jekyll build error.

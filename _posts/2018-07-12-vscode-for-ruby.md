---
layout: post
title: VSCode Setting for Rubyist
tags: vscode ruby
---

## Intellisense

To use VSCode `go to`/`peek definition`/`symbol`, you have to set `ruby.intellisense`.

Valid options are `rubyLocate` and `false`. Default option is `false`, so set `rubyLocate`.

```json
{
    ...
    "ruby.intellisense": "rubyLocate"
}
```

Now, you can use `Go to Symbols` and `Go to Definition`.

## Lint

You can also use `ruby -wc` syntax check as a lint(By default no linters are turned on).


```json
{
    ...
    "ruby.lint": {
        "ruby": true
    }
}
```

If you are unicode user, set `unicode`.

```json
{
    ...
    "ruby.lint": {
        "ruby": { "unicode": true }
    }
}
```

## Reference

[rubyide/vscode-ruby](https://github.com/rubyide/vscode-ruby)

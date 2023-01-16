---
layout: post
title: VSCode Setting for Rubyist
tags: vscode ruby
last_modified_at: 2022-12-17
---

## tl;dr

```json
{
    "ruby.lint": {
        "ruby": true,
        "rubocop": true
    },
    "ruby.intellisense": "rubyLocate",
    "ruby.codeCompletion": "rcodetools",
}
```

## Intellisense

To use VSCode `go to`/`peek definition`/`symbol`, you have to set `ruby.intellisense`.

Valid option is `rubyLocate` or `false`. Default value is `false`, so set `rubyLocate`.

```json
{
    ...
    "ruby.intellisense": "rubyLocate"
}
```

Now, `Go to Symbols` and `Go to Definition` are avilable.

## Lint

You can also use `ruby -wc` syntax check as a lint (No linters are turned on by default).

`rubocop` is also available as a Ruby linter.

```json
{
    ...
    "ruby.lint": {
        "ruby": true,
        "rubocop": true
    }
}
```

### For multibyte user

For multibyte character user(such as Japanese), use `{ "unicode": true }`.

```json
{
    "ruby.lint": {
        "ruby": { "unicode": true }
    }
}
```

## Completion

Enable `rcodetools`.

```json
{
    "ruby.codeCompletion": "rcodetools",
}
```

## Reference

[rubyide/vscode-ruby](https://github.com/rubyide/vscode-ruby)

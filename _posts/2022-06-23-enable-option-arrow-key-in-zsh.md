---
layout: post
title: Enable option + arrow(⌥←, ⌥→) keys in Zsh/iTerm2
tags: zsh macos
last_modified_at: 2023-12-19
---

When you use `option` + `arrow` keys (such as `⌥` + `←`, `⌥` + `→`) in your macOS teminal, the cursor doesn't move.

```console
$ [D [C # option + arrow key doesn't work!
```

There are two ways to fix this:

1. zsh bindkey
2. Key Mapping on iTerm2

## 1. zsh bindkey

To fix this, put this in your `~/.zshrc`.

```zsh
bindkey "[D" backward-word
bindkey "[C" forward-word
```

### See also

- [Moving Left and Right in zsh (in macOS) – Seaside Testing](https://seasidetesting.com/2021/03/19/moving-left-and-right-in-zsh-in-macos/)
- [zsh + iTerm2 OSX shortcuts (Example)](https://coderwall.com/p/a8uxma/zsh-iterm2-osx-shortcuts)

## 2. Key Mapping on iTerm2

- open iTerm2
- Profiles -> Edit Profiles -> Keys
- Click on Presets
- Select **Natural Text Editing**

![](/images/iterm2-presets-text.png)

### See also

- [How to easy fix iTerm2 text navigation (cmd+arrow) · Raul Melo](https://www.raulmelo.dev/til/how-to-easy-fix-iterm2-text-navigation)


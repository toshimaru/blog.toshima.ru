---
layout: post
title: Enable option + arrow(⌥←, ⌥→) keys in Zsh/iTerm2
tags: zsh macos
---

When you use option + arrow keys in your macOS teminal(such as `⌥ + ←` `⌥ + →`), you can't move cursor.

```console
$ [D [C # option + arrow key doesn't work!
```

## fix with zsh bindkey

To fix this, put this in your `~/.zshrc`.

```zsh
bindkey "[D" backward-word
bindkey "[C" forward-word
```

### See also

- [Moving Left and Right in zsh (in macOS) – Seaside Testing](https://seasidetesting.com/2021/03/19/moving-left-and-right-in-zsh-in-macos/)
- [zsh + iTerm2 OSX shortcuts (Example)](https://coderwall.com/p/a8uxma/zsh-iterm2-osx-shortcuts)

## fix with iTerm2 Key mapping

> Just open iTerm2, Profiles -> Edit Profiles -> Keys. Then you click on Presets and select: Natural Text Editing.

[How to easy fix iTerm2 text navigation (cmd+arrow) · Raul Melo](https://www.raulmelo.dev/til/how-to-easy-fix-iterm2-text-navigation)

![](/images/iterm2-presets-text.png)

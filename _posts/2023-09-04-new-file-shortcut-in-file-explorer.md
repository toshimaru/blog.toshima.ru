---
layout: post
title: New file and folder shortcut in file explorer
tags: vscode
---

`keybindings.json`:

```json
{
  "key": "cmd+n",
  "command": "explorer.newFile",
  "when": "explorerViewletFocus"
},
{
  "key": "cmd+shift+n",
  "command": "explorer.newFolder",
  "when": "explorerViewletFocus"
}
```

## Reference

- [add shortcut keybinding for new file and new folder when focus on file explorer · Issue #136662 · microsoft/vscode](https://github.com/microsoft/vscode/issues/136662)

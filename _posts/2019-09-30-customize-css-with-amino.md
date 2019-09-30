---
layout: post
title: Customize CSS with Amino(Chrome Extension)
tags: chrome
image: /images/amino.png
---

If you'd like to customize CSS style for a website, [Amino](https://chrome.google.com/webstore/detail/amino-live-css-editor/pbcpfbcibpcbfbmddogfhcijfpboeaaf) Chrome Extension is useful.

![](/images/amino.png)

[Amino: Live CSS Editor](https://chrome.google.com/webstore/detail/amino-live-css-editor/pbcpfbcibpcbfbmddogfhcijfpboeaaf?lang=en)

## Customize CSS Style

Let's say you want to change header `background-color` on github.com. Just set custom CSS for the domain.


![](/images/amino2.png)

The style is:

```css
.Header {
    background-color: #511e80;
}
```

You can change whatever you want.

The result is:

![](/images/amino-header.png)

The header background color has changed to `#511e80`.

## Use Case in Read World

- Change style for each environments(`development`, `staging`, `production`)
- Change sytle for your own secret/important page(e.g. Password page)

## Reference

- [Amino: Live CSS Editor for Chrome](https://aminoeditor.com/)

---
layout: post
title: Escape ERB tag string in ERB file
tags: erb ruby
---

How can we output erb tag string like `<% erb %>` in erb file without being interpreted as erb? You can do this by using double percent `<%% %>`!

```erb
<%% escaped %>
```

Let's look at how it changes on `irb`.

```
$  irb
>  ERB.new("<%% escaped? %>").result
=> "<% escaped? %>"
>  ERB.new("<% escaped? %>").result
NoMethodError: undefined method `escaped?' for main:Object
	from (erb):1:in `<main>'
```

`<%%` becomes string without an error.

## See also

- (JAPANESE) <http://koseki.hatenablog.com/entry/20090416/erbtag>

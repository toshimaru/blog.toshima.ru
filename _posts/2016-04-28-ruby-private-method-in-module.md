---
title: Private method in module in Ruby
tags: ruby
---

In Ruby, private method can be defined in module:

{% highlight ruby %}
module Hoge
  private

  def p_method
    puts 1
  end
end

class Foo
  include Hoge
end
{% endhighlight %}

Try it on IRB.

```
irb(main)> Foo.new
=> #<Foo:0x007fd66103f220>

irb(main)> Foo.new.p_method
NoMethodError: private method `p_method' called for #<Foo:0x007fd660b9de88>
	from (irb):13
	from /Users/toshi/.rbenv/versions/2.2.4/bin/irb:11:in `<main>'
```

It worked!!

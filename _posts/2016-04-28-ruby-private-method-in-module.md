---
title: Private method in module in Ruby
tags: ruby
---

In Ruby, private method can be defined in module:

```ruby
module Hoge
  private

  def p_method
    puts 1
  end
end

class Foo
  include Hoge
end
```

Try it on IRB.

```
irb(main)> Foo.new.p_method
NoMethodError: private method `p_method' called for #<Foo:0x007fd660b9de88>
	from (irb):13
	from /Users/toshi/.rbenv/versions/2.2.4/bin/irb:11:in `<main>'
```

As expected, private method defined in `Hoge` module cannot be called from `Foo` instance.

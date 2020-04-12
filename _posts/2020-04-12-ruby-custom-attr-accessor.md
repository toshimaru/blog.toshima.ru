---
layout: post
title: My custom attr_accessor in Ruby
tags: ruby
---

Do you imagin how `attr_accessor` is implemented in Ruby? Let's implement it by yourself.

## My `attr_accessor` module

Create `CustomAttrAccessor` module which overrides Ruby's `attr_accessor` method.

```rb
module CustomAttrAccessor
  def self.included(base)
    base.extend ClassMethods
  end

  module ClassMethods
    def attr_accessor(attr)
      define_method(attr) do
        puts "trying to get @#{attr}"
        instance_variable_get "@#{attr}"
      end

      define_method("#{attr}=") do |value|
        instance_variable_set "@#{attr}", value  
        puts "@#{attr} has been set"
      end
    end
  end
end
```

## inlcude `attr_accessor` module 

You can use your custom `attr_accessor` by including the module you've created in the class.

```rb
class A
  include CustomAttrAccessor

  attr_accessor :bar
end
```

## Test your `attr_accessor`

Let's test the `attr_accessor`.

```rb
a = A.new

val = a.bar # trying to get @bar
p val # => nil

a.bar = "my value" # @bar has been set

val = a.bar # trying to get @bar
p val # => "my value"
```

## Ruby Technique: Class Macro 

You can create your own class macro like the following:

```rb
module ClassMacro
  def self.included(base)
    base.extend ClassMethods
  end

  module ClassMethods
    def my_class_macro
      puts "my_class_macro!"
    end
  end
end

class Macro
  include ClassMacro
  my_class_macro # => my_class_macro!
end
```

## Reference

- [Metaprogramming Ruby 2: Program Like the Ruby Pros by Paolo Perrotta \| The Pragmatic Bookshelf](https://pragprog.com/book/ppmetr2/metaprogramming-ruby-2)
- [Ruby Custom Class Macros with Class Instance Variables](https://www.thegreatcodeadventure.com/ruby-custom-class-macros-with-class-instance-variables/)

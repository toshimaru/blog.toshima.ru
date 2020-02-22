---
layout: post
title: Ruby Private Constant
tags: ruby
---

How can we define a private constant in Ruby.

Let' define `PRIVATE_CONSTANT` in the `private` section.

```rb
# private_constant.rb
module MyModule
  private

  PRIVATE_CONSTANT = 'Is this private?'
end
```

The result:

```rb
require './private_constant'
puts MyModule::PRIVATE_CONSTANT # => Is this private?
```

**It's not private!** 👎

## private_constant

To make it private, use `private_constant`.

```rb
# private_constant.rb
module MyModule
  PRIVATE_CONSTANT = 'Is this private?'
  private_constant :PRIVATE_CONSTANT
end
```

The result:

```rb
require './private_constant'
puts MyModule::PRIVATE_CONSTANT # => private constant MyModule::PRIVATE_CONSTANT referenced (NameError)
```

The error:

```
private constant MyModule::PRIVATE_CONSTANT referenced (NameError)
```

It raises `NameError` because the code tries to reference private constant.

## Conclusion

Use `private_constant` to make a private constant in Ruby.

```rb
private_constant :YOUR_CONSTANT
```

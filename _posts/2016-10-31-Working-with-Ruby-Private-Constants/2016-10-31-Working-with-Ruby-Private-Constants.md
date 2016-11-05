---
layout: post
title: Working with Ruby Private Constants
---

One of the most common way to refactor your code is to extract a class. However, many times this class should not be used by anyone else but the module in which it is defined.

Let's run some examples on irb:
```
# user.rb
class User
 NUMBER = 100
end
```
running it:

`User::NUMBER # => 100`

In many cases, you should not make these constant publics. For that, we have to use private constants.

You may be wondering if it’s not possible to just declare the constant to be private. Well, that's unfortunately not the case:
```
# user.rb
class User
  private
  NUMBER = 100
end```

running it:

`User::NUMBER # => 100`

Bummer. It’s still accessible… So, what do we do?

That's where private_constant comes up:

```# user.rb
class User
  NUMBER = 100
  private_constant :NUMBER
end```

Let’s test if it’s still accessible: 

```User::NUMBER
# => NameError: private constant User::NUMBER referenced```

Nope. We've just made it that constant private. That’s it.

As a rule of thumb, this is usually a good implementation when it's necessary to ensure such constant is an implementation detail and only meant to be used internally.

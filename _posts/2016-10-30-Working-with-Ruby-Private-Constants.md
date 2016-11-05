---
layout: post
title: Working with Ruby Private Constants
---

By default, Ruby will take your constant to be publicly available. However, it's important to note these should *not* be visible by anyone else but the module in which it was defined.

Let's run some examples on irb:

```ruby
class User
 NUMBER = 100
end
```
and then running it:

```bash
User::NUMBER # => 100
```
as expected, we are able to access the value of the constant `NUMBER`.

Still, as I've said before, you should often not make them public. For that, we must use *private constants*.

With that in mind, you may be wondering if it’d be possible to simply declare the constant to be private. Well, that's unfortunately not the case:

```ruby
class User
  private
  NUMBER = 100
end
```

running it:

```bash
User::NUMBER # => 100
```

Bummer. It’s still accessible… So, what do we do?

That's where *private_constant* comes up:

```ruby
class User
  NUMBER = 100
  private_constant :NUMBER
end
```

Let’s test if it’s still accessible: 

```bash
User::NUMBER
# => NameError: private constant User::NUMBER referenced
```

Nope. We've just made it that constant private! That’s it.

As a rule of thumb, this is a good implementation whenever it's necessary to ensure a constant is an implementation detail and only meant to be used internally. 

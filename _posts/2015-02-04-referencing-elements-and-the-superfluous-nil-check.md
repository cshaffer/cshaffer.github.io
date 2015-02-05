---
layout: post
title: "Referencing Elements and the Superfluous Nil Check"
date: 2015-02-04 20:03:21
tags: ruby API
---
On behalf of all consumers of APIs written in Ruby, I'd like to make a general
request.

When building an API, you may find yourself exposing access to something that
acts like an `Array`, allowing retrieval of specific elements in a collection
via a `#[]` method.

In this likely situation, I ask that you follow a clever little pattern I
stumbled across when looking at [`Regexp::last_match`][last_match].

Notice there are "two forms" to this method. The first, without any arguments,
returns the entire collection object, in this case an instance of `MatchData`.
The second form is where it gets really nice, if you pass in an optional index,
you'll get that element in return.

But wait, why don't you just let users access that element with the `#[]`
method on the returned collection object? By following this path, you are
dooming consumers of your API to see this:

```
NoMethodError: undefined method `[]' for nil:NilClass`
```

That's right, you forgot, your collection could be `nil`.

By adding this nicety, all consumers of `Regexp::last_match` are saved from
having to check if there were any matches before trying to access one of them.
And it's simple to adopt this pattern in your API too:

{% highlight ruby %}
def awesome_things(index = nil)
  if index && @awesome_things
    @awesome_things[index]
  else
    @awesome_things
  end
end
{% endhighlight %}

[last_match]: http://www.ruby-doc.org/core-2.2.0/Regexp.html#method-c-last_match

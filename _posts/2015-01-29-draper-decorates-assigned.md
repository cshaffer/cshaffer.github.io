---
layout: post
title: "Staying DRY with draper's decorates_assigned"
date: 2015-01-29 16:37:00
tags: ruby rails draper DRY
---
If you're like me you hate using Rails helpers to write view specific logic.

Also, if you're like me, you use the [draper gem][draper] to avoid this hatred.

In the [draper README][draper-readme] there is some wise advice to hold off on
decorating your objects until the last minute in your controller action. This
makes sense, since the whole purpose of decorating these objects is to add some
sweet methods to use specifically in your views.

In an attempt to heed this advice, if you were like me, you were repeating
yourself all over your controllers by explicitly decorating the same model
in each action, like this:

{% highlight ruby %}
# app/controllers/widgets_controller.rb
def show
  @widget = Widget.find(params[:id]).decorate
  respond_with(@widget)
end

def create
  @widget = Widget.new(widget_params)
  @widget.save
  @widget = @widget.decorate
  respond_with(@widget)
end

def update
  @widget = Widget.find(params[:id])
  @widget.update_attributes(widget_params)
  @widget = @widget.decorate
  respond_with(@widget)
end
{% endhighlight %}

Silly me, I should have kept reading the draper documentation and got to
the part about `decorates_assigned` which would let me do this instead:

{% highlight ruby %}
# app/controllers/widgets_controller.rb
decorates_assigned :widget

def show
  @widget = Widget.find(params[:id])
  respond_with(@widget)
end

def create
  @widget = Widget.new(widget_params)
  @widget.save
  respond_with(@widget)
end

def update
  @widget = Widget.find(params[:id])
  @widget.update_attributes(widget_params)
  respond_with(@widget)
end
{% endhighlight %}

Draper adds a helper method to access a decorated version of your assigned
instance variable for you, providing the added benefit of being a little more
ecapsulation-friendly by using the helper `widget` instead of directly
accessing `@widget` in your views.

If you're like me, this makes you happy.

[draper]: https://github.com/drapergem/draper
[draper-readme]: https://github.com/drapergem/draper#when-to-decorate-objects

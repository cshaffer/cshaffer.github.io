---
layout: post
title: "The Case For Controller Concerns"
date: 2015-02-02 15:19:30
tags: ruby rails concerns
---
Most examples you'll find for [Rails ActiveSupport::Concern][rails-concern] is
related to modularizing fat models. However, you're not limited to only
splitting up your models, concerns work for controllers to.

But wait, shouldn't your controllers be skinny already? Ideally, yes. But
check out your private methods in your controllers, there might be an
opportunity for DRYing off your application, especially if you have a similar
controller for your API.

Often I'll see something like this:

{% highlight ruby %}
# app/controllers/widgets_controller.rb

# All your widget controller actions for your html site

private

def widget_params
  params.require(:widget).permit(:name, :description)
end

def find_widget
  Widget.find(params[:id])
end
{% endhighlight %}

{% highlight ruby %}
# app/controllers/api/v1/widgets_controller.rb

# All your widget controller actions for your API

private

def widget_params
  params.require(:widget).permit(:name, :description)
end

def find_widget
  Widget.find(params[:id])
end
{% endhighlight %}

Wouldn't it be nice to not have to change your strong parameters code in two
places each time you add/remove attributes on your widget? Add a controller
concern and mix it in!

{% highlight ruby %}
# app/controllers/concerns/controlling_widgets.rb

module ControllingWidgets
  extend ActiveSupport::Concern

  private

  def widget_params
    params.require(:widget).permit(:name, :description)
  end

  def find_widget
    Widget.find(params[:id])
  end
end
{% endhighlight %}

If you decide to follow this pattern for other things, maybe your decorators
or serializers, don't forget to add the corresponding concerns directory to
your `eager_load_paths`.

Happy coding!

[rails-concern]: http://api.rubyonrails.org/classes/ActiveSupport/Concern.html

---
layout: post
title: Focusing Autotest
---

Looking at [micronaut][m] made me realize that I often want to iterate
very quickly on a single test, rather than having Autotest re-run
every test in the file each time I save. After a quick chat with
[Ryan][z] -- whose suggestion was *way*
simpler than what I was considering -- here's what popped out:

[m]: http://github.com/spicycode/micronaut
[z]: http://blog.zenspider.com

{% highlight ruby %}
class Test::Unit::TestCase
  def self.focus *focused
    focused.collect! { |m| m.to_s }

    instance_methods.
      collect { |m| m.to_s }.
      select  { |m| m =~ /^test/ }.
      reject  { |m| focused.include? m }.
      each    { |m| undef_method m }
  end
end
{% endhighlight %}

With this snippet in my test helper file, I can easily focus on just
one test:

{% highlight ruby %}
class MyTest < Test::Unit::TestCase
  # lots of tests

  def test_thingy
    # ...
  end

  # lots more tests

  focus :test_thingy
end
{% endhighlight %}

...and remove the focus when I'm ready to zoom out. Awesome. Sprinkle
on some editor support and it'll be *epic*.

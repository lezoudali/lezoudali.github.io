---
layout: post
title:  Defaut Argument and ArgumentError
date:   2015-01-27 13:39:00
categories: coding
---

Let's say you want to define a method __add__, which takes two arguments and return their sum.
{% highlight ruby %}
def add(x, y)
  x + y 
end
{% endhighlight %}
This method will take two arguments ``(x, y)`` and will return ``x + y``.
`x` and `y` will both be assigned to 1 and 3, respectively. If we call __add__ with the values 1 and 3. We expect to get 4 as the return value. 
{% highlight ruby %}
>> add(1, 3)
=> 4
{% endhighlight %}

Now I want you to try and answer this question, what would happen if we don't pass any arguments, or pass one argument, to __add__? Like so,

{% highlight ruby %}
>> add()
ArgumentError: wrong number of arguments (0 for 2)
{% endhighlight %}


{% highlight ruby %}
>> add(1)
ArgumentError: wrong number of arguments (1 for 2)
{% endhighlight %}

As you see, we get this `ArgumentError` in both cases. In the first case, __add__ is expecting values for both `x` and `y`, but gets nothing. In the second case, __add__ is still expecting two values, for `x` and `y`, but gets no value for `y`. Thus, if we call the __add__ without passing exactly two values we get an `ArgumentError` because the method doesn't have anything to add. This brings us to our second main focus of this post, **default arguments**.
Setting a default value to your paramater(s) can prevent you from getting an `ArgumentError`. Let's rewrite the __add__ method using default arguments for `x` and `y`.
{% highlight ruby %}
def add(x = 0, y = 0)
  x + y
end
{% endhighlight %}

Here we set both `x` and `y` with a default value of 0. if we now call the method __add(1, 3)__. It will still return 4. As before, `x` will get assigned the value 1 and `y` will get 3. Now what will happen if we call __add()__ and __add__(1)? 

{% highlight ruby %}
>> add()
=> 0
{% endhighlight %}

{% highlight ruby %}
>> add(1)
=> 1
{% endhighlight %}

We don't get the `ArgumentError` as we did before, why? Because we gave default values to `x` and `y` when we redefined the add method; **`add(x = 0, y = 0)`**. The default value, for both `x` and `y`, is 0. We could've given them any default values, but 0 makes more sense for this particular method. Therefore, when don't explicitly pass any arguments to `x` and `y`. They will get assigned to their default values of 0. And that is how default arguments work.

**P.S What will happen if we pass more than two values to add? stay tuned to find out to fix that error. Thanks for reading.**

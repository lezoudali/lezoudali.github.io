---
layout: post
title:  Defaut Argument, ArgumentError and the Splat operator.
date:   2015-01-27 13:39:00
categories: coding
---

Let's say you want to define a method __add__, which takes two arguments and return their sum.
{% highlight ruby linenos%}
def add(x, y)
  x + y 
end
{% endhighlight %}
This method will take two arguments ``(x, y)`` and will return ``x + y``. If we call __add__ with the values 1 and 3, then the expected return value is 4. `x` and `y` will be assigned 1 and 3, respectively.
{% highlight ruby linenos%}
>> add(1, 3)
=> 4
{% endhighlight %}

Now I want you to try and answer this question, what would happen if we don't pass any arguments, or pass one argument, to __add__? Like so,

{% highlight ruby linenos%}
>> add()
ArgumentError: wrong number of arguments (0 for 2)
{% endhighlight %}


{% highlight ruby linenos%}
>> add(1)
ArgumentError: wrong number of arguments (1 for 2)
{% endhighlight %}

As you see, we get this `ArgumentError` in both cases. In the first case, __add__ is expecting values for both `x` and `y`, but gets nothing. In the second case, __add__ is still expecting two values, for `x` and `y`, but gets no value for `y`. Thus, if we call the __add__ method without passing exactly two values we get an `ArgumentError` because the method doesn't have anything to add. This is where setting **default arguments** could come in handy.
Setting a default value to your paramater(s) can prevent you from getting an `ArgumentError`. Let's rewrite the __add__ method using default arguments for `x` and `y`.
{% highlight ruby linenos%}
def add(x = 0, y = 0)
  x + y
end
{% endhighlight %}

Here we set both `x` and `y` with a default value of 0. if we now call the method __add(1, 3)__. It will still return 4. As before, `x` will get assigned the value 1 and `y` will get 3. Now what will happen if we call __add()__ and __add__(1)? 

{% highlight ruby linenos%}
>> add()
=> 0
>> add(1)
=> 1
{% endhighlight %}

We don't get the `ArgumentError` as we did before, why? Because we gave default values to `x` and `y` when we redefined the add method; **`add(x = 0, y = 0)`**. The default value, for both `x` and `y`, is 0. We could've given them any default values but 0 makes more sense for this particular method; therefore, when don't explicitly pass any arguments to `x` and `y`. They will get assigned to their default values of 0. And that is how default arguments work.

Now, what will happen if we pass more than two values to __add__? As it is, we should expect an ArgumentError; but what if we wanted to add 3, 4 or 10 integers? Wouldn't it be nice if there was a way to pass more than 2 integers to our __add__ method without getting an ArgumentError?

{% highlight ruby linenos%}
>> add(1, 2, 3)
ArgumentError: wrong number of arguments (3 for 0..2)
{% endhighlight %}

Since we set a default value to both our parameters, `0..2` means the __add__ method can only accepts 0 to 2 arguments.
We can use the splat operator `(*)` to get the remaining arguments. In our case, any other argument passed after the first two arguments, `(x, y)`, will be stored in an array and be assigned to the parameter with the splat operator. Let's see this action:

{% highlight ruby linenos%}
def test(a, *b)
  puts "a is #{a.inspect}"
  puts "b is #{b.inspect}"
end
{% endhighlight %}
{% highlight ruby linenos%}
>> test(1)
a is 1
b is []
=> nil
>> test(1, 2)
a is 1
b is [2]
=> nil
>> test(1, 2, 3)
a is 1
b is [2, 3]
=> nil
{% endhighlight %}

With our new knowlegde let's rewrite our __add__ method with the splat operator and see if this gets rid of the previous `ArgumentError`. We should now be able to pass more than two integers to our __add__ method.

{% highlight ruby linenos%}
def add(x=0, y=0, *z)
  puts "x equals #{x.inspect}"
  puts "y equals #{y.inspect}"
  puts "z equals #{z.inspect}"

  sum = x+y
  z.each {|num| sum += num}
  sum
end
{% endhighlight %}

{% highlight ruby linenos%}
>> add(1)
x equals 1
y equals 0
z equals []
=> 1
>> add(1, 2)
x equals 1
y equals 2
z equals []
=> 3
>> add(1, 2, 3)
x equals 1
y equals 2
z equals [3]
=> 6
>> add(1, 2, 3, 4, 5)
x equals 1
y equals 2
z equals [3, 4, 5]
=> 15
{% endhighlight %}


###More examples with the splat operator


{% highlight ruby linenos%}
>> first,* list = ['a', 'b', 'c', 'd']
=> ["a", "b", "c", "d"]
>> first
=> "a"
>> list
=> ["b", "c", "d"]
{% endhighlight %}

{% highlight ruby linenos%}
>> *list, last = ['a', 'b', 'c', 'd']
=> ["a", "b", "c", "d"]
>> list
=> ["a", "b", "c"]
>> last
=> "d"
{% endhighlight %}

{% highlight ruby linenos%}
>> first, *center, last = [1,2,3,4]
=> [1, 2, 3, 4]
>> center
=> [2, 3]
>> first
=> 1
>> last
=> 4
{% endhighlight %}

{% highlight ruby linenos%}
>> range = *(1..5)
=> [1, 2, 3, 4, 5]
{% endhighlight %}

{% highlight ruby linenos%}
>> def add(a,b)
>>   a + b
>> end
=> :add
>> nums = [1, 2]
=> [1, 2]
>> add(*nums)
=> 3
{% endhighlight %}


















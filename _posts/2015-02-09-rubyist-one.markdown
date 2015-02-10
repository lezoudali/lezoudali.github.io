---
layout: post
title:  Coding Like a Rubyist Part 1 - How to effectively use `until` and `unless`.
date:   2015-02-09 22:16:00
categories: coding
---

Most people tend to shy away from using "`until`" or "`unless`" when writing ruby code. I believe to become a true rubyist you must learn when and how to use them. They are really not that bad once you get the hang of it. "`unless`" and "`until`" are use for negative conditions. It can be confusing to understand at first but the main idea is to refactor your code to "`unless something`" whenever you catch yourself writing "`if not something`". Same goes for "`until something`" and "`while not something`". The idea is to get rid of the negation in your conditions.

##Example:

{% highlight ruby %}
if not @full
  :eat
end
{% endhighlight %}

Refactors to:

{% highlight ruby %}
unless @full
  :eat
end
{% endhighlight %}

##Example:

{% highlight ruby %}
if 1 != 2
  puts "1 is not equal to 2"
end
{% endhighlight %}

Refactors to:

{% highlight ruby %}
unless 1 == 2
  puts "1 is not equal to 2"
end
{% endhighlight %}

##Example:

{% highlight ruby %}
while !@full
  :keep_eating
end
{% endhighlight %}

Refactors to:

{% highlight ruby %}
until @full
  :keep_eating
end
{% endhighlight %}

##Example:

{% highlight ruby %}
while x != 3
  puts x
  x += 1
end
{% endhighlight %}

Refactors to:

{% highlight ruby %}
until x == 3
  puts x
  x += 1
end
{% endhighlight %}

The last example outputs `1` and `2` for both while and until loops. In conclusion, when using "`unless`" or "`until`", the body of the statement is executed when the condition is false.



















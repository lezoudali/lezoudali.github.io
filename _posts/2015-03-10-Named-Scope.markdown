---
layout: post
title:  Named Scope for ActiveRecord models.
date:   2015-03-10 01:12:00
categories: coding
---

Named scope is a feature on ActiveRecord to help you write better queries for your models. I created a User model with an id, name, gender and donated (boolean). The table has a total of 6 users with different values. Before writing named scopes, how would we write the query to find the female users?

{% highlight ruby %}
pry(main)> User.where(gender: 'F')
=> [#<User:0x007fa823980030 id: 2, name: "Sheneneh Jenkins", age: 32, gender: "F", donated: false>,
 #<User:0x007fa82397bda0 id: 4, name: "Rene Dumont", age: 17, gender: "F", donated: true>]
{% endhighlight %}

The query returned two female users. We can write a named scope `females` in our User model which will return the two females when we call the method `females` on our `User` model. 

{% highlight ruby %}
class User < ActiveRecord::Base
  scope :females, ->{where(gender: 'F')}
end
{% endhighlight %}

By adding the named scope `females` to our model; we could now call `User.females` and expect to get back the 2 female users. You can also chain the named scopes together, see examples below.

{% highlight ruby %}
pry(main)> User.females
=> [#<User:0x007ffc123ed148 id: 2, name: "Sheneneh Jenkins", age: 32, gender: "F", donated: false>,
 #<User:0x007ffc123ecfb8 id: 4, name: "Rene Dumont", age: 17, gender: "F", donated: false>]
{% endhighlight %}

##Examples

{% highlight ruby %}
class User < ActiveRecord::Base
  scope :females, ->{where(gender: 'F')}
  scope :adults, ->{where('age > 18')}
  scope :males, ->{where(gender: 'M')}
  scope :donated, ->{where(donated: true)}
end
{% endhighlight %}

{% highlight ruby %}
pry(main)> User.donated
=>[#<User:0x007fd10d4fc348 id: 1, name: "John Doe", age: 34, gender: "M", donated: true>,
 #<User:0x007fd10d4fc0f0 id: 3, name: "Dragon Fly Jones", age: 50, gender: "M", donated: true>,
 #<User:0x007fd10d4fcf28 id: 5, name: "Inho Peterson", age: 19, gender: "M", donated: true>,
 #<User:0x007fd10c413ef0 id: 6, name: "Steven K Blake", age: 17, gender: "T", donated: true>]
{% endhighlight %}

{% highlight ruby %}
pry(main)> User.donated.males
=> [#<User:0x007fd10d45e260 id: 1, name: "John Doe", age: 34, gender: "M", donated: true>,
 #<User:0x007fd10d45e0d0 id: 3, name: "Dragon Fly Jones", age: 50, gender: "M", donated: true>,
 #<User:0x007fd10d45df68 id: 5, name: "Inho Peterson", age: 19, gender: "M", donated: true>]
{% endhighlight %}

{% highlight ruby %}
pry(main)> User.adults.males.donated
=> [#<User:0x007fd10d27dae0 id: 1, name: "John Doe", age: 34, gender: "M", donated: true>,
 #<User:0x007fd10d27d018 id: 3, name: "Dragon Fly Jones", age: 50, gender: "M", donated: true>,
 #<User:0x007fd10d27c9b0 id: 5, name: "Inho Peterson", age: 19, gender: "M", donated: true>]
{% endhighlight %}



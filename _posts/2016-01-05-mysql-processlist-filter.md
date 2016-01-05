---
title: Filter MySQL processlist
---

You can see MySQL processes by `show processlist`.

{% highlight sql %}
show processlist;
{% endhighlight %}

But, it cannot be filtered. If you'd like to retrieve processes like usual SQL syntax, it can be replaced with:

{% highlight sql %}
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST;
{% endhighlight %}

Now, you can filter process with `WHERE` clause.

{% highlight sql %}
SELECT * FROM INFORMATION_SCHEMA.PROCESSLIST WHERE DB = 'development' AND USER = 'myuser';
{% endhighlight %}

See also
---
* [how to customize `show processlist` in mysql? - Stack Overflow](http://stackoverflow.com/questions/929612/how-to-customize-show-processlist-in-mysql)

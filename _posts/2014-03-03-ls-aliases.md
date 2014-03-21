---
layout: post
title: "Useful ls Aliases"
modified: 2014-03-03 00:37:19 +0100
tags: [bash, aliases, unix, ls]
comments: 
share: 
---
# ls - list directory contents

This blog post is part of the [aliases series](/aliases). If you just get 
started and want to know more about aliases, start there.

Years ago when I started with Linux, it was not obvious how a simple
command like [````ls```` ](http://en.wikipedia.org/wiki/Ls) could be of much use. In the mean time, my opinion
has changed and I want to highlight, how I use ````ls```` to my 
advantage.

As described in my initial [aliases](/aliases) post, aliases allows
you to be lazy with typing. Apart from that, you can set better default
values.

On any Unix-like system, there are a lot of files/directories starting with a ````.````,
known as [hidden files](http://en.wikipedia.org/wiki/Hidden_file_and_hidden_directory). In case you just want to see all these hidden files/directories, use:
{% highlight bash %}alias l.="ls -a | egrep '^\.'"{% endhighlight %}

To see only directories, use:
{% highlight bash %}alias ld="ls -ltr | grep ^d"{% endhighlight %}

To sort the by modification date, use:
{% highlight bash %}alias lt="ls -latr"{% endhighlight %}
Or without the ````-r```` option (oldest files last)
{% highlight bash %}alias ltr="ls -lat"{% endhighlight %}
This is one alias I use very frequently, since I most often are
interested in the newest files.

To search for the newest file recursively, use:
{% highlight bash %}alias lnew='find . -type f -exec stat -f "%m %N" {} \; | sort -rn | head -n10 | cut -f2- -d" "'{% endhighlight %}
No exactly an ````ls```` command, but I use it as such.

In case you finger type faster than you think,
which occasionally happens, catch this typo with:
{% highlight bash %}alias sl="ls"{% endhighlight %}

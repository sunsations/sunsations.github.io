---
layout: post
title: "Use cat to create a File"
modified: 2014-02-19 06:58:49 +0100
tags: [bash tricks, cat]
comments: 
share: 
---
# Cat your next File

Here is a neat bash trick to create a new file,
without opening a text editor at all. When you are working on the 
command line, this is probably the leanest way of doing it.


{% highlight bash %}
cat >> your_new_file
Type or paste your content here...
{% endhighlight %}

To finish type ````Ctrl+D````. Done.

The big disadvantage of course is, that your are unable
to edit text this way. But for simple pasting content
or just a one or two line file, it's perfect.

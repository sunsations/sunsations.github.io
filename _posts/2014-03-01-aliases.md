---
layout: post
title: "Use Bash Aliases"
modified: 2014-03-19 00:37:19 +0100
tags: [bash, aliases, unix]
comments: 
share: 
---

# Bash Aliases

If you are like me and love working on the command line
you sooner or later start customizing your work flow to 
exactly match your preferences.

I just did that over the last couple of years and want
to share some of the most useful aliases I created in this time.
This will be a series of blog post about my aliases.

But first things firsts. What is an alias? According to 
[tlpd.org](http://tldp.org/LDP/abs/html/aliases.html):

> A Bash alias is essentially nothing more than a keyboard shortcut, an abbreviation, a means of avoiding typing a long command sequence.

Lets make an example of this useful Unix tool. Instead of typing ````ls -lah```` over
and over again, you just want to type ````l```` instead. Type the following command in your console:

{% highlight bash %}alias l="ls -lah"{% endhighlight %}

Now you can save yourself some typing and just use ````l````.

To get all your defined aliases, use:
{% highlight bash %}alias{% endhighlight %}

To remove an alias, use:
{% highlight bash %}unalias l{% endhighlight %}

Use ````type```` to get information about your alias
{% highlight bash %}type l # => l is aliased to `ls -lah'{% endhighlight %}

The problem with defining aliases on the fly is that after you
close your shell or open a new one, your alias is gone. Thus,
you need a way to persist them. Here comes ````~/.bashrc```` into play.
Simple add your alias there. Afterwards each new terminal is aware of your 
new alias, except the current one if you defined it only in ````~/.bashrc````.
To use your alias in your current shell after you defined it in ````~/.bashrc````,
you must ````source```` your ````~/.bashrc```` file with:

{% highlight bash %}source ~/.bashrc{% endhighlight %}

# Streamline your alias definitions and usage
I personally use an alias to streamline creating and using
aliases. Depending on your settings, customize the following
alias ````val```` to match you needs. Val is an mnemonic for
Vim Aliases. So what is ````val````? As described above, use
````type```` to find it out.

{% highlight bash %}type val # => val is aliased to `vim ~/.bashrc; source ~/.bashrc'{% endhighlight %}

It basically lets you create, update or delete aliases in you editor (Vim in this case).
As soon as you exit your editor, your aliases get sourced and
are immediately available in your current shell. I found that tremendously useful.

# Maintainability of aliases
Since it is very easy to create new aliases with ````val````, I defined
more and more aliases. I personally group related aliases together and 
store them in a separate file (`````~/.bash_aliases`````) and source
it from ````~/.bashrc````. 

In case I forget one, I'm fortunate enough to always remember ````a````,
which is bash helper function to grep over all aliases:

{% highlight bash %}function a() {
  cat ~/.bash_aliases | grep -i "$1";
}{% endhighlight %}




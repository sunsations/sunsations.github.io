---
layout: post
title: "Tree, a quick discovery tool"
modified: 2014-03-21 01:15:54 +0100
tags: [tree, unix, bash]
comments: 
share: 
---
# Tree

[````tree````](http://en.wikipedia.org/wiki/Tree_(Unix)) is a recursively directory listing tool.

With some customizations, ````tree```` has become one of my favorite tools to quickly and easily get an
overview of any directory structure. 

Lets start with the following helper function:
{% highlight bash %}
# tree.sh
t1() { 
  _tree_with_level 1 $1
}
t2() {
  _tree_with_level 2 $1
}
t3() {
  _tree_with_level 3 $1
}
t4() {
  _tree_with_level 4 $1
}
t5() {
  _tree_with_level 5 $1
}

_tree_with_level() { 
  LEVEL=$1
  DIR=$2
  if [ -z "$DIR" ]
  then
     DIR="."
  fi
  tree -L $LEVEL $DIR | more
}
{% endhighlight %}

Make sure to ````source```` this file in your ````~/.bashrc````.

What is this function doing? It creates some short and nice helper
wrappers that uses ````tree```` with the level option. Since most
of the time the output of ````tree```` is too long to fit into
the console, the output is piped to ````more````.

Now, whenever I clone a repository and or download anything, 
one of the first thing I do, is get an overview of the directory
structure. ````tree```` is a perfect fit for that. I start
with ````t2````, proceed with ````t3```` and so forth. If want
to get more information of a specific directory, I use ````t2 directory````.
For me that is much faster and more convenient than for example with [Finder](http://en.wikipedia.org/wiki/Finder_(software)).

# Options
Apart from the level option there are some other option worth mentioning.

* ````-C```` to get colorful output
* ````-d```` to list only directories
* ````-a```` to list also hidden files

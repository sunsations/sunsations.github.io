---
layout: post
title: "Useful Git Aliases"
modified: 2014-03-19 00:37:19 +0100
tags: [bash, aliases, unix, git]
comments: 
share: 
---
# Git Command Line Helpers (Aliases and Functions)

This blog post is part of the [aliases series](/aliases). If you just get 
started and want to know more about aliases, start there.

If you don't yet use a [versioning control system](http://en.wikipedia.org/wiki/Revision_control), stop reading and look for a [tutorial on git](https://www.google.com/?#q=git+tutorial). In my humble opinion it's absolutely essential, even
just for yourself, to always use a versioning system. The benefits always outweigh the costs.

So lets get started. Git itself allows for various customization.
Here is the alias excerpt of my ````~/.gitconfig````. I strongly recommend the ````lg```` alias.
The log output is just so much nicer.

{% highlight bash %} 
[alias]
        lol = log --oneline --graph --decorate
        st = status
        co = checkout
        ci = commit
        br = branch
        lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
{% endhighlight %}

The aliases I created are most of the time just a combination
of the first one or two letters of the full git command and thus
easy to remember. They all start with the letter g.

{% highlight bash %}# GIT Aliases
alias gcl="git clone "
alias gp="git pull"
alias gpl="git pull && git lg"
alias gi="git init"
alias gaa='git add -A && git status'
alias gb='git branch'
alias gbd='git branch -d'
alias gbD='git branch -D'
alias gl="git lg"
alias gs='git status'
alias gsa='git status --untracked-files'
alias gsm='git status | more'
alias gd='git diff'
alias gdc='git diff --cached'
alias gw='git whatchanged'
alias gdh="git diff HEAD~1..HEAD"
alias gdh2="git diff HEAD~2..HEAD~1"
alias gpom='git push origin master'
alias gphm='git push heroku master'
alias gcom='git checkout master'
alias gco='git checkout '
alias gcob='git checkout -b '
alias gm='git merge '
alias grh='git reset HEAD '
alias giac='git init && git add -A && gc '     # gc helper function defined in .bashrc
alias gac='git add -A && gc '                  # gc helper function defined in .bashrc
{% endhighlight %}

Some of the really useful aliases (````giac```` and ````gac````) depend
on git helper functions. I defined them in a ````git.sh```` script and 
source it from ````~/.bashrc````. 

{% highlight bash %}# git.sh
## Git: commit helper function
gc() { 
  git commit -m "$*" && echo "---COMMITED---" && git status && git lg head -n5;
}

## Git: add helper function
ga() { 
  git add "$*" && echo "---ADDED---" && git status && git lg | head -n5;
}

## Git: commit push helper function
gcp() { 
  git commit -m "$*" && git push origin master && echo "---COMMITED and PUSHED---" && git status && git lg | head -n5;
}

## Git: Combine add / commit and push in one command
gacp() { 
  git add -A && git commit -m "$*" && git push origin master && echo "---ADDED, COMMITED and PUSHED---" && git status && git lg | head -n5;
}
{% endhighlight %}

Whenever I start a new project (even a small and disposable one), the absolutely
first thing I do in that directory is ````giac "Inital commit"````. This initializes a new Git repository,
adds all files and commits them with the message "Initial commit".
As soon I have snapshot, to revert back in case I have to, I use ````gac "my commit message"````.
It's as easy as that. 

## Conclusion
Make Git with the help of aliases and functions part of your tool chain.


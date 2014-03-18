---
layout: post
title: "Fast way to create a Ruby file with Vim"
modified: 2014-02-10 00:48:09 +0100
tags: [vim, ruby]
comments: 
share: 
---
# Quick and easy way to write Ruby file with Vim

What is the fastest and most convenient way to create
a new ruby file? My guess:

````vimr <filename.rb>````

After executing this command, you are within Vim on line 2 in insert mode and can start
writing right away. Additionally the file is made executable
and contains a ruby shebang line. 

If you would do it manually there are a several steps 
involved, you have to make each and every time. We as
programmers want to automate as much as possible to keep
boring and repetitive task to an absolute minimum.

So what is `````vimr`````? It's just a bash script:

{% highlight bash %}
#!/usr/bin/env ruby
# Taken from the ruby book
# Ruby for System Administration
# and adapted it slightly.
#
# This automates step 1 to 5
# 1. Open an editor.
# 2. Create a new file.
# 3. Throw a shebang line at it: #!/usr/bin/env ruby.
# 4. Save the file as something.rb.
# 5. Switch to the console and render the script executable: chmod 755 something.rb. 
# 6. Start writing the actual script.
path = ARGV[0]
fail "specify filename to create" unless path
File.open(path, "w") { |f| f.puts "#!/usr/bin/env ruby -w"; f.puts "" }
File.chmod(0755, path)
system "vim +2 -c 'startinsert' #{path}"
{% endhighlight %}

That's it. Fast and easy. Depending on your needs adapt it to create
bash or whatever files. I also frequently use ````vimb```` to create
bash scripts.

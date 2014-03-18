---
layout: post
title: Ruby Date Calculations
description: "Performance comparison between Ruby's standard library and Rails ActiveSupport for Date calculations."
modified: 2014-03-18
category: articles
tags: [ruby, date, benchmark]
comments: false
share: false
---

In a hobby project I had to calculate quite a few dates. Rails ActiveSupport extensions are great for readable code. Here are a few examples:

{% highlight ruby %}
Date.new(2014, 1, 1) + 1.day    # => Thu, 02 Jan 2014
Date.new(2014, 1, 1) + 2.months # => Sat, 01 Mar 2014
{% endhighlight %}

However, I noticed it's quite slow when doing heaps of calculations. Here is the same calculation with Ruby's standard library.

{% highlight ruby %}
Date.new(2014, 1, 1).next_day(1)   # => Thu, 02 Jan 2014
Date.new(2014, 1, 1).next_month(2) # => Sat, 01 Mar 2014
{% endhighlight %}

## Performance Comparison
I was curious how big the performance difference is. Using [Benchmark](http://www.ruby-doc.org/stdlib-2.1.0/libdoc/benchmark/rdoc/Benchmark.html) it's easy to get this information.

{% highlight ruby %}
#!/usr/bin/env ruby

require 'benchmark'
require 'date'
require 'active_support/all'

ITERATIONS=100000

Benchmark.bm(25) do |bm|
  bm.report "Ruby Standard Library" do
    ITERATIONS.times do
      Date.today.next_year(1).next_month(1).next_day(1)
    end  
  end  
  bm.report "Rails ActiveSupport" do
    ITERATIONS.times do
      Date.today + 1.year + 1.month + 1.day
    end  
  end  
end
{% endhighlight %}

Here is the output:

{% highlight bash %}
                                user     system      total        real
Ruby standard library       0.390000   0.000000   0.390000 (  0.383113)
Rails ActiveSupport         4.180000   0.000000   4.180000 (  4.186447)
{% endhighlight %}

## Conclusion
Using ActiveSupport instead of Ruby's Standard Library for Date calculation
is around 10 times slower.

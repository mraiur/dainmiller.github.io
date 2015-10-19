---
published: true
title: CSV Generation in Ruby
layout: post
tags: [ruby, csv]
categories: [ruby]
summary: The beauty of CSV.generate.
---
Did you know can convert a simple ruby hash to a CSV pretty painlessly? 

Here's an example:

{% highlight ruby %}
example = [{ one: 1, two: 2, three: 3, four: 4 },{ five: 5, six: 6, seven: 7, eight: 8 }]
headers = [ 'Word', 'Integer' ]

CSV.generate do |csv|
  csv << headers
  example.each do |obj|
    csv << obj.values
  end
end
{% endhighlight %}

Andddd, you're done. Works like magic. 

---
layout: post
title: "Learning, muscle memory, typing"
date: 2013-01-20 16:39
comments: true
categories: [learning, ruby, learn-ruby-the-hard-way, typing]
---
Going through Zed Shaw's [Learn Ruby the Hard Way](http://ruby.learncodethehardway.org/book/), I now recognize the importance of typing in the context of learning to program a new language. My professional experience in software development consisted of .NET development in C#, which is extremely similar to JAVA in syntax. So, upon encountering Ruby syntax elements such as pipes '|', typing the code becomes slow due to a lack of practice, which impedes and constricts thinking. 

```ruby Exercise 12: Libraries http://ruby.learncodethehardway.org/book/ex12.html Source Article

require 'open-uri'

open("http://www.ruby-lang.org/en") do |f|
  f.each_line {|line| p line}
  puts f.base_uri         # <URI::HTTP:0x40e6ef2 URL:http://www.ruby-lang.org/en/>
  puts f.content_type     # "text/html"
  puts f.charset          # "iso-8859-1"
  puts f.content_encoding # []
  puts f.last_modified    # Thu Dec 05 02:45:02 UTC 2002
end
```
Typing code like the excerpt above has developed muscle memory for me, and made me think of solutions faster, just as Zed said it would. 

Happy typing!

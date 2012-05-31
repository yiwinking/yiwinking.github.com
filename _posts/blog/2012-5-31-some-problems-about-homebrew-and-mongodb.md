---
layout: post
category : blog
title :  Homebrew problem
tags : [ Homebrew , Problems ]
---

when I use homebrew to reinstall mongodb today,it comes `/usr/local/Library/Homebrew/tab.rb:1:in `require': no such file to load -- ruby:ostruct (LoadError)`

so I checked the file , and found that ostruct.rb is from ruby libs.

then check the libs under `/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/1.8/` and compared with kevin's, lots of libs missed.

so I got a copy from kevin, and this problem resolved.




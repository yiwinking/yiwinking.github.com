---
layout: post
category : blog
title : Ruby exception
tags : [ Ruby , Exception ]
---



ruby exception

Exception  

1. NoMemoryError  

2. ScriptError  

   LoadError  

   NotImplementedError  

   SyntaxError  

3. SignalException  

   Interrupt  

4. StandardError  

   ArgumentError  

   IOError  

     EOFError  

   IndexError  

   LocalJumpError  

   NameError  

     NoMethodError  

   RangeError  

     FloatDomainError  

   RegexpError  

   RuntimeError  

   SecurityError  

   SystemCallError  

   SystemStackError  

   ThreadError  

   TypeError  

   ZeroDivisionError  

4. SystemExit  

 fatal  


  If we need to throw a Exception,we can use the exception class above ,or create one from StandardError.

  We use `begin`,'rescue',`end`,`raise`,`ensure`,`retry`,`catch`,`throw` to deal with Exception.

for example, put the code which will create Exception between `begin`,`end`. and the code after `rescue`, will deal with the Exception.such as:

`open_file = File.open(open_file_name, "w")`

`begin`

`while data = socket.read(512)`

`    open_file.write(data) `

`end` 

`rescue SystemCallError  `

`  $stderr.print "IO failed: " + $!  `

`  open_file.close  `

`  File.delete(open_file_name)  `

`  raise  `

`end   `

But as we all known , use `$!` is not a good way to controller the Exception, cause thewe can get this Exception everywhere. So we can create a variable for it.

If we want to know the kind of  Exceptions, use `exception.kind_of?`

In many cases, we need to do sth , no matter `resuce` work or not, here we can use `ensure`,for example,

`f = File.open("testfile")  `

`begin  `

`  # .. what you want to do  `

`rescue  `

`  # .. handle error  `

`else  `

`  puts "OK"`

`ensure  `

`  f.close unless f.nil?  `

`end   `

http://rails-weekly.group.iteye.com/group/wiki/1821-rails-questions-weekly-12-ruby-exception-mechanism
http://my4java.itpub.net/post/9983/63710
rails
http://clark1231.iteye.com/blog/1446693
http://hlee.iteye.com/blog/353732


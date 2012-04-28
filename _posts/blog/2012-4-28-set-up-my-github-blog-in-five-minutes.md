---
layout : post
category : blog
title : Set Up My Github Blog in Five Minutes 
tags : [Gem , Jekyll , Jekyll-Bootstrap ]
---

## First step : create a account in github and install git

 Create your account <a href = "https://github.com/signup/free">here</a>.

 Set up git <a href = "http://help.github.com/mac-set-up-git/">here</a>.

 Read <a href = "http://en.wikipedia.org/wiki/Git_(software)">git information</a>. 

#### Install Git : 
#####   in <a href = "http://help.github.com/linux-set-up-git/">Linux</a>
#####   in <a href = "http://help.github.com/mac-set-up-git/">mac-OSX</a>
#####   in <a href = "http://help.github.com/win-set-up-git/">Windows</a>

## Second step : add Gem  `Jekyll` 

## `gem install jekyll`

Jekyll is a ruby Gem for blog aware, documents  in <a href = "https://github.com/mojombo/jekyll">English</a>, <a href = "http://chen.yanping.me/cn/blog/2011/12/15/building-static-sites-with-jekyll/">Chinese </a>.


## Third stpe : Clone a blog with Jekyll-bootstrap

 Now we use <a href = "https://github.com/plusjade/jekyll-bootstrap">Jekyll-Bootstrap</a> to clone a blog for us.
#### USERNAME is your github name.

## `git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com`
## `cd USERNAME.github.com`
## `git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git`
## `git push origin master`

 USERNAME.github.com can be seen when steps finished.

###Run at local
## `jekll --server`
local server starts at port 4000, type http://localhost:4000/ in your brower, blog works.


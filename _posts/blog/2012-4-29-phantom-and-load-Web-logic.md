---
layout: post
category : blog
title : Phantom usage and loading webpage logic 
tags : [Phoantom , WebLoading logic]
---

I used phantom to get information from a SNS community last week , it's considerably cool and easy to use. But if we don't take care of these two points ,maybe we will  waste time for our working and get nothing.  

####<a href ="http://code.google.com/p/phantomjs/wiki/QuickStart">phantom document</a>

### Usage:
1.create a webpage object object.

`var page = require ("webpage").create();`

2.open the page with URL 

`page.open("url",function(status){ Function_loading })`

3.loading page

we can divide Function_loading into two parts.

part one for judging open page with URL, by status ,with 'true' or 'false'.

part two for loading successfully,and page object can be used to evaluate.

for example:

`var page_body_information = page.evaluate(function(){`

`  var body_info = document.body.innerHTML;`

`  return body_info;`

`}); `


4.destroy the object.

`phantom.exit();` 

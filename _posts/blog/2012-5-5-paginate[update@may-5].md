---
layout: post
category : blog
title : Paginate and it's thought
tags : [ Paginate , Thought , Gem ]
---

Paginate,my thought about it was wrong before.

the lastest time I used paginate is no long ago,whit `Gem
'kaminari'`(like Gem 'will_paginate')

In controller, I wrote method like this:

`@model_variables = Model.page(params[:page]).per(5)`

with the 'parms' page and per,I thought it was Model find all the variable objs one time, then separate them into pages.and show them on views with

`<%= paginate @model_variables%>`

In fact,it is wrong and it doesn't work like this.

The thought of paginate should find objs as the limit count in a page,it will find them when the page need. That means ,to save time and to improve efficiency, each page should call the database for its' calling ,and should call the database every page change.

 

---
layout: post
category : blog
title : Rails custom error page
tags : [ Rails , Error page , Custom ]
---
Custom dynamic error pages in Ruby on Rails:

Document :

.1: <http://wildjcrt.pixnet.net/blog/post/28742487-rails-3-%E8%99%95%E7%90%86-errors-%E7%9A%84%E9%A0%81%E9%9D%A2>

.2: <http://techoctave.com/c7/posts/36-rails-3-0-rescue-from-routing-error-solution>

.3: <http://www.perfectline.ee/blog/custom-dynamic-error-pages-in-ruby-on-rails>

.4: <http://blog.aizatto.com/2009/02/06/building-custom-error-pages/>


####First :

  we should set the config environment,defaults,true for development, false for production:

`config.action_controller.consider_all_requests_local = false`

####Second :

  use method : `rescue_from` in `ApplicationController`

  something about rescue:

`ActiveSupport::Rescuable::ClassMethods`

`activesupport/lib/active_support/rescuable.rb`

<http://api.rubyonrails.org/classes/ActiveSupport/Rescuable/ClassMethods.html>

then use it ,like this:

rescue_from Exception, :with => :render_error

####Third :

define `render_error`

  def render_not_found(exception)

    log_error(exception)

    render :template => "/error/404.html.erb", :status => 404

  end

####Fourth :

add 404 page or something else .

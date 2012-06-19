---
layout: post
category : blog
title : Gem capybara-webkit install problem and tencent weibo cookies 
tags : [ Gem , Capybara-webkit , Cookies , Problems ]
---

Installing capybara-webkit (0.11.0) with native extensions Unfortunately, a fatal error has occurred. Please report this error to the Bundler issue tracker at https://github.com/carlhuda/bundler/issues so that we can fix it. Thanks!

/home/ubuntu/.rvm/rubies/ruby-1.9.3-p125/lib/ruby/site_ruby/1.9.1/rubygems/installer.rb:552:in `rescue in block in build_extensions': ERROR: Failed to build gem native extension. (Gem::Installer::ExtensionBuildError)


Solution:

https://github.com/thoughtbot/capybara-webkit/wiki/Installing-Qt-and-compiling-capybara-webkit


tencent weibo problem :

=================
Cookie expired
=================

Solution:

login in tencentweibo, use firfox or chrome to find the cookies, and add it to the cookies.txt

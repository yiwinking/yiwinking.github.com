---
layout : post
category : blog
tags : [Gem , sinaweibo , authentication , oauth2]
---

Cause weibo update its oauth into oauth2, and abandon the first one on September , all the websites those use oauth should follow its update. So Gem "omniauth-weibo-oauth2"
may be a good choose for ruby guys. 

if we test this gem with "localhost:3000" ,it will come Error "你所访问的站点在新浪微博的认证失败，请你联系注册者或者稍后再试。(error:redirect_uri_mismatch)",  I fixed this problem with the following steps , hope will be helpful for U . :)

 here comes solution. 

first , you need to register one weibo account for this , then update your developer info <a href = "http://open.weibo.com/developers/basicinfo">Here</a>.
then also add website info <a href = "http://open.weibo.com/webmaster/add">here</a>for verification, remember `api_key` ,`api_secret`, and the websit domain ,make "www.winking.com" as an example.

second , add "127.0.0.1 www.winking.com" to /etc/hosts

third , config/services.yml for setting your weibo api_key and api_secret , set redirect_uri like this , "http://www.winking.com:3000/users/auth/weibo/callback"

then `rails s`

fourth, type "http://www.winking.com:3000" for testing.

---
layout : post
category : blog
title : how to deploy a padrino project into a server
tags : [Padrino , Deploy , Ruby , Mysql , Server ]
---

To deploy a padrino project with passenger and nginx to a new server,it should be a easy job.

But when I deployed ,quite a lot of  problems come up. so this page will be helpful to 

first should add the linux first 

install nesseilly linux libs
 
(安装所需的linux包)

sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev  libxml2-dev libxslt-dev autoconf libc6-dev zlib1g-dev libssl-dev build-essential curl git-core libc6-dev g++ gcc

then install  RVM,the manager for Ruby controller

安装 rvm

bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)

加载rvm (只需第一次安装时加载)

source .bashrc

use  `` to show if the rvm installed successfully.


安装ruby libs.

sudo aptitude install build-essential bison openssl libreadline5 libreadline5-dev curl git-core zlib1g zlib1g-dev libssl-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libmysqlclient-dev

rvm install 1.9.3

then rvm list ,got

#get Problem one:

Default ruby not set. Try 'rvm alias create default ruby'.

#solvtion then type:
rvm alias create default 1.9.3

add 1.9.3 as default
rvm use 1.9.3 --default

add passenger as ruby version  1.9.3

rvm 1.9.3 --passenger

but get Note message :
NOTE: If you are using Passenger 3 you no longer need the passenger_ruby,
use the wrapper script for your ruby instead (see 'rvm wrapper')
 
so no need to take care of this Note,cause the ENV will be setted by itself.



rvm use 1.9.3 default

then install passenger and nginx with Gem and rvmsudo

gem install passenger
rvmsudo passenger-install-nginx-module

when we install the passenger-install-nginx-module , there comes problem 2 
#Problem two:
Curl development headers with SSL support... not found

just go on ,cause it will 提示 us which libs we need
(go on)
To install Curl development headers with SSL support:
   Please run apt-get install libcurl4-openssl-dev or libcurl4-gnutls-dev, whichever you prefer.
#solvtion:
so sudo apt-get install libcurl4-openssl-dev

try to get passenger start with it's command:
but alse got problems:
#Problem three
passenger start
passenger start
=============== Phusion Passenger Standalone web server started ===============
PID file: /home/ubuntu/humanoid/tmp/pids/passenger.3000.pid
Log file: /home/ubuntu/humanoid/log/passenger.3000.log
Environment: development
Accessible via: http://0.0.0.0:3000/

You can stop Phusion Passenger Standalone by pressing Ctrl-C.
===============================================================================
[ pid=32362 thr=13093500 file=utils.rb:176 time=2012-05-03 01:02:55.601 ]: *** Exception PhusionPassenger::UnknownError in PhusionPassenger::Rack::ApplicationSpawner (undefined method `<<' for nil:NilClass (NoMethodError)) (process 32362, thread #<Thread:0x000000018f94f8>):
	from /home/ubuntu/.rvm/gems/ruby-1.9.2-p320/gems/rack-flash-0.1.2/lib/rack/flash.rb:20:in `run'

I don't know how to fix this problem,so try to restart the nginx:
also ,comes problems 

restart ngnix 
sudo /etc/init.d/nginx start
 * Starting Nginx Server...                                                                                                                                                                                                                 Segmentation fault

Segmentation fault ,dump,another problem comes ,I try to find out what  the problems are,but false, the solvtions google gives can't help

so I ask kevin and Yasith for help.

It may cause by  diffrent versions,so sooyoung create anouther new server for me ,so the problem get out .

 
then I clone the project from the server.
first I should create a key and add it to the server system.

how to add ssh key document.click the link <http://help.github.com/mac-set-up-git/>

then git clone the code.
we cannot run the project without database,so install Mysql.
install mysql
sudo apt-get install mysql-client mysql-server
and  install padrino by Gem.

gem install padrino
 
we should bundle install, but some small problems happen,so after bundle install,just use bundle update
bundle install
bundle update

then create the database for this project.

bundle exec padrino rake ar:create
=> Executing Rake ar:create ...
rake aborted!
uninitialized constant Mysql

Tasks: TOP => ar:create
(See full trace by running task with --trace)

so bundle exec padrino rake ar:create --trace 
Can't connect to local MySQL server through socket '/tmp/mysql.sock'
 ln -s /var/run/mysqld/mysqld.sock /tmp/mysql.sock


create % migrate

rake aborted!
undefined method `name' for nil:NilClass


/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb:44:in `header'
/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb:26:in `dump'
/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb:21:in `dump'
/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/padrino-gen-0.10.1/lib/padrino-gen/padrino-tasks/activerecord.rb:244:in `block (4 levels) in <top (required)>'
/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/padrino-gen-0.10.1/lib/padrino-gen/padrino-tasks/activerecord.rb:243:



home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb :44

if stream.respond_to?(:external_encoding).nil?
          stream.puts "# encoding: #{stream.external_encoding.name}"
        end

 sudo /etc/init.d/nginx start
 * Starting Nginx Server...                                                                                         nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)

stop other nginx ,use bin ,not init.d/nginx
sudo /opt/nginx/sbin/nginx -s stop


undefined method '<<' for nil:NilClass
https://github.com/nakajima/rack-flash/issues/8

Confirmed with these:
Using bundler (1.0.21)
Using rack (1.3.5)
Using rack-flash (0.1.2)
Using sinatra (1.3.1)
ruby 1.9.3p0
https://github.com/nakajima/rack-flash/issues/8

Passenger encountered the following error:
The application spawner server exited unexpectedly: Connection closed

Exception class:
PhusionPassenger::Rack::ApplicationSpawner::Error
http://code.google.com/p/phusion-passenger/issues/detail?id=590







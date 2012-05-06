---
layout : post
category : blog
title : how to deploy a padrino project into a server
tags : [Padrino , Deploy , Ruby , Mysql , Server ]
---

To deploy a padrino project with passenger and nginx to a new server,it should be a easy job,but I did not use nginx before,and It seems quite a lot of problems came out.

This article may be useful for those who get the same probelms.

###First we should install some necessary  linux libs. 

`sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev  libxml2-dev libxslt-dev autoconf libc6-dev zlib1g-dev libssl-dev build-essential curl git-core libc6-dev g++ gcc`

###then  install RVM and loading RVM ENV.

`bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)`

Loading rvm ENV

`source .bashrc`

use  `rvm info` or `type rvm|head -n 1` to check if the rvm installed successfully.


###install necessary ruby libs.

`sudo aptitude install build-essential bison openssl libreadline5 libreadline5-dev curl git-core zlib1g zlib1g-dev libssl-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libmysqlclient-dev`

###install ruby in rvm
rvm install 1.9.3

then rvm list ,got

#####get Problem :

Default ruby not set. Try 'rvm alias create default ruby'.

#####solution :
`rvm alias create default 1.9.3`

then add 1.9.3 as default:

`rvm use 1.9.3 --default`

add passenger as ruby version  1.9.3

rvm 1.9.3 --passenger

but get Note message :
NOTE: If you are using Passenger 3 you no longer need the passenger_ruby,
use the wrapper script for your ruby instead (see 'rvm wrapper')
 
 No need to take care of this Note,cause the ENV will be setted by itself.

`rvm use 1.9.3 default`.

###then install passenger and nginx with Gem and rvmsudo

`gem install passenger`

`rvmsudo passenger-install-nginx-module`

when we install the passenger-install-nginx-module , there comes another problem ,

#####Problem:
Curl development headers with SSL support... not found

#####Solution:
just go on ,cause it will prompt  us that which libs we need and should be installed

To install Curl development headers with SSL support:
   Please run apt-get install libcurl4-openssl-dev or libcurl4-gnutls-dev, whichever you prefer.

#####Solution:
`sudo apt-get install libcurl4-openssl-dev`


try to get "passenger start" with it's command:`passenger start`,

but alse got problems:

#####Problem three

passenger start

"=============== Phusion Passenger Standalone web server started ==============="
PID file: /home/ubuntu/humanoid/tmp/pids/passenger.3000.pid
Log file: /home/ubuntu/humanoid/log/passenger.3000.log
Environment: development
Accessible via: http://0.0.0.0:3000/

You can stop Phusion Passenger Standalone by pressing Ctrl-C.

: [ pid=32362 thr=13093500 file=utils.rb:176 time=2012-05-03 01:02:55.601 ]  Exception PhusionPassenger::UnknownError in PhusionPassenger::Rack::ApplicationSpawner (undefined method `<<' for nil:NilClass (NoMethodError)) (process 32362, thread #<Thread:0x000000018f94f8>)
from /home/ubuntu/.rvm/gems/ruby-1.9.2-p320/gems/rack-flash-0.1.2/lib/rack/flash.rb:20:in `run'
:

I don't know how to fix this problem,try to restart the nginx,

comes other problems 

restart ngnix 

`sudo /etc/init.d/nginx start`


: * Starting Nginx Server...                                                                                                                                                                                                                 Segmentation fault:

Segmentation fault ,I tried to find out what the problems were ,but fail, the solutions which  google gives can't help.

so I ask kevin and Yasith for help.

It may arise  by diffrent versions of  passenger and nginx ,so sooyoung create anouther new server ,and start to install again,`Segmentation` problem disappear.

 
Then I clone the project from the server.

##First I should create a key and add it to the server system.

how to add ssh key document.click the link <http://help.github.com/mac-set-up-git/>

then git clone the code,`git clone "code address"`

we cannot run the project without database,so install Mysql.

###install mysql
`sudo apt-get install mysql-client mysql-server`

###and  install padrino by Gem.

`gem install padrino`
 
we should bundle install, but some small problems happen,so after bundle install,just use bundle update

`bundle install` and `bundle update`.

###create the database for this project.

`bundle exec padrino rake ar:create`

#####problem 
=> Executing Rake ar:create ...
rake aborted!
uninitialized constant Mysql

Tasks: TOP => ar:create
(See full trace by running task with --trace)

so `bundle exec padrino rake ar:create --trace `

Can't connect to local MySQL server through socket '/tmp/mysql.sock'

then I found the database ENV has another link,just ln it to that which  the server needs.

#####Solution

`ln -s /var/run/mysqld/mysqld.sock /tmp/mysql.sock`

Try again,creates migrations

#####problem

rake aborted!
undefined method `name' for nil:NilClass

/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb:44:in `header'

/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb:26:in `dump'

/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb:21:in `dump'

/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/padrino-gen-0.10.1/lib/padrino-gen/padrino-tasks/activerecord.rb:244:in `block (4 levels) in <top (required)>'

/home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/padrino-gen-0.10.1/lib/padrino-gen/padrino-tasks/activerecord.rb:243:

#####solution
then open the file,

home/ubuntu/.rvm/gems/ruby-1.9.3-p194/gems/activerecord-3.0.12/lib/active_record/schema_dumper.rb :44

add `.nil?` to jump this problem.

if stream.respond_to?(:external_encoding).nil?
          stream.puts "# encoding: #{stream.external_encoding.name}"
        end


### start nginx again

` sudo /etc/init.d/nginx start`

#####problem

 * Starting Nginx Server...                                                                              

nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)

nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)

#####solution:

stop other nginx ,use bin ,not init.d/nginx

`sudo /opt/nginx/sbin/nginx -s stop`

###start nginx again

#####problem

undefined method '<<' for nil:NilClass

thanks to the article,<https://github.com/nakajima/rack-flash/issues/8>

Confirmed with these:

Using bundler (1.0.21)
Using rack (1.3.5)
Using rack-flash (0.1.2)
Using sinatra (1.3.1)
ruby 1.9.3p0

#####solution
` degrade the versions of rack,rack-flash,sinatra`

But another problem comes,

#####problem

Passenger encountered the following error:

`The application spawner server exited unexpectedly: Connection closed`

`Exception class:`

`PhusionPassenger::Rack::ApplicationSpawner::Error`

It is hard to find out the solution for this problem, <http://code.google.com/p/phusion-passenger/issues/detail?id=590>,this article may be helpful,
but after my trying,it seems not.

In fact,I don't know why I can meet these quite a lot of problems,finally,another new server was created to deploy for the project,with kevin,yasith,sooyoung's help,
It works. I should ask them for steps and attention about deploying this padrino project on Monday.










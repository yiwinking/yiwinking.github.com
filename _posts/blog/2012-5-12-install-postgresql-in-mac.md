---
layout: post
category : blog
title : Install postgresql in mac
tags : [ Postgres SQL , Database ]
---


`sudo brew install postgresql`

`sudo mkdir /usr/local/var/postgres`

`sudo chown seven /usr/local/var/postgres`

`initdb /usr/local/var/postgres`

after finished, it will says,

database user : /usr/local/Cellar/postgresql/9.1.3/homebrew.mxcl.postgresql.plist

start:

`postgres -D /usr/local/var/postgres`

or

`pg_ctl -D /usr/local/var/postgres -l logfile start`

stop :

`xpg_ctl -D /usr/local/var/postgres stop -s -m fast`

Document:

<http://gibuloto.com/blog/install-postgresql-in-mac-osx-lion/>

start padrino with postgres:

<http://www.padrinorb.com/guides/basic-projects>

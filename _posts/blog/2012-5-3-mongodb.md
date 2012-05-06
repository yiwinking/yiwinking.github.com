---
layout: post
category : blog
title : Mongodb and MongoMapper
tags : [Mongodb , Database , MongoMapper ]
---
### Install mongodb
`brew install mongodb`

mongodb homepage <http://www.mongodb.org/display/DOCS/Home>

####some usual mongo commands :

`show  dbs`
`show  collections`
`show  users`              
`show  profile`     
`use <db name>`    
`db.help()`                    help on DB methods
`db.foo.help()`                help on collection methods
`db.foo.find()`                list objects in collection foo
`db.foo.find( { a : 1 } )`     list objects in foo where a == 1 

####CURD

#####create

db.createCollection("user"); 

#####insert

db.user.insert({uid:1,username:"yiwinking",age:1});

#####find

db.user.find(); 

db.user.find({uid:1}); 

find methods :limit ，sort ，findOne，distinct

#####update

db.user.update({uid:1},{$set:{age:26}})

update method :$unset、$push 、$pushAll 、$pop 、$pull 、$pullAll


###some skills

find out using db :`db`

change db :`use "db"`

find out mongodb commands: `help`

find out db methods : `db.help()`


###Mongo mapper
Document:<http://mongomapper.com/>

install `gem install mongo_mapper`

####Querying
Finders methods:
(Actually,the methods like rails)

`Model.all` => find all

`Model.find(id)` => find though id

`Model.first' , `Model.last` => first and last one

Model.paginate({

  :order    => :created_at.asc,

  :per_page => 25, 

  :page     => 3,

})

`per_page` means per in every page

`page` means in which page.

`models = Model.where(:first_name => "winking", :last_name => "Yi")` 

`Model.count` => number of model's obj

`Model.sort(:first_name)` => sort by first_name

`Model.sort(:first_name).limit(100)` find  objs with 100 limit


 




http://blog.csdn.net/yczz/article/details/5972624

collenction :http://www.51099.com/comp/dade/20101019/354845.html

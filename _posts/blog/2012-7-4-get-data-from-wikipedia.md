---
layout: post
title : 
category : blog
tags : [Wikipedia , Ruby , Script]
---

 Gems list : 

    .
    require "rubygems"

    require "rdf" : http://rubydoc.info/github/ruby-rdf/rdf/master/frames

    require "linkeddata" : http://rdf.greggkellogg.net/yard/index.html

    require "active_record"

    require "uri"

    require "json"

    require "rest_client" : http://rubydoc.info/gems/rest-client/1.6.7/frames

    require "escape_utils" : http://rubydoc.info/gems/escape_utils/0.2.4/frames

    require "date"

This script is for getting data from wikipeida (in fact , from dbpedia) and update english part from live.dbpeida.org.

Make "http://dbpedia.org/page/Sergio_Agüero" as an example ,

BTW , this link will encode to "http://dbpedia.org/page/Sergio_Ag%C3%BCero" , and if we want its rdf format ,please  check  

"http://dbpedia.org/resource/Sergio_Ag%C3%BCero" or 

"http://dbpedia.org/data/Sergio_Ag%C3%BCero.rdf" , 

 and its live site link is  "http://live.dbpedia.org/data/Sergio_Ag%C3%BCero.json", for json.

######part two : functions

Function 1 : `update_log_file` for updating log and writing to log.txt . 

Function 2 : `get_live_english_abstract(name)` for getting  english abstract from live site. 

 this function use `RestClient.get(json_url)` to get  json data and return Json parser by using `JSON.parse(json_data)` , then match abstract .

Function 3 : `self.find(search_url)`
 
    
     









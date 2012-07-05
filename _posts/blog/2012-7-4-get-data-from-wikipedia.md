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

#####part one : logic

`csvparser.rb` script, it read a CSV file, which has identity and wiki_link, then update identity (`update_identity(wiki_data_hash)`) from ??API.  

    .

`wikibot.rb` script, `fetch_wiki_urls` creates wiki_identity_list (identity hash) , and identities  have keys : "id","name","wiki_url" . 

 then `parse_wiki_json_url(search_url)` (let http://dbpedia.org/resource/Sergio_Ag%C3%BCero as search_url) , first change search_url into Json_url, and make it into json hash, match abstract(for "ru" and "zh" , "en" is from `get_live_english_abstract()`) and name .  

    
`self.find(search_url)` first load rdf page , then use `load_rdf_query_list` to get other data , like "name", "birthDate", "deathDate", "abstract", "thumbnail", "subject", "type", make data into two part , "data_query_list" and "data_name_list" .  


`run_artirix_category_create_update(category_list)` , list all the category from webpage, and use `Category.find(category_id)` to find and check if those categories from website in the ??API, if not , create and save it . In fact , it means ,  category will update if there are new ones.


`run_artirix_identity_create_update(identity,final_output,category_id_list_identity)` , add all the data from above functions, then save identity to ??API.



    .


#####part two : wikibot functions

Function 1 : `update_log_file` for updating log and writing to log.txt . 

Function 2 : `get_live_english_abstract(name)` for getting  english abstract from live site. 

 this function use `RestClient.get(json_url)` to get  json data and return Json parser by using `JSON.parse(json_data)` , then match abstract .

Function 3 : `self.find(search_url)`
 
    
     









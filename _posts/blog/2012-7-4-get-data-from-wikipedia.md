---
layout: post
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


#####How To :

######Where to get data from wikipedia ? 

Actually , we can use DBpedia , DBpedia is a community effort to extract structured information from Wikipedia and to make this information available on the Web. Take a look at "http://en.wikipedia.org/wiki/Sergio_Ag%C3%BCero" , "http://live.dbpedia.org/page/Sergio_Ag%C3%BCero" , and "http://dbpedia.org/page/Sergio_Ag%C3%BCero" . the "live" one just for english . 

So now , from dbpedia, we can get json and rdf format data from different URL , such as "http://dbpedia.org/data/Sergio_Agüero.rdf" and "http://dbpedia.org/data/Sergio_Agüero.json" , data or file should be shown to us .   

######How to get data from dbpedia ?

But how can we deal with the data ? try this :

First : use Gem "RestClient" and  json link
("http://dbpedia.org/data/Sergio_Agüero.json") to get json , json_hash =  JSON.parse(RestClient.get(Json_link)) , if the link need to change encode, then create a loop and judgment to decode, like "URI.decode(json_link)"

Second : match and catch data. 

for example : 

redirects = json_hash[search_url]["http://dbpedia.org/ontology/wikiPageRedirects"]
 
abstract = json_hash[search_url]["http://dbpedia.org/ontology/abstract"]

match_info can be get from "rdf" format webpage. 
 
Then we can get what we want . "live" site should be newer for enlish , replace it . 


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

Function 1 : `update_log_file` , for updating log and writing to log.txt . 

Function 2 : `get_live_english_abstract(name)` ,  for getting  english abstract from live site. 

 this function use `RestClient.get(json_url)` to get  json data and return Json parser by using `JSON.parse(json_data)` , then match abstract .

Function 3 : `self.find(search_url)` , first use "RDF::Graph.load(search_url)" to load RDF page, the use Function 4 `load_rdf_query_list` help to query data , as output. 

Function 4 : `load_rdf_query_list` , create data_query_list and data_name_query_list.
 
Function 5 : `abstract_subject_live(search_url)` , to get english text acstract content from live site.    

Function 6 : `run_artirix_category_create_update(category_list)` , get category list from parameter ,check categories from ??API by using `Category.find(category_id)` , if not exist , create and update categories.

Function 7 : `run_artirix_identity_create_update(identity,final_output,category_id_list_identity)` , match data , and update . save "external_links" doesn't work? 

Function 8 : `fetch_wiki_urls_dummy` fetch wiki urls , here we can use a = [idetity_id] to test. It will find identity by `find` , then match and give us wiki_urls. 

Function 9 : `fetch_wiki_urls` , it works is same to fetch_wiki_urls_dummy, but it get identities by `wiki_urls.length` to limit . 

function 10 : then `parse_wiki_json_url(search_url)` ,  first change search_url into Json_url, and make it into json hash, match abstract(for "ru" and "zh" , "en" is from `get_live_english_abstract()`) and name . 



asdfaaf


adfafad  afafafadfa  fadafad  
afsdfaf

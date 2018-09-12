# ELASTIC SEARCH / KIBANA


https://www.elastic.co/fr/downloads/elasticsearch

http://www.mkyong.com/elasticsearch/elasticsearch-hello-world-example/

## ELSATIC SEARCH

Note : installer java runtime

1 - Download and unzip Elasticsearch
2 - Run bin/elasticsearch (or bin\elasticsearch.bat on Windows)
3 - Run curl http://localhost:9200/ or Invoke-RestMethod http://localhost:9200 with PowerShell
4 - Dive into the getting started guide and video.


HTTP://   SERVEUR:PORT    / INDEX  /   TYPE

HTTP Request Mothod Usage
GET To get or select or read data from ElasticSearch
POST    To create or update data to ElasticSearch
PUT To create or update data to ElasticSearch
DELETE  To delete or remove existing data from ElasticSearch


CREATE Operation Example
To insert a new Document with /mkyong/posts/1001 and the following Request Data:

{
  "title": "Java 8 Optional In Depth",
  "category":"Java",
  "published_date":"23-FEB-2017",
  "author":"Rambabu Posa"
}

READ example
HTTP://   SERVEUR:PORT    / INDEX  / _search    // all result
HTTP://   SERVEUR:PORT    / INDEX  / ?q=_id:1001    // query



## KIBANA

1 - Download and unzip Kibana
2 - Open config/kibana.yml in an editor
Set elasticsearch.url to point at your Elasticsearch instance
3 - Run bin/kibana (or bin\kibana.bat on Windows)
4 - Point your browser at http://localhost:5601
5 - Dive into the getting started guide and video.




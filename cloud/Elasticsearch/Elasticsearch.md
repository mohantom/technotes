# Elasticsearch

Udemy: Elasticsearch 7 and the Elastic Stack - In depth and hands on

## Install Elasticsearch
[Elasticsearch on docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)
Note: use Postman for GET/PUT/POST

```shell script
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name es7 docker.elastic.co/elasticsearch/elasticsearch:7.7.0
curl -X GET "localhost:9200/_cat/nodes?v&pretty"
curl -XGET localhost:9200
```

## Import data
Get Shakespeare datatype mapping: 
[Shakespeare](http://media.sundog-soft.com/es7/shakes-mapping.json)
```shell script
curl -H "Content-Type: application/json" -XPUT localhost:9200/shakespeare --data-binary @shakes-mapping.json
curl -o shakespeare_7.0.json http://media.sundog-soft.com/es7/shakespeare_7.0.json
curl -H "Content-Type: application/json" -XPOST localhost:9200/shakespeare/_bulk --data-binary @shakespeare_7.0.json
culr http://localhost:9200/shakespeare/_search?pretty
```

- http://localhost:9200/shakespeare/_search
- Kibana, Logstash/Beats, X-Pack (security, alerting, monitoring, reporting, machine learning, graph exploration)

- Documents: things you are searching for, deprecated in ES7
- Index: inverted indices
- Mappings: schema for the data
- Term frequency (TF): how often a term appears in a given document
- Document frequency (DF): how often a term appears in all documents
- TF/DF: relevance of a term in a document 
- Primary (write/read) and replica (read) shards. Not easy to scale primary shards.

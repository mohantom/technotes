Elasticsearch

Udemy: Elasticsearch 7 and the Elastic Stack - In depth and hands on

[Elasticsearch on docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)

```shell script
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name es7 docker.elastic.co/elasticsearch/elasticsearch:7.7.0
curl -X GET "localhost:9200/_cat/nodes?v&pretty"
```
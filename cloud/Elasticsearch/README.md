## Run elastic stack in docker
```shell script
docker-compose -d -f es7.yaml up
docker-compose -f es7.yaml down
```
1. [ES7](http://localhost:9200),  [Kibana](localhost:5601)
2. Import data using Postman or curl.

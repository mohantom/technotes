## Run elastic stack in docker
```shell script
docker-compose -f es7.yaml up -d
docker-compose -f es7.yaml down
```
1. [ES7](http://localhost:9200),  [Kibana](http://localhost:5601)
2. Import data (es7 mapping and es7 json) using Postman or curl.
3. Import csv data using Kibana -> Machine Learning -> Data Visualizer -> Import data

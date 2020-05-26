## Run mysql in docker
```shell script
docker-compose -d -f mysql.yaml up
docker-compose -f mysql.yaml down
```
1. Go to localhost:8080 or use your Sql client (eg, DBeaver) and connect to localhost:3306, root/test
2. Import sample from /data

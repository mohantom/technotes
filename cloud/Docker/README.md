## Run mysql in docker
```shell script
docker-compose -f mysql.yaml -d up
docker-compose -f mysql.yaml down
```
1. Go to localhost:8080 or use your Sql client (eg, DBeaver) and connect to localhost:3306, root/test
2. Import sample from /data


### Execution plan
1.	Go to localhost:8080 (does not work with DBeaver)
2.	import sakila-db schema and data files(film data https://dev.mysql.com/doc/sakila/en/) 
3.	execution plan
```shell script
SELECT f.*, a.first_name, a.last_name FROM sakila.film f
join sakila.film_actor fa on f.film_id = fa.film_id 
join sakila.actor a on fa.actor_id = a.actor_id
where release_year=2006
and rating='PG-13'
```

If a database driver supports execution plan visualization, you can see the execution plan of the current query
 (under cursor) by pressing Ctrl+Shift+E or clicking Explain execution plan on the context menu or in the main toolbar:  
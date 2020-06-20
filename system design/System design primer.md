System Design Primer
=========================
https://github.com/donnemartin/system-design-primer
1.	Step 1: problem statement
Use case: scenario, how it’s used, what does the system do, who are the users
Constraints:  inputs/outputs, dependencies
Volume: how many users, how much data, requests per second, read write ratio
2.	High level design
a.	Sketch main concepts and components
b.	Justify your ideas
3.	Design core components
4.	How to test, exception handling, concurrency handling, monitoring/alert/auditing, 
5.	Scale the design
a.	Load balancer: horizontal scaling
b.	Database replication (master-slave), partition (federation), sharding
c.	Caching: prefer caching objects than db query caching; CDN is like a cache
d.	Async: pre-process it or do it async (RabbitMQ, ActiveMQ, Redis list, Kafka)

MD5, Base62
RPC (for internal?) vs REST
Analytics: MapReduce logs to get hit counts (or use Spark?)


Database – RDBMS
	ACID
	Master-slave replication
	Master-master replication
	Federation (partition based on feature): does not solve huge table issue
	Sharding (based on letters, need load balancer?): app logic to where to write, not event distributed -> consistent hashing, hard to join
	Denormalization (materialized views): duplicated data, not good for heavy write
	SQL tuning: tighten up schema, good indices, avoid expensive joins, partition tables, tune query cache
	
	
Execution plan

1.	Install mysql community installer
2.	Open MySQL Workbench
3.	import sakila-db (film data https://dev.mysql.com/doc/sakila/en/) 
4.	execution plan
	SELECT f.*, a.first_name, a.last_name FROM sakila.film f
join sakila.film_actor fa on f.film_id = fa.film_id 
join sakila.actor a on fa.actor_id = a.actor_id
where release_year=2006
and rating='PG-13'


NoSQL
•	Key-value store
•	Document store
•	Wide column store
•	Graph database
•	SQL vs NoSQL


Caching
•	Where to cache
o	Client caching
o	CDN caching
o	Web server caching
o	Database caching
o	Application caching
•	What to cache
o	Caching at the database query level
o	Caching at the object level
•	When to update the cache
o	Cache-aside
o	Write-through
o	Write-behind (write-back async)
o	Refresh ahead
Asynchronism and microservices
•	Message queues
•	Task queues
•	Back pressure
•	Microservices

JMS: between JVMs
AMQP: between different platforms, eg JVM and Ruby

Numbers Everyone Should Know
•	Read sequentially from disk at 30 MB/s (read 1MB: 30ms)
•	Read sequentially from 1 Gbps Ethernet at 100 MB/s (read 1MB: 10ms)
•	Read sequentially from SSD at 1 GB/s (read 1MB: 1ms)
•	Read sequentially from main memory at 4 GB/s (read 1MB: 0.25ms)
•	6-7 world-wide round trips per second
•	2,000 round trips per second within a data center
•	Writes are 40 times more expensive than reads.
•	Compress 1M bytes with Zippy 10 ms
•	Disk seek 10 ms

Raid
	Raid-0: performance
	Raid-1: image
	Raid-5: 1 is bad, the rest is ok
	Raid-6: 2 are bad, the rest id ok
	Raid-10: combination of raid-0 and raid-1, needs 4 drives

Cookie and Session
	Sticky session: keep session on file or on database
	
Load balancer on DNS level for different data centers

Load balance
o	Random allocation
o	Round robin allocation
o	Weighted allocation
o	Dynamic load balancing (least connections, least server CPU): need get info from workers
•	SSL termination - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations
o	Removes the need to install X.509 certificates on each server
•	Session persistence - Issue cookies and route a specific client's requests to same instance if the web apps do not keep track of sessions

Webserver vs platform server


Reverse proxy
Public face
•	Increased security: hide backend servers
•	Increased scalability and flexibility
•	Compression
•	SSL termination: encrypting traffic between clients and servers
•	Caching

Communication
 



Concurrency
	State: java concurrency
	Actors: async, non-blocking


Event-driven architecture

Separate command(CRUD) and query 

Enterprise Integration Patterns: Apache Camel


Parallel computing
	Master-worker
	Fork/Join: for simple tasks relationship, good for recursive data processing, work-stealing; task created dynamically
		Java 7 ParrelArray
	MapReduce: work divided upfront; mapping->grouping->reducing

Consistency Patterns
	Weak consistency
	Eventual consistency
	Strong consistency

Availability Patterns
	Fail-over: active-passive, active-active
	Replication

Stability Patterns
Timeouts: always use timeouts if possible
Circuit breaker
Fail fast: avoid slow response
	Separate systemError (resources not available), applicationError (bad user input)
Steady state: clean up after you; logging
Throttling: count requests, queue requests

Microservices

Service discovery
	Consul, Etcd, Zookeeper

Monitoring


Security

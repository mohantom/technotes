Redis
======
Course: Building NoSQL Apps With Redis
## Introduction
Extremely fast.
Store more than just Strings
Persistence
Replication
Built in LUA support (stored procedure)
No index: query by key

	netstat -tunpl | grep redis

## Redis basics
Data type

### String
	Set, get, append, incr, decr, getrange, mget, mset, strlen

```shell script
Set user:1 "{'name':'Joe', 'email':'test@gmail.com'}
Get user:1
Set user:id 1
Append user:1 "extra data"
Set customer:1 "abcd001"
Getrange customer:1 5 7  // "001"
Mset order:1 "order 1" order:2 "order 2"
```


### List
Lpush, rpush, lrem, lset, lindex, lrange, llen, lpop, rpop, ltrim
```shell script
Lpush recentcomments "comment 1" // push to head
Lrange recentcomments 0 1
```


### Set
Sad, scard, sdiff, sinter, sunion, sismember, smembers, smove, srem
```shell script
Sad post:1:likes "joe" "bob" "mary"
Scard post:1:likes // count
Smembers post:1:likes	// no order
Sad post:2:likes "joe" "tim"
Sdiff post:1:likes post:2:likes	// likes in common
Sinter post:1:likes post:2:likes
```


### Hashes
Similar to a map!
Hset, hmset, hget, hmget, getall, hdel, hexists, hincrby, hkeys, havls
```shell script
Hset user:1:h name "joe"	// name is the key
Hget user:1:h name
Hset user:1:h email joe@joe.com id 1
Hget user:1:h name email id //joe, joe@joe.com, 1
Hgetall user:1:h
Hkeys user:1:h
Hvals user:1:h
```


### Sorted set
Zadd, zcard, zcount, zincrby, zrange, zrank, zrem, zscore
```shell script
Zadd hs 120 "joe" 100 "bob" 150 "mary" 90 "tim"
Zrange hs 0 4
Zrange hs 0 4 withscore
Zadd hs 125 "joe"	// update Joe's score
Zrank hs bob	// 1
Zscore h tim	// 90
```


## Pub and sub
```shell script
Subscribe greetings
Publish greeetings "hello redis"
Subscribe greetings error
Subscribe greet*
```


## Transactions
No roll back!
```shell script
Multi
Set account-a 100
Set account-b 200
Incrby account-a -50	//queued
Incrby account-b 50	//queued
Exec	// execute
Watch account-a	// (nil), exec won't run
```


1.	Administration and Configuration
To watch

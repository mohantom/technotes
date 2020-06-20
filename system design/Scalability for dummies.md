Sacalability for dummies
=========================
Just recently I was asked what it would take to make a web service massively scalable. My answer was lengthy and maybe it is also for other people interesting. So I share it with you here in my blog and split it into parts to make it easier to read. New parts are released on a regular basis. Have fun and your comments are always welcomed!
The other parts of the series “Scalability for Dummies” you can (soon) find here.

## Part 1 - Clones
Public servers of a scalable web service are hidden behind a load balancer.  This load balancer evenly distributes load (requests from your users) onto your group/cluster of  application servers. That means that if, for example, user Steve interacts with your service, he may be served at his first request by server 2, then with his second request by server 9 and then maybe again by server 2 on his third request. 
Steve should always get the same results of his request back, independent what server he  “landed on”. That leads to the first golden rule for scalability: every server contains exactly the same codebase and does not store any user-related data, like sessions or profile pictures, on local disc or memory. 

Sessions need to be stored in a centralized data store which is accessible to all your application servers. It can be an external database or an external persistent cache, like Redis. An external persistent cache will have better performance than an external database. By external I mean that the data store does not reside on the application servers. Instead, it is somewhere in or near the data center of your application servers. 

But what about deployment? How can you make sure that a code change is sent to all your servers without one server still serving old code? This tricky problem is fortunately already solved by the great tool Capistrano. It requires some learning, especially if you are not into Ruby on Rails, but it is definitely both the effort.
After “outsourcing” your sessions and serving the same codebase from all your servers, you can now create an image file from one of these servers (AWS calls this AMI - Amazon Machine Image.) Use this AMI as a “super-clone” that all your new instances are based upon. Whenever you start a new instance/clone, just do an initial deployment of your latest code and you are ready!


## Part 2 - Database
After following Part 1 of this series, your servers can now horizontally scale and you can already serve thousands of concurrent requests. But somewhere down the road your application gets slower and slower and finally breaks down. The reason: your database. It’s MySQL, isn’t it?
Now the required changes are more radical than just adding more cloned servers and may even require some boldness. In the end, you can choose from 2 paths:
Path #1 is to stick with MySQL and keep the “beast” running. Hire a database administrator (DBA,) tell him to do master-slave replication (read from slaves, write to master) and upgrade your master server by adding RAM, RAM and more RAM. In some months, your DBA will come up with words like “sharding”, “denormalization” and “SQL tuning” and will look worried about the necessary overtime during the next weeks. At that point every new action to keep your database running will be more expensive and time consuming than the previous one. You might have been better off if you had chosen Path #2 while your dataset was still small and easy to migrate.
Path #2 means to denormalize right from the beginning and include no more Joins in any database query. You can stay with MySQL, and use it like a NoSQL database, or you can switch to a better and easier to scale NoSQL database like MongoDB or CouchDB. Joins will now need to be done in your application code. The sooner you do this step the less code you will have to change in the future. But even if you successfully switch to the latest and greatest NoSQL database and let your app do the dataset-joins, soon your database requests will again be slower and slower. You will need to introduce a cache.


## Part 3- Caching
After following Part 2 of this series, you now have a scalable database solution. You have no fear of storing terabytes anymore and the world is looking fine. But just for you. Your users still have to suffer slow page requests when a lot of data is fetched from the database. The solution is the implementation of a cache.
With “cache” I always mean in-memory caches like Memcached or Redis. Please never do file-based caching, it makes cloning and auto-scaling of your servers just a pain. 

But back to in-memory caches. A cache is a simple key-value store and it should reside as a buffering layer between your application and your data storage. Whenever your application has to read data it should at first try to retrieve the data from your cache. Only if it’s not in the cache should it then try to get the data from the main data source. Why should you do that? Because a cache is lightning-fast. It holds every dataset in RAM and requests are handled as fast as technically possible. For example, Redis can do several hundreds of thousands of read operations per second when being hosted on a standard server. Also writes, especially increments, are very, very fast. Try that with a database!


There are 2 patterns of caching your data. An old one and a new one:

1 - Cached Database Queries
That’s still the most commonly used caching pattern. Whenever you do a query to your database, you store the result dataset in cache. A hashed version of your query is the cache key. The next time you run the query, you first check if it is already in the cache. The next time you run the query, you check at first the cache if there is already a result. This pattern has several issues. The main issue is the expiration. It is hard to delete a cached result when you cache a complex query (who has not?). When one piece of data changes (for example a table cell) you need to delete all cached queries who may include that table cell. You get the point?
2 - Cached Objects
That’s my strong recommendation and I always prefer this pattern. In general, see your data as an object like you already do in your code (classes, instances, etc.). Let your class assemble a dataset from your database and then store the complete instance of the class or the assembed dataset in the cache. Sounds theoretical, I know, but just look how you normally code. You have, for example, a class called “Product” which has a property called “data”. It is an array containing prices, texts, pictures, and customer reviews of your product. The property “data” is filled by several methods in the class doing several database requests which are hard to cache, since many things relate to each other. Now, do the following: when your class has finished the “assembling” of the data array, directly store the data array, or better yet the complete instance of the class, in the cache! This allows you to easily get rid of the object whenever something did change and makes the overall operation of your code faster and more logical.

And the best part: it makes asynchronous processing possible! Just imagine an army of worker servers who assemble your objects for you! The application just consumes the latest cached object and nearly never touches the databases anymore!

Some ideas of objects to cache:
user sessions (never use the database!)
fully rendered blog articles
activity streams
user<->friend relationships 
As you maybe already realized, I am a huge fan of caching. It is easy to understand, very simple to implement and the result is always breathtaking. In general, I am more a friend of Redis than Memcached, because I love the extra database-features of Redis like persistence and the built-in data structures like lists and sets. With Redis and a clever key’ing there may be a chance that you even can get completly rid of a database. But if you just need to cache, take Memcached, because it scales like a charm.

Happy caching! 


## Part 4 - Async
This 4th part of the series starts with a picture: please imagine that you want to buy bread at your favorite bakery.  So you go into the bakery, ask for a loaf of bread, but there is no bread there! Instead, you are asked to come back in 2 hours when your ordered bread is ready. That’s annoying, isn’t it?

To avoid such a “please wait a while” - situation, asynchronism needs to be done.  And what’s good for a bakery, is maybe also good for your web service or web app.
In general, there are two ways / paradigms asynchronism can be done. 

Async #1
Let’s stay in the former bakery picture. The first way of async processing is the “bake the breads at night and sell them in the morning” way. No waiting time at the cash register and a happy customer.  Referring to a web app this means doing the time-consuming work in advance and serving the finished work with a low request time.

Very often this paradigm is used to turn dynamic content into static content.  Pages of a website, maybe built with a massive framework or CMS, are pre-rendered and locally stored as static HTML files on every change. Often these computing tasks are done on a regular basis, maybe by a script which is called every hour by a cronjob. This pre-computing of overall general data can extremely improve websites and web apps and makes them very scalable and performant. Just imagine the scalability of your website if the script would upload these pre-rendered HTML pages to AWS S3 or Cloudfront or another Content Delivery Network! Your website would be super responsive and could handle millions of visitors per hour!

Async #2
Back to the bakery. Unfortunately, sometimes customers has special requests like a birthday cake with “Happy Birthday, Steve!” on it. The bakery can not foresee these kind of customer wishes, so it must start the task when the customer is in the bakery and tell him to come back at the next day. Refering to a web service that means to handle tasks asynchronously.

Here is a typical workflow:

A user comes to your website and starts a very computing intensive task which would take several minutes to finish. So the frontend of your website sends a job onto a job queue and immediately signals back to the user: your job is in work, please continue to the browse the page. The job queue is constantly checked by a bunch of workers for new jobs. If there is a new job then the worker does the job and after some minutes sends a signal that the job was done. The frontend, which constantly checks for new “job is done” - signals, sees that the job was done and informs the user about it. I know, that was a very simplified example. 

If you now want to dive more into the details and actual technical design, I recommend you take a look at the first 3 tutorials on the RabbitMQ website. RabbitMQ is one of many systems which help to implement async processing. You could also use ActiveMQ or a simple Redis list. The basic idea is to have a queue of tasks or jobs that a worker can process. Asynchronism seems complicated, but it is definitely worth your time to learn about it and implement it yourself. Backends become nearly infinitely scalable and frontends become snappy which is good for the overall user experience. 

If you do something time-consuming, try to do it always asynchronously. 


An Unorthodox Approach To Database Design : The Coming Of The Shard
THURSDAY, AUGUST 6, 2009 AT 3:24PM
Update 4: Why you don’t want to shard. by Morgon on the MySQL Performance Blog. Optimize everything else first, and then if performance still isn’t good enough, it’s time to take a very bitter medicine. 
Update 3: Building Scalable Databases: Pros and Cons of Various Database Sharding Schemes by Dare Obasanjo. Excellent discussion of why and when you would choose a sharding architecture, how to shard, and problems with sharding.
Update 2: Mr. Moore gets to punt on sharding by Alan Rimm-Kaufman of 37signals. Insightful article on design tradeoffs and the evils of premature optimization. With more memory, more CPU, and new tech like SSD, problems can be avoided before more exotic architectures like sharding are needed. Add features not infrastructure. Jeremy Zawodnysays he's wrong wrong wrong. we're running multi-core CPUs at slower clock speeds. Moore won't save you.
Update: Dan Pritchett shares some excellent Sharding Lessons: Size Your Shards, Use Math on Shard Counts, Carefully Consider the Spread, Plan for Exceeding Your Shards

Once upon a time we scaled databases by buying ever bigger, faster, and more expensive machines. While this arrangement is great for big iron profit margins, it doesn't work so well for the bank accounts of our heroic system builders who need to scale well past what they can afford to spend on giant database servers. In a extraordinary two article series, Dathan Pattishall, explains his motivation for a revolutionary new database architecture--sharding--that he began thinking about even before he worked at Friendster, and fully implemented at Flickr. Flickr now handles more than 1 billion transactions per day, responding in less then a few seconds and can scale linearly at a low cost.
What is sharding and how has it come to be the answer to large website scaling problems?
Information Sources
	Unorthodox approach to database design Part1:History
	Unorthodox approach to database design Part 2:Friendster
What Is Sharding?
While working at Auction Watch, Dathan got the idea to solve their scaling problems by creating a database server for a group of users and running those servers on cheap Linux boxes. In this scheme the data for User A is stored on one server and the data for User B is stored on another server. It's a federated model. Groups of 500K users are stored together in what are called shards.

The advantages are:
•  High availability. If one box goes down the others still operate.
•  Faster queries. Smaller amounts of data in each user group mean faster querying.
•  More write bandwidth. With no master database serializing writes you can write in parallel which increases your write throughput. Writing is major bottleneck for many websites.
•  You can do more work. A parallel backend means you can do more work simultaneously. You can handle higher user loads, especially when writing data, because there are parallel paths through your system. You can load balance web servers, which access shards over different network paths, which are processed by separate CPUs, which use separate caches of RAM and separate disk IO paths to process work. Very few bottlenecks limit your work.

How Is Sharding Different Than Traditional Architectures?
Sharding is different than traditional database architecture in several important ways:
•  Data are denormalized. Traditionally we normalize data. Data are splayed out into anomaly-less tables and then joined back together again when they need to be used. In sharding the data are denormalized. You store together data that are used together. 

This doesn't mean you don't also segregate data by type. You can keep a user's profile data separate from their comments, blogs, email, media, etc, but the user profile data would be stored and retrieved as a whole. This is a very fast approach. You just get a blob and store a blob. No joins are needed and it can be written with one disk write.
•  Data are parallelized across many physical instances. Historically database servers are scaled up. You buy bigger machines to get more power. With sharding the data are parallelized and you scale by scaling out. Using this approach you can get massively more work done because it can be done in parallel.
•  Data are kept small. The larger a set of data a server handles the harder it is to cash intelligently because you have such a wide diversity of data being accessed. You need huge gobs of RAM that may not even be enough to cache the data when you need it. By isolating data into smaller shards the data you are accessing is more likely to stay in cache. 

Smaller sets of data are also easier to backup, restore, and manage.
•  Data are more highly available. Since the shards are independent a failure in one doesn't cause a failure in another. And if you make each shard operate at 50% capacity it's much easier to upgrade a shard in place. Keeping multiple data copies within a shard also helps with redundancy and making the data more parallelized so more work can be done on the data. You can also setup a shard to have a master-slave or dual master relationship within the shard to avoid a single point of failure within the shard. If one server goes down the other can take over.
•  It doesn't use replication. Replicating data from a master server to slave servers is a traditional approach to scaling. Data is written to a master server and then replicated to one or more slave servers. At that point read operations can be handled by the slaves, but all writes happen on the master. 

Obviously the master becomes the write bottleneck and a single point of failure. And as load increases the cost of replication increases. Replication costs in CPU, network bandwidth, and disk IO. The slaves fall behind and have stale data. The folks at YouTube had a big problem with replication overhead as they scaled.

Sharding cleanly and elegantly solves the problems with replication.

Some Problems With Sharding
Sharding isn't perfect. It does have a few problems.
•  Rebalancing data. What happens when a shard outgrows your storage and needs to be split? Let's say some user has a particularly large friends list that blows your storage capacity for the shard. You need to move the user to a different shard.

On some platforms I've worked on this is a killer problem. You had to build out the data center correctly from the start because moving data from shard to shard required a lot of downtime.

Rebalancing has to be built in from the start. Google's shards automatically rebalance. For this to work data references must go through some sort of naming service so they can be relocated. This is what Flickr does. And your references must be invalidateable so the underlying data can be moved while you are using it.
•  Joining data from multiple shards. To create a complex friends page, or a user profile page, or a thread discussion page, you usually must pull together lots of different data from many different sources. With sharding you can't just issue a query and get back all the data. You have to make individual requests to your data sources, get all the responses, and the build the page. Thankfully, because of caching and fast networks this process is usually fast enough that your page load times can be excellent.
•  How do you partition your data in shards? What data do you put in which shard? Where do comments go? Should all user data really go together, or just their profile data? Should a user's media, IMs, friends lists, etc go somewhere else? Unfortunately there are no easy answer to these questions.
•  Less leverage. People have experience with traditional RDBMS tools so there is a lot of help out there. You have books, experts, tool chains, and discussion forums when something goes wrong or you are wondering how to implement a new feature. Eclipse won't have a shard view and you won't find any automated backup and restore programs for your shard. With sharding you are on your own. 
•  Implementing shards is not well supported. Sharding is currently mostly a roll your own approach. LiveJournal makes their tool chain available. Hibernate has a library under development. MySQL has added support for partioning. But in general it's still something you must implement yourself.

See Also
•  The Flickr Architecture for more interesting ideas on how to implement sharding.
•  The Google Arhitecture.
•  The LiveJournal Architecture. They talk quite a bit about their sharding approach and give a lot of helpful details.
•  The Shard category.


Guide to the Most Important JVM Parameters


1. Overview
In this quick tutorial, we’ll explore the most well-known options which can be used to configure the Java Virtual Machine.
2. Explicit Heap Memory
One of the most common performance-related practices is to initialize the heap memory as per the application requirements.
That’s why we should specify minimal and maximal heap size. Below parameters can be used for achieving it:
1
2	-Xms<heap size>[unit] 
-Xmx<heap size>[unit]
Here, unit denotes the unit in which the memory (indicated by heap size) is to be initialized. Units can be marked as ‘g’ for GB, ‘m’ for MB and ‘k’ for KB.
For example, if we want to assign minimum 2 GB and maximum 5 GB to JVM, we need to write:
1	-Xms2G -Xmx5G
Starting with Java 8, the size of Metaspace is not defined. Once it reaches the global limit, JVM automatically increases it, However, to overcome any unnecessary instability, we can set Metaspace size with:
1	-XX:MaxMetaspaceSize=<metaspace size>[unit]
Here, metaspace size denotes the amount of memory we want to assign to Metaspace.
As per Oracle guidelines, after total available memory, the second most influential factor is the proportion of the heap reserved for the Young Generation. By default, the minimum size of the YG is 1310 MB, and maximum size is unlimited.
We can assign them explicitly:
1
2	-XX:NewSize=<young size>[unit] 
-XX:MaxNewSize=<young size>[unit]
3. Garbage Collection
For better stability of the application, choosing of right Garbage Collection algorithm is critical.
JVM has four types of GC implementations:
•	Serial Garbage Collector
•	Parallel Garbage Collector
•	CMS Garbage Collector
•	G1 Garbage Collector
These implementations can be declared with the below parameters:
1
2
3
4	-XX:+UseSerialGC
-XX:+UseParallelGC
-XX:+USeParNewGC
-XX:+UseG1GC
More details on Garbage Collection implementations can be found here.
4. GC Logging
To strictly monitor the application health, we should always check the JVM’s Garbage Collection performance. The easiest way to do this is to log the GC activity in human readable format.
Using the following parameters, we can log the GC activity:
1
2
3
4	-XX:+UseGCLogFileRotation 
-XX:NumberOfGCLogFiles=< number of log files > 
-XX:GCLogFileSize=< file size >[ unit ]
-Xloggc:/path/to/gc.log
UseGCLogFileRotation specifies the log file rolling policy, much like log4j, s4lj, etc. NumberOfGCLogFiles denotes the max number of log files that can be written for a single application life cycle. GCLogFileSize specifies the max size of the file. Finally, loggc denotes its location.
Point to note here is that, there are two more JVM parameters available (-XX:+PrintGCTimeStamps and -XX:+PrintGCDateStamps) which can be used to print date-wise timestamp in the GC log.
For example, if we want to assign a maximum of 100 GC log files, each having a maximum size of 50 MB and want to store them in ‘/home/user/log/’ location, we can use below syntax:
1
2
3
4	-XX:+UseGCLogFileRotation  
-XX:NumberOfGCLogFiles=10
-XX:GCLogFileSize=50M 
-Xloggc:/home/user/log/gc.log
However, the problem is that one additional daemon thread is always used for monitoring system time in the background. This behavior may create some performance bottleneck; that’s why it’s always better not to play with this parameter in production.
5. Handling Out of Memory
It’s very common for a large application to face out of memory error which, in turn, results in the application crash. It’s a very critical scenario and very hard to replicate to troubleshoot the issue.
That’s why JVM comes with some parameters which dump heap memory into a physical file which can be used later for finding out leaks:
1
2
3
4	-XX:+HeapDumpOnOutOfMemoryError 
-XX:HeapDumpPath=./java_pid<pid>.hprof
-XX:OnOutOfMemoryError="< cmd args >;< cmd args >" 
-XX:+UseGCOverheadLimit
A couple of points to note here:
•	HeapDumpOnOutOfMemoryError instructs the JVM to dump heap into physical file in case of OutOfMemoryError
•	HeapDumpPath denotes the path where the file is to be written; any filename can be given; however, if JVM finds a <pid> tag in the name, the process id of the current process causing the out of memory error will be appended to the file name with .hprof format
•	OnOutOfMemoryError is used to issue emergency commands to be executed in case of out of memory error; proper command should be used in the space of cmd args. For example, if we want to restart the server as soon as out of memory occur, we can set the parameter:
1	-XX:OnOutOfMemoryError="shutdown -r"
•	UseGCOverheadLimit is a policy that limits the proportion of the VM’s time that is spent in GC before an OutOfMemory error is thrown
6. 32/64 bit
In the OS environment where both 32 and 64-bit packages are installed, the JVM automatically chooses 32-bit environmental packages.
If we want to set the environment to 64 bit manually, we can do so using below parameter:
1	-d<OS bit>
OS bit can be either 32 or 64. More information about this can be found here.
7. Misc
•	-server: enables “Server Hotspot VM”; this parameter is used by default in 64 bit JVM
•	-XX:+UseStringDeduplication: Java 8u20 has introduced this JVM parameter for reducing the unnecessary use of memory by creating too many instances of the same String; this optimizes the heap memory by reducing duplicate String values to a single global char[] array
•	-XX:+UseLWPSynchronization: sets LWP (Light Weight Process) – based synchronization policy instead of thread-based synchronization
•	-XX:LargePageSizeInBytes: sets the large page size used for the Java heap; it takes the argument in GB/MB/KB; with larger page sizes we can make better use of virtual memory hardware resources; however, this may cause larger space sizes for the PermGen, which in turn can force to reduce the size of Java heap space
•	-XX:MaxHeapFreeRatio: sets the maximum percentage of heap free after GC to avoid shrinking.
•	-XX:MinHeapFreeRatio: sets the minimum percentage of heap free after GC to avoid expansion; to monitor the heap usage you can use VisualVM shipped with JDK.
•	-XX:SurvivorRatio: Ratio of eden/survivor space size – for example, -XX:SurvivorRatio=6 sets the ratio between each survivor space and eden space to be 1:6,
•	-XX:+UseLargePages: use large page memory if it is supported by the system; please note that OpenJDK 7tends to crash if using this JVM parameter
•	-XX:+UseStringCache: enables caching of commonly allocated strings available in the String pool
•	-XX:+UseCompressedStrings: use a byte[] type for String objects which can be represented in pure ASCII format
•	-XX:+OptimizeStringConcat: it optimizes String concatenation operations where possible
8. Conclusion
In this quick article, we learned about some important JVM parameters – which can be used to tune and improve general application performance.
Some of these can also be used for debugging purposes.
If you want to explore the reference parameters in more detail, you can get started here.
Requrements clarification:
- Users/Customers
   Who will use the system?
   How the system will be used?
- Scale(read and write)
   How many read queries per second?
   How  much data is queried per request?
   How many video views are processed per second?
   Can there be spikes in traffic?
- Performance
   What is expected write-to-read data delay?
   What is expected p99 latency for read queries?
- Cost
   Should the design minimize the cost of development?
   Should the design minimize the cost of maintenance?

Functional requirements - API

The system has to count video view events

countViewEvent(videoId) ->
countViewEvent(videoId, eventType) -> processEvent(videoId, eventType, function) ->
processEvents(listOfEvents)

The system has to return video views count for a time period

getViewsCount(videoId, startTime, endTime) -> getCount(videoId, eventType, startTime, endTime) -> getStats(videoId, eventType, function, startTime, endTIme )

High level arhitecture

User -> Browser -> Processing Service -> Database <-Query Service <- Browser <- User

What we store:
Indivudual Events(every click)     Aggregate data(e.g per minute) in real time

Define a data model

VideoId Timestamp ...                                VideoId TimeStamp Count

Fast writes                                                    Fast reads
Can slice and dice data however we need   Data is ready for decision making
Can recalculate numbers if needed

Slow reads                                                    Can query only the way data was agg-
Costly for a large scale(many events)           regated
                                                                     Requires data aggregation pipeline
                                                                     Hard or even impossible to fix errors

	Stream data process                   Batch data process

How to scale writes? How to scale reads? How to make both writes and read fast?
How not to lose data in case of hardware faults and network partitions?
How to achieve strong consistency? What are the tradeoffs?
How to recover data in case of an outage?
How to ensure data security?
How to make it extensible for data model changes in the future?
Where to run (cloud vs on-premises data centers)?
How much money will it all cost?

Cluster Proxy(Configuratuin Service(e.g ZooKeeper)) Now about database
Shard Proxy in front of database cache query result, monitor database instance health and publish metrics 
Availability replicate master and read replica(different data centers)

Simplify 
NoSQL database(Cassandra) no need configuratuin service for monitor database instance health (Gossip protocol) Round robin algo. Coordinator node(consistent hashing) Quorum writes or Quorum writes

Mysql nouns  and use foreign keys to reference related table

Report (Video, Views, Channel)

Video_info(VideoId, Name, ChannelId)
Video_stats(VideoId, Timestamp, Count)
Channel_info(ChannelId, Name, ...)

Run join query(data normalized, no duplication)

Nosql table(videoId, ChannelName, VideoName, 15:00, 16:00, 17:00, ...) everyting related to report in the one table

Qorum, key-value, document and graph
Cassandra column oriented database
HBase master slave architecture

How to scale?
How to achieve high throuput?
How not to lose data when processing node crashes?
What to do when database is unavailable or slow?

Main question: How to make date processing scalable, reliable and fast?

Scalable=Partitioning
Reliable=Replication and checkpoint
Fast=In-memory

push or pull(better fauler tolerance)
a,b write to queu and processing service pull and put to database

Checkpointing offset
Events consumed sequentianally

Partioning - have several queus

Processing Service(detailed design)

Partition/shard -> Partition Consumer -> Aggregator -> Internal Queue -> Database Writer
							Deduplication Cache    In-memory Store                            Dead-lett
																  Hash-table                                     er Queue
																  
																														 Data Enri
                                                                                                                         ment
                                                                                                                         
                                                                                                                         Embedded
                                                                                                                         database
                                                                                                          additional parameters read from embedded database

State keeping for sometime in memory store or queue
Inmemory sometimes store data in persistent storage

User -> API Gateway -> Load Balancer -> Partitioner Service

Ingestion path components:

Partitioner Service Client            |        Load Balancer               | Partitioner Service and Partitions

Blocking vs non-blocking           Software vs hardware load    Partition strategy
I/O                                              balancing

Buffering and batching               Networking protocols           Deal with hot partition

Timeouts                                     Load balancing algorithms    Service discovery(server side
																								 client side)
Retries                                         DNS                                        Replication(single leader, leaderless,
                                                                                                   multi leader)
Exponential backoff and jitter     Health checking                      
(add randomness) algo
                                                                                                  multi leader used across serviral data service 
Circuit breaker(make system       High availability                     Message format 
difficult to test)

Data retrieval path

User -> Browser -> API Gateway -> Query Service -> Database 
																					 Object Storage(cold storage and hot storage)
																					 Distrubuted Cache 

 Data flow simulation:

Users -> Api Gateway -> Load Balancer -> Partitioner Service -> Partitions -> Partition Consumer  
																										                          In-memory Store
-> Aggregator -> Queue -> Database Writer -> Database


QueryService -> Distributed Cache -> Database

Client Side   Load balancing Messaging systems  Data processing   Storage

Netty           NetScaler          Apache Kafka            Apache Spark      Apache Cassandra

Netflix Hystrix  NGINX          AWS Kinesis              Apache Flink        Apache HBase

Polly                 AWS ELB                                        AWS Kinesis         Data  Influx db
																				Analytics
																				                           Apache Hadoop

	                                                                                                        AWS Redshift, AWS S3

Other

Vitess, distributed cache(redis), message broker(AWS SQS/RabbitMQ), Data enrychment(RocksDB), Leader Election(Zookeeper), Netflix Eureka, Monitoring(AWS CloudWatch/ELK), Avro, Thrift, ProtoBuff, for hash Murmur Hash
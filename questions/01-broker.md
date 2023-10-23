# Broker Questions

## Question 1 (1-3)
If I produce to a topic that does not exist, and the broker setting auto.create.topic.enable=true, what will happen?

1. Kafka will automatically create the topic with the indicated producer settings num.partitions and default.replication.factor
2. Kafka will automatically create the topic with the broker settings num.partitions and default.replication.factor
3. Kafka will automatically create the topic with 1 partition and replication factor 1
4. Kafka will automatically create the topic with #numOfBrokers partitions and replication factor 3


## Question 2 (1-16)
A bank uses a Kafka cluster for credit card payments. What should be the value of the property unclean.leader.election.enable?

1. false
2. true

## Question 3 (1-23)
You have a Kafka cluster and all the topics have a replication factor of 3. One intern at your company stopped a broker, and accidentally deleted all the data of that broker on the disk. What will happen if the broker is restarted?

1. The broker will start, and won't be online untill all the data it needs to have is replicated from other leaders.
2. The broker will crash
3. The broker will starrt, and won't have any data. If the broker becomes leader we have a data loss
4. The broker will start, and other topics will also be deleted as the broker data on the disk got deleted.

## Question 4 (1-36)
How do Kafka brokers ensure great performance between the producers and consumers? (select two)

1. it does not transform the message
2. it buffers the messages on disk, and send messages from the disk reads
3. It transforms the messages into a binary format
4. It compresses the messages as it writes to the disk
5. It leverages zero-copy optimisations to send data straight from the page cache

## Question 5 (1-49)
There are 3 producers writing to a topic with 5 partitions. There are 5 consumers consuming from the topic. How many Controllers will be present in the cluster?

1. 1
2. 2
3. 3
4. 5


## Question 6 (1-50)
Where are the dynamic configurations for a topic stored?

1. In Zookeeper
2. On the Kafka broker file system
3. In server.properties
4. In an internal Kafka topic '_topic_configurations'


## Question 7 (2-23)
A producer application was sending messages to a partition with a replication factor of 2 by connecting to Broker 1 that was hosting partition leader. If the Broker 1 goes down, what will happen?

1. The producer will stop working
2. The topic will become unavailable
3. The producer will automatically produce to the broker that has been elected leader



## Question 8 (2-29)
Kafka is configured with following parameters - log.retention.hours = 168 log.retention.minutes = 168 log.retention.ms = 168 How long will the messages be retained for?

1. 168 minutes
2. Broker will not start due to bad configuration
3. 168 hours
4. 168 ms

Explanation
If more than one similar config is specified, the smaller unit size will take precedence.

## Question 9 (2-35)
How often is log compaction evaluated?

1. Everytime a new partition is created
2. Everytime a message is sent to Kafka
3. Everytime a segment is closed
4. Everytime a message is flushed to disk


Explanation
Log compaction is evaluated every time a segment is closed. It will be triggered if enough data is "dirty" (see dirty ratio config)

## Question 10 (2-36)
Once sent to a topic, a message can be modified

1. Yes
2. No

## Question 11 (2-50)
The Controller is a broker that is... (select two)

1. elected by broker majority
2. elected by Zookeeper ensemble
3. is responsible for consumer group re-balances
4. is responsible for partition leader election

## Question 12 (3-6)
Suppose you have 6 brokers and you decide to create a topic with 10 partitions and a replication factor of 3. The brokers 0 and 1 are on rack A, the brokers 2 and 3 are on rack B, and the brokers 4 and 5 are on rack C. If the leader for partition 0 is on broker 4, and the first replica is on broker 2, which broker can host the last replica? (select two)

1. 1
2. 2
3. 3
4. 5
5. 6
6. 0

## Question 13 (3-9)
What is the disadvantage of request/response communication?

1. Scalability
2. Cost
3. Coupling
4. Reliability


## Question 14 (3-13)
What are the requirements for a Kafka broker to connect to a Zookeeper ensemble? (select two)

1. Unique value for each broker's 'zookeeper.connect' parameter
2. All the brokers must share the same 'broker.id'
3. Unique values for each's broker's 'broker.id' parameter
4. All brokers must share the same 'zookeeper.connect' parameter

Explanation
Each broker must have a unique broker id and connect to the same zk ensemble and root zNode

## Question 15 (3-26)
There are five brokers in a cluster, a topic with 10 partitions and replication factor of 3, and a quota of producer_bytes_rate of 1 MB/sec has been specified for the client. What is the maximum throughput allowed for the client?

1. 10 MBps
2. 1 MBps
3. 0.33 MBps
4. 5 MBps


Explanation
Each producer is allowed to produce @ 1MB/s to a broker. Max throughput 5 * 1MB, because we have 5 brokers.

## Question 16 (3-27)
What happens when broker.rack configuration is provided in broker configuration in Kafka cluster?

1. Replicas for a partition are spread across different racks
2. You can use the same 'broker.id' as long as they have different 'broker.rack' configuration
3. Replicas for a partition are placed in the sam rack
4. Each rack contains all the topics and partitions, effectively making Kafka high available.


## Question 17 (3-36)
Partition leader election is done by

1. The consumers
2. Vote among the brokers
3. The Kafka Broker that is the Controller
4. Zookeeper


## Question 18 (3-38)
How much should be the heap size of a broker in a production setup on a machine with 256 GB of RAM, in PLAINTEXT mode?

1. 4GB
2. 16GB
3. 512GB
4. 128GB

## Question 19 (3-39)
A topic "sales" is being produced to in the Americas region. You are mirroring this topic using Mirror Maker to the European region. From there, you are only reading the topic for analytics purposes. What kind of mirroring is this?

1. Passive-Passive
2. Active-Active
3. Active-Passive


Explanation
This is active-passing as the replicated topic is used for read-only purposes only

## Question 20 (3-45)
In Kafka, every broker... (select three)

1. knows all the metadata for the topics and partitions it has on its disk
2. knows all the metadata for all topics and partitions
3. Contains only a subset of topics and partitions
4. is a controller
5. is a bootstrap broker
6. contains all the topics and partitions

## Question 21 3-46)
Your manager would like to have topic availability over consistency. Which setting do you need to change in order to enable that?

1. min.insync.replicas
2. unclean.leader.election.enable
3. compression.type



# Broker Answers
## Question 1 (1-3)
If I produce to a topic that does not exist, and the broker setting auto.create.topic.enable=true, what will happen?

- 2 Kafka will automatically create the topic with the broker settings num.partitions and default.replication.factor

Explanation
The broker settings comes into play when a topic is auto created


## Question 2 (1-16)
A bank uses a Kafka cluster for credit card payments. What should be the value of the property unclean.leader.election.enable?

- (1.) false


Explanation
Setting unclean.leader.election.enable to true means we allow out-of-sync replicas to become leaders, we will lose messages when this occurs, effectively losing credit card payments and making our customers very angry.

## Question 3 (1-23)
You have a Kafka cluster and all the topics have a replication factor of 3. One intern at your company stopped a broker, and accidentally deleted all the data of that broker on the disk. What will happen if the broker is restarted?

- 1 The broker will start, and won't be online until all the data it needs to have is replicated from other leaders.

Explanation
Kafka replication mechanism makes it resilient to the scenarios where the broker lose data on disk, but can recover from replicating from other brokers. This makes Kafka amazing!


## Question 4 (1-36)
How do Kafka brokers ensure great performance between the producers and consumers? (select two)

- 1 it does not transform the message
- 5 It leverages zero-copy optimisations to send data straight from the page cache


Explanation
Kafka transfers data with zero-copy and sends the raw bytes it receives from the producer straight to the consumer, leveraging the RAM available as page cache

## Question 5 (1-49)
There are 3 producers writing to a topic with 5 partitions. There are 5 consumers consuming from the topic. How many Controllers will be present in the cluster?

- 1 1

Explanation
There is only one controller in a cluster at all times.

## Question 6 (1-50)
Where are the dynamic configurations for a topic stored?

- 1 In Zookeeper
- 
Explanation
Dynamic topic configurations are maintained in Zookeeper.

## Question 7 (2-23)
A producer application was sending messages to a partition with a replication factor of 2 by connecting to Broker 1 that was hosting partition leader. If the Broker 1 goes down, what will happen?

- 3 The producer will automatically produce to the broker that has been elected leader


Explanation
Once the client connects to any broker, it is connected to the entire cluster and in case of leadership changes, the clients automatically do a Metadata Request to an available broker to find out who is the new leader for the topic. Hence the producer will automatically keep on producing to the correct Kafka Broker



## Question 8 (2-29)
Kafka is configured with following parameters - log.retention.hours = 168 log.retention.minutes = 168 log.retention.ms = 168 How long will the messages be retained for?

- 4 168 ms

Explanation
If more than one similar config is specified, the smaller unit size will take precedence.



## Question 9 (2-35)
How often is log compaction evaluated?


- (3.) Everytime a segment is closed


Explanation
Log compaction is evaluated every time a segment is closed. It will be triggered if enough data is "dirty" (see dirty ratio config)


## Question 10 (2-36)
Once sent to a topic, a message can be modified

- 2 No

Explanation
Kafka logs are append-only and the data is immutable

## Question 11 (2-50)
The Controller is a broker that is... (select two)

- 2 elected by Zookeeper ensemble
- 4 is responsible for partition leader election



Explanation
Controller is a broker that in addition to usual broker functions is responsible for partition leader election. The election of that broker happens thanks to Zookeeper and at any time only one broker can be a controller


## Question 12 (3-6)
Suppose you have 6 brokers and you decide to create a topic with 10 partitions and a replication factor of 3. The brokers 0 and 1 are on rack A, the brokers 2 and 3 are on rack B, and the brokers 4 and 5 are on rack C. If the leader for partition 0 is on broker 4, and the first replica is on broker 2, which broker can host the last replica? (select two)

- 1   1
- 6   0
## Question 13 (3-9)
What is the disadvantage of request/response communication?

- 3 Coupling


Explanation
Point-to-point (request-response) style will couple client to the server._`

## Question 14 (3-13)
What are the requirements for a Kafka broker to connect to a Zookeeper ensemble? (select two)

- 3 Unique values for each's broker's 'broker.id' parameter
- 4 All brokers must share the same 'zookeeper.connect' parameter

Explanation
Each broker must have a unique broker id and connect to the same zk ensemble and root zNode

## Question 15 (3-26)
There are five brokers in a cluster, a topic with 10 partitions and replication factor of 3, and a quota of producer_bytes_rate of 1 MB/sec has been specified for the client. What is the maximum throughput allowed for the client?

- 4 5 MBps

Explanation

Each producer is allowed to produce @ 1MB/s to a broker. Max throughput 5 * 1MB, because we have 5 brokers.


## Question 16 (3-27)
What happens when broker.rack configuration is provided in broker configuration in Kafka cluster?

- 1 Replicas for a partition are spread across different racks

Explanation
Partitions for newly created topics are assigned in a rack alternating manner, this is the only change broker.rack does

## Question 17 (3-36)
Partition leader election is done by

- 3 The Kafka Broker that is the Controller


Explanation

The Controller is a broker that is responsible for electing partition leaders

## Question 18 (3-38)
How much should be the heap size of a broker in a production setup on a machine with 256 GB of RAM, in PLAINTEXT mode?

- 1 4GB

Explanation
In Kafka, a small heap size is needed, while the rest of the RAM goes automatically to the page cache (managed by the OS). The heap size goes slightly up if you need to enable SSL


## Question 19 (3-39)
A topic "sales" is being produced to in the Americas region. You are mirroring this topic using Mirror Maker to the European region. From there, you are only reading the topic for analytics purposes. What kind of mirroring is this?

- 3 Active-Passive


Explanation
This is active-passing as the replicated topic is used for read-only purposes only

## Question 20 (3-45)
In Kafka, every broker... (select three)

- 2 knows all the metadata for all topics and partitions
- 3 Contains only a subset of topics and partitions
- 5 is a bootstrap broker

Explanation
Kafka topics are divided into partitions and spread across brokers. Each brokers knows about all the metadata and each broker is a bootstrap broker, but only one of them is elected controller


## Question 21 (3-46)
Your manager would like to have topic availability over consistency. Which setting do you need to change in order to enable that?

- 2 unclean.leader.election.enable


Explanation
unclean.leader.election.enable=true allows non ISR replicas to become leader, ensuring availability but losing consistency as data loss will occur


# Template
## Question 1
## Question 2
## Question 3
## Question 4
## Question 5
## Question 6
## Question 7
## Question 8
## Question 9
## Question 10
## Question 11
## Question 12
## Question 13
## Question 14
## Question 15
## Question 16
## Question 17
## Question 18
## Question 19
## Question 20
## Question 21
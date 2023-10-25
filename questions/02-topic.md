# Questions Topic

## Question 1 (1-13)
A Zookeeper ensemble contains 3 servers. Over which ports the members of the ensemble should be able to communicate in default configuration? (select three)

1. 3888
2. 443
3. 2181
4. 2888
5. 80
6. 9092


## Question 2 (1-37)
A kafka topic has a replication factor of 3 and min.insync.replicas setting of 1. What is the maximum number of brokers that can be down so that a producer with acks=all can still produce to the topic?

1. 0
2. 1
3. 2
4. 3

## Question 3 (1- 45)
If a topic has a replication factor of 3...

1. Each partition will live on 1 different brokers
2. Each partition will live on 2 different brokers
3. Each partition will live on 3 different brokers
4. Each partition will live on 4  different brokers


## Question 4 (2-13)
Your topic is log compacted and you are sending a message with the key K and value null. What will happen?

1. The producer will throw a Runtime Exception
2. The message will be ignored by the Kafka broker
3. The broker will delete the message with the key K and null value only upon cleanup
4. The broker will delete all messages with the key K upon cleanup.

## Question 5 (2- 28)
Compaction is enabled for a topic in Kafka by setting log.cleanup.policy=compact. What is true about log compaction?

1. After cleanup, only one message per key is retained with the first value
2. Kafka automatically de-duplicates incoming messages based on key hashes
3. Compaction changes the offsets of messages
4. After cleanup, only one message per key is retained with the latest value
5. Each message stored in the topic is compressed.

## Question 6 (2- 40)
When auto.create.topics.enable is set to true in Kafka configuration, what are the circumstances under which a Kafka broker automatically creates a topic? (select three)

1. Client requests metadata from a topic
2. Consumers reads message from a topic
3. Producer sends message to a topic
4. Client alters number of partitions of a topic

## Question 7 (2-  46)
What is true about partitions? (select two)

1. A partition has one replica that is the leader, while the other replicas are followers
2. A broker can have a partition and its replica on disk
3. A broker can have different partitions numbers for the same topic on its disk
4. Only out of sync replicas are replicas, the remaining partitions that are in sync are also leaders
5. You cannot have more partitions that the number of brokers in your cluster


## Question 8 (3-  10)
How will you set the retention for the topic named Lalakis to 1 hour?

1. Set the producer config retention.ms to 3600000
2. Set the broker config log.retention.ms to 3600000
3. Set the topic config retention.ms to 3600000
4. Set the consumer config retention.ms to 3600000

## Question 9 (3-  21)
There are 3 brokers in the cluster. You want to create a topic with a single partition that is resilient to one broker failure and one broker maintenance. What is the replication factor will you specify while creating the topic?

1. 6
2. 2
3. 3
4. 1

Explanation
1 is not possible as it doesn't provide resilience to failure, 2 is not enough as if we take a broker down for maintenance, we cannot tolerate a broker failure, and 6 is impossible as we only have 3 brokers (RF cannot be greater than the number of brokers). Here the correct answer is 3

## Question 10 (3- 28)
What is true about replicas ?

1. Follower replica handles all consume requests
2. Leader replica handles all produce and consume requests
3. Produce requests can be done to the replicas that are followers
4. Produce and consume requests are load balanced between Leader and Followers replicas


## Question 11 (3- 35)
What's a Kafka partition made of?
1. One file and two indexes
2. One file and one index
3. One file and two indexes per segment
4. One file

## Question 12 (3-48)
By default, which replica will be elected as a partition leader? (select two)

1. An in sync replica
2. Any of the replicas
3. Preferred leader broker if in sync and auto.leader.rebalance.enable=false
4. Preferred leader broker if in sync and auto.leader.rebalance.enable=ture

## Question 13 (3-50)
Which of the following statements are true regarding the number of partitions of a topic?

1. We can add partitions in a topic by adding a broker to the cluster
2. We can remove partitions in a topic using the kafka-topics.sh command
3. The number of partitions in a topic cannot be altered
4. We can add partitions in a topic using the kafka-topics.sh command


Explanation

We can only add partitions to an existing topic, and it must be done using the kafka-topics.sh command


# Answers Topic
## Answer 1 (1-13)
A Zookeeper ensemble contains 3 servers. Over which ports the members of the ensemble should be able to communicate in default configuration? (select three)

- (1.) 3888
- (3.) 2181
- (4.) 2888

Explanation

2181 - client port, 2888 - peer port, 3888 - leader port

## Answer 2 (1-37)
A kafka topic has a replication factor of 3 and min.insync.replicas setting of 1. What is the maximum number of brokers that can be down so that a producer with acks=all can still produce to the topic?

- (3.) 2

Explanation

Two brokers can go down, and one replica will still be able to receive and serve data

## Answer 3 (1- 45)
If a topic has a replication factor of 3...

- (3.) Each partition will live on 3 different brokers

Explanation

Replicas are spread across available brokers, and each replica = one broker. RF 3 = 3 brokers


## Answer 4 (2-13)
Your topic is log compacted and you are sending a message with the key K and value null. What will happen?

- (4.) The broker will delete all messages with the key K upon cleanup.

Explanation

Sending a message with the null value is called a tombstone in Kafka and will ensure the log compacted topic does not contain any messages with the key K upon compaction


## Answer 5 (2- 28)
Compaction is enabled for a topic in Kafka by setting log.cleanup.policy=compact. What is true about log compaction?

- (4.) After cleanup, only one message per key is retained with the latest value

Explanation

Log compaction retains at least the last known value for each record key for a single topic partition. All compacted log offsets remain valid, even if record at offset has been compacted away as a consumer will get the next highest offset.


## Answer 6 (2- 40)
When auto.create.topics.enable is set to true in Kafka configuration, what are the circumstances under which a Kafka broker automatically creates a topic? (select three)

1. Client requests metadata from a topic
2. Consumers reads message from a topic
3. Producer sends message to a topic

Explanation

A kafka broker automatically creates a topic under the following circumstances: - When a producer starts writing messages to the topic - When a consumer starts reading messages from the topic - When any client requests metadata for the topic



## Answer 7 (2-  46)
What is true about partitions? (select two)

- (1.) A partition has one replica that is the leader, while the other replicas are followers
- (3.) A broker can have different partitions numbers for the same topic on its disk

- Explanation

Only one of the replicas is elected as partition leader. And a broker can definitely hold many partitions from the same topic on its disk, try creating a topic with 12 partitions on one broker!

## Answer 8 (3-  10)
How will you set the retention for the topic named Lalakis to 1 hour?

- (3.) Set the topic config retention.ms to 3600000

Explanation

retention.ms can be configured at topic level while creating topic or by altering topic. It shouldn't be set at the broker level (log.retention.ms) as this would impact all the topics in the cluster, not just the one we are interested in

## Answer 9 (3-  21)
There are 3 brokers in the cluster. You want to create a topic with a single partition that is resilient to one broker failure and one broker maintenance. What is the replication factor will you specify while creating the topic?

- (3.) 3


Explanation

1 is not possible as it doesn't provide resilience to failure, 2 is not enough as if we take a broker down for maintenance, we cannot tolerate a broker failure, and 6 is impossible as we only have 3 brokers (RF cannot be greater than the number of brokers). Here the correct answer is 3

## Answer 10 (3- 28)
What is true about replicas ?
- (2.) Leader replica handles all produce and consume requests

Explanation

Replicas are passive - they don't handle produce or consume request. Produce and consume requests get sent to the node hosting partition leader.

## Answer 11 (3- 35)
What's a Kafka partition made of?

- (3.) One file and two indexes per segment


Explanation

Kafka partitions are made of segments (usually each segment is 1GB), and each segment has two corresponding indexes (offset index and time index)

## Answer 12 (3-48)
By default, which replica will be elected as a partition leader? (select two)

- (1.) An in sync replica
- (4.) Preferred leader broker if in sync and auto.leader.rebalance.enable=ture

Explanation

Preferred leader is a broker that was leader when topic was created. It is preferred because when partitions are first created, the leaders are balanced between brokers. Otherwise, any of the in-sync replicas (ISR) will be elected leader, as long as unclean.leader.election=false (by default)

## Answer 13 (3-50)
Which of the following statements are true regarding the number of partitions of a topic?

1. We can add partitions in a topic by adding a broker to the cluster
2. We can remove partitions in a topic using the kafka-topics.sh command
3. The number of partitions in a topic cannot be altered
4. We can add partitions in a topic using the kafka-topics.sh command


Explanation

We can only add partitions to an existing topic, and it must be done using the kafka-topics.sh command

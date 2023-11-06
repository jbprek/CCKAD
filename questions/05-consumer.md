# Consumers/Groups 

# Questions

## Question 1 (1): (-)
We would like to be in an at-most once consuming scenario. Which offset commit strategy would you recommend?

1. Commit the offsets in Kafka, before processing the data
2. Commit the offsets on disk, after processing the data
3. Do not commit any offsets and read from the beginning
4. Commit the offsets in Kafka, after processing the data


## Question 2 (1): 
There are two consumers C1 and C2 belonging to the same group G subscribed to topics T1 and T2. Each of the topics has 3 partitions. How will the partitions be assigned to consumers with PartitionAssignor being RoundRobinAssignor?

1. C1 will be assigned partitions 0 and 1 from T1 and T2, C2 will be assigned partition 2 from T1 and T2
2. Two consumers cannot read from two topics at the same time
3. C1 will be assigned partitions 0 and 2 from T1 and partition 1 from T2. C2 will have partition 1 from T1 and partitions 0 and 2 from T2
4. All consumers will read all partitions

## Question 3 (1): : (-)
A consumer starts and has auto.offset.reset=latest, and the topic partition currently has data for offsets going from 45 to 2311. The consumer group has committed the offset 643 for the topic before. Where will the consumer read from?

1. offset 45
2. offset 643
3. it will crash
4. offset 2311

## Question 4: : (-)
A consumer wants to read messages from a specific partition of a topic. How can this be achieved?

1. Call assign() passing a Collection of TopicPartitions as the argument
2. Call subscribe() passing TopicPartition as the argument
3. Call subscribe(String topic, int partition) passing the topic and partition number as arguments


## Question 5 (1): : (-)
Select all the way for one consumer to subscribe simultaneously to the following topics - topic.history, topic.sports, topic.politics? (select two)
1. 
    ````
    consumer.subscribePrefix("topic.")
    ````
2.
     ````
     consumer.subscribe("topic.history")
     consumer.subscribe("topic.sports")
     consumer.subscribe("topic.politics")
     ````
3.
    ````
    consumer.subscribe(Arrays.asList("topic.history","topic.sports", "topic.politics")
    ````
4. 
    ````
    consumer.subscribe(Pattern.compile("topic\..*")
    ````

## Question 6 (1): 
A topic receives all the orders for the products that are available on a commerce site. Two applications want to process all the messages independently - order fulfilment and monitoring. The topic has 4 partitions, how would you organise the consumers for optimal performance and resource usage?

1. Create 4 consumers in the same group, one for each partition, 2  for fulfilment and 2 for monitoring
2. Create 8 consumers in the same group with 4 consumers in each application
3. Create 2 consumer groups for 2 applications with 8 consumers in each
4. Create 2 consumer groups for 2 applications with 4 consumers each.


## Question 7: 
How can you gracefully make a Kafka consumer to stop immediately polling data from Kafka and gracefully shut down a consumer application?

1. Call consumer.poll() in another thread
2. Call consumer.wakeUp() and catch a WakeUpException
3. Kill the consumer thread

Explanation

See https://stackoverflow.com/a/37748336/3019499

## Question 8: (-)
A topic has three replicas, and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a consume request is sent to broker?

1. Data will be returned from the remaining in-sync replica
2. NotEnoughReplicasException will be returned
3. A new leader for the partition will be elected
4. An empty message will be returned

## Question 9 (2):  (-)
A consumer sends a request to commit offset 2000. There is a temporary communication problem, so the broker never gets the request and therefore never responds. Meanwhile, the consumer processed another batch and successfully committed offset 3000. What should you do?

1. Use kafka-consumer-group command to manually commit the offsets 2000 for the consumer group
2. Nothing
3. Add a new consumer to the group
4. Restart the consumer

## Question 10 (2):  (-)
A producer just sent a message to the leader broker for a topic partition. The producer used acks=1 and therefore the data has not yet been replicated to followers. Under which conditions will the consumer see the message?

1. When the high watermark has advanced
2. Never the produce request will fail
3. Right away
4. When the message has been fully replicated to all replicas

## Question 11 (2):  (-)
A consumer wants to read messages from partitions 0 and 1 of a topic topic1. Code snippet is shown below.
````
consumer.subscribe(Arrays.asList("topic1"));
List<TopicPartition> pc = new ArrayList<>();
pc.add(new PartitionTopic("topic1", 0));
pc.add(new PartitionTopic("topic1", 1));
consumer.assign(pc);
````
1. This will work fine. subscribe() will subscribe to thge topic and assign() will assign partitions to the consumer
2. Throws IllegalStateException

## Question 12: 
There are 3 producers writing to a topic with 5 partitions. There are 10 consumers consuming from the topic as part of the same group. How many consumers will remain idle?

1. 10
2. 3
3. None
4. 5

## Question 13 (2):  (-)
````
while (true) {
   ConsumerRecords<String, String> records = consumer.poll(100);
   try {
      consumer.commitSync();
   } catch (CommitFailedException e) {
      log.error("commit failed", e)
   }
   for (ConsumerRecord<String, String> record : records)
   {
      System.out.printf("topic = %s, partition = %s, offset =
      %d, customer = %s, country = %s
      ",
      record.topic(), record.partition(),
      record.offset(), record.key(), record.value());
   }
}
````
What kind of delivery guarantee this consumer offers?

1. At least once
2. At most once
3. Exactly once

## Question 14 (2):  (-)
A consumer starts and has auto.offset.reset=none, and the topic partition currently has data for offsets going from 45 to 2311. The consumer group has committed the offset 10 for the topic before. Where will the consumer read from?

1. offset 10
2. it will crash
3. offset 2311
4. offset 45

## Question 15 (2):  (-)
You are doing complex calculations using a machine learning framework on records fetched from a Kafka topic. It takes more about 6 minutes to process a record batch, and the consumer enters rebalances even though it's still running. How can you improve this scenario?

1. increase heartbeat.interval.ms to 600000
2. Add consumers to consumer group and kill them right away
3. increase session.timeout.ms to 600000
4. increase max.pol.interval.ms to 600000


## Question 16 (2): 
Which actions will trigger partition rebalance for a consumer group? (select three)

1. Remove a broker from the cluster
2. Add a new consumer to the group
3. Increase partitions of a topic
4. A consumer in consumer group shutsdown
5. Add a broker to the cluster


## Question 17 (2):  (-)
In the Kafka consumer metrics it is observed that fetch-rate is very high and each fetch is small. What steps will you take to increase throughput?

1. increase fetch.max.bytes
2. decrease fetch.min.bytes
3. decrease fetch.max.bytes
4. increase fetch.max.wait
5. increase fetch.min.bytes


## Question 18 (2): 
To allow consumers in a group to resume at the previously committed offset, I need to set the proper value for...

1. value.deserializer
2. auto.offsets.resets
3. enable.auto.commit
4. group.id

## Question 19 (2): 
To read data from a topic, the following configuration is needed for the consumers

1. the list of brokers that have the data, the topic name and the partition list
2. any broker and the list of topic partitions
3. all brokers of the cluster, and the topic name
4. any broker to connect to and the topic name

## Question 20 (2): 
How does a consumer commit offsets in Kafka?

1. it interacts with the Group Coordinator broker
2. it directly sends a message to the __consumer_offsets topic
3. it directly commits the offsets in Zookeeper

## Question 21 (3):
Two consumers share the same group.id (consumer group id). Each consumer will

1. Read mutually exlcusive offset blocks on all the partitions
2. Read all the data on mutual exclusive partitions
3. Read all the data from all partitions


## Question 22 (3): (-)
A consumer is configured with enable.auto.commit=false. What happens when close() is called on the consumer object?

1. A rebalance in the consumer group will happen immediately
2. The group coordinator will discover that the consumer stopped sending heartbeats. I will cause rebalance after session.timeout.ms
3. The uncommitted offsets are committed.


## Question 23 (3):
What is a generic unique id that I can use for messages I receive from a consumer?

1. topic + timestamp
2. topic + partition + offset
3. topic + partition + timestamp

Explanation

(Topic,Partition,Offset) uniquely identifies a message in Kafka

## Question 24 (3): (-)
Consumer failed to process record # 10 and succeeded in processing record # 11. Select the course of action that you should choose to guarantee at least once processing

1. Commit offsets at 11
2. Commit offsets at 10
3. Do not commit until successfully processing the record 10

## Question 25 (3):
A consumer has auto.offset.reset=latest, and the topic partition currently has data for offsets going from 45 to 2311. The consumer group never committed offsets for the topic before. Where will the consumer read from?

1. offset 2311
2. it will crash
3. offset 45
4. offset 0

Explanation

Latest means that data retrievals will start from where the offsets currently end

## Question 26 (3):  (-)
You have a consumer group of 12 consumers and when a consumer gets killed by the process management system, rather abruptly, it does not trigger a graceful shutdown of your consumer. Therefore, it takes up to 10 seconds for a rebalance to happen. The business would like to have a 3 seconds rebalance time. What should you do? (select two)


1. Decrease heartbeat.interval.ms
2. Increase heartbeat.interval.ms
3. Decrease session.timeout.ms
4. Increase session.timeout.ms
5. Decrease max.poll.interval.ms
6. Increase  max.poll.interval.ms

## Question 27 (2):
A topic has three replicas and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a consume request is sent to broker?

- (1) Data will be returned from the remaining in-sync replica
- (2) NotEnoughReplicasException will be returned
- (3) A new leader for the partition will be elected
- (4) An empty message will be returned 

## Question 28 (E): (-)
Using the Range partition assignment strategy, which of the specified partition assignments will
occur? (Choose one)

![img](05-consumer-images/question28.png)
- (1) Topic A partition 0 and topic A partition 1 will be assigned to the same consumer
- (2) Topic A partition 0 and topic B partition 1 will be assigned to the same consumer
- (3) Topic A partition 0 and topic B partition 0 will be assigned to the same consumer
- (4) Topic B partition 0 and topic B partition 1 will be assigned to the same consumer

# Answers

## Answer 1: 
We would like to be in an at-most once consuming scenario. Which offset commit strategy would you recommend?

- (1) Commit the offsets in Kafka, before processing the data
Explanation
Here, we must commit the offsets right after receiving a batch from a call to .poll()


## Answer 2:
There are two consumers C1 and C2 belonging to the same group G subscribed to topics T1 and T2. Each of the topics has 3 partitions. How will the partitions be assigned to consumers with PartitionAssignor being RoundRobinAssignor?

- (3) C1 will be assigned partitions 0 and 2 from T1 and partition 1 from T2. C2 will have partition 1 from T1 and partitions 0 and 2 from T2

Explanation

The  option is the only one where the two consumers share an equal number of partitions amongst the two topics of three partitions. An interesting article to read is: https://medium.com/@anyili0928/what-i-have-learned-from-kafka-partition-assignment-strategy-799fdf15d3ab


## Answer 3:
A consumer starts and has auto.offset.reset=latest, and the topic partition currently has data for offsets going from 45 to 2311. The consumer group has committed the offset 643 for the topic before. Where will the consumer read from?

- (2) offset 643


Explanation

The offsets are already committed for this consumer group and topic partition, so the property auto.offset.reset is ignored


## Answer 4 (1): 
A consumer wants to read messages from a specific partition of a topic. How can this be achieved?

- (1) Call assign() passing a Collection of TopicPartitions as the argument

Explanation

assign() can be used for manual assignment of a partition to a consumer, in which case subscribe() must not be used. Assign() takes a collection of TopicPartition object as an argument https://kafka.apache.org/23/javadoc/org/apache/kafka/clients/consumer/KafkaConsumer.html#assign-java.util.Collection-


## Answer 5:
Select all the way for one consumer to subscribe simultaneously to the following topics - topic.history, topic.sports, topic.politics? (select two)

- (3)
 ````
 consumer.subscribe(Arrays.asList("topic.history","topic.sports", "topic.politics")
 ````
- (4)
 ````
 consumer.subscribe(Pattern.compile("topic\..*")
 ````

Explanation

Multiple topics can be passed as a list or regex pattern.


## Answer 6:
A topic receives all the orders for the products that are available on a commerce site. Two applications want to process all the messages independently - order fulfilment and monitoring. The topic has 4 partitions, how would you organise the consumers for optimal performance and resource usage?


- (4) Create 2 consumer groups for 2 applications with 4 consumers each.


Explanation

two partitions groups - one for each application so that all messages are delivered to both the application. 4 consumers in each as there are 4 partitions of the topic, and you cannot have more consumers per groups than the number of partitions (otherwise they will be inactive and wasting resources)


## Answer 7:
How can you gracefully make a Kafka consumer to stop immediately polling data from Kafka and gracefully shut down a consumer application?

- (2) Call consumer.wakeUp() and catch a WakeUpException

Explanation

See https://stackoverflow.com/a/37748336/3019499

## Answer 8:
A topic has three replicas, and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a consume request is sent to broker?

- (1) Data will be returned from the remaining in-sync replica

Explanation
With this configuration, a single in-sync replica is still readable, but not writeable if the producer using acks=all


## Answer 9:
A consumer sends a request to commit offset 2000. There is a temporary communication problem, so the broker never gets the request and therefore never responds. Meanwhile, the consumer processed another batch and successfully committed offset 3000. What should you do?

- (2) Nothing

Explanation

In this case, because the offset 3000 has been committed and all the messages between 0 and 3000 have all been processed, it is okay not to have committed offset 2000. The right answer is to do "nothing", this behaviour is acceptable



## Answer 10:
A producer just sent a message to the leader broker for a topic partition. The producer used acks=1 and therefore the data has not yet been replicated to followers. Under which conditions will the consumer see the message?

- (1.) When the high watermark has advanced

Explanation

The high watermark is an advanced Kafka concept, and is advanced once all the ISR replicates the latest offsets. A consumer can only read up to the value of the High Watermark (which can be less than the highest offset, in the case of acks=1)


## Answer 11:
A consumer wants to read messages from partitions 0 and 1 of a topic topic1. Code snippet is shown below.
````
consumer.subscribe(Arrays.asList("topic1"));
List<TopicPartition> pc = new ArrayList<>();
pc.add(new PartitionTopic("topic1", 0));
pc.add(new PartitionTopic("topic1", 1));
consumer.assign(pc);
````

- (2) Throws IllegalStateException

Explanation

subscribe() and assign() cannot be called by the same consumer, subscribe() is used to leverage the consumer group mechanism, while assign() is used to manually control partition assignment and reads assignment


## Answer 12 (2):
There are 3 producers writing to a topic with 5 partitions. There are 10 consumers consuming from the topic as part of the same group. How many consumers will remain idle?

- (4) 5

Explanation

One consumer per partition assignment will keep 5 consumers idle.


## Answer 13:
````
while (true) {
   ConsumerRecords<String, String> records = consumer.poll(100);
   try {
      consumer.commitSync();
   } catch (CommitFailedException e) {
      log.error("commit failed", e)
   }
   for (ConsumerRecord<String, String> record : records)
   {
      System.out.printf("topic = %s, partition = %s, offset =
      %d, customer = %s, country = %s
      ",
      record.topic(), record.partition(),
      record.offset(), record.key(), record.value());
   }
}
````
What kind of delivery guarantee this consumer offers?

2. At most once

Explanation

Here offset is committed before processing the message. If consumer crashes before processing the message, message will be lost when it comes back up.

## Answer 14:
A consumer starts and has auto.offset.reset=none, and the topic partition currently has data for offsets going from 45 to 2311. The consumer group has committed the offset 10 for the topic before. Where will the consumer read from?

- (2) it will crash

Explanation

auto.offset.reset=none means that the consumer will crash if the offsets it's recovering from have been deleted from Kafka, which is the case here, as 10 < 45

## Question 15:
You are doing complex calculations using a machine learning framework on records fetched from a Kafka topic. It takes more about 6 minutes to process a record batch, and the consumer enters rebalances even though it's still running. How can you improve this scenario?


- (4) increase max.pol.interval.ms to 600000

Explanation

Here, we need to change the setting max.poll.interval.ms (default 300000) to its double in order to tell Kafka a consumer should be considered dead if the consumer only if it hasn't called the .poll() method in 10 minutes instead of 5.


## Answer 16:
Which actions will trigger partition rebalance for a consumer group? (select three)

- (2) Add a new consumer to the group
- (3) Increase partitions of a topic
- (4) A consumer in consumer group shutsdown

Explanation

Rebalance occurs when a new consumer is added, removed or consumer dies or paritions increased.

## Answer 17:
In the Kafka consumer metrics it is observed that fetch-rate is very high and each fetch is small. What steps will you take to increase throughput?


- (5). increase fetch.min.bytes

Explanation

This will allow consumers to wait and receive more bytes in each fetch request.


## Answer 18:
To allow consumers in a group to resume at the previously committed offset, I need to set the proper value for...

- (4.) group.id

Explanation

Setting a group.id that's consistent across restarts will allow your consumers part of the same group to resume reading from where offsets were last committed for that group


## Answer 19 :
To read data from a topic, the following configuration is needed for the consumers

- (4.) any broker to connect to and the topic name

Explanation

All brokers can respond to Metadata request, so a client can connect to any broker in the cluster.


## Answer 20:
How does a consumer commit offsets in Kafka?

- (1.) it interacts with the Group Coordinator broker

Explanation

Consumers do not directly write to the __consumer_offsets topic, they instead interact with a broker that has been elected to manage that topic, which is the Group Coordinator broker

## Answer 21:
Two consumers share the same group.id (consumer group id). Each consumer will

- (2.) Read all the data on mutual exclusive partitions

Explanation

Each consumer is assigned a different partition of the topic to consume.

## Answer 22:
A consumer is configured with enable.auto.commit=false. What happens when close() is called on the consumer object?

- (1.) A rebalance in the consumer group will happen immediately

Explanation

Calling close() on consumer immediately triggers a partition rebalance as the consumer will not be available anymore.

## Answer 23:
What is a generic unique id that I can use for messages I receive from a consumer?

- (2.) topic + partition + topic


Explanation

(Topic,Partition,Offset) uniquely identifies a message in Kafka

Calling close() on consumer immediately triggers a partition rebalance as the consumer will not be available anymore.

## Answer 24:
Consumer failed to process record # 10 and succeeded in processing record # 11. Select the course of action that you should choose to guarantee at least once processing

- (2.) Commit offsets at 10


Explanation

Here, you shouldn't commit offsets 11 or 10 as it would indicate that the message #10 has been processed successfully.

## Answer 25:
A consumer has auto.offset.reset=latest, and the topic partition currently has data for offsets going from 45 to 2311. The consumer group never committed offsets for the topic before. Where will the consumer read from?

- (1.) offset 2311

Explanation

Latest means that data retrievals will start from where the offsets currently end

## Answer 26:
You have a consumer group of 12 consumers and when a consumer gets killed by the process management system, rather abruptly, it does not trigger a graceful shutdown of your consumer. Therefore, it takes up to 10 seconds for a rebalance to happen. The business would like to have a 3 seconds rebalance time. What should you do? (select two)


- (1) Decrease heartbeat.interval.ms
- (3) Decrease session.timeout.ms

Explanation

session.timeout.ms must be decreased to 3 seconds to allow for a faster rebalance, and the heartbeat thread must be quicker, so we also need to decrease heartbeat.interval.ms

## Answer 27 (2):
A topic has three replicas and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a consume request is sent to broker?

- (1) Data will be returned from the remaining in-sync replica

Explanation
With this configuration, a single in-sync replica is still readable, but not writeable if the producer using acks=all


## Answer 28 (E):
Using the Range partition assignment strategy, which of the specified partition assignments will
occur? (Choose one)

![img](05-consumer-images/question28.png)

- (3) Topic A partition 0 and topic B partition 0 will be assigned to the same consumer

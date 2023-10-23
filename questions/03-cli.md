# CLI Questions

## Question 1 (1)
How will you find out all the partitions where one or more of the replicas for the partition are not in-sync with the leader?

- (1) kafka-topics.sh --broker-list=localhost:9092 --describe --under-replicated-partitions
- (2) kafka-topics.sh --bootstrap-server=localhost:9092 --describe --unavailable-partitions
- (3) kafka-topics.sh --zookeeper=localhost:2181 --describe --unavailable-partitions
- (4) kafka-topics.sh --zookeeper=localhost:2181 -describe --under-replicated-partitions
- (4*) kafka-topics.sh --bootstrap-server=localhost:9092 --describe --under-replicated-partitions

## Question 2 (2)
How will you find out all the partitions without a leader?

- (1) kafka-topics.sh --broker-list=localhost:2181 --describe --unavailable-partitions
- (2) kafka-topics.sh --zookeeper=localhost:2181 --describe --under-replicated-partitions
- (3) kafka-topics.sh --broker-list=localhost:9092 --describe --under-replicated-partitions
- (4) kafka-topics.sh --zookeeper=localhost:2181 --describe --unavailable-partitions
- (4*) kafka-topics.sh --bootstrap-server=localhost:9092 --describe --unavailable-partitions

## Question 3 (2)
Which Kafka CLI should you use to consume from a topic?

- (1) kafka-console
- (2) kafka-topics
- (3) kafka-consumer-groups
- (4) kafka-console-consumer

## Question 4 (2)
The kafka-console-consumer CLI, when used with the default options

- (1) always uses the same group-id
- (2) does not use a group-id
- (3) uses a random group-id

## Question 5 (3)
How do you create a topic named test with 3 partitions and 3 replicas using the Kafka CLI?

- (1) kafka-topics.sh --bootstrap-server=localhost:9092  --create --replication-factor 3 --partitions 3 --topic test
- (2) kafka-topics.sh --broker-list localhost:9092  --create --replication-factor 3 --partitions 3 --topic test
- (3) kafka-topics.sh --bootstrap-server=localhost:2181  --create --replication-factor 3 --partitions 3 --topic test
- (4) kafka-topics.sh --zookeeper=localhost:9092  --create --replication-factor 3 --partitions 3 --topic test

# CLI Answers
## Answer  1 (1-3)
How will you find out all the partitions where one or more of the replicas for the partition are not in-sync with the leader?

- (4) kafka-topics.sh --zookeeper=localhost:2181 -describe --under-replicated-partitions
- (4*) kafka-topics.sh --bootstrap-server=localhost:9092 --describe --under-replicated-partitions

Explanation
4* version with  Kafka versions > 2.2 


## Answer 2 (2)
How will you find out all the partitions without a leader?

- (4) kafka-topics.sh --zookeeper=localhost:2181 --describe --unavailable-partitions
- (4*) kafka-topics.sh --broker-list=localhost:9092--describe --unavailable-partitions

Explanation
4* version with  Kafka versions > 2.2 

## Answer 3 (2)
Which Kafka CLI should you use to consume from a topic?

- (4) kafka-console-consumer

Explanation
Example: kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic test --from-beginning

## Answer 4 (2)
The kafka-console-consumer CLI, when used with the default options
- (3) uses a random group-id

Explanation
If a group is not specified, the kafka-console-consumer generates a random consumer group.

## Question 5 (3)
How do you create a topic named test with 3 partitions and 3 replicas using the Kafka CLI?

- (1) kafka-topics.sh --bootstrap-server=localhost:9092  --create --replication-factor 3 --partitions 3 --topic test

Explanation
As of Kafka 2.3, the kafka-topics.sh command can take --bootstrap-server localhost:9092 as an argument. You could also use the (now deprecated) option of --zookeeper localhost:2181.
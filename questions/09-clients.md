# Questions Clients

## Question 1 (1-40)
A client connects to a broker in the cluster and sends a fetch request for a partition in a topic. It gets an exception NotLeaderForPartitionException in the response. How does client handle this situation?

1. Send fetch request for each Broker in the cluster
2. Send metadata request to the same broker for the topic and select the broker hosting the lead replica
3. Get the Broker id from Zookeeper that is hosting the leader replica and send request to it.
4. Send metadata request to Zookeeper for the topic and select the broker hosting the leader replica.

## Question 2 (3- 14)
Which of the following is true regarding thread safety in the Java Kafka Clients?

1. One consumer can be safely used in multiple threads
2. One producer needs to be run in one thread
3. One producer can be safely used in multiple threads
4. One Consumer need to run in one thread


## Question 3 (3-  16)
What's is true about Kafka brokers and clients from version 0.10.2 onwards?

1. A newer client can't talk to a newer broker, but an older client can talk to a newer broker
2. A newer client can talk to a newer broker, but an older client cannot talk to a newer broker
3. Client and brokers must have the exact same version to be able to communicate
4. A newer client can talk to a newer broker, but an older client can talk to a newer broker

# Answers Clients
## Question 1 (1-40)
A client connects to a broker in the cluster and sends a fetch request for a partition in a topic. It gets an exception NotLeaderForPartitionException in the response. How does client handle this situation?


- (2.) Send metadata request to the same broker for the topic and select the broker hosting the lead replica

Explanation

In case the consumer has the wrong leader of a partition, it will issue a metadata request. The Metadata request can be handled by any node, so clients know afterwards which broker are the designated leader for the topic partitions. Produce and consume requests can only be sent to the node hosting partition leader.

## Question 2 (3- 14)
Which of the following is true regarding thread safety in the Java Kafka Clients?

- (3.) One producer can be safely used in multiple threads
- (4.) One Consumer need to run in one thread

Explanation

KafkaConsumer is not thread-safe, KafkaProducer is thread safe.


## Question 3 (3-  16)
What's is true about Kafka brokers and clients from version 0.10.2 onwards?

- (4.) A newer client can talk to a newer broker, but an older client can talk to a newer broker

Explanation

Kafka's new bidirectional client compatibility introduced in 0.10.2 allows this. Read more here: https://www.confluent.io/blog/upgrading-apache-kafka-clients-just-got-easier/

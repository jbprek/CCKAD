# Questions
## Question 1
Which of the following setting increases the chance of batching for a Kafka Producer?

1. Increase batch.size
2. Increase the number of producer threads
3. Increase linger.ms
4. Increase message.max.bytes


## Question 2 (1): 
Producing with a key allows to...

1. Add more information to my message
2. Influence partitioning of the producer messages
3. Allow a Kafka Consumer to subscribe to a (topic,key) pair and only receive that data
4. Ensure per-record level security

## Question 3 (1-1): 
A customer has many consumer applications that process messages from a Kafka topic. Each consumer application can only process 50 MB/s. Your customer wants to achieve a target throughput of 1 GB/s. What is the minimum number of partitions will you suggest to the customer for that particular topic?

1. 1
2. 20
3. 10
4. 50


## Question 4 (1): 
Which of the following errors are retryable from a producer perspective? (select two)
1. INVALID_REQUIRED_ACKS
2. NOT_ENOUGH_REPLICAS
3. NOT_LEADER_FOR_PARTITION
4. TOPIC_AUTHORIZATION_FAILED
5. MESSAGE_TOO_LARGE

## Question 5: (-)
Your producer is producing at a very high rate and the batches are completely full each time. How can you improve the producer throughput? (select two)
1. Increase linger.ms
2. Decrease batch.size
3. Increase batch.size
4. Disable compression
5. Enable compression
6. Decrease linger.ms

## Question 6: 
Select all that applies (select THREE)
1. acks is a producer setting
2. min.insync.replicas is a producer setting
3. min.insync.replicas only matters if acks=all
4. min.insync.replicas only matters regardless of the value of acks
5. min.insync.replicas is a topic setting
6. acks is a topic settting

## Question 7 (1): 
To get acknowledgement of writes to only the leader partition, we need to use the config...

1. acks=0
2. acks=1
3. acks=all

## Question 8: (-) Is this correct
What is the risk of increasing max.in.flight.requests.per.connection while also enabling retries in a producer?

1. At least once delivery is not guaranteed
2. Reduce throughput
3. Message order is not preserved
4.  Less resilient

## Question 9: (-)
A Kafka producer application wants to send log messages to a topic that does not include any key. What are the properties that are mandatory to configure for the producer configuration? (select three)

1. value.serializer
2. bootstrap.servers
3. partition
4. value
5. key
6. key.serializer

## Question 10 (1): 
If I want to have an extremely high confidence that leaders and replicas have my data, I should use

1. acks=all,replication factor=3, min insync.replicas=2
2. acks=1,replication factor=3, min insync.replicas=2
3. acks=all,replication factor=3, min insync.replicas=1
4. acks=all,replication factor=2, min insync.replicas=1

## Question 11 (2): 
You are sending messages with keys to a topic. To increase throughput, you decide to increase the number of partitions of the topic. Select all that apply.

1. New records with the same key, will get written to the partition where old records with that key were written.
2. All the existing records will be rebalanced among the partitions to balance load
3. Old records will stay in their partitions
4. New records may get written to a different partition

## Question 12 (2): 
To prevent network-induced duplicates when producing to Kafka, I should use

1. batch.size=1
2. retries=200000
3. enable.idempotence=true
4. max.in.flight.requests.per.connection=1

## Question 13 (2): 
The rule "same key goes to the same partition" is true unless...

1. the number of partitions change
2. the number of producers change
3. the replication factor changes
4. the number of kafka brokers change


## Question 14 (1): 
When is the onCompletion() method called?
````
private class ProducerCallback implements Callback {
    @Override
    public void onCompletion(RecordMetadata recordMetadata, Exception e) {
        if (e != null) {
            e.printStackTrace();
        }
    }
}

ProducerRecord<String, String> record =
        new ProducerRecord<>("topic1", "key1", "value1");
producer.send(record, new ProducerCallback()); 
````
1. when the broker response is received
2. when send() method is called
3. when the message is partitioned and batched successfully
4. when the message is serialized successfully


## Question 15 (2): 
A producer is sending messages with null key to a topic with 6 partitions using the DefaultPartitioner. Where will the messages be stored?

1. Partition 5
2. The partition for null key
3. Any of the topic partitions
4. partition 0


## Question 16 (2): 
What is returned by a producer.send() call in the Java API?

1. A Boolean indicating if the call succeeded
2. Future<RecordMetadata> object
3. Unit
4. Future<ProducerRecord> object


## Question 17 (2): 
A kafka topic has a replication factor of 3 and min.insync.replicas setting of 2. How many brokers can go down before a producer with acks=all can't produce?
Meaning with how many servers down the producer will keep working.
1. 2
2. 3
3. 0
4. 1

## Question 18: 
What happens if you write the following code in your producer? 

producer.send(producerRecord).get()

1. throughput will be decreased
2. it will force all brokers in Kafka to acknowledge the producer record
3. batching will be increased
4. compression will be increased

## Question 19 : 
A topic has three replicas and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a produce request with acks=all is sent to broker?

1. NotEnoughReplicasException will be returned
2. producer request is honored with single in-sync replica
3. producer request will block till one of the two unavailable partition is available again


## Question 20 (3):
You are receiving orders from different customer in an "orders" topic with multiple partitions. Each message has the customer name as the key. There is a special customer named ABC that generates a lot of orders and you would like to reserve a partition exclusively for ABC. The rest of the message should be distributed among other partitions. How can this be achieved? 

1. Not possible since messages with the same key will go to the same partition, but a partition may contain messages with different keys.
2. Add metadata to the producer record
3. define a Kafka Broker routing table
4. Create a custom partitioner

## Question 21: 
If I supply the setting compression.type=snappy to my producer, what will happen? (select two)


1. The Producers have to compress the data
2. The kafka brokers have to compress the data
3. The Consumers have to decompress the data
4. The Consumers have to compress the data
5. The Kafka brokers have to decompress the data

## Question 22: (-)
What exceptions may be caught by the following producer? (select two)
````
ProducerRecord<String, String> record = new ProducerRecord<>("topic1", "key1", "value1");
try {
    producer.send(record);
} catch (Exception e) {
    e.printStackTrace();
}
````

1. BufferExchaustedException
2. InvalidPartitionsException
3. SerializationException
4. BrokerNoAvailableException


## Question 23: 
To produce data to a topic, a producer must provide the Kafka client with...

1. any broker from the cluster and the topic name
2. any broker from the cluster, the topic name and the partition list
3. the list of brokers that have the data, the topic name and the partition list
4. all the brokers from the cluster and the topic name

## Question 24: 
A kafka topic has a replication factor of 3 and min.insync.replicas setting of 2. How many brokers can go down before a producer with acks=1 can't produce?

1. 0
2. 1
3. 3
4. 2


## Question 25: 
You want to send a message of size 3 MB to a topic with default message size configuration. How does KafkaProducer handle large messages?

1. MessageSizeTooLargeException will be thrown, KafkaProducer will not retry and return exception immediately
2. MessageSizeTooLargeException will be thrown, KafkaProducer retries until the number of retries is exhausted
3. KafkaProducer divides messages into sizes of message.max.bytes and sends them in order
4. KafkaProducer divides messages into sizes of message.max.request.size and sends them in order


## Question 26 (3):
What happens if you write the following code in your producer? 
```
producer.send(producerRecord).get()
```
- (1) Throughput will be decreased
- (2) It will force all brokers in Kafka to acknowledge the producerRecord
- (3) Batching will be increased
- (4) Compression will be increased

## Question 27 (3):
A topic has three replicas and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a produce request with acks=all is sent to broker?

- (1) NotEnoughReplicasException will be returned.
- (2) Produce rqquest is honored with single in sync replica
- (3) Produce request will block till one of the two unavailable partition is available again

## Question 28 (1): (-) ?
To enhance compression, I can increase the chances of batching by using

- (1) batch.size=65536
- (2) max.message.size=10MB
- (3) linger.ms=20
- (4) acks=all

## Question 29 (1):
What Are the parts of a producer message?

# Answers
## Answer 1
Which of the following setting increases the chance of batching for a Kafka Producer?

(3) Increase linger.ms

Explanation

linger.ms forces the producer to wait to send messages, hence increasing the chance of creating batches


## Answer 2:
Producing with a key allows to...

(2) Influence partitioning of the producer messages

Explanation

Keys are necessary if you require strong ordering or grouping for messages that share the same key. If you require that messages with the same key are always seen in the  order, attaching a key to messages will ensure messages with the same key always go to the same partition in a topic. Kafka guarantees order within a partition, but not across partitions in a topic, so alternatively not providing a key - which will result in round-robin distribution across partitions - will not maintain such order.

## Answer 3: 
A customer has many consumer applications that process messages from a Kafka topic. Each consumer application can only process 50 MB/s. Your customer wants to achieve a target throughput of 1 GB/s. What is the minimum number of partitions will you suggest to the customer for that particular topic?

(2) 20

Explanation

each consumer can process only 50 MB/s, so we need at least 20 consumers consuming one partition so that 50 * 20 = 1000 MB target is achieved.


## Answer 4: 
Which of the following errors are retryable from a producer perspective? (select two)
- (2) NOT_ENOUGH_REPLICAS
- (3) NOT_LEADER_FOR_PARTITION
- 
Explanation

Both of these are retriable errors, others non-retriable errors. See the full list of errors and their "retriable" status here: https://kafka.apache.org/protocol#protocol_error_codes


## Answer 5: 
Your producer is producing at a very high rate and the batches are completely full each time. How can you improve the producer throughput? (select two)

- (3) Increase batch.size
- (5) Enable compression
- 
Explanation

batch.size controls how many bytes of data to collect before sending messages to the Kafka broker. Set this as high as possible, without exceeding available memory. Enabling compression can also help make more compact batches and increase the throughput of your producer. Linger.ms will have no effect as the batches are already full


## Answer 6: 
Select all that applies (select THREE)

-  (1) acks is a producer setting
-  (3) min.insync.replicas only matters if acks=all
-  (5) min.insync.replicasl is a topic setting

Explanation

acks is a producer setting min.insync.replicas is a topic or broker setting and is only effective when acks=all


## Answer 7: 
To get acknowledgement of writes to only the leader partition, we need to use the config...

- (2) acks=1

Explanation

Producers can set acks=1 to get acknowledgement from partition leader only.



## Answer 8:
What is the risk of increasing max.in.flight.requests.per.connection while also enabling retries in a producer?

- (1) At least once delivery is not guaranteed

Explanation

Some messages may require multiple retries. If there are more than 1 requests in flight, it may result in messages received out of order. Note an exception to this rule is if you enable the producer setting: enable.idempotence=true which takes care of the out of ordering case on its own. See: https://issues.apache.org/jira/browse/KAFKA-5494


## Answer 9:
A Kafka producer application wants to send log messages to a topic that does not include any key. What are the properties that are mandatory to configure for the producer configuration? (select three)

- 1. value.serializer
- 2. bootstrap.servers
- 6. key.serializer

Explanation

Both key and value serializer are mandatory.



## Answer 10: 
If I want to have an extremely high confidence that leaders and replicas have my data, I should use

- (1) acks=all,replication factor=3, min insync.replicas=2
- 
Explanation

acks=all means the leader will wait for all in-sync replicas to acknowledge the record. Also the min in-sync replica setting specifies the minimum number of replicas that need to be in-sync for the partition to remain available for writes.


## Answer 11 (2):
You are sending messages with keys to a topic. To increase throughput, you decide to increase the number of partitions of the topic. Select all that apply.

- (3) Old records will stay in their partitions
- (4) New records may get written to a different partition

Explanation

Increasing the number of partition causes new messages keys to get hashed differently, and breaks the guarantee "same keys goes to the same partition". Kafka logs are immutable and the previous messages are not re-shuffled


## Answer 12:
To prevent network-induced duplicates when producing to Kafka, I should use

- (3) enable.idempotence=true

Explanation

Producer idempotence helps prevent the network introduced duplicates. More details here: https://cwiki.apache.org/confluence/display/KAFKA/Idempotent+Producer


## Answer 13:
The rule "same key goes to the same partition" is true unless...

- (1) the number of partitions change

Explanation

Increasing the number of partition causes new messages keys to get hashed differently, and breaks the guarantee "same keys goes to the same partition". Kafka logs are immutable and the previous messages are not re-shuffled.


## Answer 14:
When is the onCompletion() method called?
````
private class ProducerCallback implements Callback {
    @Override
    public void onCompletion(RecordMetadata recordMetadata, Exception e) {
        if (e != null) {
            e.printStackTrace();
        }
    }
}

ProducerRecord<String, String> record =
        new ProducerRecord<>("topic1", "key1", "value1");
producer.send(record, new ProducerCallback()); 
````
1. when the broker response is received

Explanation

Callback is invoked when a broker response is received.


## Answer 15:
A producer is sending messages with null key to a topic with 6 partitions using the DefaultPartitioner. Where will the messages be stored?


- (3) Any of the topic partitions

Explanation

Message with no keys will be stored with round-robin strategy among partitions.


## Answer 16:
What is returned by a producer.send() call in the Java API?

2. Future<RecordMetadata> object

Explanation

See: https://kafka.apache.org/21/javadoc/org/apache/kafka/clients/producer/KafkaProducer.html

## Answer 17:
A kafka topic has a replication factor of 3 and min.insync.replicas setting of 2. How many brokers can go down before a producer with acks=all can't produce?

- (4) 1

Explanation

acks=all and min.insync.replicas=2 means we must have at least 2 brokers up for the partition to be available

## Answer 18: 
What happens if you write the following code in your producer?

producer.send(producerRecord).get()

- (1.) throughput will be decreased

Explanation

Using Future.get() to wait for a reply from Kafka will limit throughput.

## Answer 19 : 
A topic has three replicas and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a produce request with acks=all is sent to broker?

- (1.) NotEnoughReplicasException will be returned
.
Explanation

With this configuration, a single in-sync replica becomes read-only. Produce request will receive NotEnoughReplicasException.

## Answer 20:
You are receiving orders from different customer in an "orders" topic with multiple partitions. Each message has the customer name as the key. There is a special customer named ABC that generates a lot of orders and you would like to reserve a partition exclusively for ABC. The rest of the message should be distributed among other partitions. How can this be achieved?

- (4.) Create a custom partitioner

Explanation

A Custom Partitioner allows you to easily customise how the partition number gets computed from a source message.


## Answer 21:
If I supply the setting compression.type=snappy to my producer, what will happen? (select two)


- (1.) The Producers have to compress the data
- (3.) The Consumers have to decompress the data


Explanation

Kafka transfers data with zero copy and no transformation. Any transformation (including compression) is the responsibility of clients.

## Answer 22:
What exceptions may be caught by the following producer? (select two)
````
ProducerRecord<String, String> record = new ProducerRecord<>("topic1", "key1", "value1");
try {
    producer.send(record);
} catch (Exception e) {
    e.printStackTrace();
}
````

- (1) BufferExhaustedException
- (3) SerializationException

Explanation

These are the client side exceptions that may be encountered before message is sent to the broker, and before a future is returned by the .send() method.


## Answer 23:
To produce data to a topic, a producer must provide the Kafka client with...

- (1.) any broker from the cluster and the topic name

Explanation

All brokers can respond to a Metadata request, so a client can connect to any broker in the cluster and then figure out on its own which brokers to send data to.


## Answer 24:
A kafka topic has a replication factor of 3 and min.insync.replicas setting of 2. How many brokers can go down before a producer with acks=1 can't produce?

- (4) 2

Explanation

min.insync.replicas does not impact producers when acks=1 (only when acks=all)

## Answer 25:
You want to send a message of size 3 MB to a topic with default message size configuration. How does KafkaProducer handle large messages?

- (1.) MessageSizeTooLargeException will be thrown, KafkaProducer will not retry and return exception immediately


Explanation

MessageSizeTooLarge is not a retryable exception.


## Answer 26 (3):
What happens if you write the following code in your producer?
```
producer.send(producerRecord).get()
```
- (1) Throughput will be decreased

Explanation
Using Future.get() to wait for a reply from Kafka will limit throughput.


## Answer 27 (3):
A topic has three replicas and you set min.insync.replicas to 2. If two out of three replicas are not available, what happens when a produce request with acks=all is sent to broker?

- (1) NotEnoughReplicasException will be returned.

Explanation
With this configuration, a single in-sync replica becomes read-only. Produce request will receive NotEnoughReplicasException.


## Answer 28 (1):
To enhance compression, I can increase the chances of batching by using

- (3) linger.ms=20

Explanation
linger.ms forces the producer to wait before sending messages, hence increasing the chance of creating batches that can be heavily compressed.

## Answer 29

1. Key (Binary)
2. Message (Binary)
3. Compression Type
4. Headers (optional)
5. partition + offset
6. timestamp (system or user set)

# Answers summary


## Answer 1 - 3
## Answer 2 - 2
## Answer 3 - 2
## Answer 4 - 2,3
## Answer 5 - 3,5
## Answer 6 - 1,3,5
## Answer 7 - 2
## Answer 8 - 1
## Answer 9 - 1,2,6
## Answer 10 - 1
## Answer 11 - 3,4
## Answer 12 - 3
## Answer 13 - 1
## Answer 14 - 1
## Answer 15 - 3
## Answer 16 - 2
## Answer 17 - 1
## Answer 18 - 1
## Answer 19  -1
## Answer 20 - 4
## Answer 21 - 1,3
## Answer 22 - 1,3
## Answer 23 - 1
## Answer 24 - 4
## Answer 25 - 1
## Answer 26 - 1 
## Answer 27 - 1
## Answer 28 - 3

## Answer 29

1. Key (Binary)
2. Message (Binary)
3. Compression Type
4. Headers (optional)
5. partition + offset
6. timestamp (system or user set)
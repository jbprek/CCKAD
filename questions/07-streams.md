# Questions Streams 
## Question 1 (1-4)
Which of the following event processing application is stateless? (select two)

1. Read log messages from a stream and writes ERROR event into a high-priority stream and the rest of the events into a low priority stream
2. Find the minimum and maximum stock prices from each day of trading
3. Read events from a stream and modifies them from JSON to AVRO
4. Publish the top 10 stocks each day.


## Question 2 (1-15)
You are running a Kafka Streams application in a Docker container managed by Kubernetes, and upon application restart, it takes a long time for the docker container to replicate the state and get back to processing the data. How can you improve dramatically the application restart?

1. Increase the number of partitions in your inputs topic
2. Mount a persistent volume for your RocksDB
3. Reduce the Streams caching property
4. Increase the number of Streams Threads

## Question 3 (1-28)
Which of the following Kafka Streams operators are stateful? (select all that apply)

1. reduce
2. flatMap
3. peek
4. count
5. joining[
6. aggregate

## Question 4 (1-35)
You want to perform table lookups against a KTable everytime a new record is received from the KStream. What is the output of KStream-KTable join?

1. KTable
2. KStream
3. GlobalKTable
4. You choose between KTable and KStream


## Question 5 (1-38)
The exactly once guarantee in the Kafka Streams is for which flow of data?

1. Kafka=>External
2. Kafka=>Kafka
3. External=>Kafka

## Question 6 (2-5)
We have a store selling shoes. What dataset is a great candidate to be modeled as a KTable in Kafka Streams?

1. Inventory contents right now
2. Items returned
3. Money mad until now
4. The transaction stream


## Question 7 (2-9)
An ecommerce website maintains two topics - a high volume "purchase" topic with 5 partitions and low volume "customer" topic with 3 partitions. You would like to do a stream-table join of these topics. How should you proceed?

1. Repartition customer topic to have 5 partitions
2. Reparttion the purchase topic to have 3 partitions
3. Do a KStream/Ktable join after a repartition step
4. Model customer as a GlobalKTable


## Question 8 (2-11)
To transform data from a Kafka topic to another one, I should use

1. Kafka Connect Source
2. Consumer + Producer
3. Kafka Connect Sink
4. Kafka Streams

## Question 9 (2-26)
Select the Kafka Streams joins that are always windowed joins.

1. KStream-KStream join
2. KStream-GlobalKTable
3. Ktable-KTable jon
4. KStream-Ktable join


## Question 10 (2-38)
````java
StreamsBuilder builder = new StreamsBuilder();
KStream<String, String> textLines = builder.stream("word-count-input");
KTable<String, Long> wordCounts = textLines
    .mapValues(textLine -> textLine.toLowerCase())
    .flatMapValues(textLine -> Arrays.asList(textLine.split("\W+")))
    .selectKey((key, word) -> word)
    .groupByKey()
    .count(Materialized.as("Counts"));
wordCounts.toStream().to("word-count-output", Produced.with(Serdes.String(), Serdes.Long()));
builder.build();
````
What is an adequate topic configuration for the topic word-count-output?

1. cleanup.policy=compact
2. max.message.bytes=10000000
3. cleanup.policy=delete
4. compression.type=lz4

Explanation

Result is aggregated into a table with key as the unique word and value its frequency. We have to enable log compaction for this topic to align the topic's cleanup policy with KTable semantics.

## Question 11 (2-47)
In Kafka Streams, by what value are internal topics prefixed by?

1. application.id
2. group.id
3. kafka-streams-
4. tasks-<number>-



Explanation
In Kafka Streams, the application.id is also the underlying group.id for your consumers, and the prefix for all internal topics (repartition and state)


## Question 12 (3-12)
An ecommerce wesbite sells some custom made goods. What's the natural way of modeling this data in Kafka streams?

1. Purchase as stream, Product as stream, Customer as Stream
2. Purchase as table,Product as table, Customer as table
3. Purchase as stream,Procuct as table,Customer as stream
4. Purchase as stream,Product as table,Customer as table

## Question 13 (3-17)
Which of the following Kafka Streams operators are stateless? (select all that apply)

1. flatmap
2. filter
3. aggregate
4. map
5. branch
6. groupBy

## Question 14 (3-30)
Which of these joins does not require input topics to be sharing the same number of partitions?

1. KStream-KTable join
2. KStream-GlobalKTable join
3. KTable-KTable join
4. KStream-KStream join


## Question 15 (3-32)
Your streams application is reading from an input topic that has 5 partitions. You run 5 instances of your application, each with num.streams.threads set to 5. How many stream tasks will be created and how many will be active?

1. 5 created, 1 active
2. 25 created, 5 active
3. 5 created, 5 active
4. 25 created, 25 active

Explanation
One partition is assigned a thread, so only 5 will be active, and 25 threads (i.e. tasks) will be created

## Question 15 (3-44)
We want the average of all events in every five-minute window updated every minute. What kind of Kafka Streams window will be required on the stream?

1. Sliding window
2. Tumbling window
3. Session window
4. Hopping window



Explanation
A hopping window is defined by two properties: the window's size and its advance interval (aka "hop"), e.g., a hopping window with a size 5 minutes and an advance interval of 1 minute.



# Answers Streams 
## Question 1 (1-4)
Which of the following event processing application is stateless? (select two)

- (1.) Read log messages from a stream and writes ERROR event into a high-priority stream and the rest of the events into a low priority stream
- (3.) Read events from a stream and modifies them from JSON to AVRO


Explanation
Stateless means processing of each message depends only on the message, so converting from JSON to Avro or filtering a stream are both stateless operations


## Question 2 (1-15)
You are running a Kafka Streams application in a Docker container managed by Kubernetes, and upon application restart, it takes a long time for the docker container to replicate the state and get back to processing the data. How can you improve dramatically the application restart?

- (2.) Mount a persistent volume for your RocksDB

## Question 3 (1-28)
Which of the following Kafka Streams operators are stateful? (select all that apply)

- 1 reduce
- 4 count
- joining 
- aggregate



Explanation
See: https://kafka.apache.org/20/documentation/streams/developer-guide/dsl-api.html#stateful-transformations




## Question 4 (1-35)
You want to perform table lookups against a KTable everytime a new record is received from the KStream. What is the output of KStream-KTable join?


- 2 KStream

Explanation

Here KStream is being processed to create another KStream.


## Question 5 (1-38)
The exactly once guarantee in the Kafka Streams is for which flow of data?

- 2 Kafka=>Kafka


Explanation
Kafka Streams can only guarantee exactly once processing if you have a Kafka to Kafka topology.

## Question 6 (2-5)
We have a store selling shoes. What dataset is a great candidate to be modeled as a KTable in Kafka Streams?

- 1 Inventory contents right now
- 3 Money made until now

Explanation

Aggregations of stream are stored in table, whereas Streams must be modeled as a KStream to avoid data explosion

## Question 7 (2-9)
An ecommerce website maintains two topics - a high volume "purchase" topic with 5 partitions and low volume "customer" topic with 3 partitions. You would like to do a stream-table join of these topics. How should you proceed?

- 4 Model customer as a GlobalKTable

Explanation

In case of KStream-KStream join, both need to be co-partitioned. This restriction is not applicable in case of join with GlobalKTable, which is the most efficient here.

## Question 8 (2-11)
To transform data from a Kafka topic to another one, I should use

- 4 Kafka Streams

Explanation

Kafka Streams is a library for building streaming applications, specifically applications that transform input Kafka topics into output Kafka topics


## Question 9 (2-26)
Select the Kafka Streams joins that are always windowed joins.

- 1 KStream-KStream join



Explanation
See: https://docs.confluent.io/current/streams/developer-guide/dsl-api.html#joining



## Question 10 (2-38)
````java
StreamsBuilder builder = new StreamsBuilder();
KStream<String, String> textLines = builder.stream("word-count-input");
KTable<String, Long> wordCounts = textLines
    .mapValues(textLine -> textLine.toLowerCase())
    .flatMapValues(textLine -> Arrays.asList(textLine.split("\W+")))
    .selectKey((key, word) -> word)
    .groupByKey()
    .count(Materialized.as("Counts"));
wordCounts.toStream().to("word-count-output", Produced.with(Serdes.String(), Serdes.Long()));
builder.build();
````
What is an adequate topic configuration for the topic word-count-output?

- 1 cleanup.policy=compact

Explanation

Result is aggregated into a table with key as the unique word and value its frequency. We have to enable log compaction for this topic to align the topic's cleanup policy with KTable semantics.


## Question 11 (2-47)
In Kafka Streams, by what value are internal topics prefixed by?

- 1 application.id

Explanation
In Kafka Streams, the application.id is also the underlying group.id for your consumers, and the prefix for all internal topics (repartition and state)


## Question 12 (3-12)
An ecommerce wesbite sells some custom made goods. What's the natural way of modeling this data in Kafka streams?


- 4 Purchase as stream,Product as table,Customer as table



Explanation
Mostly-static data is modeled as a table whereas business transactions should be modeled as a stream.


## Question 13 (3-17)
Which of the following Kafka Streams operators are stateless? (select all that apply)

- 1 flatmap
- filter
- map
- branch
- groupBy


Explanation

See: https://kafka.apache.org/20/documentation/streams/developer-guide/dsl-api.html#stateless-transformations

## Question 14 (3-30)
Which of these joins does not require input topics to be sharing the same number of partitions?

- 2 KStream-GlobalKTable join


Explanation

GlobalKTables have their datasets replicated on each Kafka Streams instance and therefore no repartitioning is required


## Question 15 (3-32)
Your streams application is reading from an input topic that has 5 partitions. You run 5 instances of your application, each with num.streams.threads set to 5. How many stream tasks will be created and how many will be active?

- 2 25 created, 5 active

Explanation
One partition is assigned a thread, so only 5 will be active, and 25 threads (i.e. tasks) will be created



## Question 15 (3-44)
We want the average of all events in every five-minute window updated every minute. What kind of Kafka Streams window will be required on the stream?

- 4 Hopping window



Explanation
A hopping window is defined by two properties: the window's size and its advance interval (aka "hop"), e.g., a hopping window with a size 5 minutes and an advance interval of 1 minute.

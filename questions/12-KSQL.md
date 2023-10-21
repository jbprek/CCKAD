# KSQL questions
## Question 1 (1-22)
How will you read all the messages from a topic in your KSQL query? (Select one)

1. KSQL reads from the end of the topic, this cannot be changed.
2. KSQL reads from the beginning of a topic, this is the default.
3. Use KSQL CLI to set auto.offset.reset property to earliest


## Question 2 (1-27)
Which KSQL queries write to Kafka?

1. SHOW STREAMS and EXPLAIN <query> statements
2. COUNT and JOIN
3. CREATE STREAM WITH <topic> and CREATE TABLE WITH <topic>
4. CREATE STREAM AS SELECT and CREATE TABLE AS SELECT

## Question 3 (1-44)
is KSQL ANSI SQL compliant?

1. true
2. false


## Question 4 (2-7)
What Java library is KSQL based on?

1. Kafka Streams
2. Kafka Connect
3. Schema Registry
4. REST Proxy

## Question 5 (3-37)
Where are KSQL-related data and metadata stored?

1. Zookeeper
2. Kafka Topics
3. Schema Registry
4. PostresSQL database


## Question 6 (3-49)
What is the default port that the KSQL server listens on?

1. 9092
2. 9088
3. 2181
4. 8083


# Answers

## Question 1 (1-22)
How will you read all the messages from a topic in your KSQL query? (Select one)

- (3.) Use KSQL CLI to set auto.offset.reset property to earliest

Explanation
Consumers can set auto.offset.reset property to earliest to start consuming from beginning. For KSQL, SET 'auto.offset.reset'='earliest';



## Question 2 (1-27)
Which KSQL queries write to Kafka?

- (3.) CREATE STREAM WITH <topic> and CREATE TABLE WITH <topic>
- (4.) CREATE STREAM AS SELECT and CREATE TABLE AS SELECT


Explanation
SHOW STREAMS and EXPLAIN <query> statements run against the KSQL server that the KSQL client is connected to. They don't communicate directly with Kafka. CREATE STREAM WITH <topic> and CREATE TABLE WITH <topic> write metadata to the KSQL command topic. Persistent queries based on CREATE STREAM AS SELECT and CREATE TABLE AS SELECT read and write to Kafka topics. Non-persistent queries based on SELECT that are stateless only read from Kafka topics, for example SELECT ‚Ä¶ FROM foo WHERE ‚Ä¶. Non-persistent queries that are stateful read and write to Kafka, for example, COUNT and JOIN. The data in Kafka is deleted automatically when you terminate the query with CTRL-C.


## Question 3 (1-44)
is KSQL ANSI SQL compliant?

- (2.) false


Explanation
KSQL is not ANSI SQL compliant, for now there are no defined standards on streaming SQL languages


## Question 4 (2-7)
What Java library is KSQL based on?

- (1.) Kafka Streams

Explanation
KSQL is based on Kafka Streams and allows you to express transformations in the SQL language that get automatically converted to a Kafka Streams program in the backend


## Question 5 (3-37)
Where are KSQL-related data and metadata stored?

- (2.) Kafka Topics

Explanation
metadata is stored in and built from the KSQL command topic. Each KSQL server has its own in-memory version of the metastore.


## Question 6 (3-49)
What is the default port that the KSQL server listens on?


- (2.) 8088

Explanation
Default port of KSQL server is 8088
# Questions
## Question 1 (1-2)
You want to sink data from a Kafka topic to S3 using Kafka Connect. There are 10 brokers in the cluster, the topic has 2 partitions with replication factor of 3. How many tasks will you configure for the S3 connector? (Select one)

1. 2
2. 3
3. 10
4. 6

## Question 2 (1-24)
To import data from external databases, I should use: (Select one)

1. Kafka Streams
2. Confluent Rest Proxy
3. Kafka Connect Source
4. Kafka Connect Sink


## Question 3 (1-39)
You are using JDBC source connector to copy data from 2 tables to two Kafka topics. There is one connector created with max.tasks equal to 2 deployed on a cluster of 3 workers. How many tasks are launched? (Select one)

1. 1
2. 2
3. 3
4. 6

## Question 4 (1-42)
What isn't an internal Kafka Connect topic?  (Select one)

1. connect-status
2. connect-configs
3. connect-offsets
4. connect-jars

## Question 5 (2-1)
When using plain JSON data with Connect, you see the following error message: org.apache.kafka.connect.errors.DataException: JsonDeserializer with schemas.enable requires "schema" and "payload" fields and may not contain additional fields. How will you fix the error?

1. Set key.converter,value.converter to JsonConverter and the schema registry URL
2. Set key.converter.schemas.enable and value.converter.schemas.enable to false
3. Use Single Message Transfroms to add schema and payload fields in the message
4. Set key.converter, value.converter to AvroConverter and the schema registry url

## Question 6 (2-21)
You are using JDBC source connector to copy data from 3 tables to three Kafka topics. There is one connector created with max.tasks equal to 2 deployed on a cluster of 3 workers. How many tasks are launched?

1. 1
2. 2
3. 3
4. 6

## Question 7 (3-4)
To continuously export data from Kafka into a target database, I should use

1. Kafka Streams
2. Kafka Connect Source
3. Kafka Connect Sink
4. Kafka Producer

## Question 8 (3-29)
You are using JDBC source connector to copy data from a table to Kafka topic. There is one connector created with max.tasks equal to 2 deployed on a cluster of 3 workers. How many tasks are launched?

1. 1
2. 2
3. 3
4. 6


# Answers 

## Question 1 (1-2)
You want to sink data from a Kafka topic to S3 using Kafka Connect. There are 10 brokers in the cluster, the topic has 2 partitions with replication factor of 3. How many tasks will you configure for the S3 connector?

- (1.) 2


Explanation
You cannot have more sink tasks (= consumers) than the number of partitions, so 2.

## Question 2 (1-24)
To import data from external databases, I should use

- (3.) Kafka Connect Source


Explanation
Kafka Connect Sink is used to export data from Kafka to external databases and Kafka Connect Source is used to import from external databases into Kafka.



## Question 3 (1-39)
You are using JDBC source connector to copy data from 2 tables to two Kafka topics. There is one connector created with max.tasks equal to 2 deployed on a cluster of 3 workers. How many tasks are launched?

- (2.) 2
 
Explanation
we have two tables, so the max number of tasks is 2


## Question 4 (1-42)
What isn't an internal Kafka Connect topic?  (Select one)

- (4.) connect-jars

Explanation
connect-configs stores configurations, connect-status helps to elect leaders for connect, and connect-offsets store source offsets for source connectors


## Question 5 (2-1)
When using plain JSON data with Connect, you see the following error message: org.apache.kafka.connect.errors.DataException: JsonDeserializer with schemas.enable requires "schema" and "payload" fields and may not contain additional fields. How will you fix the error?

- (2.) Set key.converter.schemas.enable and value.converter.schemas.enable to false

Explanation
You will need to set the schemas.enable parameters for the converter to false for plain text with no schema.


## Question 6 (2-21)
You are using JDBC source connector to copy data from 3 tables to three Kafka topics. There is one connector created with max.tasks equal to 2 deployed on a cluster of 3 workers. How many tasks are launched?

- (2.) 2

Explanation
here, we have three tables, but the max.tasks is 2, so that's the maximum number of tasks that will be created


## Question 7 (3-4)
To continuously export data from Kafka into a target database, I should use

- (3.) Kafka Connect Sink

Explanation
Kafka Connect Sink is used to export data from Kafka to external databases and Kafka Connect Source is used to import from external databases into Kafka.


## Question 8 (3-29)
You are using JDBC source connector to copy data from a table to Kafka topic. There is one connector created with max.tasks equal to 2 deployed on a cluster of 3 workers. How many tasks are launched?

- (1.) 1

Explanation
JDBC connector allows one task per table.




# Schema  Questions

## Question 1 (1-1): 

A consumer application is using KafkaAvroDeserializer to deserialize Avro messages. What happens if message schema is not present in AvroDeserializer local cache?

1. Throws Deserialization Exception
2. Fetches schema from schema registry
3. Throws Serialization Exception
4. Fails silently

## Question 2 (1-6) SOS (-)
I am producing Avro data on my Kafka cluster that is integrated with the Confluent Schema Registry. After a schema change that is incompatible, I know my data will be rejected. Which component will reject the data?

1. Zookeeper
2. The Kafka producer himself
3. The Kafka Broker
4. Confluent Schema Registry

## Question 3 (1-11)
What client protocol is supported for the schema registry? (select two)

1. JDBC
2. Websocket
3. HTTP
4. HTTPS

## Question 4 (1- 21)
Which is an optional field in an Avro record?

1. name
2. doc
3. fields
4. namespace

## Question 5 (1- 31) 
What is NOT a feature of the Confluent schema registry?

1. Enforce compatibility rules
2. Store schemas
3. Store Avro Data


## Question 6 (1- 33)
Using the Confluent Schema Registry, where are Avro schema stored?

1. In Zookeeper node schemas
2. In Schema registry embedded SQL database
3. in the _schemas topic
4. In the message bytes themselves



## Question 7 (1- 34) SOS (-)
In Avro, adding a field to a record without default is a __ schema evolution

1. breaking
2. forward
3. backward
4. full

## Question 8 (2-8)
When using the Confluent Kafka Distribution, where does the schema registry service reside?

1. As an in memory plugin on your Zookeeper cluster
2. As an in memory plugin on your Kafka Connect Workers
3. As a separate JVM Component
4. As an in memory plugin on your Kafka Brokers

## Question 9 (2-31)  SOS (-)
In Avro, removing a field that does not have a default is a __ schema evolution

1. backward
2. breaking
3. forward
4. full

## Question 10 (2-39)
In Java, Avro SpecificRecords classes are

1. automatically generated from an Avro Schema + a Maven/Gradle Plugin
2. automatically generated from an Avro Schema
3. written manually by the programmer

## Question 11 (3-7)  SOS (-)
In Avro, removing or adding a field that has a default is a __ schema evolution

1. full
2. backward
3. forward
4. breaking

## Question 12 (3-23)
In Avro, adding an element to an enum without a default is a __ schema evolution
1. full
2. backward
3. forward
4. breaking

## Question 13 (3):
Which of the following is not an Avro primitive type?

1. int
2. long
3. string
4. date
5. null


# Schema  Answers

## Answer 1 (1-1):

A consumer application is using KafkaAvroDeserializer to deserialize Avro messages. What happens if message schema is not present in AvroDeserializer local cache?

-(2) Fetches schema from schema registry

Explanation

First local cache is checked for the message schema. In case of cache miss, schema is pulled from the schema registry. An exception will be thrown in the Schema Registry does not have the schema (which should never happen if you set it up properly)


## Answer 2 (1-6) 
I am producing Avro data on my Kafka cluster that is integrated with the Confluent Schema Registry. After a schema change that is incompatible, I know my data will be rejected. Which component will reject the data?

- (4.) Confluent Schema Registry

Explanation

The Confluent Schema Registry is your safeguard against incompatible schema changes and will be the component that ensures no breaking schema evolution will be possible. Kafka Brokers do not look at your payload and your payload schema, and therefore will not reject data

## Answer 3 (1-11)
What client protocol is supported for the schema registry? (select two)

- (3.) HTTP
- (4.) HTTPS

Explanation

clients can interact with the schema registry using the HTTP or HTTPS interface


## Answer 4 (1- 21)
Which is an optional field in an Avro record?

- (2.) doc

Explanation

doc represents optional description of message

## Answer 5 (1- 31)
What isn't a feature of the Confluent schema registry?


- (3.) Store Avro Data


Explanation
Data is stored on brokers.

## Answer 6 (1- 33)
Using the Confluent Schema Registry, where are Avro schema stored?

- (3.) in the _schemas topic

Explanation

The Schema Registry stores all the schemas in the _schemas Kafka topic

## Answer 7 (1- 34) 
In Avro, adding a field to a record without default is a __ schema evolution

- (2). forward

Explanation

Clients with old schema will be able to read records saved with new schema.

## Answer 8 (2-8)
When using the Confluent Kafka Distribution, where does the schema registry service reside?

- (3.) As a separate JVM Component


Explanation

Schema registry is a separate application that provides RESTful interface for storing and retrieving Avro schemas.

## Answer 9 (2-31)
In Avro, removing a field that does not have a default is a __ schema evolution

- (1.) backward

Explanation

Clients with new schema will be able to read records saved with old schema.


## Answer 10 (2-39)
In Java, Avro SpecificRecords classes are

- (1) automatically generated from an Acro Scchema + a Maven/Gradle Plugin

Explanation

SpecificRecord is created from generated record classes

## Answer 11 (3-7)
In Avro, removing or adding a field that has a default is a __ schema evolution

- (1.) full

Explanation

Clients with new schema will be able to read records saved with old schema and clients with old schema will be able to read records saved with new schema.


## Answer 12 (3-23)
In Avro, adding an element to an enum without a default is a __ schema evolution

- (4.) breaking

Explanation

Since Confluent 5.4.0, Avro 1.9.1 is used. Since default value was added to enum complex type , the schema resolution changed from:

(<1.9.1) if both are enums:** if the writer's symbol is not present in the reader's enum, then an error is signalled. **(>=1.9.1) if both are enums:

if the writer's symbol is not present in the reader's enum and the reader has a default value, then that value is used, otherwise an error is signalled.


## Answer 13 (3-42) 
Which of the following is not an Avro primitive type?

- (4.) date

Explanation

date is a logical type


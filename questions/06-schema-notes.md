# AVRO Format

## Primitive types 
- null
- int
- long
- float
- double
- bytes
- string
- boolean

## Avro Record
- name
- namespace
- doc
- aliases
- fields
  - name
  - doc
  - type (can be primitive)
  - default 

## Avro Complex Types

You can have complex types such as:
- Enums
- Arrays
- Maps
- Unions
- Using other schemas as type
## Avro Enums

example:
 ````json
 {
  "type": "enum",
  "name": "CustomerStatus",
  "symbols": [
    "BRONZE",
    "SILVER",
    "GOLD"
  ]
}
 ````

## Avro Arrays
example:
 ````json
 {
  "type": "array",
  "items": "string"
}
 ````

## Avro Maps
example:
 ````json
 {
  "type": "map",
  "values": "string"
}
 ````


## Avro Union
Way to define fields with muliple types

Most common use to have optional values in a field

example:

 ````json
 {
  "name" : "middle_name",
  "type": ["null", "string"],
  "default": null
}
 ````

## TODO Logical types

## TODO the complex case of Decimals, Floats, Doubles

## Schema Evolution
### Evolution types
1. **Backward** : a backward compatible change. **new schema can read old data**.
2. **Forward** :  a forward compatible change. **old schema can read new data**.
3. **Full** : when is backward and forward at the same time
4. **Breaking** : when none of those

### Breaking changes
- Adding removing elements from Enum
- Changing the type of the field (i.e. string to int)
- Renaming a field

### Backward evolution
- removing a field without a default
### Forward
- adding a field without a default
### Full
- adding or removing a field with a default
### Breaking
- adding an element in an Enum

### Rules to avoid breaking changes
1. Make your primary key required
2. Give default values to fields that can be removed in the future
3. Be very careful when using enums
4. Don't rename fields
5. When evolving a schema **always** give default values
6. When evolving a schema **never** delete a required field

# Schema  Answers

## Question 8 (2-8)
When using the Confluent Kafka Distribution, where does the schema registry service reside?

- (3.) As a separate JVM Component


Explanation

Schema registry is a separate application that provides RESTful interface for storing and retrieving Avro schemas.

## Question 1 (1-1):

A consumer application is using KafkaAvroDeserializer to deserialize Avro messages. What happens if message schema is not present in AvroDeserializer local cache?

-(2) Fetches schema from schema registry

Explanation

First local cache is checked for the message schema. In case of cache miss, schema is pulled from the schema registry. An exception will be thrown in the Schema Registry does not have the schema (which should never happen if you set it up properly)


## Question 2 (1-6)
I am producing Avro data on my Kafka cluster that is integrated with the Confluent Schema Registry. After a schema change that is incompatible, I know my data will be rejected. Which component will reject the data?

- (4.) Confluent Schema Registry

Explanation

The Confluent Schema Registry is your safeguard against incompatible schema changes and will be the component that ensures no breaking schema evolution will be possible. Kafka Brokers do not look at your payload and your payload schema, and therefore will not reject data

## Question 3 (1-11)
What client protocol is supported for the schema registry? (select two)

- (3.) HTTP
- (4.) HTTPS

Explanation

clients can interact with the schema registry using the HTTP or HTTPS interface

## Question 5 (1- 31)
What isn't a feature of the Confluent schema registry?


- (3.) Store Avro Data


Explanation
Data is stored on brokers.

## Question 6 (1- 33)
Using the Confluent Schema Registry, where are Avro schema stored?

- (3.) in the _schemas topic

Explanation

The Schema Registry stores all the schemas in the _schemas Kafka topic


## Question 4 (1- 21)
Which is an optional field in an Avro record?

- (2.) doc

Explanation

doc represents optional description of message


## Question 7 (1- 34)
In Avro, adding a field to a record without default is a __ schema evolution

- (2). forward

Explanation

Clients with old schema will be able to read records saved with new schema.

## Question 9 (2-31)
In Avro, removing a field that does not have a default is a __ schema evolution

- (4.) full

Explanation

Clients with new schema will be able to read records saved with old schema.

## Question 11 (3-7)
Question 7: Incorrect
In Avro, removing or adding a field that has a default is a __ schema evolution

- (1.) full

Explanation

Clients with new schema will be able to read records saved with old schema and clients with old schema will be able to read records saved with new schema.


## Question 12 (3-23)
In Avro, adding an element to an enum without a default is a __ schema evolution

- (4.) breaking

Explanation

Since Confluent 5.4.0, Avro 1.9.1 is used. Since default value was added to enum complex type , the schema resolution changed from:

(<1.9.1) if both are enums:** if the writer's symbol is not present in the reader's enum, then an error is signalled. **(>=1.9.1) if both are enums:

if the writer's symbol is not present in the reader's enum and the reader has a default value, then that value is used, otherwise an error is signalled.


## Question 13 (3-42: Incorrect
Which of the following is not an Avro primitive type?

- (4.) date

Explanation

date is a logical type



## Question 10 (2-39)
In Java, Avro SpecificRecords classes are

- (1) automatically generated from an Acro Scchema + a Maven/Gradle Plugin

Explanation

SpecificRecord is created from generated record classes

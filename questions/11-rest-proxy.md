# Questions Rest Proxy

## Question 1
If I want to send binary data through the REST proxy to topic "test_binary", it needs to be base64 encoded. A consumer connecting directly into the Kafka topic "test_binary" will receive:

1. json data
2. avro data
3. base 64 data , it will need to decode it
4. binary data

## Question 2
What data format isn't natively available with the Confluent REST Proxy?
1. protobuf
2. avro
3. json
4. binary

## Question 3
If I want to send binary data through the REST proxy, it needs to be base64 encoded. Which component needs to encode the binary data into base 64?

1. The Kafka Broker
2. Zookeeper
3. REST Proxy
4. The Producer

# Answers  Rest Proxy
## Answer 1 
If I want to send binary data through the REST proxy to topic "test_binary", it needs to be base64 encoded. A consumer connecting directly into the Kafka topic "test_binary" will receive:

- (4) binary data
 
Overall explanation

On the producer side, after receiving base64 data, the REST Proxy will convert it into bytes and then send that bytes payload to Kafka. Therefore consumers reading directly from Kafka will receive binary data.

## Answer 2
What data format isn't natively available with the Confluent REST Proxy?
1. protobuf

Overall explanation

Protocol buffers isn't a natively supported type for the Confluent REST Proxy, but you may use the binary format instead


## Answer 3
If I want to send binary data through the REST proxy, it needs to be base64 encoded. Which component needs to encode the binary data into base 64?


- (4)The Producer

Overall explanation

The REST Proxy requires to receive data over REST that is already base64 encoded, hence it is the responsibility of the producer
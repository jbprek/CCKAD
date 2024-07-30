# REST Proxy Questions


## Question 1: (1)
If I want to send binary data through the REST proxy to topic "test_binary", it needs to be base64 encoded. A consumer connecting directly into the Kafka topic "test_binary" will receive

1. avro data
2. binary data
3. base64 encoded data, it will need to decode it
4. json data

Explanation:  On the producer side, after receiving base64 data, the REST Proxy will convert it into bytes and then send that bytes payload to Kafka. Therefore consumers reading directly from Kafka will receive binary data.

## Question 2 (2)
What data format isn't natively available with the Confluent REST Proxy?

1. protobuf
2. avro
3. json
4. binary

## Question 3:  (3)
If I want to send binary data through the REST proxy, it needs to be base64 encoded. Which component needs to encode the binary data into base 64?

1. Kafka broker
2. Zookeeper
3. REST Proxy
4. Producer

# REST Proxy Answers

## Answer 1: (1)
If I want to send binary data through the REST proxy to topic "test_binary", it needs to be base64 encoded. A consumer connecting directly into the Kafka topic "test_binary" will receive


- (2) binary data

Explanation:  On the producer side, after receiving base64 data, the REST Proxy will convert it into bytes and then send that bytes payload to Kafka. Therefore consumers reading directly from Kafka will receive binary data.


## Answer 2
What data format isn't natively available with the Confluent REST Proxy? 
- (1) protobuf
 
Explanation:  Protocol buffers isn't a natively supported type for the Confluent REST Proxy, but you may use the binary format instead


## Abswer 3:  (3)
If I want to send binary data through the REST proxy, it needs to be base64 encoded. Which component needs to encode the binary data into base 64?

- (4). Producer

Explanation: The REST Proxy requires to receive data over REST that is already base64 encoded, hence it is the responsibility of the producer
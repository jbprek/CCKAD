# Questions Security
## Question 1 (1-47)
Where are the ACLs stored in a Kafka cluster by default?

1. Inside the broker's data directory
2. In Kafka topic __kafka_acls
3. Inside Zookeeper's data directory
4. Under Zookeeper node /kafka-acl/

## Question 2 (2-34)
A producer application in a developer machine was able to send messages to a Kafka topic. After copying the producer application into another developer's machine, the producer is able to connect to Kafka but unable to produce to the same Kafka topic because of an authorization issue. What is the likely issue?

1. You cannot copy a producer application from one machine to another
2. Broker configuration needs to be changed to allow a different producer
3. The Kafka Broker needs to be restarted
4. The Kafka ACL does not allow another machine IP

## Question 3 (3-5)
If you enable an SSL endpoint in Kafka, what feature of Kafka will be lost?

1. Zero Copy
2. Cross cluster mirroring
3. Support for Avro format
4. Exactly once delivery


## Question 4 (3-24)
What is the protocol used by Kafka clients to securely connect to the Confluent REST Proxy?

1. HTTP
2. Kerberos
3. HTTPS
4. SASL


## Question 4 (3-34)
What is not a valid authentication mechanism in Kafka?
1. SASL/GSSAPI
2. SAML
3. SSL
4. SASL/SCRAM


Explanation
Learn more about security here: https://kafka.apache.org/documentation/#security


# Answers Security

## Question 1 (1-47)
Where are the ACLs stored in a Kafka cluster by default?


- (4.) Under Zookeeper node /kafka-acl/


Explanation

ACLs are stored in Zookeeper node /kafka-acls/ by default.

## Question 2 (2-34)
A producer application in a developer machine was able to send messages to a Kafka topic. After copying the producer application into another developer's machine, the producer is able to connect to Kafka but unable to produce to the same Kafka topic because of an authorization issue. What is the likely issue?


- (4.) The Kafka ACL does not allow another machine IP

Explanation

ACLs take "Host" as a parameter, which represents an IP. It can be * (all IP), or a specific IP. Here, it's a specific IP as moving a producer to a different machine breaks the consumer, so the ACL needs to be updated

## Question 3 (3-5)
If you enable an SSL endpoint in Kafka, what feature of Kafka will be lost?

- (1.) Zero Copy

Explanation

With SSL, messages will need to be encrypted and decrypted, by being first loaded into the JVM, so you lose the zero copy optimization. See more information here: https://twitter.com/ijuma/status/1161303431501324293?s=09


## Question 4 (3-24)
What is the protocol used by Kafka clients to securely connect to the Confluent REST Proxy?

- (3.) HTTPS


Explanation
TLS - but it is still called SSL.


## Question 4 (3-34)
What is not a valid authentication mechanism in Kafka?

- (2) SAML


Explanation
Learn more about security here: https://kafka.apache.org/documentation/#security

# Producer

## General

## Use of key

## Configuration

## Parameters

- max.block.ms : This parameter controls how long the producer may block when calling send() and when explicitly requesting metadata via partitionsFor() Default 1 minute
- delivery.timeout.ms : If the producer exceeds delivery.timeout.ms while retrying, the callback will be called with the exception that corresponds to the error that the broker returned before retrying. If delivery.timeout.ms is exceeded while the record batch was still waiting to be sent, the callback will be called with a timeout exception. delivery.timeout.ms > linger.ms + retry.backoff.ms + request.rimeout.ms, default value 2 min.
- linger.ms

## Retryable errors/exceptions

- [REf](https://kafka.apache.org/protocol#protocol_error_codes)
### Related questions


- Q1 Producer config linger.ms - linger.ms increases the chances of batching
- Q2 General key use 
- Q3 num of partition effect on throughput
- Q4 Retryable conditions
- Q5 Improve producer throughput client side (Increase batch.size, Enable compression )
- Q6 acks producer setting, min.insync.replicas broker or topic setting
- Q7 acks producer setting
- Q8 max.in.flight.requests.per.connection & enabling retries in a producer =>  At least once delivery is not guaranteed
- Q9 Producer mandatory settings (bootstrap.servers, key.serializer,value.serializer)
- Q10 Use of acks, replication factor, min.insync.replicas ex of high confidence acks=all,replication factor=3, min.insync.replicas=2
- Q11 Topic increase number of partitions, old and new records with same key? old in old, new to new
- Q12 Prevention of network induced duplicates - enable.idempotence=true
- Q13 Condition where messages with same key do not end to the same partition - number of partitions has been changed
- Q14 Producer callback
- Q15 use of null as key, in which partition message will be written? will be stored with round-robin strategy among partitions
- Q16 Return Type of send() method
- Q17 Quiz, given replication factor and min.insync.replicas how many brokers can go down before producer with acks=all can't produce?
- Q18 Synchronous producer send, effect on throughput
- Q19 Exception when acks=all and not all replicas are available  (NotEnoughReplicasException)
- Q20 Custom Partitioner - Use case send specific key values to specific partitions
- Q21 Compression - Not supported by the brokers automatically, must be implemented on producers and respective consumers
- Q22 Producer - Exceptions that may be due to errors before sending to the broker
- Q23 Producer - what must be supplied as bootstrap.server properties
- Q24  Quiz, given replication factor 3  and min.insync.replicas 2 how many brokers can go down before producer with acks=1 can't produce?
- Q25 What happens when messsage exceeds message limit - MessageSizeTooLarge is thrown which is not a retryable exception


### Missed Questions
 - 1 WIMM
 - 6
 - 8
 - 16 WIMM
 - 17
 - 21 
 - 22
 - 24

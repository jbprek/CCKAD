# Streams Notes

## Concepts
### Topology
Definition: Topology is a graph of processors chained together by streams.

Components
- streams
- processors
  - Source processor (Input can have multiple)
  - Sink processor 

### KStream
- all **inserts**
- similar to a log
- infinite
- unbounded
Note: Stream def is a sequence of immutable data records, that's fully ordered and can be replayed.

#### KStream Usage:
- Reading from a non compacted topic
- Partial Information transactional
- 
### KTable
- all **upserts**
- deletes on null values
- similar to a table
- parallel with log compacted topics

#### KTable Usage:
- Reading from a log compacted topic (aggregates)
- DB like structure is needed, every update is self-sufficient

### Stateless vs Stateful operations
- **Stateless** when the result of the operation depends on the actual data-point
- **Stateful** when the result of the operation depends on external information (the state)

### Simple operations

#### map & mapValues
##### map 
- only affecting values
  - => does not change keys
  - => does not trigger a repartition
- for KStream and KTable
##### mapValues
- affects both key & values
- Triggers a repartition
- for KStream only

example:
````java
uppercased = stream.mapValues(value -> value.toUpperCase());
````
#### filter & filterNot
##### filter
- does not change keys/values
    - => does not trigger a repartition
- for KStream and KTable
##### filterNot
- inverse of filter

example:
````java
KStream<String,Long> onlyPositives = stream.filter((key,value)-> value > 0);
````
 
 

# Questions Zookeeper


## Question 1 (1-5)
What information is NOT stored inside of Zookeeper? (select two)

1. Consumer offset
2. Controller registration 
3. Broker Registration info
4. ACL information
5. Schema Registry schemas


## Question 2 (2-19)
You have a Zookeeper cluster that needs to be able to withstand the loss of 2 servers and still be able to function. What size should your Zookeeper cluster have?

1. 6
2. 5
3. 4
4. 2
5. 3

Explanation

Your Zookeeper cluster needs to have an odd number of servers, and must maintain a majority of servers up to be able to vote. Therefore, a 2N+1 zookeeper cluster can survive to N zookeeper being down, so here the right answer is N=2, 2*N+1=5


## Question 3 (2-37)
A Zookeeper ensemble contains 5 servers. What is the maximum number of servers that can go missing and the ensemble still run?

1. 3
2. 1
3. 2
4. 4

## Question 4 (2-18)
A Zookeeper configuration has tickTime of 2000, initLimit of 20 and syncLimit of 5. What's the timeout value for followers to connect to Zookeeper?

1. 40s
2. 10s
3. 2000ms
4. 20s


# Answers Zookeeper
## Question 1 (1-5)
What information is NOT stored inside of Zookeeper? (select two)

- (1.) Consumer offset
- (5.) Schema Registry schemas


## Question 2 (2-19)
You have a Zookeeper cluster that needs to be able to withstand the loss of 2 servers and still be able to function. What size should your Zookeeper cluster have?

- (2.) 5

Explanation

Your Zookeeper cluster needs to have an odd number of servers, and must maintain a majority of servers up to be able to vote. Therefore, a 2N+1 zookeeper cluster can survive to N zookeeper being down, so here the right answer is N=2, 2*N+1=5

## Question 3 (2-37)
A Zookeeper ensemble contains 5 servers. What is the maximum number of servers that can go missing and the ensemble still run?

- (3.) 2

Explanation

majority consists of 3 zk nodes for 5 nodes zk cluster, so 2 can fail


## Question 4 (2-18)
A Zookeeper configuration has tickTime of 2000, initLimit of 20 and syncLimit of 5. What's the timeout value for followers to connect to Zookeeper?

- (1.) 40s

Explanation

tick time is 2000 ms, and initLimit is the config taken into account when establishing a connection to Zookeeper, so the answer is 2000 * 20 = 40000 ms = 40s
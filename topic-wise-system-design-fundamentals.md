# Distributed Systems for Applied Scientists / AI-ML Engineers

## Topic 1: Horizontal Scaling vs Vertical Scaling

This is one of the most fundamental concepts in ML System Design interviews.

---

# What Is Vertical Scaling?

Vertical scaling means increasing resources of an existing machine.

Example:

```text
Before
------
8 CPU
32 GB RAM

After
-----
64 CPU
512 GB RAM
```

You are making the machine bigger.

Also called:

```text
Scale Up
```

---

## Real Production Example

Suppose you have:

```text
Fraud Detection API
```

Current traffic:

```text
100 requests/sec
```

CPU utilization:

```text
90%
```

Instead of redesigning architecture, you move from:

```text
16 CPU
```

to

```text
64 CPU
```

Machine.

Problem solved.

---

# What Is Horizontal Scaling?

Adding more machines.

```text
Server 1
Server 2
Server 3
Server 4
Server 5
```

Traffic distributed among them.

Also called:

```text
Scale Out
```

---

## Real Production Example

ChatGPT-like service:

```text
1000 QPS
```

becomes

```text
100,000 QPS
```

One machine cannot serve traffic.

Solution:

```text
Load Balancer
      |
------------------
|   |   |   |   |
S1  S2  S3  S4  S5
```

---

# Applied Scientist Perspective

Interviewers care because:

Your model may be amazing.

But if:

```text
Model Accuracy = 99%
```

and

```text
System crashes at 1000 QPS
```

the model is useless.

You must understand:

```text
Can my inference system scale?
```

---

# What To Discuss In Interviews

A senior candidate should discuss:

### Traffic

Current QPS

Peak QPS

Future QPS

Example:

```text
Current: 5K QPS
Peak: 50K QPS
Future: 500K QPS
```

---

### Latency

```text
P50
P95
P99
```

Example:

```text
P95 < 100 ms
```

---

### Availability

```text
99.9%
99.99%
99.999%
```

---

### Cost

```text
Scale Up Cost
vs
Scale Out Cost
```

---

### Failure

What happens if one node dies?

---

# Production Scale Discussion

Suppose:

Amazon Product Recommendation Service

Traffic:

```text
50 Million Users
```

Peak:

```text
1 Million Requests/sec
```

Vertical scaling impossible.

Need:

```text
Thousands of Servers
```

Horizontal scaling mandatory.

---

# Questions Interviewer May Ask

## Q1

Why not always vertically scale?

### Answer

Because:

1. Hardware limits exist.
2. Cost grows exponentially.
3. Single point of failure.
4. No redundancy.

Example:

```text
512 CPU server dies
=
Entire service down
```

---

## Q2

Why is horizontal scaling harder?

### Answer

Need:

* Load balancing
* Distributed cache
* Replication
* Service discovery
* Monitoring

Distributed systems complexity increases.

---

## Q3

How would you scale an LLM inference service?

### Answer

Use:

* Multiple inference servers
* Load balancer
* Request batching
* GPU autoscaling
* Cache frequent prompts

---

---

# Topic 2: Stateless vs Stateful Services

Extremely common in ML system design interviews.

---

# What Is Stateless Service?

Server stores no user state.

Every request contains everything needed.

Example:

```http
GET /recommendation?user=123
```

Server computes response.

Nothing stored locally.

---

## Production Example

Recommendation API

```text
User Request
     |
API Server
     |
Feature Store
     |
Model
```

API node stores nothing.

Any node can process request.

---

# Benefits

Easy scaling.

```text
Add More Servers
```

No data migration.

No synchronization.

---

# What Is Stateful Service?

Server remembers information.

Example:

```text
Shopping Cart
```

User cart stored on server.

---

# Example

User session stored on node:

```text
Node A
```

If request goes to:

```text
Node B
```

Session lost.

---

# Production Example

Feature Store

Stores:

```text
User Embeddings
Feature Vectors
Historical Features
```

This is state.

---

# Applied Scientist Perspective

Many ML systems contain both:

### Stateless

```text
Inference API
Ranking API
Feature Retrieval API
```

### Stateful

```text
Feature Store
Vector Database
Model Registry
```

---

# Interview Discussion Points

Discuss:

### Scaling

Stateless:

```text
Easy
```

Stateful:

```text
Hard
```

---

### Failure Recovery

Stateless:

```text
Restart node
Done
```

Stateful:

Need:

```text
Replication
Backups
Recovery
```

---

### Data Consistency

Important for:

```text
Feature Stores
User Profiles
Embeddings
```

---

# Questions

## Q1

Why are inference services usually stateless?

### Answer

Because:

* Easier scaling
* Easier deployment
* Easier failover

Model weights loaded locally.

User state stored elsewhere.

---

## Q2

Can an LLM service be stateful?

### Answer

Yes.

Conversation history creates state.

Usually stored in:

```text
Redis
Vector DB
Database
```

not inside inference server.

---

---

# Topic 3: CAP Theorem

Almost guaranteed in senior interviews.

---

# What Is CAP?

Distributed systems cannot simultaneously guarantee:

### C

Consistency

### A

Availability

### P

Partition Tolerance

---

# Network Partition

Suppose:

```text
US Region
```

and

```text
Europe Region
```

cannot communicate.

Partition occurred.

---

# CAP States

## CP

Consistency + Partition Tolerance

Sacrifice Availability.

Example:

```text
ZooKeeper
etcd
```

---

## AP

Availability + Partition Tolerance

Sacrifice Consistency.

Example:

```text
Cassandra
DynamoDB (eventual mode)
```

---

## CA

Impossible in distributed systems.

Because partitions eventually happen.

---

# Applied Scientist Example

Feature Store

User feature:

```text
Credit Score = 700
```

One region:

```text
700
```

Another:

```text
650
```

Which one should model use?

CAP becomes important.

---

# Production Discussion

Recommendation systems:

Often AP.

Slight stale data acceptable.

---

Fraud Detection:

Often CP.

Wrong data can cost money.

---

# Interview Questions

## Q1

Why is CA impossible?

### Answer

Network partitions always possible.

Therefore distributed systems must choose between:

```text
Consistency
Availability
```

during partition.

---

## Q2

Would you choose CP or AP for recommendation system?

### Answer

Usually AP.

Serving recommendations is better than failing requests.

Minor inconsistency acceptable.

---

## Q3

Would you choose CP or AP for payment processing?

### Answer

CP.

Incorrect balance is worse than temporary unavailability.

---

# Topic 4: Consistency Models

---

# Strong Consistency

After write:

```text
X=10
```

every read returns:

```text
10
```

immediately.

---

## Example

Bank account.

Balance:

```text
1000
```

Withdraw:

```text
100
```

Every user sees:

```text
900
```

instantly.

---

# Eventual Consistency

Update propagates later.

Temporary stale reads allowed.

---

## Example

Amazon Product Reviews

You post review.

Friend may not see it immediately.

After few seconds:

Visible.

---

# Causal Consistency

Cause-effect ordering preserved.

---

## Example

Chat Application

Message:

```text
Hello
```

Then:

```text
How are you?
```

Second message cannot appear first.

---

# Applied Scientist Perspective

Feature stores frequently use:

```text
Eventual Consistency
```

because:

```text
Latency < Strong Consistency
```

---

# Interview Questions

## Q1

Why not use strong consistency everywhere?

### Answer

Because:

* Higher latency
* Reduced availability
* Expensive coordination

---

## Q2

What consistency would you choose for real-time fraud detection?

### Answer

Strong consistency.

Incorrect feature values can produce wrong decisions.

---

## Q3

What consistency would you choose for recommendation systems?

### Answer

Eventual consistency.

Small staleness is acceptable.

Latency and availability matter more.

---

This covers the **first four foundational topics**. The next major topics are:

5. Availability
6. Fault Tolerance
7. High Availability
8. Reliability
9. Durability
10. Leader-Follower Replication
11. Multi-Leader Replication
12. Quorum Reads/Writes
13. Distributed Transactions
14. 2PC
15. Saga Pattern
16. Raft
17. Paxos
18. Load Balancing
19. Auto Scaling
20. Elasticity
21. Distributed Caching
22. Sharding
23. Partitioning

These are the topics where most senior ML System Design interviews spend the majority of their time, especially around feature stores, RAG systems, vector databases, Kafka, and LLM inference platforms.

# Topic 5: Availability

One of the most misunderstood concepts in interviews.

---

# What is Availability?

Availability measures whether the system is able to serve requests when users need it.

Formula:

```text
Availability =
Successful Requests
-------------------
Total Requests
```

Example:

```text
1000 requests
999 succeeded

Availability = 99.9%
```

---

# Production Example

Imagine an LLM chatbot.

User asks:

```text
"What is the weather?"
```

System responds.

Service is available.

If service returns:

```text
503 Service Unavailable
```

Service is unavailable.

---

# Availability Targets

| Availability | Downtime / Year |
| ------------ | --------------- |
| 99%          | 3.65 days       |
| 99.9%        | 8.76 hours      |
| 99.99%       | 52.56 mins      |
| 99.999%      | 5.26 mins       |

Interviewers love asking this.

---

# Applied Scientist Perspective

Suppose:

```text
Fraud Detection Model
```

Accuracy:

```text
99%
```

Availability:

```text
90%
```

Then 10% of transactions are not protected.

Business impact huge.

---

# Production Scale Discussion

Amazon Search

Traffic:

```text
Millions/sec
```

Even:

```text
99.9%
```

availability means thousands of failed requests.

Thus systems target:

```text
99.99%
or
99.999%
```

---

# What To Discuss In Interviews

### SLA

Service Level Agreement

Example:

```text
99.99%
```

---

### SLO

Service Level Objective

Example:

```text
P95 Latency < 100ms
```

---

### Error Budget

Allowed failures.

Example:

```text
0.01%
```

downtime permitted.

---

### Dependency Analysis

System may depend on:

```text
Database
Cache
Feature Store
Kafka
Vector DB
```

Availability is only as good as weakest dependency.

---

# Interview Question

## Q1

How can you improve availability?

### Answer

* Multi-region deployment
* Replication
* Load balancing
* Auto-scaling
* Graceful degradation
* Circuit breakers

---

## Q2

Can strong consistency reduce availability?

### Answer

Yes.

CAP theorem.

During partition:

```text
Strong Consistency
```

may reject requests.

Availability decreases.

---

# Senior-Level Discussion

Mention:

```text
Availability != Reliability
```

System may be available but serving wrong results.

Interviewers love this distinction.

---

# Topic 6: Fault Tolerance

---

# What Is Fault Tolerance?

Ability to continue operating despite failures.

---

# Example

Suppose:

```text
10 Inference Servers
```

One crashes.

Users continue getting predictions.

System is fault tolerant.

---

# Production Example

ChatGPT Inference Cluster

```text
1000 GPUs
```

If:

```text
5 GPUs fail
```

System continues serving.

---

# Applied Scientist Example

Real-time Recommendation System

Components:

```text
Feature Store
Ranking Model
Cache
Database
```

If cache fails:

System falls back to database.

Fault tolerance achieved.

---

# What To Discuss

### Single Point of Failure

Identify:

```text
Database
Leader Node
Feature Store
```

---

### Redundancy

```text
Replica Nodes
Backup Systems
```

---

### Failover

Automatic switching.

---

### Graceful Degradation

Example:

```text
Personalized Recommendations unavailable

Fallback:
Popular Products
```

System still works.

---

# Interview Question

## Q1

How would you design a fault-tolerant recommendation service?

### Answer

Use:

* Replicated feature stores
* Multiple inference nodes
* Cache fallback
* Retry mechanisms
* Circuit breakers

---

## Q2

How is fault tolerance different from availability?

### Answer

Fault tolerance is a mechanism.

Availability is an outcome.

Fault tolerance helps achieve availability.

---

# Topic 7: High Availability (HA)

---

# What Is HA?

System remains available even when components fail.

Typically achieved through redundancy.

---

# Production Example

```text
Region A
Region B
Region C
```

If Region A fails:

Traffic routed to B and C.

Users unaffected.

---

# ML Example

Feature Store Cluster

```text
Primary
Replica1
Replica2
```

Primary fails.

Replica promoted.

Service continues.

---

# What To Discuss

### Active-Active

```text
Region A
Region B
```

both serving traffic.

---

### Active-Passive

```text
Primary
Standby
```

Standby activated upon failure.

---

### Failover Time

Discuss:

```text
RTO
```

Recovery Time Objective.

---

### Data Loss

Discuss:

```text
RPO
```

Recovery Point Objective.

---

# Interview Question

## Q1

How would you design a highly available vector database?

### Answer

* Multi-node cluster
* Replication
* Automatic leader election
* Load balancing
* Multi-region deployment

---

# Topic 8: Reliability

---

# What Is Reliability?

System consistently behaves correctly.

---

# Example

Suppose:

```text
Recommendation API
```

Available:

```text
100%
```

But returning:

```text
Random Recommendations
```

System is available.

Not reliable.

---

# Reliability Means

Correctness.

Consistency.

Predictability.

---

# Applied Scientist Example

Model:

```text
99% Accuracy
```

Yesterday.

Today:

```text
65%
```

due to feature drift.

System became unreliable.

---

# Production Considerations

Discuss:

### Data Quality

### Feature Drift

### Model Drift

### Dependency Reliability

### Retry Policies

### Monitoring

---

# Interview Question

## Q1

How do you improve reliability in ML systems?

### Answer

* Data validation
* Feature monitoring
* Drift detection
* Canary deployments
* Rollbacks
* Automated testing

---

# Topic 9: Durability

---

# What Is Durability?

Once data is acknowledged as written,

it should never be lost.

---

# Example

Bank Transfer

```text
₹10000 transferred
```

Response:

```text
Success
```

Power failure occurs.

Transfer should still exist.

---

# ML Example

Training Job

```text
10 days training
```

Checkpoint saved.

Node crashes.

Checkpoint survives.

Durability.

---

# Production Mechanisms

### Write-Ahead Log (WAL)

PostgreSQL

Kafka

---

### Replication

Multiple copies.

---

### Distributed Storage

S3

HDFS

Azure Blob

---

# Interview Question

## Q1

Difference between durability and availability?

### Answer

Availability:

```text
Can I access data now?
```

Durability:

```text
Will data survive forever?
```

---

# Topic 10: Leader-Follower Replication

One of the most frequently asked distributed systems concepts.

---

# What Is It?

One node:

```text
Leader
```

Handles writes.

Followers replicate data.

```text
       Leader
      /   |   \
Follower Follower Follower
```

---

# Example

PostgreSQL

MySQL

MongoDB Replica Set

---

# Write Flow

```text
Client
  |
Leader
  |
Followers
```

Writes only to leader.

---

# Read Flow

Reads can come from:

```text
Leader
Followers
```

---

# Applied Scientist Example

Feature Store

User feature update:

```text
Age = 30
```

Write:

Leader

Read:

Followers

---

# Advantages

### Simplicity

### Strong Consistency

### Read Scaling

---

# Problems

### Leader Bottleneck

All writes go through leader.

---

### Replication Lag

Followers may be stale.

---

### Leader Failure

Need failover.

---

# Production Discussion

Amazon-scale:

```text
Millions of reads
Thousands of writes
```

Leader-follower ideal.

Read traffic distributed.

---

# Interview Question

## Q1

Why use leader-follower?

### Answer

Because:

* Simpler consistency
* Easier implementation
* Scales reads effectively

---

## Q2

What happens if leader crashes?

### Answer

Replica promoted.

New leader elected.

---

## Q3

Would you use leader-follower for feature store?

### Answer

Usually yes.

Read traffic dominates.

Strong consistency often required.

---

# Senior-Level Interview Points

For every topic above proactively discuss:

### Scale

```text
QPS
TPS
Data Volume
```

---

### Latency

```text
P50
P95
P99
```

---

### Failure Modes

```text
Node Failure
Network Failure
Region Failure
```

---

### Recovery

```text
RTO
RPO
```

---

### Cost

```text
Storage
Network
Compute
```

---

### Monitoring

```text
Availability
Latency
Error Rate
Replication Lag
```

---

### ML Impact

Always relate back to:

* Feature Store
* Model Registry
* Vector DB
* RAG Pipeline
* LLM Serving
* Recommendation Engine
* Fraud Detection

That is what differentiates a senior Applied Scientist from a generic distributed-systems engineer.

The next set (Topics 11–17) covers the most heavily tested senior interview material:

* Multi-Leader Replication
* Quorum Reads/Writes
* Distributed Transactions
* Two-Phase Commit (2PC)
* Saga Pattern
* Raft
* Paxos

These are especially important for large-scale ML platforms, feature stores, Kafka-based architectures, and multi-region AI systems.


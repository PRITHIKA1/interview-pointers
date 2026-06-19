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

---

This is where interviews start moving into **“real distributed systems design thinking”** (the part Amazon / Google / JPM love).

---

# Topic 11: Multi-Leader Replication

---

## What is it?

Multiple nodes can accept writes.

```text id="m1"
US Leader  <---->  EU Leader  <---->  APAC Leader
```

Each region can write independently.

---

## Example (Production)

Global ML product catalog:

* US users update product price
* EU users update discount
* India users update inventory sync

All regions accept writes locally.

---

## Why it exists?

Because:

* Low latency writes
* Multi-region availability
* No dependency on single leader region

---

## Interview Discussion Points

### 1. Latency Optimization

Write locally instead of cross-region.

```text id="m2"
India user → India DB (fast)
```

---

### 2. Availability

If US region fails:

EU + APAC still write.

---

### 3. Conflict Problem (MOST IMPORTANT)

Two writes happen:

```text id="m3"
US: price = 100
EU: price = 90
```

Now what?

---

### 4. Conflict Resolution Strategies

Discuss:

* Last Write Wins (LWW)
* Version vectors
* Timestamp ordering
* Domain-based resolution

---

### 5. ML System Angle

Feature stores:

* Different regions updating same feature
* Risk of inconsistent embeddings

---

## When to choose?

Use when:

* Global users
* Low latency writes required
* Eventual consistency acceptable

Avoid when:

* Strong correctness needed (banking)

---

## Interview Question

### Q: Why not use multi-leader everywhere?

**Answer:**

Because:

* Conflict resolution complexity
* Hard debugging
* Eventual consistency issues
* Data divergence risk

---

---

# Topic 12: Quorum Reads/Writes

---

## What is it?

System requires majority agreement.

```text id="q1"
N = 5 replicas
W = 3 writes
R = 3 reads
```

Rule:

```text id="q2"
R + W > N
```

---

## Example

Distributed feature store:

* 5 replicas store embeddings
* Write to 3 nodes
* Read from 3 nodes

Ensures overlap → consistency

---

## Interview Discussion Points

### 1. Consistency Guarantee

At least one overlapping node ensures latest data.

---

### 2. Tradeoff

Higher consistency → higher latency

---

### 3. Failure tolerance

Can tolerate:

```text id="q3"
N - W failures for writes
N - R failures for reads
```

---

### 4. ML System Relevance

Used in:

* DynamoDB
* Cassandra
* Feature stores

---

## When to choose?

Use when:

* Need balance of consistency + availability
* Distributed key-value store needed

---

## Interview Question

### Q: Why not always use quorum?

**Answer:**

Because:

* Higher latency
* More network calls
* Reduced throughput

---

---

# Topic 13: Distributed Transactions

---

## What is it?

A transaction spanning multiple services.

```text id="t1"
Order Service
Payment Service
Inventory Service
```

All must succeed or fail together.

---

## Example

E-commerce checkout:

1. Deduct inventory
2. Charge payment
3. Create order

---

## Interview Discussion Points

### 1. Failure scenario

```text id="t2"
Payment success
Inventory failure
```

System inconsistency

---

### 2. Need for atomicity

Either:

* All succeed
* Or all rollback

---

### 3. Challenges

* Network failures
* Partial commits
* Latency overhead

---

## ML System Angle

Used in:

* Feature updates
* Training pipelines
* Multi-store writes (DB + vector DB + cache)

---

## Interview Question

### Q: Why are distributed transactions hard?

**Answer:**

Because:

* Partial failure is common
* Network is unreliable
* Coordination cost is high
* Locking reduces scalability

---

---

# Topic 14: Two Phase Commit (2PC)

---

## What is it?

A coordinator ensures all participants agree.

### Phase 1: Prepare

```text id="p1"
Coordinator → All services: "Can you commit?"
```

### Phase 2: Commit

If all agree:

```text id="p2"
Commit everywhere
```

Else:

```text id="p3"
Rollback everywhere
```

---

## Production Example

Bank transfer across systems.

---

## Interview Discussion Points

### 1. Blocking problem

If coordinator fails:

```text id="p4"
System stuck waiting
```

---

### 2. Performance issue

Too many round trips:

* High latency
* Low throughput

---

### 3. Scalability issue

More participants → worse performance

---

## ML System Angle

Rarely used in large-scale ML systems because:

* Too slow for real-time inference pipelines

---

## Interview Question

### Q: Why is 2PC not used in large ML systems?

**Answer:**

Because:

* Blocking behavior
* High latency
* Poor scalability
* Failure sensitivity

---

---

# Topic 15: Saga Pattern

---

## What is it?

Instead of global transaction:

Break into local steps + compensation.

---

## Example

Order flow:

```text id="s1"
Create Order
Reserve Inventory
Process Payment
Ship Product
```

---

## If failure happens:

```text id="s2"
Payment fails
```

Compensation:

```text id="s3"
Cancel Inventory Reservation
Delete Order
```

---

## Interview Discussion Points

### 1. Eventual consistency model

System is temporarily inconsistent.

---

### 2. Compensation logic complexity

Must define rollback actions.

---

### 3. Retry handling

Network failures may duplicate events.

Need idempotency.

---

## ML System Angle

Used in:

* Feature pipeline updates
* ETL workflows
* Training orchestration systems

---

## Interview Question

### Q: Saga vs 2PC?

**Answer:**

| 2PC                | Saga                 |
| ------------------ | -------------------- |
| Strong consistency | Eventual consistency |
| Blocking           | Non-blocking         |
| Low scalability    | High scalability     |

---

---

# Topic 16: Raft

---

## What is it?

Consensus algorithm used to maintain replicated logs.

---

## Example

Distributed feature store leader election.

---

## Core Idea

One leader coordinates all writes.

---

## Interview Discussion Points

### 1. Leader election

If leader fails → new leader chosen.

---

### 2. Log replication

All followers replicate leader log.

---

### 3. Majority rule

```text id="r1"
Majority = N/2 + 1
```

---

### 4. Safety guarantee

No conflicting states accepted.

---

## ML System Angle

Used in:

* Metadata services
* Feature store coordination
* Model registry consistency

---

## Interview Question

### Q: Why Raft instead of Paxos?

**Answer:**

Because:

* Easier to understand
* Easier to implement
* Same guarantees

---

---

# Topic 17: Paxos

---

## What is it?

Older consensus algorithm ensuring agreement in distributed systems.

---

## Interview Discussion Points

### 1. Extremely complex

Most engineers avoid full implementation.

---

### 2. Conceptual understanding

Key idea:

* Proposers
* Acceptors
* Learners

---

### 3. Used in theory-heavy systems

---

## ML System Angle

Rare in application layer.

More relevant in:

* Infrastructure systems
* Distributed coordination systems

---

## Interview Question

### Q: Do you need to know Paxos deeply?

**Answer:**

No.

But you must:

* Understand consensus problem
* Understand why Raft is preferred

---

---

# Senior-Level Summary (VERY IMPORTANT)

At this stage, interviewers expect you to naturally bring:

## 1. Consistency vs Availability tradeoff

## 2. Failure scenarios

## 3. Distributed coordination cost

## 4. Latency impact of replication

## 5. Real ML system mapping:

* Feature Stores
* Vector DBs
* RAG pipelines
* LLM inference clusters
* Kafka pipelines

---

# Next Set (Very Important)

Next topics are HIGHLY asked in senior ML system design:

## 18. Load Balancing

## 19. Auto Scaling

## 20. Elasticity

## 21. Distributed Caching

## 22. Sharding

## 23. Partitioning

These directly map to:

* LLM serving systems
* Recommendation systems
* Real-time ranking pipelines
* Feature store design
* Vector database design

---

# Topic 18: Load Balancing (Senior Applied Scientist / ML System Design Interview Perspective)

This is one of the most important concepts because **almost every production ML system sits behind a load balancer**.

Examples:

* ChatGPT
* Amazon Recommendation Service
* Netflix Ranking Service
* Fraud Detection APIs
* RAG Systems
* Feature Stores
* Vector Databases

---

# 1. What Is Load Balancing?

Load balancing is the process of distributing requests across multiple servers so that no single server becomes overloaded.

Without load balancing:

```text
                100K Requests/sec
                       |
                       V
                  Server-1
```

Server crashes.

---

With load balancing:

```text
                100K Requests/sec
                       |
                 Load Balancer
               /      |      \
              /       |       \
            S1       S2       S3
```

Traffic distributed.

---

# Interview Definition

A senior-level answer:

> Load balancing is the process of intelligently distributing traffic across multiple service instances to improve scalability, availability, fault tolerance, and resource utilization.

Notice:

We don't simply say:

> "It distributes traffic."

That sounds junior.

---

# Why Do We Need It?

Suppose:

```text
Inference latency = 50ms
Single server capacity = 500 QPS
```

Traffic becomes:

```text
50,000 QPS
```

Impossible for one machine.

Need:

```text
100 servers
```

Load balancer distributes traffic.

---

# Real ML Example

Recommendation Service

```text
User
 |
API Gateway
 |
Load Balancer
 |
---------------------------------
|       |       |       |       |
R1      R2      R3      R4      R5
```

Each recommendation server:

```text
Loads model
Loads embeddings
Serves predictions
```

---

# Interview Discussion Point #1

## What Are We Balancing?

Most candidates say:

```text
Requests
```

Senior candidates discuss:

### CPU

```text
CPU utilization
```

---

### Memory

```text
Embedding cache
```

---

### Network

```text
Bandwidth
```

---

### GPU

For LLM systems:

```text
GPU utilization
```

---

### Active Connections

For streaming systems.

---

# Interview Discussion Point #2

## Load Balancing Algorithms

Interviewers love this.

---

# Round Robin

Simple.

```text
Req1 → S1
Req2 → S2
Req3 → S3
Req4 → S1
```

---

## Advantages

Simple.

Fast.

---

## Problems

Assumes all servers equal.

Not true in production.

---

# Interview Question

Would Round Robin work for LLM serving?

Answer:

Usually not.

Reason:

```text
Prompt lengths vary
GPU loads vary
Inference times vary
```

One request:

```text
50 tokens
```

Another:

```text
10,000 tokens
```

Round robin becomes inefficient.

---

# Least Connections

Request sent to server with fewest active connections.

```text
S1 = 100 connections
S2 = 50 connections

Choose S2
```

---

## Where Used

Streaming

WebSockets

SignalR systems

---

# Least Response Time

Choose fastest node.

---

Useful for:

```text
Inference APIs
Recommendation APIs
```

---

# Weighted Round Robin

Suppose:

```text
S1 = 64 CPU
S2 = 32 CPU
S3 = 16 CPU
```

Weights:

```text
S1 = 4
S2 = 2
S3 = 1
```

Traffic proportional.

---

# Production Interview Discussion

Most real systems use:

```text
Weighted routing
```

not pure round robin.

---

# Consistent Hashing

Very important.

---

Used when:

```text
Request must hit same server
```

Example:

```text
User Embedding Cache
```

---

Without hashing:

```text
User-123
```

may go anywhere.

Cache misses.

---

With hashing:

```text
hash(User-123)
```

always goes to same node.

---

Used heavily in:

* Redis clusters
* Feature stores
* Distributed caches
* Vector DBs

---

# Interview Question

Why does consistent hashing scale better?

Answer:

Adding one server only remaps a small fraction of keys.

Normal hashing remaps almost everything.

---

# Interview Discussion Point #3

## Load Balancer Layers

---

# Layer 4

Operates at:

```text
TCP
UDP
```

Level.

Fast.

No HTTP understanding.

---

Example:

```text
AWS NLB
```

---

# Layer 7

Operates at:

```text
HTTP
HTTPS
```

Level.

---

Can route based on:

```text
URL
Headers
Cookies
```

---

Example:

```text
AWS ALB
NGINX
Envoy
```

---

Interview Question

When would you choose Layer 4?

Answer:

Ultra-low latency.

High throughput.

No application-aware routing needed.

---

# Interview Discussion Point #4

## Health Checks

Production systems continuously verify:

```text
Server healthy?
```

---

Example:

```http
GET /health
```

---

Server responds:

```json
{
 "status":"UP"
}
```

---

If unhealthy:

```text
Removed from rotation
```

---

Interview Question

What happens if health checks don't exist?

Answer:

Traffic continues to dead servers.

Availability drops.

---

# Interview Discussion Point #5

## Load Balancer as SPOF

Most candidates miss this.

Interviewer asks:

```text
Can LB fail?
```

Answer:

Yes.

---

Need:

```text
LB1
LB2
LB3
```

or cloud-managed LB.

---

Production systems eliminate:

```text
Single Point of Failure
```

---

# Interview Discussion Point #6

## Geographic Load Balancing

Very common in LLM systems.

---

User:

```text
India
```

Should not hit:

```text
US-East
```

if:

```text
Mumbai region available
```

---

Route to nearest region.

---

Benefits:

### Lower Latency

### Lower Cost

### Better User Experience

---

# Interview Question

User in India sees 2-second latency.

How can you reduce it?

Answer:

* Regional deployment
* Geo-routing
* CDN
* Edge caching

---

# Interview Discussion Point #7

## Load Balancing for LLM Systems

Very important.

---

Traditional API:

```text
Request cost ≈ constant
```

---

LLM Request:

```text
Cost varies massively
```

---

Prompt:

```text
Hello
```

vs

```text
100-page PDF
```

---

Huge difference.

---

Therefore LLM serving uses:

### Dynamic Routing

### GPU-aware Scheduling

### Queue Length Routing

### Token-aware Routing

---

# Senior-Level Discussion

Say:

> For LLM inference, I wouldn't use pure round robin. I would route requests based on GPU utilization, queue length, and estimated token count because request costs are highly variable.

Interviewers love this answer.

---

# Interview Discussion Point #8

## Load Balancing + Auto Scaling

Load balancer works with autoscaling.

---

Suppose:

```text
10 Servers
```

Traffic spikes.

Autoscaler creates:

```text
20 Servers
```

Load balancer starts routing traffic.

---

Without LB:

new servers useless.

---

# Interview Discussion Point #9

## Metrics

Always discuss metrics.

---

### QPS

```text
Requests/sec
```

---

### Active Connections

---

### CPU

---

### Memory

---

### P95 Latency

---

### P99 Latency

---

### Error Rate

---

### Queue Length

Important for LLM serving.

---

# ML System Examples

---

## Feature Store

Load balance:

```text
Feature Retrieval APIs
```

---

## Recommendation System

Load balance:

```text
Ranking Servers
```

---

## Fraud Detection

Load balance:

```text
Prediction Services
```

---

## Vector Database

Load balance:

```text
Embedding Search Requests
```

---

## RAG System

Load balance:

```text
Retriever Nodes
Generator Nodes
```

---

# Most Common Interview Questions

---

## Q1

What algorithm would you use for LLM serving?

### Senior Answer

Queue-length based routing + GPU utilization aware routing.

Reason:

Request cost highly variable.

---

## Q2

What happens if one server becomes slow but doesn't fail?

### Answer

Health checks may pass.

Need:

```text
Latency-aware routing
```

to avoid sending traffic.

---

## Q3

How do you avoid cache misses in distributed systems?

### Answer

Consistent hashing.

---

## Q4

Can load balancing improve availability?

### Answer

Yes.

Traffic automatically routed away from failed nodes.

---

## Q5

How would you load balance a recommendation system serving 1M QPS?

### Answer

* Multi-layer load balancing
* Regional routing
* Consistent hashing for caches
* Autoscaling
* CDN
* Health checks
* Weighted routing

---

# What Separates a Senior Applied Scientist?

A junior candidate says:

> Load balancer distributes traffic.

A senior candidate says:

> I would choose a routing strategy based on workload characteristics. For recommendation APIs, least-response-time routing may work. For LLM inference, I'd consider token-aware routing and GPU utilization. I'd also discuss health checks, failover, regional routing, autoscaling integration, cache locality, and latency metrics such as P95/P99.

That answer immediately signals production-scale system design experience.

---

# Topic 19: Auto Scaling

# Topic 20: Elasticity

These are among the most frequently asked concepts in:

* Amazon Applied Scientist
* Google ML Engineer
* Meta ML System Design
* JPM AI Engineer
* Uber ML Platform
* Netflix ML Infrastructure

For senior roles, interviewers are not checking whether you know Kubernetes HPA.

They want to know:

> How do you design a system that survives traffic spikes, GPU shortages, Black Friday events, model launches, and viral growth?

---

# Topic 19: Auto Scaling

---

# What Is Auto Scaling?

Auto Scaling means:

> Automatically adding or removing resources based on workload.

Without Auto Scaling:

```text
Traffic = 10K QPS

Servers = 10
```

Traffic suddenly becomes:

```text
100K QPS
```

System crashes.

---

With Auto Scaling:

```text
Traffic ↑

Servers ↑
```

System survives.

---

# Interview Definition

A senior answer:

> Auto scaling is the automatic adjustment of compute resources based on demand, utilization metrics, or service-level objectives to maintain performance while optimizing cost.

Notice:

Performance + Cost

Both matter.

---

# Why Does It Exist?

Traffic is not constant.

Example:

Amazon

```text
Normal Day:
100K QPS

Prime Day:
10 Million QPS
```

---

ChatGPT

```text
Normal:
50K QPS

New GPT Release:
500K QPS
```

---

Fraud Detection

```text
Night:
5K TPS

Day:
100K TPS
```

---

Static capacity becomes wasteful.

---

# Applied Scientist Perspective

Suppose:

Recommendation model latency:

```text
40 ms
```

Goal:

```text
P95 < 100 ms
```

Traffic spikes.

Latency becomes:

```text
300 ms
```

Auto scaling adds servers.

Latency restored.

---

# Production Architecture

```text
Users
   |
Load Balancer
   |
Inference Cluster
   |
Autoscaler
```

Autoscaler continuously monitors:

* CPU
* Memory
* Latency
* Queue length

---

# Interview Discussion Point #1

## Scaling Metrics

Most candidates say:

```text
CPU > 80%
```

Scale up.

That's a junior answer.

---

A senior answer discusses:

### CPU

Good for:

```text
Stateless APIs
```

---

### Memory

Good for:

```text
Embedding systems
```

---

### Request Rate

```text
QPS
TPS
```

---

### Latency

```text
P95
P99
```

---

### Queue Length

Very important for AI systems.

---

### GPU Utilization

Critical for LLM serving.

---

# Interview Question

What metric would you use for LLM autoscaling?

---

Senior Answer:

Not CPU.

Use:

```text
GPU Utilization
Token Throughput
Queue Length
P95 Latency
```

because GPUs are the bottleneck.

---

# Interview Discussion Point #2

## Reactive Scaling

Most common.

---

Example:

```text
CPU > 80%
```

Scale out.

---

Problem:

Traffic already increased.

Scaling happens late.

---

This causes:

```text
Latency spike
```

before scaling completes.

---

# Interview Question

What's wrong with reactive scaling?

Answer:

Scaling happens after the problem starts.

Users already experience degradation.

---

# Interview Discussion Point #3

## Predictive Scaling

Scale before traffic arrives.

---

Example:

Every day:

```text
9 AM
```

traffic increases.

Predictive model learns pattern.

Scale at:

```text
8:55 AM
```

---

Production Examples

Amazon:

Prime Day

Netflix:

Evening traffic

Stock Trading:

Market opening

---

# Applied Scientist Angle

This is where ML enters infrastructure.

We can train models to predict:

```text
Future QPS
Future GPU demand
Future latency
```

and scale proactively.

---

Interviewers love this answer.

---

# Interview Discussion Point #4

## Scale Up vs Scale Out

---

Scale Up

```text
8 CPU
→
64 CPU
```

---

Scale Out

```text
10 Servers
→
100 Servers
```

---

Production systems prefer:

```text
Scale Out
```

---

Why?

Because:

### Better Fault Tolerance

### Better Availability

### Better Elasticity

---

Interview Question

Why not keep buying bigger machines?

Answer:

Eventually:

* Hardware limits reached
* Expensive
* Single point of failure

---

# Interview Discussion Point #5

## Cooldown Period

Huge interview favorite.

---

Suppose:

Traffic spikes.

Autoscaler creates:

```text
100 servers
```

Traffic drops.

Removes:

```text
100 servers
```

Traffic spikes again.

Adds:

```text
100 servers
```

---

Result:

```text
Thrashing
```

---

Solution:

Cooldown window.

Example:

```text
Wait 10 minutes before scaling again
```

---

# Interview Discussion Point #6

## Cost Optimization

Interviewers love this.

---

Example:

Night traffic:

```text
5K QPS
```

Need:

```text
5 Servers
```

not

```text
500 Servers
```

---

Auto scaling reduces:

### Compute Cost

### GPU Cost

### Power Cost

---

# Interview Question

What happens if autoscaler is too aggressive?

Answer:

Cost explosion.

---

What happens if too conservative?

Answer:

Latency explosion.

---

Need balance.

---

# Interview Discussion Point #7

## Failure Scenarios

---

### Scenario 1

Autoscaler fails.

Result:

No scaling.

---

### Scenario 2

Wrong metric.

Example:

CPU low.

But:

```text
GPU queue exploding.
```

System overloaded.

---

### Scenario 3

Scaling delay.

New instance startup:

```text
2 minutes
```

Traffic spike:

```text
10 seconds
```

Problem persists.

---

# Production Discussion

Senior candidates discuss:

### Warm Pools

Pre-created instances.

---

### Pre-loaded Models

Models already in memory.

---

### Hot Standby Nodes

Ready immediately.

---

# LLM Specific Scaling

Most candidates fail here.

---

Traditional API

```text
Request cost ≈ fixed
```

---

LLM API

```text
Cost varies massively
```

---

Prompt A:

```text
20 tokens
```

Prompt B:

```text
50,000 tokens
```

---

Difference:

2500x

---

Therefore scale using:

### Queue Length

### Token Throughput

### GPU Memory

### GPU Utilization

---

Not just request count.

---

# Topic 20: Elasticity

---

# What Is Elasticity?

Elasticity means:

> Ability to automatically expand and shrink resources based on demand.

---

Interviewers often ask:

Difference between:

```text
Scalability
Elasticity
```

---

# Scalability

Can system handle growth?

Example:

```text
10K QPS
→
1 Million QPS
```

---

# Elasticity

Can system automatically adjust resources?

Example:

```text
Morning:
100 servers

Night:
10 servers
```

---

# Interview Answer

A system can be scalable but not elastic.

Example:

```text
Supports 1M QPS
```

But engineer manually adds servers.

Scalable.

Not elastic.

---

# Production Example

Netflix

Morning:

```text
Low traffic
```

Evening:

```text
Huge traffic
```

Resources expand automatically.

---

# Applied Scientist Example

Training Cluster

---

Normal:

```text
10 GPUs
```

Large training job arrives:

```text
500 GPUs
```

Cluster expands.

---

Job completes:

```text
10 GPUs
```

Cluster shrinks.

---

This is elasticity.

---

# Interview Discussion Point #1

## Resource Efficiency

Elasticity optimizes:

### Cost

### Utilization

### Energy

---

# Interview Discussion Point #2

## Elasticity Challenges

### Cold Start

New server:

```text
Model loading
```

may take:

```text
60 seconds
```

---

LLM loading:

```text
Several minutes
```

sometimes.

---

### Data Locality

New server:

No cache.

No embeddings.

Performance temporarily worse.

---

### State Synchronization

Stateful systems harder.

Example:

Feature Store

Vector DB

Redis Cluster

---

# Interview Question

Why is elasticity harder for stateful systems?

Answer:

Need:

* Data movement
* Replication
* Rebalancing
* Synchronization

Stateless systems simply start new instances.

---

# Interview Discussion Point #3

## Elasticity in Kubernetes

Interviewers often ask.

---

HPA

Horizontal Pod Autoscaler

Uses:

```text
CPU
Memory
Custom Metrics
```

---

Cluster Autoscaler

Adds:

```text
New Nodes
```

---

For ML systems:

Custom metrics:

```text
GPU Utilization
Queue Length
Inference Latency
```

---

# Senior-Level Interview Questions

---

## Q1

How would you autoscale an LLM inference platform?

### Answer

Monitor:

* GPU utilization
* Token throughput
* Queue length
* P95 latency

Scale GPU workers dynamically.

Use warm pools to reduce startup delay.

---

## Q2

How would you autoscale a recommendation system?

### Answer

Monitor:

* QPS
* CPU
* Memory
* Latency

Use stateless inference nodes behind load balancer.

---

## Q3

Can elasticity improve cost?

### Answer

Yes.

Resources released when demand decreases.

Particularly important for expensive GPU clusters.

---

## Q4

Why doesn't request count alone work for LLM scaling?

### Answer

Request cost varies dramatically.

Need token-aware metrics.

---

## Q5

How would you handle sudden 100× traffic spike?

### Senior Answer

1. Predictive scaling if possible.
2. Warm pools.
3. Queue buffering.
4. Graceful degradation.
5. Regional failover.
6. Rate limiting.
7. Emergency scale-out.

---

# What Separates a Senior Applied Scientist?

A junior candidate says:

> Autoscaling adds more servers when CPU is high.

A senior candidate says:

> I would choose scaling signals based on the workload. For recommendation systems, CPU, memory, and QPS may be sufficient. For LLM inference, queue length, token throughput, GPU utilization, and latency are better indicators. I would also discuss predictive scaling, warm pools, cold-start mitigation, cost tradeoffs, and failure scenarios.

That answer demonstrates production-scale AI infrastructure thinking.

---

# Topic 21: Distributed Caching

# (Senior Applied Scientist / AI-ML Engineer Interview Perspective)

If there is **one optimization topic that appears everywhere**, it is caching.

Used in:

* ChatGPT
* Amazon Search
* Netflix Recommendations
* Uber Matching
* Feature Stores
* Vector Databases
* RAG Systems
* Fraud Detection

A huge percentage of large-scale system performance comes from caching.

---

# What is a Cache?

A cache is a faster storage layer that stores frequently accessed data to avoid expensive computation or database access.

Without Cache:

```text
User Request
     |
Application
     |
Database
     |
Response
```

Every request hits DB.

---

With Cache:

```text
User Request
      |
Application
      |
   Cache
   /    \
Hit     Miss
 |        |
Resp     DB
```

---

# Interview Definition

A senior answer:

> A cache is a high-speed storage layer that stores frequently accessed or computationally expensive data closer to consumers to reduce latency, increase throughput, and decrease backend load.

Notice:

Not just speed.

Also:

* Throughput
* Scalability
* Cost reduction

---

# Why Does Caching Exist?

Suppose:

Feature Store lookup:

```text
Latency = 20 ms
```

Recommendation service:

```text
100,000 QPS
```

Database receives:

```text
100,000 queries/sec
```

Potential overload.

---

Cache lookup:

```text
1 ms
```

Huge improvement.

---

# Production Example

Amazon Product Page

User requests:

```text
iPhone 20
```

Product information rarely changes.

Cache stores:

```json
{
  "name":"iPhone 20",
  "price":999
}
```

No DB access needed.

---

# Applied Scientist Perspective

What do we cache?

---

## Feature Vectors

Most common.

```text
User Embeddings
Product Embeddings
```

---

## Recommendations

```text
Top 100 Products
```

for a user.

---

## LLM Responses

Prompt cache.

---

## Retrieval Results

RAG systems.

---

## Vector Search Results

Frequently queried embeddings.

---

# Interview Discussion Point #1

## Cache Hit Ratio

Extremely important.

Formula:

```text
Hits
-----------
Hits + Misses
```

---

Example:

```text
900 hits
100 misses
```

Hit rate:

```text
90%
```

---

Interviewers love asking:

> What cache hit rate would you target?

Answer:

Depends on workload.

Typical:

```text
80-95%
```

---

# Interview Discussion Point #2

## Cache-Aside Pattern

Most common.

---

Read Flow

```text
Check Cache
      |
     Hit
      |
   Return

Miss
 |
DB
 |
Update Cache
 |
Return
```

---

Used by:

* Amazon
* Netflix
* Most web services

---

# Interview Question

Why is Cache-Aside popular?

Answer:

Simple.

Application controls caching.

Works with existing databases.

---

# Interview Discussion Point #3

## Write Through Cache

---

Write:

```text
Application
     |
Cache
     |
Database
```

---

Advantages:

Cache always updated.

---

Problems:

Write latency increases.

---

# Interview Discussion Point #4

## Write Back Cache

---

Write:

```text
Application
    |
Cache
```

DB updated later.

---

Advantages:

Very fast writes.

---

Problems:

Risk of data loss.

---

Interviewers often ask:

When would you use write-back?

Answer:

Analytics systems.

Not critical transactional systems.

---

# Interview Discussion Point #5

## TTL (Time To Live)

Very common interview topic.

---

Example:

```text
Cache Entry
TTL = 5 minutes
```

After 5 minutes:

Removed.

---

Used when:

```text
Stale data acceptable
```

---

ML Example

Recommendation cache:

```text
TTL = 30 min
```

---

Fraud score:

```text
TTL = 5 sec
```

---

# Interview Question

How do you choose TTL?

Answer:

Based on:

* Data freshness requirement
* Update frequency
* Latency goals

---

# Interview Discussion Point #6

## Cache Invalidation

One of the hardest problems.

---

Example:

DB:

```text
Price = 100
```

Cache:

```text
Price = 100
```

---

DB updated:

```text
Price = 80
```

Cache still:

```text
Price = 100
```

Now inconsistent.

---

Solutions:

### TTL

Eventually expires.

---

### Event-Based Invalidation

Kafka event:

```text
Product Updated
```

Remove cache entry.

---

### Versioning

Store version numbers.

---

Interviewers LOVE this topic.

---

# Interview Question

What is the hardest problem in caching?

Answer:

Maintaining consistency between cache and source of truth.

---

# Interview Discussion Point #7

## Distributed Cache

Single cache becomes bottleneck.

---

Example:

```text
Redis Node
```

receives:

```text
1 Million QPS
```

Not enough.

---

Need:

```text
Redis Cluster
```

---

```text
Redis-1
Redis-2
Redis-3
Redis-4
```

---

# Interview Discussion Point #8

## Consistent Hashing

Very important.

---

Without consistent hashing:

Adding node:

```text
3 Nodes
→
4 Nodes
```

moves almost all keys.

---

With consistent hashing:

Only small portion moves.

---

Used heavily in:

* Redis
* Memcached
* Cassandra

---

Interview Question

Why does consistent hashing matter?

Answer:

Allows cluster growth with minimal cache rebalancing.

---

# Interview Discussion Point #9

## Cache Stampede

Very common senior interview question.

---

Example:

Popular key expires.

```text
User Embedding
```

100,000 requests arrive.

All hit DB.

DB crashes.

---

Solutions:

### Request Coalescing

One request rebuilds cache.

Others wait.

---

### Randomized TTL

Avoid simultaneous expiry.

---

### Background Refresh

Refresh before expiry.

---

# Interview Discussion Point #10

## Multi-Level Cache

Production systems use:

---

L1

```text
Application Memory
```

---

L2

```text
Redis
```

---

L3

```text
Database
```

---

```text
Request
  |
L1 Cache
  |
L2 Cache
  |
Database
```

---

# ML-Specific Caching

---

# Recommendation Systems

Cache:

```text
Top-N Recommendations
```

---

# Feature Stores

Cache:

```text
User Features
```

---

# RAG Systems

Cache:

```text
Retrieved Chunks
```

---

# LLM Systems

Cache:

```text
Prompt Embeddings
KV Cache
Generated Responses
```

---

# Interview Question

How does ChatGPT use caching?

Answer:

Examples include:

* Prompt cache
* Embedding cache
* Retrieval cache
* KV cache

to reduce inference cost and latency.

---

# Topic 22: Sharding

This is arguably the most important database scaling concept.

---

# What is Sharding?

Sharding means:

> Splitting data across multiple machines.

---

Without sharding:

```text
1 Database
10 TB
```

---

With sharding:

```text
Shard1 = 2 TB
Shard2 = 2 TB
Shard3 = 2 TB
Shard4 = 2 TB
Shard5 = 2 TB
```

---

# Why Do We Need It?

Eventually:

```text
CPU limit
Memory limit
Storage limit
IO limit
```

of a single machine reached.

---

Need horizontal scaling.

---

# Production Example

Amazon Products

```text
10 Billion Products
```

Cannot fit in one DB.

Need sharding.

---

# Applied Scientist Example

Feature Store

```text
500 Million Users
```

Each:

```text
1000 Features
```

Single machine impossible.

Need sharding.

---

# Interview Discussion Point #1

## Sharding Key

Most important discussion.

---

Example:

```text
UserID
```

---

```text
Shard = hash(UserID)
```

---

Interviewers often ask:

How do you choose sharding key?

---

Answer:

Must provide:

* Uniform distribution
* High cardinality
* Minimal hotspots

---

# Bad Example

Shard by:

```text
Country
```

---

India:

```text
500 Million Users
```

Luxembourg:

```text
600K Users
```

Skewed.

---

# Interview Discussion Point #2

## Hot Partitions

Huge interview favorite.

---

Example:

Shard by:

```text
CelebrityID
```

---

Taylor Swift gets:

```text
10 Million Requests
```

One shard overloaded.

---

This is hotspotting.

---

Solutions:

### Better shard key

### Virtual shards

### Request replication

---

# Interview Discussion Point #3

## Rebalancing

New node added.

Need redistribute data.

---

Interviewers ask:

What happens when adding shard?

---

Senior Answer:

Need:

* Data migration
* Rebalancing
* Minimal downtime

---

# Interview Discussion Point #4

## Cross-Shard Queries

Example:

```sql
SELECT *
FROM users
WHERE age > 25
```

Need all shards.

---

Problems:

* High latency
* High network cost

---

Interviewers love asking this.

---

# ML Example

Find:

```text
All users interested in cricket
```

Requires scanning many shards.

---

# Interview Discussion Point #5

## Sharding vs Replication

Common question.

---

Replication:

```text
Copies data
```

for availability.

---

Sharding:

```text
Splits data
```

for scalability.

---

Most production systems use both.

---

```text
Shard1
 |- Replica1
 |- Replica2

Shard2
 |- Replica1
 |- Replica2
```

---

# Topic 23: Partitioning

Many candidates confuse this with sharding.

Interviewers intentionally ask.

---

# Difference

---

## Partitioning

Logical division of data.

Can exist inside same DB.

---

Example:

```sql
Orders_2024
Orders_2025
Orders_2026
```

---

Still same database.

---

## Sharding

Physical distribution.

```text
Machine1
Machine2
Machine3
```

---

# Example

PostgreSQL Range Partitioning

```sql
PARTITION BY RANGE(order_date)
```

---

Interviewers ask:

Why partition?

Answer:

Reduce query scan.

---

# Partition Types

---

## Range Partitioning

```text
Jan-Jun
Jul-Dec
```

---

## Hash Partitioning

```text
hash(user_id)
```

---

## List Partitioning

```text
Country
```

---

# Applied Scientist Example

Training Data

Partition by:

```text
Date
```

---

Query:

```text
Last 7 Days
```

Only recent partitions scanned.

Huge speed improvement.

---

# Senior-Level Interview Summary

For **Caching, Sharding, Partitioning**, always discuss:

### Scale

* Data volume
* QPS
* Storage growth

### Latency

* Cache hit ratio
* Query latency

### Failure

* Cache failure
* Shard failure

### Rebalancing

* Data movement
* Consistent hashing

### Cost

* Memory cost
* Storage cost

### ML Impact

* Feature Stores
* Vector DBs
* RAG Retrieval
* Recommendation Systems
* Embedding Storage

---

### Common Interview Question

**"You have 500M users and 5M QPS on a recommendation platform. Walk me through scaling the feature store."**

A strong answer naturally includes:

1. Sharding user features.
2. Replication for availability.
3. Redis caching.
4. Consistent hashing.
5. Load balancing.
6. Autoscaling.
7. Monitoring hot partitions.
8. Multi-region deployment.
9. Eventual vs strong consistency tradeoffs.
10. Failover strategy.

That level of discussion is what distinguishes a senior Applied Scientist from someone who only knows ML models.




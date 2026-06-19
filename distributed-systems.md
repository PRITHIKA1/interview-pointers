This is exactly how senior engineers and applied scientists approach system design interviews.

For every concept, you should be able to answer **3 things**:

1. **What is it?** (Definition)
2. **When do I use it?** (Design decision)
3. **What tradeoffs should I discuss?** (Interview differentiator)

---

# 1. Horizontal vs Vertical Scaling

## Definition

### Vertical Scaling (Scale Up)

Increase resources of a single machine.

```text
4 CPU → 16 CPU
16 GB RAM → 128 GB RAM
```

### Horizontal Scaling (Scale Out)

Add more machines.

```text
1 Server → 10 Servers → 100 Servers
```

---

## Design Considerations

### Traffic Growth

Ask:

```text
Can a single machine handle future traffic?
```

If not:

```text
Horizontal Scaling
```

---

### Fault Tolerance

Single machine:

```text
Machine failure = System down
```

Multiple machines:

```text
Failure of one node ≠ System down
```

---

### Cost

Vertical scaling:

```text
High-end machines become expensive.
```

Horizontal scaling:

```text
Commodity hardware.
```

---

## Interview Discussion Points

* Current QPS
* Future QPS
* Scaling bottlenecks
* Single point of failure

---

# 2. Stateless vs Stateful Services

## Definition

### Stateless

No request-specific information stored locally.

Any server can handle any request.

---

### Stateful

Server maintains data between requests.

Examples:

```text
Database
Kafka
Redis
```

---

## Design Considerations

### Can requests go to any node?

If yes:

```text
Stateless
```

Easy scaling.

---

### Does data need persistence?

If yes:

```text
Stateful
```

Need replication strategy.

---

### Failure Recovery

Ask:

```text
What happens if node dies?
```

Stateful systems require:

* Recovery
* Backup
* Replication

---

## Interview Discussion Points

Always try:

```text
Keep compute stateless
Keep storage stateful
```

Common industry pattern.

---

# 3. CAP Theorem

## Definition

A distributed system can only fully guarantee 2 of:

### C

Consistency

Every node sees same data.

---

### A

Availability

Every request gets response.

---

### P

Partition Tolerance

System survives network failures.

---

## Design Considerations

### Banking System

Need:

```text
Consistency
```

Prefer:

```text
CP
```

---

### Product Catalog

Need:

```text
Availability
```

Prefer:

```text
AP
```

---

## Interview Discussion Points

Always ask:

```text
Can stale data be tolerated?
```

If yes:

```text
AP
```

If no:

```text
CP
```

---

# 4. Strong Consistency

## Definition

After write:

```text
Write(X=100)

Read(X)
→ Always 100
```

---

## Design Considerations

Useful for:

* Payments
* Trading
* Banking

---

## Questions

### Can stale reads cause loss?

If yes:

```text
Strong Consistency
```

---

## Tradeoffs

Higher:

* Latency
* Coordination overhead

---

## Interview Discussion Points

Discuss:

```text
Consistency vs Latency
```

---

# 5. Eventual Consistency

## Definition

Replicas become consistent later.

```text
Node1 = Updated

Node2 = Old

After few seconds

Node2 = Updated
```

---

## Design Considerations

Useful for:

* Recommendations
* Catalogs
* Social media

---

## Questions

Can users tolerate:

```text
1-5 seconds stale data?
```

---

## Tradeoffs

Pros:

* Fast
* Highly available

Cons:

* Temporary inconsistency

---

# 6. Causal Consistency

## Definition

Cause-effect order preserved.

Example:

```text
Comment posted

Then like appears
```

Not vice versa.

---

## Design Considerations

Useful for:

* Chat
* Collaboration tools
* Social media

---

## Interview Discussion Points

Need ordering guarantees without full strong consistency.

---

# 7. Availability

## Definition

Probability system is accessible.

Example:

```text
99.99% uptime
```

---

## Design Considerations

Ask:

### SLA?

```text
99.9?
99.99?
99.999?
```

---

### Downtime Impact?

* Revenue loss
* User impact

---

## Interview Discussion Points

How availability is achieved:

* Replication
* Load balancing
* Failover

---

# 8. Fault Tolerance

## Definition

System continues despite failures.

---

## Design Considerations

Assume failures:

```text
Node crash
Network failure
Disk failure
```

---

## Questions

Can system survive:

```text
1 node failure?
2 node failures?
```

---

## Interview Discussion Points

Never assume machines won't fail.

---

# 9. High Availability

## Definition

Minimal downtime.

Usually:

```text
99.99%+
```

---

## Design Considerations

Need:

* Redundancy
* Failover
* Replication

---

## Interview Discussion Points

Ask:

```text
How quickly can traffic fail over?
```

---

# 10. Reliability

## Definition

System behaves correctly over time.

---

## Design Considerations

Questions:

```text
Can requests be lost?
Can messages be duplicated?
Can data be corrupted?
```

---

## Interview Discussion Points

Reliability ≠ Availability.

A system can be available but wrong.

---

# 11. Durability

## Definition

Committed data survives failures.

---

## Design Considerations

Need:

* Replication
* WAL logs
* Persistent storage

---

## Questions

What happens after power loss?

---

## Interview Discussion Points

Critical for:

* Transactions
* User data

---

# 12. Leader-Follower Replication

## Definition

Single write node.

Multiple read replicas.

```text
      Leader
      /   \
   F1      F2
```

---

## Design Considerations

### Read-heavy?

Great choice.

### Write-heavy?

Leader becomes bottleneck.

---

## Interview Discussion Points

Discuss:

* Replication lag
* Failover
* Read scaling

---

# 13. Multi-Leader Replication

## Definition

Multiple writable leaders.

```text
US Leader
EU Leader
APAC Leader
```

---

## Design Considerations

Useful:

* Global applications

---

## Questions

How conflicts resolved?

```text
Last write wins?
Versioning?
```

---

## Interview Discussion Points

Conflict resolution is mandatory.

---

# 14. Quorum Reads/Writes

## Definition

Need majority agreement.

```text
N = 5 replicas

W = 3
R = 3
```

---

## Design Considerations

Condition:

```text
R + W > N
```

Ensures consistency.

---

## Interview Discussion Points

Tradeoff:

```text
Higher consistency
Higher latency
```

---

# 15. Distributed Transactions

## Definition

Transaction spans multiple services/databases.

---

## Design Considerations

Questions:

```text
Can partial failure occur?
```

Must maintain consistency.

---

## Interview Discussion Points

Distributed transactions are expensive.

Avoid if possible.

---

# 16. Two Phase Commit (2PC)

## Definition

Coordinator asks:

```text
Prepare?
Commit?
```

---

## Design Considerations

Strong consistency.

---

## Problems

Coordinator failure.

Blocking protocol.

---

## Interview Discussion Points

Works but poor scalability.

---

# 17. Saga Pattern

## Definition

Sequence of local transactions.

Failures trigger compensation.

---

## Example

```text
Create Order

Reserve Inventory

Charge Payment

Failure

Refund Payment
```

---

## Design Considerations

Microservices architecture.

---

## Interview Discussion Points

Preferred over 2PC.

---

# 18. Raft

## Definition

Consensus algorithm.

Elects leader.

Replicates logs.

---

## Design Considerations

Need:

```text
Strong consistency
Leader election
```

---

## Interview Discussion Points

Understand:

* Leader election
* Log replication
* Majority voting

---

# 19. Paxos

## Definition

Consensus algorithm.

More theoretical than Raft.

---

## Interview Discussion Points

Know:

```text
Raft easier to understand.
```

Most companies use Raft concepts.

---

# 20. Load Balancing

## Definition

Distributes requests.

---

## Design Considerations

Need:

* Traffic distribution
* Health checks

---

## Questions

Algorithm?

* Round Robin
* Least Connections
* Weighted

---

## Interview Discussion Points

Always place LB before stateless services.

---

# 21. Auto Scaling

## Definition

Automatically adds/removes resources.

---

## Design Considerations

Metrics:

* CPU
* Memory
* QPS
* Queue length

---

## Interview Discussion Points

Prevent:

```text
Overprovisioning
Underprovisioning
```

---

# 22. Elasticity

## Definition

Ability to scale dynamically.

---

## Design Considerations

Traffic spikes?

```text
Black Friday
IPL Finals
Prime Day
```

---

## Interview Discussion Points

Elasticity saves cost.

---

# 23. Distributed Caching

## Definition

Cache spread across nodes.

Example:

* Redis Cluster

---

## Design Considerations

What to cache?

* Hot data
* Frequent reads

---

## Questions

Cache invalidation?

TTL?

---

## Interview Discussion Points

Cache consistency is usually the hardest problem.

---

# 24. Sharding

## Definition

Split data across machines.

```text
User 1-1M
User 1M-2M
User 2M-3M
```

---

## Design Considerations

Shard Key Selection.

Most important decision.

---

## Questions

Will shard become hot?

---

## Interview Discussion Points

Always discuss:

* Rebalancing
* Hot shards
* Cross-shard queries

---

# 25. Partitioning

## Definition

Split large dataset into smaller chunks.

---

## Types

### Horizontal

Rows split.

```text
Users A-M
Users N-Z
```

---

### Vertical

Columns split.

```text
User Table

Basic Info
Profile Info
```

---

## Design Considerations

Improves:

* Query performance
* Maintenance

---

## Interview Discussion Points

Difference:

```text
Partitioning
→ Usually inside DB

Sharding
→ Across machines
```

---

# Senior-Level Interview Checklist

For every ML/System Design interview component, explicitly discuss:

### Scale

* QPS
* Data size
* Users

### Latency

* P50
* P95
* P99

### Availability

* SLA target

### Consistency

* Strong or eventual?

### Reliability

* Failure handling

### Cost

* Compute
* Storage
* Network

### Monitoring

* Metrics
* Alerts

### Recovery

* Backup
* Failover

### Future Growth

* 10x scale scenario

These are the dimensions interviewers expect senior candidates to proactively bring into the discussion rather than waiting to be asked.

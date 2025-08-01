## Question 1

```markdown
What is the primary role of a Kafka broker?
```

**Options**
```markdown
- A. To act as a load balancer for consumer requests.
- B. To serve as a stateless proxy between producers and consumers.
- C. To handle message ingestion, storage, and delivery.
- D. To manage ZooKeeper coordination.
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Incorrect. Brokers do not primarily act as load balancers.
- B. Incorrect. Brokers are not stateless; they manage state via disk logs and metadata.
- C. Correct. Brokers handle message ingestion, storage, and delivery, including managing partitions and replication.
- D. Incorrect. Brokers do not manage ZooKeeper; they may use it for coordination (unless using KRaft).
```

</details>

---

## Question 2

```markdown
What is the purpose of partitioning a Kafka topic?
```

**Options**
```markdown
- A. To ensure global ordering of messages across the entire topic.
- B. To enable parallelism and fault tolerance.
- C. To reduce disk usage by compressing messages.
- D. To limit the number of producers for a topic.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. Partitions only guarantee ordering within a single partition, not globally.
- B. Correct. Partitions enable parallelism (spreading data across brokers) and fault tolerance (via replication).
- C. Incorrect. Partitioning does not inherently reduce disk usage or compress messages.
- D. Incorrect. Partitioning does not limit producers; it allows more producers to write in parallel.
```

</details>

---

## Question 3

```markdown
Which of the following best describes an "In-Sync Replica" (ISR) in Kafka?
```

**Options**
```markdown
- A. A replica that is fully caught up with the leader's log.
- B. A replica that is temporarily offline but will recover automatically.
- C. A replica that is read-only for consumers.
- D. A replica that is manually promoted to leader.
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
- A. Correct. ISR replicas are fully caught up with the leader and can be promoted to leader if needed.
- B. Incorrect. Offline replicas are not part of the ISR until they recover and sync.
- C. Incorrect. Followers can replicate data but are not read-only for consumers (only leaders serve reads).
- D. Incorrect. Replicas are elected automatically from the ISR, not manually promoted.
```

</details>

---

## Question 4

```markdown
What happens if a Kafka producer sets `acks=all` but fewer than `min.insync.replicas` are available?
```

**Options**
```markdown
- A. The message is written to the leader only.
- B. The producer receives a `NotEnoughReplicasException`.
- C. The message is stored in a buffer until replicas recover.
- D. The producer automatically reduces the replication factor.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. `acks=all` requires acknowledgment from all ISR replicas, not just the leader.
- B. Correct. The producer will fail with `NotEnoughReplicasException` if the ISR count is below the minimum.
- C. Incorrect. Kafka does not buffer messages for later replication in this scenario.
- D. Incorrect. The replication factor is fixed; it cannot be dynamically adjusted by the producer.
```

</details>

---

## Question 5

```markdown
How does Kafka physically store messages for a partition on disk?
```

**Options**
```markdown
- A. As a single monolithic file per topic.
- B. As an append-only log segmented into multiple files.
- C. As a relational database table.
- D. As compressed binary blobs.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. Topics are split into partitions, each stored as segmented logs, not monolithic files.
- B. Correct. Each partition is an append-only log split into segment files (e.g., `000000.log`, `000001.log`).
- C. Incorrect. Kafka does not use relational databases; it relies on log-structured storage.
- D. Incorrect. While Kafka supports compression, messages are not stored as opaque blobs.
```

</details>

---

## Question 6

```markdown
What is the role of the Kafka controller in a cluster?
```

**Options**
```markdown
- A. To serve as the primary broker for all read/write requests.
- B. To manage leader elections and partition reassignments.
- C. To compress topic data for storage efficiency.
- D. To act as a gateway for external systems.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. The controller does not handle all read/write requests; it manages cluster state.
- B. Correct. The controller oversees leader elections, ISR changes, and partition assignments.
- C. Incorrect. The controller does not handle data compression.
- D. Incorrect. External systems interact with brokers directly, not through the controller.
```

</details>

---

## Question 7

```markdown
Which configuration setting determines how long Kafka retains messages for a topic?
```

**Options**
```markdown
- A. `segment.bytes`
- B. `retention.ms`
- C. `replication.factor`
- D. `unclean.leader.election.enable`
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. `segment.bytes` controls log segment file size, not retention time.
- B. Correct. `retention.ms` defines the time-based retention period for messages.
- C. Incorrect. `replication.factor` sets the number of replicas, not retention.
- D. Incorrect. This setting controls whether out-of-sync replicas can become leaders.
```

</details>

---

## Question 8

```markdown
What is the risk of enabling `unclean.leader.election.enable=true` in Kafka?
```

**Options**
```markdown
- A. Increased disk usage due to redundant logs.
- B. Potential data loss if an out-of-sync replica becomes leader.
- C. Slower consumer throughput.
- D. Higher network latency between brokers.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. This setting does not affect disk usage.
- B. Correct. Enabling this may elect a stale replica as leader, causing data loss.
- C. Incorrect. Consumer throughput is not directly impacted by this setting.
- D. Incorrect. Network latency is unrelated to leader election configuration.
```

</details>

---

## Question 9

```markdown
How does Kafka ensure message ordering guarantees?
```

**Options**
```markdown
- A. By globally ordering messages across all partitions in a topic.
- B. By guaranteeing order only within a single partition.
- C. By using timestamps to sequence messages.
- D. By requiring consumers to acknowledge messages in order.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. Kafka does not guarantee global ordering across partitions.
- B. Correct. Messages are strictly ordered within a partition but not across partitions.
- C. Incorrect. Timestamps are metadata and do not enforce ordering.
- D. Incorrect. Consumer acknowledgments do not affect Kafka's internal ordering.
```

</details>

---

## Question 10

```markdown
What is the default behavior when a Kafka producer writes to a non-existent topic?
```

**Options**
```markdown
- A. The message is discarded silently.
- B. The topic is auto-created with default partitions/replication.
- C. The producer receives an error and must retry.
- D. The message is routed to a dead-letter queue.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. Kafka does not discard messages in this case.
- B. Correct. By default (`auto.create.topics.enable=true`), Kafka auto-creates topics with 1 partition and replication factor 1.
- C. Incorrect. The producer does not receive an error unless auto-creation is disabled.
- D. Incorrect. Dead-letter queues are not a default Kafka feature.
```

</details>

---

## Question 11

```markdown
What happens when you increase the number of partitions for an existing Kafka topic?
```

**Options**
```markdown
- A. Existing messages are redistributed across all partitions.
- B. New messages may be routed differently, but old messages remain in their original partitions.
- C. The topic is temporarily unavailable during repartitioning.
- D. All replicas are rebuilt from scratch.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. Existing messages stay in their original partitions.
- B. Correct. New messages use the updated partition count, but old messages are unaffected.
- C. Incorrect. The topic remains available during the operation.
- D. Incorrect. Replicas are not rebuilt; only new partitions are assigned.
```

</details>

---

## Question 12

```markdown
Which of the following is true about Kafka log segments?
```

**Options**
```markdown
- A. They are merged into a single file after compaction.
- B. They consist of a `.log` file for messages and an `.index` file for offsets.
- C. They are stored in memory for fast access.
- D. They are encrypted by default.
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Incorrect. Segments are not merged; they are deleted or compacted individually.
- B. Correct. Each segment has a `.log` file (messages) and `.index` file (offset mappings).
- C. Incorrect. Segments are stored on disk, not in memory.
- D. Incorrect. Encryption is not enabled by default.
```

</details>

--- 

## Question 2

```markdown
A Kafka broker is configured with the following settings:

`num.replication.fetchers=4`  
`replica.fetch.max.bytes=1048576`

What is the maximum amount of data that can be fetched by the broker for replication purposes in a single request?
```

**Options**

```markdown
- A. 1 MB
- B. 4 MB
- C. 1048576 bytes
- D. 4194304 bytes
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
`replica.fetch.max.bytes` is the per-fetcher limit, set to 1 MB (1048576 bytes).  
Each of the 4 fetchers operates independently, so per request the max fetch size is 1 MB.

- A. Correct — per fetch request limit is 1 MB.
- B. Incorrect — 4 MB is total across all fetchers, not per request.
- C. Correct in bytes but answer expects MB format, so A preferred.
- D. Incorrect — 4 * 1 MB = 4 MB total across fetchers, not per request.
```

</details>

---

## Question 3

```markdown
What happens to the replicas when a broker in a Kafka cluster goes down?
```

**Options**

```markdown
- A. All replicas on the failed broker are permanently lost
- B. The replicas on the failed broker are automatically redistributed to other brokers
- C. The replicas on the failed broker become unavailable until the broker is restarted
- D. The replicas on the failed broker are immediately promoted to be leaders on other brokers
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
When a broker fails:

- C. Its replicas are temporarily unavailable.
- Leader roles are transferred to other in-sync replicas.
- When the broker comes back, it catches up and resumes replica duties.

Kafka ensures availability unless too many replicas are lost.
```

</details>

---

## Question 8

```markdown
How does Kafka ensure data integrity and consistency across replicas?

- A. By using a two-phase commit protocol
- B. By relying on ZooKeeper for distributed consensus
- C. By implementing a leader-follower replication model
- D. By using a gossip protocol for eventual consistency
```

**Options**

```markdown
- A. Two-phase commit protocol
- B. ZooKeeper for consensus
- C. Leader-follower replication model
- D. Gossip protocol
```

<details><summary>Response:</summary> 

**Answer:** C

**Explanation:**

```markdown
Kafka achieves consistency through replication:

- A. Two-phase commit – ❌ Not used for replication integrity.
- B. ZooKeeper for consensus – ❌ Used for metadata, not replication consistency.
- C. Leader-follower model – ✅ Producers write to leader, followers replicate.
- D. Gossip protocol – ❌ Not applicable in Kafka's architecture.
```

</details>

## Question 9

```markdown
What happens to the replicas when a broker in a Kafka cluster goes down?

- A. All replicas on the failed broker are permanently lost
- B. The replicas on the failed broker are automatically redistributed to other brokers
- C. The replicas on the failed broker become unavailable until the broker is restarted
- D. The replicas on the failed broker are immediately promoted to be leaders on other brokers
```

**Options**

```markdown
- A. All replicas on the failed broker are permanently lost
- B. The replicas on the failed broker are automatically redistributed to other brokers
- C. The replicas on the failed broker become unavailable until the broker is restarted
- D. The replicas on the failed broker are immediately promoted to be leaders on other brokers
```

<details><summary>Response:</summary> 

**Answer:** C

**Explanation:**

```markdown
When a broker fails:

- A. All replicas on the failed broker are permanently lost – ❌ Data isn't lost.
- B. Automatically redistributed – ❌ Kafka does not automatically move replicas.
- C. Become unavailable until restart – ✅ Correct behavior.
- D. Promoted to leaders – ❌ Only existing in-sync replicas can become leaders.
```

</details>

---

## Question 11

```markdown
How does Kafka ensure data integrity and consistency across replicas?
```

**Options**

```markdown
- A. By using a two-phase commit protocol
- B. By relying on ZooKeeper for distributed consensus
- C. By implementing a leader-follower replication model
- D. By using a gossip protocol for eventual consistency
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
Kafka uses:

- C. A leader-follower model for consistency.
  - Leader handles all writes.
  - Followers replicate data.
  - Data is committed once replicated to all in-sync replicas.

Other options are incorrect:
- A. Kafka doesn’t use two-phase commit.
- B. ZooKeeper manages metadata, not replication.
- D. Gossip protocols aren’t used by Kafka.
```

</details>

## Question 6

```markdown
A Kafka consumer is consuming from a topic partition. It sends a fetch request to the broker and receives a 'Replica Not Available' error. What is the consumer's next action?

```

**Options**

```markdown
- A. Backs off and retries the fetch request after a short delay
- B. Sends an offset commit request to trigger partition rebalancing
- C. Sends a metadata request to refresh its view of the cluster
- D. Closes the connection and tries connecting to a different broker
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
The consumer should refresh metadata to identify a healthy broker that can serve the partition. Rebalancing, retries, or switching brokers won't help without fresh metadata.

- A. Not optimal, consumer needs updated metadata first.
- B. Offset commit doesn't solve replica availability.
- C. Correct — refresh metadata to get current cluster info.
- D. Closing connection unnecessarily without metadata update.
```

</details>

---

## Question 16
```markdown
What is the purpose of the `unclean.leader.election.enable` configuration in Kafka?  
```  

**Options**
```markdown  
- A. To allow out-of-sync replicas to become leaders during failures  
- B. To enable automatic cleanup of corrupted log segments  
- C. To force all replicas to sync before a leader election  
- D. To disable replication for topics with low priority  
```  

<details><summary>Response:</summary>  

**Answer:** A

**Explanation:**
```markdown  
- A. Correct — When `true`, allows non-ISR replicas to become leaders (risk data loss).  
- B. Incorrect — Unrelated to log cleanup.  
- C. Incorrect — This describes `min.insync.replicas` behavior.  
- D. Incorrect — No priority-based replication exists.  
```  
</details>  

---  

## Question 17
```markdown
A Kafka topic has `replication.factor=3` and `min.insync.replicas=2`. If two brokers fail simultaneously, what happens to the partition?  
```  

**Options**
```markdown  
- A. The partition becomes unavailable until one broker recovers.  
- B. The partition continues serving requests with the remaining replica.  
- C. Kafka automatically reduces `min.insync.replicas` to 1.  
- D. The partition is deleted to preserve cluster stability.  
```  

<details><summary>Response:</summary>  

**Answer:** A

**Explanation:**
```markdown  
- A. Correct — With only 1 replica left (below `min.insync.replicas`), writes are blocked.  
- B. Incorrect — Writes fail if ISR count drops below the minimum.  
- C/D. Incorrect — Kafka doesn’t auto-adjust configs or delete partitions.  
```  
</details>  

---  

## Question 18
```markdown
How does a Kafka broker determine if a follower replica is "in-sync" (ISR)?  
```  

**Options**
```markdown  
- A. By comparing its log offset with the leader’s latest offset.  
- B. By checking ZooKeeper for replica health status.  
- C. By validating checksums of all replicated messages.  
- D. By measuring network latency to the follower.  
```  

<details><summary>Response:</summary>  

**Answer:** A

**Explanation:**
```markdown  
- A. Correct — Followers must catch up to the leader’s high-water mark.  
- B. Incorrect — ZooKeeper doesn’t track replica sync status.  
- C/D. Incorrect — Checksums and latency aren’t used for ISR checks.  
```  
</details>  

---  

## Question 19
```markdown
What happens when a previously failed Kafka broker rejoins the cluster?  
```  

**Options**
```markdown  
- A. It immediately resumes leadership for all its partitions.  
- B. It synchronizes with leaders before rejoining the ISR.  
- C. It triggers a full cluster rebalance.  
- D. It deletes stale data to avoid conflicts.  
```  

<details><summary>Response:</summary>  

**Answer:** B

**Explanation:**
```markdown  
- B. Correct — The broker must catch up to the leader’s log before rejoining ISR.  
- A. Incorrect — Leadership is reassigned only after synchronization.  
- C/D. Incorrect — No full rebalance or auto-deletion occurs.  
```  
</details>  

---  

## Question 20
```markdown
Which Kafka metric indicates potential replication lag issues?  
```  

**Options**
```markdown  
- A. `UnderReplicatedPartitions`  
- B. `ActiveControllerCount`  
- C. `RequestQueueSize`  
- D. `NetworkProcessorAvgIdlePercent`  
```  

<details><summary>Response:</summary>  

**Answer:** A

**Explanation:**
```markdown  
- A. Correct — High `UnderReplicatedPartitions` suggests replicas aren’t keeping up.  
- B. Incorrect — Tracks Controller availability, not replication.  
- C/D. Incorrect — Measure request backlog and CPU, not replication health.  
```  
</details>  



## Question 4

```markdown
A client connects to a broker in a Kafka cluster and sends a produce request for a topic partition.  
The broker responds with a 'Not Enough Replicas' error. What does the client do next?
```

**Options**

```markdown
- A. Retries sending the produce request to the same broker
- B. Sends metadata request to the same broker to refresh its metadata
- C. Sends produce request to the controller broker
- D. Sends metadata request to the Zookeeper to find the controller broker
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Upon 'Not Enough Replicas' error, the client refreshes its metadata from the broker to get updated ISR and broker status.  
The client does not contact the controller or Zookeeper directly.

- A. Incorrect — retry without metadata update unlikely to succeed.
- B. Correct — refresh metadata to get latest ISR info.
- C. Incorrect — produce requests go to leader brokers, not necessarily controller.
- D. Incorrect — clients do not query Zookeeper directly.
```

</details>

---


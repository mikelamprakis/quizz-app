## Question 1

```markdown
Which Kafka component must MirrorMaker 2 connect to in the destination cluster to replicate topic data?
```

**Options**

```markdown
- A. Schema Registry
- B. Kafka Broker
- C. Kafka Connect
- D. Zookeeper
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Schema Registry is used for schema data, not topic replication.
- B. Brokers are involved, but Kafka Connect is the entry point for MM2.
- C. Correct: MirrorMaker 2 runs on top of Kafka Connect.
- D. Zookeeper is not required for MM2 to function directly.
```

</details>

---

## Question 2

```markdown
What is the correct format for a replicated topic name by default in MirrorMaker 2?
```

**Options**

```markdown
- A. {topic_name}.mirror
- B. {topic_name}_remote
- C. {source-cluster-name}.{topic_name}
- D. {destination-cluster-name}-{topic_name}
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Not a valid format.
- B. Arbitrary; not used by MM2.
- C. Correct: The default naming convention is {source-cluster}.{topic}.
- D. Not part of MM2 naming conventions.
```

</details>

---

## Question 3

```markdown
How does MirrorMaker 2 track and sync consumer group offsets?
```

**Options**

```markdown
- A. Through topic metadata replication
- B. By using offset syncs via the heartbeat mechanism
- C. By exporting offsets from ZooKeeper
- D. Through Avro serialization
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Metadata alone is insufficient.
- B. Correct: MM2 uses heartbeats to track and sync offsets.
- C. Zookeeper is not involved in offset sync.
- D. Avro is unrelated to offset syncing.
```

</details>

---

## Question 4

```markdown
Which internal topic does MirrorMaker 2 use to track heartbeat status between clusters?
```

**Options**

```markdown
- A. __consumer_offsets
- B. __mm2_heartbeats
- C. __mirror_heartbeat
- D. __connect_status
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. That’s Kafka's internal consumer offset topic.
- B. Correct: MirrorMaker uses __mm2_heartbeats for heartbeat detection.
- C. Close, but not correct naming.
- D. Used by Kafka Connect for task status, not MM2.
```

</details>

---

## Question 5

```markdown
How does MirrorMaker 2 avoid infinite replication loops in active-active setups?
```

**Options**

```markdown
- A. Filtering by message key
- B. Loop detection using topic names
- C. Preventing re-replication using source cluster alias
- D. Only replicating from topics with the “mirror” suffix
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. MM2 doesn't inspect keys for loop detection.
- B. Naming helps but isn’t the full mechanism.
- C. Correct: MM2 avoids looping by recognizing the source cluster alias in the topic name.
- D. Not a supported MM2 feature.
```

</details>

---

## Question 6

```markdown
Which MirrorMaker 2 feature ensures that a failover to the destination cluster can resume consumption correctly?
```

**Options**

```markdown
- A. Topic compression
- B. Offset translation
- C. Retention policy mirroring
- D. SSL authentication
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Not related to failover behavior.
- B. Correct: Offset translation ensures consumer group continuity across clusters.
- C. Retention is important, but not the core feature for failover.
- D. SSL provides security, not offset coordination.
```

</details>

---

## Question 7

```markdown
What determines which topics are eligible for replication in MM2?
```

**Options**

```markdown
- A. Topics with more than 1 partition
- B. Topics that are marked as "replicable" in metadata
- C. Topics matching the `topics` and `topics.blacklist` regex
- D. All topics are replicated by default
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Partition count doesn't control replication eligibility.
- B. No such metadata flag exists in Kafka.
- C. Correct: MM2 uses regex patterns to include/exclude topics.
- D. Default replication must be explicitly configured.
```

</details>

---

## Question 8

```markdown
What is the purpose of the `emit.heartbeats.enabled` property in MirrorMaker 2?
```

**Options**

```markdown
- A. To emit logs for every heartbeat
- B. To enable cluster metrics
- C. To sync offset commits via heartbeats
- D. To write heartbeat records to the heartbeat topic
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
- A. Not related to logging.
- B. Metrics are handled separately.
- C. Heartbeats do not commit offsets directly.
- D. Correct: This property controls writing heartbeats to the topic.
```

</details>

---

## Question 9

```markdown
What happens if the source and destination clusters have different topic configurations?
```

**Options**

```markdown
- A. MM2 halts replication
- B. MM2 applies destination configs only
- C. MM2 mirrors source topic configuration when auto.create.topics is enabled
- D. Topics are not created
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Replication continues even with differences.
- B. Source config drives behavior, not destination.
- C. Correct: MM2 mirrors source configs when topic auto-creation is enabled.
- D. Topics are created if auto-creation is configured properly.
```

</details>

---

## Question 10

```markdown
Which type of replication is **not** supported out of the box by MirrorMaker 2?
```

**Options**

```markdown
- A. Metadata replication
- B. Offset replication
- C. Schema Registry replication
- D. Topic data replication
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Handled through heartbeat and config topics.
- B. Done through offset sync and translation.
- C. Correct: Schema Registry is not replicated by MM2; must be handled separately.
- D. Core feature of MirrorMaker 2.
```

</details>

---

## Question 11

```markdown
In MirrorMaker 2, what does the `replication.policy.class` control?
```

**Options**

```markdown
- A. The type of compression used
- B. Whether producers are idempotent
- C. How topic names are transformed across clusters
- D. The replication interval
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Compression is set at the producer level.
- B. Not part of MM2 configuration.
- C. Correct: This class transforms topic names during replication.
- D. That’s controlled by poll intervals.
```

</details>

---

## Question 12

```markdown
Which MirrorMaker 2 connector is responsible for offset sync?
```

**Options**

```markdown
- A. MirrorSourceConnector
- B. MirrorCheckpointConnector
- C. MirrorHeartbeatConnector
- D. MirrorMetricsConnector
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Handles the actual topic data replication.
- B. Correct: It creates checkpoints of consumer offsets.
- C. Used to monitor connectivity.
- D. Not a real MM2 connector.
```

</details>

---

## Question 13

```markdown
How can you reduce lag between source and destination clusters in MM2?
```

**Options**

```markdown
- A. Increase `offset.flush.interval.ms`
- B. Reduce number of partitions
- C. Increase the replication frequency by reducing `tasks.max`
- D. Tune `refresh.topics.interval.seconds` and consumer poll settings
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
- A. Increasing flush interval slows syncs.
- B. Fewer partitions reduce parallelism.
- C. Lowering tasks reduces throughput.
- D. Correct: These settings improve sync responsiveness.
```

</details>

---

## Question 14

```markdown
Which tool should you use to translate offsets from the source to the destination cluster?
```

**Options**

```markdown
- A. `kafka-console-consumer`
- B. `kafka-mirror-maker`
- C. `MirrorMakerOffsetTool`
- D. `MirrorTopicLister`
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Console tools don’t do offset mapping.
- B. That’s MM1, not MM2.
- C. Correct: This tool provides offset translation across clusters.
- D. Not a Kafka utility.
```

</details>

---

## Question 15

```markdown
Why might a topic appear in the destination cluster but contain no data?
```

**Options**

```markdown
- A. MM2 was restarted
- B. auto.create.topics.enabled = false
- C. The topic matches the blacklist regex
- D. The heartbeat connector failed
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Restarting MM2 doesn’t prevent replication unless misconfigured.
- B. If the topic exists, auto.create is irrelevant.
- C. Correct: A matching blacklist prevents replication of topic data.
- D. Heartbeat affects monitoring, not actual data flow.
```

</details>

---

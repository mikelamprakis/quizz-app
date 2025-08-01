## Question 1

```markdown
A consumer with `fetch.min.bytes=1024` and `fetch.max.wait.ms=500` polls from a topic where messages arrive at 1KB every 300ms. How many broker roundtrips occur per minute?
```

**Options**
```markdown
- A. 60
- B. 120
- C. 20
- D. 2
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
The consumer waits up to 500ms for 1KB of data (fetch.min.bytes). With messages arriving every 300ms (faster than the wait time), it fetches on every poll call. Assuming 100ms poll intervals (typical), this results in ~120 fetches/minute (60000ms/500ms).

- A. Incorrect: Underestimates fetch frequency
- B. Correct: Accounts for both wait time and poll rate
- C. Incorrect: Overestimates batching
- D. Incorrect: Severely underestimates activity
```

</details>

---

## Question 2

```markdown
In a single-consumer+thread-pool pattern, what happens if the average processing time exceeds `max.poll.interval.ms` for just one partition's records?
```

**Options**
```markdown
- A. Only the lagging partition is reassigned
- B. The entire consumer is kicked from the group
- C. Processing continues with warnings
- D. Kafka automatically increases the timeout
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
`max.poll.interval.ms` is a global consumer setting - violation for any partition causes complete consumer removal from the group.

- A. Incorrect: Rebalance affects all partitions
- B. Correct: Whole consumer is removed
- C. Incorrect: Violations trigger rebalance
- D. Incorrect: Timeouts aren't auto-adjusted
```

</details>

---

## Question 3

```markdown
What is the risk of setting `max.partition.fetch.bytes` significantly higher than `fetch.max.bytes` in a consumer with 100 subscribed partitions?
```

**Options**
```markdown
- A. Broker OOM errors
- B. Skewed partition processing
- C. Consumer thread starvation
- D. Zookeeper connection storms
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Large `max.partition.fetch.bytes` with many partitions can cause a few large partitions to dominate the fetch response, starving smaller ones.

- A. Incorrect: Brokers limit response size via `fetch.max.bytes`
- B. Correct: Leads to uneven partition processing
- C. Incorrect: Threading isn't affected by fetch sizes
- D. Incorrect: Unrelated to Zookeeper
```

</details>

---

## Question 4

```markdown
When using pause()/resume() for backpressure, which metric should trigger pausing to avoid OOM?
```

**Options**
```markdown
- A. `records-lag` metric
- B. Consumer heap usage
- C. Internal queue size
- D. Broker disk utilization
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
Pausing should occur when the internal processing queue nears capacity, before OOM occurs.

- A. Incorrect: Lag indicates consumer speed, not memory pressure
- B. Incorrect: Heap monitoring is too indirect
- C. Correct: Queue size directly reflects backpressure need
- D. Incorrect: Broker metrics don't affect consumer memory
```

</details>

---

## Question 5

```markdown
A consumer with `fetch.min.bytes=1MB` runs against a topic with 100KB/s/partition. How does increasing partitions from 10 to 20 affect fetch efficiency?
```

**Options**
```markdown
- A. Fetch latency decreases by 50%
- B. Fetch frequency doubles
- C. Per-fetch data volume increases 2x
- D. No impact on fetch behavior
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
More partitions means more parallel streams contributing to the min bytes threshold, increasing data per fetch.

- A. Incorrect: Latency depends on slowest partition
- B. Incorrect: Frequency may decrease with larger fetches
- C. Correct: More partitions = more data per fetch
- D. Incorrect: Throughput characteristics change
```

</details>

---

## Question 6

```markdown
In a work queue pattern with manual commits, where should you commit offsets when processing fails?
```

**Options**
```markdown
- A. After the first retry succeeds
- B. At the next successful poll() call
- C. Only after all retries are exhausted
- D. Never commit failed messages
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
For exactly-once semantics, commit only after successful processing (including retries), not on failure.

- A. Correct: Commit only on eventual success
- B. Incorrect: Poll timing is unrelated to processing
- C. Incorrect: Exhaustion means giving up - shouldn't commit
- D. Incorrect: Need to commit progress
```

</details>

---

## Question 7

```markdown
What happens if `max.poll.records` is set lower than the number of records a broker returns in one fetch?
```

**Options**
```markdown
- A. Excess records are discarded
- B. Records are cached for next poll()
- C. Consumer throws BufferUnderflowException
- D. Broker truncates the response
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Kafka caches unconsumed records internally for subsequent polls, maintaining efficiency.

- A. Incorrect: No records are lost
- B. Correct: Records are preserved between polls
- C. Incorrect: No exception occurs
- D. Incorrect: Broker isn't aware of client limits
```

</details>

---

## Question 8

```markdown
Which pattern maintains partition ordering while allowing parallel processing?
```

**Options**
```markdown
- A. Single consumer + thread pool per record
- B. One consumer per thread with partition affinity
- C. Work queue with global commit thread
- D. All patterns preserve ordering
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Only partition-affinity models (one consumer/thread per partition) maintain ordering while parallelizing.

- A. Incorrect: Pool processing may reorder records
- B. Correct: Partition affinity preserves order
- C. Incorrect: Queue workers may process out-of-order
- D. Incorrect: Not all patterns preserve order
```

</details>

---

## Question 9

```markdown
When tuning `fetch.max.wait.ms`, what is the tradeoff between 10ms and 500ms settings?
```

**Options**
```markdown
- A. 10ms: higher CPU vs 500ms: higher latency
- B. 10ms: more duplicates vs 500ms: fewer commits
- C. 10ms: better ordering vs 500ms: weaker consistency
- D. 10ms: less memory vs 500ms: more connections
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
Shorter wait means more frequent empty fetches (CPU overhead), longer wait increases latency.

- A. Correct: Captures the core tradeoff
- B. Incorrect: Unrelated to duplicates/commits
- C. Incorrect: Doesn't affect ordering/consistency
- D. Incorrect: Connection count is unaffected
```

</details>

---

## Question 10

```markdown
A consumer processing 10MB/s suddenly sees throughput drop to 1MB/s. `max.poll.records=1000` and average record size is 10KB. What's the most likely issue?
```

**Options**
```markdown
- A. `fetch.min.bytes` is too low
- B. `max.poll.interval.ms` is too high
- C. Thread pool queue is full
- D. `max.partition.fetch.bytes` is limiting
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
At 10KB/record, 1000 records = ~10MB. Throughput drop suggests backpressure, likely from a full processing queue.

- A. Incorrect: Would affect network efficiency, not throughput
- B. Incorrect: High interval wouldn't reduce throughput
- C. Correct: Queue full would throttle polling
- D. Incorrect: Would manifest as skew, not uniform slowdown
```

</details>

---

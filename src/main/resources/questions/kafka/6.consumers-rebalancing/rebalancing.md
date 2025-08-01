## Question 1

```markdown
During a rebalance with CooperativeStickyAssignor, what happens to partitions that aren't being reassigned?
```

**Options**
```markdown
- A. They are temporarily revoked and reassigned
- B. They remain with their current consumer during the rebalance
- C. They are paused until the rebalance completes
- D. They are automatically committed before reassignment
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Cooperative rebalancing's key improvement is allowing consumers to retain unaffected partitions during reassignment.

- A. Incorrect: Only changing partitions are revoked
- B. Correct: Unaffected partitions stay assigned
- C. Incorrect: Partitions aren't paused unless revoked
- D. Incorrect: Commits aren't automatic in rebalance
```

</details>

---

## Question 2

```markdown
A consumer group with static membership (`group.instance.id`) experiences a network partition that lasts longer than `session.timeout.ms`. What happens when connectivity is restored?
```

**Options**
```markdown
- A. The consumer rejoins silently with its previous assignment
- B. A full rebalance occurs as if it were a new consumer
- C. The consumer is permanently removed from the group
- D. The group coordinator pauses until all members reconnect
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Static membership only prevents rebalances for graceful restarts - network partitions exceeding session timeout still trigger full rebalances.

- A. Incorrect: Session timeout violations force rebalance
- B. Correct: Treated as failure despite static ID
- C. Incorrect: Members aren't permanently removed
- D. Incorrect: Coordinators don't wait indefinitely
```

</details>

---

## Question 3

```markdown
In a group using RangeAssignor with 3 consumers and 6 partitions (p0-p5), what happens when a 4th consumer joins if the topic has 2 new partitions added simultaneously?
```

**Options**
```markdown
- A. The new consumer gets p6-p7, others keep original assignments
- B. All partitions (p0-p7) are completely reassigned
- C. Original consumers keep p0-p5, new consumer gets nothing
- D. p0-p5 are reassigned, p6-p7 go to the new consumer
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
RangeAssignor triggers complete reassignment when either membership or partition count changes.

- A. Incorrect: RangeAssignor doesn't handle additions incrementally
- B. Correct: Full reassignment occurs
- C. Incorrect: All partitions must be reassigned
- D. Incorrect: Assignment isn't split this way
```

</details>

---

## Question 4

```markdown
A consumer implementing `ConsumerRebalanceListener` crashes during `onPartitionsRevoked()`. What is guaranteed about its uncommitted offsets?
```

**Options**
```markdown
- A. They are automatically committed by the group coordinator
- B. They remain at their pre-rebalance position
- C. They are rolled back to the last stable offset
- D. They advance to the high watermark
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Until offsets are explicitly committed (in `onPartitionsRevoked` or elsewhere), they remain at their last committed position.

- A. Incorrect: No auto-commit occurs
- B. Correct: Offsets only move on explicit commit
- C. Incorrect: No rollback occurs
- D. Incorrect: Offsets don't jump ahead
```

</details>

---

## Question 5

```markdown
What is the minimum number of rebalances required when adding N consumers to a group using CooperativeStickyAssignor with no partition count changes?
```

**Options**
```markdown
- A. 1
- B. N
- C. N+1
- D. log(N)
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
Cooperative rebalancing can handle multiple membership changes in a single rebalance event.

- A. Correct: Single rebalance suffices
- B. Incorrect: Not per-consumer
- C. Incorrect: No additional rebalances needed
- D. Incorrect: Not logarithmic
```

</details>

---

## Question 6

```markdown
A consumer group with `session.timeout.ms=10000` and `heartbeat.interval.ms=3000` experiences 50% packet loss. What is the most likely outcome?
```

**Options**
```markdown
- A. No impact - heartbeats will get through eventually
- B. Frequent rebalances as consumers time out
- C. Consumers stall but don't time out
- D. The group coordinator increases timeout automatically
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
With 50% packet loss, heartbeats may fail to arrive within session timeout, triggering false failure detection.

- A. Incorrect: 50% loss is too severe
- B. Correct: Likely to cause timeout violations
- C. Incorrect: Timeouts will occur
- D. Incorrect: Timeouts aren't auto-adjusted
```

</details>

---

## Question 7

```markdown
In a transactional consumer group with `isolation.level=read_committed`, when are aborted transaction messages removed from partition assignments during rebalance?
```

**Options**
```markdown
- A. During the revocation phase
- B. During the assignment phase
- C. After the consumer seeks to committed offsets
- D. They are never removed - consumers filter them
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
Aborted messages remain in the log - consumers skip them during polling based on transaction markers.

- A. Incorrect: Revocation doesn't clean logs
- B. Incorrect: Assignment doesn't modify topics
- C. Incorrect: Seeking doesn't remove messages
- D. Correct: Consumers filter based on markers
```

</details>

---

## Question 8

```markdown
What happens if two consumers with the same `group.instance.id` attempt to join a group simultaneously?
```

**Options**
```markdown
- A. The first consumer wins, the second gets an error
- B. The group coordinator merges their subscriptions
- C. Both are admitted causing duplicate processing
- D. The group enters a permanent rebalance loop
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
Static member IDs must be unique - the coordinator rejects duplicate registrations.

- A. Correct: Second join fails with error
- B. Incorrect: No merging occurs
- C. Incorrect: Duplicates are prevented
- D. Incorrect: Coordinator handles conflicts
```

</details>

---

## Question 9

```markdown
A consumer group using CooperativeStickyAssignor has one consumer processing messages much slower than others. How does this affect rebalance frequency?
```

**Options**
```markdown
- A. No effect - rebalances are membership-triggered
- B. Increases frequency due to heartbeat delays
- C. Increases frequency due to poll timeout violations
- D. Decreases frequency to protect the slow consumer
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
Slow processing may cause `max.poll.interval.ms` violations, triggering rebalances.

- A. Incorrect: Poll timeouts can trigger rebalances
- B. Incorrect: Heartbeats are separate from processing
- C. Correct: Poll timeout violations cause rebalances
- D. Incorrect: Kafka doesn't throttle rebalances
```

</details>

---

## Question 10

```markdown
During a rebalance with 1000 partitions, what is the primary bottleneck in the assignment process?
```

**Options**
```markdown
- A. Network bandwidth between consumers
- B. Group coordinator's CPU for partition arithmetic
- C. Zookeeper's write throughput
- D. Disk I/O on partition leaders
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
The coordinator's CPU becomes the bottleneck when computing large partition assignments.

- A. Incorrect: Consumers don't communicate directly
- B. Correct: Assignment computation is CPU-intensive
- C. Incorrect: Modern Kafka doesn't use Zookeeper for this
- D. Incorrect: Partition leaders aren't involved
```

</details>

---
## Question 1

```markdown
What is the effect of setting `acks=0` in a Kafka producer?
```

**Options**

```markdown
- A. The producer will wait for the broker to acknowledge the message before sending the next one
- B. The producer will wait for the leader and all replicas to acknowledge the message
- C. The producer will not wait for any acknowledgement from the broker
- D. The producer will throw an exception if the broker does not acknowledge the message
```

<details><summary>Response:</summary> 

**Answer:** C

**Explanation:**

```markdown
With `acks=0`, the producer sends data and does not wait for any acknowledgement. It offers the highest throughput but no delivery guarantees.

- A. Describes `acks=1` or `acks=all`
- B. Describes `acks=all`
- C. Correct — no acknowledgements are expected
- D. Incorrect — producer does not throw errors when acks=0
```

</details>

---

## Question 2

```markdown
What is the relationship between `request.timeout.ms` and `delivery.timeout.ms` in a Kafka producer?
```

**Options**

```markdown
- A. `request.timeout.ms` should always be greater than `delivery.timeout.ms`
- B. `delivery.timeout.ms` should always be greater than `request.timeout.ms`
- C. They should always be set to the same value
- D. They are independent and can be set to any value
```

<details><summary>Response:</summary> 

**Answer:** B

**Explanation:**

```markdown
`delivery.timeout.ms` is the total time allowed to deliver a message including all retries. `request.timeout.ms` is per-request. If delivery timeout is less than request timeout, a send may time out before the request does, which is not ideal.

- A. Opposite — would cause premature timeouts.
- B. Correct — ensures retries work within delivery window.
- C. Not necessary, and may cause unintentional issues.
- D. Technically true, but not recommended without understanding the interplay.
```

</details>

---

## Question 3

```markdown
A Kafka producer application needs to send messages to a topic. The messages do not require any particular order. Which of the following properties are mandatory in the producer configuration? (Select two)
```

**Options**

```markdown
- A. compression.type
- B. partitioner.class
- C. bootstrap.servers
- D. key.serializer
- E. value.serializer
- F. client.id
```

<details><summary>Response:</summary> 

**Answer:** C, E

**Explanation:**

```markdown
`bootstrap.servers` is required to connect to Kafka brokers, and `value.serializer` is needed to serialize the message values. All others are optional or have defaults.

- A. Optional performance setting
- B. Optional for custom partitioning
- C. Required — without it, producer can't connect
- D. Only needed if you use keys
- E. Required — must serialize value
- F. Optional identifier for logs/metrics
```

</details>

---

## Question 4

```markdown
What is the effect of setting `acks=0` in a Kafka producer?
```

**Options**

```markdown
- A. The producer will wait for the broker to acknowledge the message before sending the next one
- B. The producer will wait for the leader and all replicas to acknowledge the message
- C. The producer will not wait for any acknowledgement from the broker
- D. The producer will throw an exception if the broker does not acknowledge the message
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
`acks=0` means fire-and-forget. No confirmation is expected, maximizing throughput but sacrificing reliability.

- A. Incorrect: That’s `acks=1` or `acks=all`.
- B. Incorrect: That’s `acks=all`.
- C. Correct: It doesn’t wait for any acknowledgment.
- D. Incorrect: No exception is thrown since no ack is expected.
```

</details>

---

## Question 5

```markdown
What is the relationship between `request.timeout.ms` and `delivery.timeout.ms` in a Kafka producer?
```

**Options**

```markdown
- A. `request.timeout.ms` should always be greater than `delivery.timeout.ms`
- B. `delivery.timeout.ms` should always be greater than `request.timeout.ms`
- C. They should always be set to the same value
- D. They are independent and can be set to any value
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
`request.timeout.ms` governs how long to wait for one request, while `delivery.timeout.ms` is the total retry budget. The latter must be greater.

- A. Incorrect: The opposite is recommended.
- B. Correct: `delivery.timeout.ms` includes potential retries.
- C. Incorrect: It could cause premature failures.
- D. Technically true, but not advised in practice.
```

</details>

---

## Question 6

```markdown
A Kafka producer application needs to send messages to a topic. The messages do not require any particular order. Which of the following properties are mandatory in the producer configuration? (Select two)
```

**Options**

```markdown
- A. `compression.type`
- B. `partitioner.class`
- C. `bootstrap.servers`
- D. `key.serializer`
- E. `value.serializer`
- F. `client.id`
```

<details><summary>Response:</summary>

**Answer:** C, E

**Explanation:**

```markdown
To connect and serialize messages, `bootstrap.servers` and `value.serializer` are required.

- A. Optional: Enhances efficiency, not required.
- B. Optional: Default partitioner is used otherwise.
- C. Required: Without this, no broker connection.
- D. Optional: Only needed if you're sending keys.
- E. Required: Values must be serialized.
- F. Optional: Useful for logging/monitoring, not mandatory.
```

</details>

---

## Question 7

```markdown
What is the purpose of setting `compression.type` in a Kafka producer configuration?
```

**Options**

```markdown
- A. To specify the compression algorithm used when sending data to Kafka
- B. To specify the compression algorithm used when storing data on Kafka brokers
- C. To enable or disable compression for the producer
- D. To set the compression level for the producer
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
The producer compresses records before transmission using the specified algorithm (e.g. `gzip`, `lz4`, `zstd`, etc.).

- A. Correct: It's about producer-to-broker compression.
- B. Misleading: Brokers store whatever is received.
- C. False: Compression is not simply on/off; it's about type.
- D. False: Kafka doesn’t let you tune compression level.
```

</details>

---

## Question 8

```markdown
What is the relationship between `linger.ms` and `request.timeout.ms` in the Kafka producer configuration?
```

**Options**

```markdown
- A. They are redundant settings that control the same thing
- B. `linger.ms` should always be set higher than `request.timeout.ms`
- C. `request.timeout.ms` should always be set higher than `linger.ms`
- D. They control independent aspects of the producer behavior
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
`linger.ms` is how long the producer waits to fill a batch before sending.
`request.timeout.ms` is how long the producer waits for a broker acknowledgment.

To avoid premature timeouts, `request.timeout.ms` should **always** be set **higher** than `linger.ms`.

- A is incorrect — they control distinct stages (before send vs after send).
- B is backwards — the opposite is true.
- D is partially true, but misses the coordination requirement.
```

</details>

---

## Question 9

```markdown
You want to produce messages to a Kafka topic using a Java client. Which of the following is NOT a required configuration for the producer?
```

**Options**

```markdown
- A. bootstrap.servers
- B. key.serializer
- C. value.serializer
- D. partitioner.class
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
Kafka producers require `bootstrap.servers`, `key.serializer`, and `value.serializer`.
- A, B, and C are essential.
- D is optional – Kafka uses a default partitioner unless a custom one is specified.
```

</details>

---

## Question 10

```markdown
What is the relationship between the `acks` parameter and the `request.required.acks` parameter in Kafka?
```

**Options**

```markdown
- A. They are the same parameter, just with different names
- B. `acks` is used in the producer configuration, while `request.required.acks` is used in the consumer configuration
- C. `acks` is used in the new producer API, while `request.required.acks` is used in the old producer API
- D. They are completely unrelated parameters
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
`acks` and `request.required.acks` serve the same purpose:

- A. Not quite – naming reflects API version.
- B. False – both are producer configs.
- C. True – `acks` is for the new producer API; `request.required.acks` was used in the legacy one.
- D. False – they are related.
```

</details>

## Question 11

```markdown
What happens if the Kafka producer exhausts its buffer memory while sending messages?
```

**Options**

```markdown
- A. The producer will block and wait until buffer memory becomes available
- B. The producer will start discarding the oldest messages to free up buffer memory
- C. The producer will start discarding the newest messages to free up buffer memory
- D. The producer will throw an exception and stop sending messages
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
If buffer memory fills up, the producer blocks until space is available or `max.block.ms` is exceeded.

- A. Correct – default behavior is blocking.
- B. Incorrect – Kafka doesn’t evict messages from buffer.
- C. Incorrect – no discarding of newest messages.
- D. Partially true, but only after blocking timeout.
```

</details>

---

## Question 12

```markdown
How does the `max.in.flight.requests.per.connection` setting affect the behavior of the Kafka producer when `acks=1`?
```

**Options**

```markdown
- A. It specifies the maximum number of unacknowledged requests allowed per broker connection
- B. It specifies the maximum number of requests that can be sent to the broker concurrently
- C. It specifies the maximum number of messages that can be buffered in the producer's memory
- D. It has no effect when `acks=1`
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
This config limits the number of unacknowledged requests per connection, which can affect ordering if retries happen.

- A. Correct – defines number of unacknowledged sends.
- B. Close, but wording is vague – not about concurrency alone.
- C. Incorrect – that’s `buffer.memory`.
- D. Incorrect – setting still matters with `acks=1`.
```

</details>

---

## Question 13

```markdown
What is the purpose of the `client.id` setting in the Kafka producer and consumer configurations?
```

**Options**

```markdown
- A. To specify a unique identifier for the client within a Kafka cluster
- B. To set the maximum number of requests the client can send or receive
- C. To determine the compression type used for message production or consumption
- D. To control the maximum amount of memory the client can use for buffering
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
The `client.id` helps uniquely identify clients in logs and metrics. It is useful for monitoring and debugging but has no impact on message delivery, memory usage, or compression.

- A. Correct – `client.id` is used for tracking/logging.
- B. Incorrect – not related to throughput or rate limits.
- C. Incorrect – compression is configured separately.
- D. Incorrect – buffering is controlled by other configs.
```

</details>

---

## Question 14

```markdown
What happens if multiple Kafka clients use the same `client.id` value?
```

**Options**

```markdown
- A. The clients will share the same configuration and connection pooling
- B. The clients will be treated as a single logical client by the Kafka brokers
- C. The behavior is undefined, and it may lead to unexpected results or errors
- D. The Kafka brokers will reject the connection attempts from clients with duplicate `client.id`
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
Using the same `client.id` across multiple clients can cause confusion in monitoring and metrics. Kafka does not enforce uniqueness, and while it won’t reject connections, it may lead to misattributed logs or unpredictable behavior.

- A. Incorrect – no configuration or connection sharing happens.
- B. Incorrect – brokers track connections independently.
- C. Correct – duplicate IDs confuse monitoring/logs.
- D. Incorrect – Kafka allows duplicate IDs.
```

</details>

---

## Question 15

```markdown
What is returned by a `producer.send()` call in the Java API?
```

**Options**

```markdown
- A. A boolean
- B. Unit
- C. Future
- D. Future object
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
`producer.send()` returns a `Future<RecordMetadata>` which can be used to track send completion or exceptions.

- A. Not a boolean.
- B. Not unit (void).
- C. Inexact — should specify Future type.
- D. Correct — returns a Future object.
```

</details>

---


## Question 1

```markdown
Which of the following best describes Avro in the context of Kafka?
```

**Options**

```markdown
- A. A message queue system
- B. A schema registry implementation
- C. A compact binary data serialization format
- D. A Kafka consumer tool
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Kafka is the message queue, not Avro.
- B. Schema Registry is a separate service.
- C. Correct – Avro is a binary serialization format with schema support.
- D. Avro is unrelated to consumption tooling directly.
```

</details>

---

## Question 2

```markdown
What role does the Schema Registry play in Avro serialization?
```

**Options**

```markdown
- A. It stores Avro-encoded Kafka messages
- B. It compresses Avro data before sending
- C. It stores and serves Avro schemas for (de)serialization
- D. It converts Avro to JSON for human readability
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Messages are stored in Kafka, not the Schema Registry.
- B. Compression is not Schema Registry's role.
- C. Correct – It stores and provides Avro schemas to producers and consumers.
- D. Human-readability is not its concern.
```

</details>

---

## Question 3

```markdown
Which component adds the schema ID to an Avro-encoded Kafka message?
```

**Options**

```markdown
- A. Kafka Broker
- B. Schema Registry itself
- C. KafkaAvroSerializer
- D. KafkaAvroDeserializer
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Brokers pass messages but don’t manage schema IDs.
- B. The registry stores schemas but doesn’t write to messages.
- C. Correct – KafkaAvroSerializer encodes the schema ID with the message.
- D. Deserializer reads the ID but doesn’t write it.
```

</details>

---

## Question 4

```markdown
What does the KafkaAvroDeserializer do using the schema ID in the message?
```

**Options**

```markdown
- A. It compresses the data
- B. It skips deserialization if ID is not found
- C. It fetches the corresponding schema from the Schema Registry
- D. It returns the raw Avro bytes to the consumer
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. No compression is performed.
- B. It attempts to resolve schema ID via registry.
- C. Correct – It retrieves the schema based on ID to deserialize the message.
- D. It converts Avro bytes into usable Java objects, not raw data.
```

</details>

---

## Question 5

```markdown
Why is Avro considered more efficient than JSON in Kafka applications?
```

**Options**

```markdown
- A. Avro is easier to read for humans
- B. Avro schemas are embedded fully in every message
- C. Avro messages are smaller due to compact binary format
- D. Avro requires no schema definition
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. JSON is more human-readable than Avro.
- B. Only the schema ID is embedded, not the full schema.
- C. Correct – Avro uses a compact binary format, making messages smaller.
- D. Avro **requires** a schema definition.
```

</details>

---

## Question 6

```markdown
Which of the following is required to produce Avro messages to a Kafka topic?
```

**Options**

```markdown
- A. KafkaJsonProducer
- B. Avro schema and KafkaAvroSerializer
- C. Kafka XML encoder
- D. Schema Registry consumer plugin
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. JSON is not used for Avro messages.
- B. Correct – You need an Avro schema and KafkaAvroSerializer to serialize data.
- C. XML is not supported natively in Kafka.
- D. Schema Registry doesn’t use plugins for this.
```

</details>

---

## Question 7

```markdown
When sending an Avro-encoded message, what does the first byte of the message typically indicate?
```

**Options**

```markdown
- A. Kafka partition number
- B. Message priority
- C. Magic byte to identify Avro encoding
- D. Compression level used
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Partition info is handled by Kafka metadata.
- B. Message priority isn’t a Kafka concept.
- C. Correct – The first byte is a magic byte (usually 0) to mark the Avro format.
- D. Compression info is not part of Avro’s schema structure.
```

</details>

---

## Question 8

```markdown
What happens if a consumer tries to deserialize an Avro message with a different schema than the one used to serialize it?
```

**Options**

```markdown
- A. The consumer automatically adjusts to the new schema
- B. The consumer uses fallback schema from local cache
- C. The deserialization fails unless schemas are compatible
- D. Kafka retries the message with a corrected schema
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Schema compatibility needs to be enforced, not automatic.
- B. Cache is used, but compatibility still matters.
- C. Correct – If schemas are incompatible, deserialization fails.
- D. Kafka doesn't retry with schema corrections.
```

</details>

---

## Question 9

```markdown
Where is the Avro schema stored when a message is serialized with KafkaAvroSerializer?
```

**Options**

```markdown
- A. Inside the Kafka topic itself
- B. In ZooKeeper
- C. In the Schema Registry under a subject name
- D. On the Kafka consumer host
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Only schema ID is in the topic, not full schema.
- B. ZooKeeper is not used for schema storage.
- C. Correct – Schemas are registered and stored in Schema Registry under subjects.
- D. Consumers retrieve schemas but don't store them permanently.
```

</details>

---

## Question 10

```markdown
What does the "subject" in Schema Registry represent when working with Avro data?
```

**Options**

```markdown
- A. A Kafka ACL group
- B. The schema namespace
- C. The name under which a schema is registered (usually topic-value or topic-key)
- D. A Kafka broker identifier
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. ACL groups are unrelated.
- B. Namespace is part of the schema but not the subject.
- C. Correct – A subject is the key used to register and version schemas (e.g., `orders-value`).
- D. Brokers are not involved in schema registration.
```

</details>

## Question 11

```markdown
Which schema type is supported by Confluent Schema Registry but not by Apache Avro?
```

**Options**

```markdown
- A. Protobuf
- B. Thrift
- C. JSON Schema
- D. XML Schema
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
Confluent Schema Registry supports JSON Schema and Protobuf, whereas Apache Avro supports only Avro.

- A. Supported by Schema Registry but not unique to it
- B. Not supported
- C. Correct — unique to Schema Registry
- D. Not supported
```

</details>

---

## Question 12

```markdown
In the context of Confluent Schema Registry, what is the main advantage of using Avro over JSON Schema?
```

**Options**

```markdown
- A. Avro schemas are human-readable
- B. Avro provides a compact and fast binary serialization format
- C. Avro does not require schema registration
- D. Avro supports all JSON types natively
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Avro is compact and optimized for performance due to its binary format.

- A. JSON is more human-readable than Avro
- B. Correct — binary serialization is fast and compact
- C. Avro does require schema registration
- D. JSON types differ from Avro’s type system
```

</details>

---

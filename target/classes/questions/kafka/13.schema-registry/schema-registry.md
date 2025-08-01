## Question 1

```markdown
What is the primary purpose of Kafka's Schema Registry?
```

**Options**

```markdown
- A. To compress Kafka messages using schemas
- B. To replicate topics across Kafka clusters
- C. To store and manage the structure of data (schemas) used in Kafka
- D. To act as a backup system for Kafka brokers
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Compression is unrelated to schema registry.
- B. Topic replication is handled by Kafka, not the schema registry.
- C. Correct – Schema Registry stores and manages schemas for Kafka topics.
- D. Schema Registry is not a backup system.
```

</details>

---

## Question 2

```markdown
Why is schema management important in a Kafka-based system?
```

**Options**

```markdown
- A. It eliminates the need for producers and consumers
- B. It ensures that producers and consumers understand the structure of data
- C. It provides encryption for message payloads
- D. It helps increase topic throughput
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Producers and consumers are still essential.
- B. Correct – Schema management ensures data structure consistency between systems.
- C. Encryption is unrelated to schema management.
- D. Throughput is not the main goal of schema registry.
```

</details>

---

## Question 3

```markdown
Which data serialization format is most commonly used with Kafka Schema Registry?
```

**Options**

```markdown
- A. JSON
- B. XML
- C. Avro
- D. CSV
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. JSON can be used, but it's not the most common with Schema Registry.
- B. XML is not typically used in Kafka.
- C. Correct – Avro is the most popular format with Schema Registry.
- D. CSV lacks schema support and is rarely used in this context.
```

</details>

---

## Question 4

```markdown
What happens when a Kafka producer uses the Schema Registry?
```

**Options**

```markdown
- A. The schema is embedded directly in the topic
- B. The schema is sent to consumers via a REST API
- C. The producer registers the schema and sends only a schema ID with the message
- D. The schema is stored on each Kafka broker
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. The schema itself is not embedded in every message.
- B. REST API is for management, not runtime delivery.
- C. Correct – The schema is registered, and only its ID is sent with the message.
- D. Brokers don't store schema information.
```

</details>

---

## Question 5

```markdown
What problem does Schema Registry solve in a distributed system?
```

**Options**

```markdown
- A. Data encryption across services
- B. Service discovery between microservices
- C. Data format agreement between producers and consumers
- D. Load balancing Kafka consumers
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Schema Registry doesn't provide encryption.
- B. It’s not a service discovery tool.
- C. Correct – It ensures all parties use the same data format.
- D. Load balancing is handled by Kafka consumer groups.
```

</details>

---

## Question 6

```markdown
In the context of Kafka, what is a schema?
```

**Options**

```markdown
- A. A Kafka topic configuration
- B. A set of rules for how data is compressed
- C. A definition of the structure of the data being transmitted
- D. A JSON object describing consumer offsets
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Topics have configs but are unrelated to schema.
- B. Schemas define structure, not compression rules.
- C. Correct – Schemas define the structure of the data.
- D. Consumer offsets are unrelated to schemas.
```

</details>

---

## Question 7

```markdown
Which of the following is NOT a benefit of using Schema Registry?
```

**Options**

```markdown
- A. Ensures schema compatibility
- B. Supports multiple data formats like Avro and Protobuf
- C. Automatically balances Kafka partition load
- D. Enables safe schema evolution
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Compatibility is a key feature of Schema Registry.
- B. It supports Avro, Protobuf, and JSON Schema.
- C. Correct – Partition load balancing is a Kafka feature, not Schema Registry.
- D. Schema Registry enables controlled schema evolution.
```

</details>

---

## Question 8

```markdown
Where does the Schema Registry store schema definitions?
```

**Options**

```markdown
- A. In ZooKeeper
- B. Inside Kafka topics
- C. In a separate metadata service
- D. In each producer and consumer application
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. ZooKeeper is used for broker metadata, not schemas.
- B. Correct – Schema Registry stores schemas in a special Kafka topic.
- C. It is not an external database or metadata service.
- D. Apps don’t carry schema definitions internally.
```

</details>

---

## Question 9

```markdown
How does Schema Registry help with schema evolution?
```

**Options**

```markdown
- A. By rewriting old messages to match the new schema
- B. By validating new schemas against old ones using compatibility rules
- C. By preventing producers from sending new schema versions
- D. By broadcasting schema updates to all consumers
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Messages are immutable in Kafka; they aren't rewritten.
- B. Correct – Schema Registry uses compatibility rules to validate changes.
- C. It allows schema evolution, not blocks it.
- D. Consumers fetch schemas as needed, not via broadcast.
```

</details>

---

## Question 10

```markdown
Which system component is primarily responsible for serializing and deserializing data using the Schema Registry?
```

**Options**

```markdown
- A. Kafka brokers
- B. The schema registry itself
- C. KafkaAvroSerializer and KafkaAvroDeserializer
- D. Zookeeper
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Brokers handle message passing, not (de)serialization.
- B. The registry only stores schemas.
- C. Correct – These classes handle Avro (de)serialization with the registry.
- D. Zookeeper is unrelated to schema handling.
```

</details>



## Question 11

```markdown
When using the Confluent Kafka Distribution, where does the schema registry reside?
```

**Options**

```markdown
- A. As an in-memory plugin on your Kafka broker
- B. As an in-memory plugin on your Kafka Connect worker
- C. As an in-memory plugin on your Zookeeper cluster
- D. As a separate JVM component
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
The Schema Registry is a separate application that provides a RESTful interface for storing and retrieving Avro schemas.

- A is incorrect because the Schema Registry is not a plugin within Kafka brokers.
- B is incorrect because it is not part of Kafka Connect workers.
- C is incorrect because it does not run within Zookeeper.
- D is correct because the Schema Registry runs as its own JVM process, separate from Kafka brokers, Connect, or Zookeeper.
```

</details>

---

## Question 12

```markdown
What is the purpose of the Confluent Schema Registry in a Kafka ecosystem?
```

**Options**

```markdown
- A. To store and manage Avro schemas for Kafka messages
- B. To provide a REST API for producing and consuming Kafka messages
- C. To handle authentication and authorization for Kafka clients
- D. To monitor and manage Kafka clusters and their performance
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
The Schema Registry's main role is to store and manage Avro schemas for Kafka messages. It enables producers and consumers to reference schemas by ID, ensures schema compatibility during evolution, and reduces payload size by avoiding full-schema repetition.

- A. ✅ Correct – Centralized schema management
- B. ❌ Schema Registry doesn't produce/consume data
- C. ❌ Handled by Kafka brokers, not Schema Registry
- D. ❌ Monitoring is done via other tools (e.g., Confluent Control Center)
```

</details>

---

## Question 13

```markdown
Which configuration is used to define the schema registry URL in Kafka clients?
```

**Options**

```markdown
- A. schema.registry.url
- B. schema.registry.endpoint
- C. schema.registry.address
- D. schema.registry.host
```

<details><summary>Response:</summary>

**Answer:** A

**Explanation:**

```markdown
The configuration `schema.registry.url` is used to specify the URL of the Confluent Schema Registry in Kafka clients. This URL is necessary for the clients to connect to the Schema Registry and retrieve the schemas.

- A. Correct configuration key for specifying the registry URL
- B. Not a valid config key
- C. Not recognized by clients
- D. Not a supported property
```

</details>

---

## Question 14

```markdown
What is the primary purpose of a subject in the Confluent Schema Registry?
```

**Options**

```markdown
- A. To group schemas by type (Avro, Protobuf, JSON Schema)
- B. To manage versions of a schema for a specific topic or entity
- C. To specify the schema storage location
- D. To define the security policies for accessing schemas
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
In the Schema Registry, a subject is used to manage schema versions for a particular topic or data type.

- A. Grouping by type is not the purpose of a subject
- B. Correct — subjects track versioned schemas
- C. Storage location is handled internally, not by subject
- D. Access control is configured separately
```

</details>

---

## Question 1

```markdown
Where does Confluent Schema Registry store the registered schema information?
```

**Options**

```markdown
- A. In Zookeeper under the `/schemas` znode
- B. In a special Kafka topic named `_schemas`
- C. In a relational database configured in Schema Registry
- D. In the Kafka broker's `schema` directory on disk
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
Confluent Schema Registry uses a special Kafka topic named `_schemas` to store the registered schema information.

- A. Incorrect – Schema data is not stored in Zookeeper.
- B. Correct – The `_schemas` topic is used internally by Schema Registry.
- C. Incorrect – No external database is used by default.
- D. Incorrect – Brokers don’t persist schema data to disk in that way.
```

</details>

---

## Question 2

```markdown
What serialization formats are supported by the Confluent Schema Registry for storing schemas? (Select all that apply)
```

**Options**

```markdown
- A. Avro
- B. Protobuf
- C. JSON Schema
- D. XML Schema
- E. Thrift
```

<details><summary>Response:</summary>

**Answer:** A, B, C

**Explanation:**

```markdown
Schema Registry supports Avro, Protobuf, and JSON Schema formats.

- A. Correct – Most common format supported.
- B. Correct – Supported by Schema Registry.
- C. Correct – Also supported.
- D. Incorrect – XML Schema is not supported.
- E. Incorrect – Thrift is not supported.
```

</details>

---

## Question 3

```markdown
Which of the following programming languages have official client libraries for interacting with the Confluent Schema Registry? (Select three)
```

**Options**

```markdown
- A. Java
- B. Python
- C. Go
- D. C++
- E. JavaScript
- F. Ruby
```

<details><summary>Response:</summary>

**Answer:** A, B, C

**Explanation:**

```markdown
Official clients are available for Java, Python, and Go.

- A. Correct – Java client is officially supported.
- B. Correct – Python client via `confluent-kafka`.
- C. Correct – Go client exists officially.
- D. Incorrect – No official C++ client.
- E. Incorrect – JavaScript can use REST, but no official client.
- F. Incorrect – Ruby also must use REST APIs.
```

</details>

---
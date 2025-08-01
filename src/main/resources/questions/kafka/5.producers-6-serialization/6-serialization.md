## Question 1

```markdown
Which of the following is true about the relationship between producers and consumers in Kafka?
```

**Options**

```markdown
- A. Producers and consumers must use the same serialization format
- B. Producers and consumers must be written in the same programming language
- C. Producers and consumers are decoupled by the Kafka topic
- D. Producers must know about the consumers to send messages to them
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
Kafka decouples producers and consumers via topics.

- A. False – Kafka supports many serialization formats.
- B. False – Kafka is language-agnostic.
- C. True – Producers and consumers operate independently through topics.
- D. False – Producers don’t know or care about consumers.
```

</details>

---

## Question 2

```markdown
Which of the following serializers is most appropriate when schema evolution and compact binary format are both important?
```

**Options**

```markdown
- A. StringSerializer
- B. KafkaJsonSchemaSerializer
- C. KafkaAvroSerializer
- D. ByteArraySerializer
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. StringSerializer: No schema support, not suitable for evolution.
- B. KafkaJsonSchemaSerializer: Human-readable but weaker schema enforcement.
- C. KafkaAvroSerializer: Supports schema evolution and compact binary format.
- D. ByteArraySerializer: No schema support at all.
```

</details>

---

## Question 3

```markdown
Which built-in Kafka serializer is best suited for sending plain log messages or readable text?
```

**Options**

```markdown
- A. KafkaAvroSerializer
- B. StringSerializer
- C. KafkaProtobufSerializer
- D. ByteArraySerializer
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Avro: Not human-readable, requires schema.
- B. StringSerializer: Perfect for simple text or logs.
- C. Protobuf: Compact, not readable.
- D. ByteArraySerializer: Low-level, not readable.
```

</details>

---

## Question 4

```markdown
What is a potential downside of using JSON serialization in Kafka?
```

**Options**

```markdown
- A. It cannot be used with a Schema Registry.
- B. It’s too compact and hard to debug.
- C. It lacks built-in schema validation and evolution.
- D. It only works with Kafka Streams.
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Incorrect – JSON can be used with Schema Registry (optional).
- B. Incorrect – JSON is actually human-readable.
- C. Correct – JSON lacks strict schema enforcement unless wrapped with Schema Registry logic.
- D. Incorrect – JSON is not tied to Kafka Streams only.
```

</details>

---

## Question 5

```markdown
Which interface must a custom Kafka serializer implement?
```

**Options**

```markdown
- A. java.io.Serializable
- B. org.apache.kafka.common.Producer
- C. org.apache.kafka.clients.producer.ProducerInterceptor
- D. org.apache.kafka.common.serialization.Serializer
```

<details><summary>Response:</summary>

**Answer:** D

**Explanation:**

```markdown
- A. Serializable is unrelated to Kafka.
- B. Producer is the producer class, not for serializers.
- C. ProducerInterceptor is for intercepting, not serialization.
- D. Serializer is the required interface for custom serializers.
```

</details>

---

## Question 6

```markdown
Which serialization format is developed by Google and known for performance and schema strictness?
```

**Options**

```markdown
- A. Avro
- B. Protobuf
- C. JSON
- D. YAML
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Avro is by Apache, not Google.
- B. Protobuf is Google’s format, compact and fast.
- C. JSON is human-readable, not as fast or strict.
- D. YAML is not commonly used with Kafka producers.
```

</details>

---

## Question 7

```markdown
Which of the following serializers is most human-readable?
```

**Options**

```markdown
- A. KafkaProtobufSerializer
- B. KafkaAvroSerializer
- C. KafkaJsonSchemaSerializer
- D. ByteArraySerializer
```

<details><summary>Response:</summary>

**Answer:** C

**Explanation:**

```markdown
- A. Protobuf is binary and not readable.
- B. Avro is compact but not human-friendly.
- C. JSON is readable and widely used.
- D. ByteArray is raw binary.
```

</details>

---

## Question 8

```markdown
Which combination is valid for configuring both key and value as plain text?
```

**Options**

```markdown
- A. key.serializer=KafkaAvroSerializer, value.serializer=StringSerializer
- B. key.serializer=StringSerializer, value.serializer=StringSerializer
- C. key.serializer=ByteArraySerializer, value.serializer=KafkaJsonSchemaSerializer
- D. key.serializer=IntegerSerializer, value.serializer=KafkaProtobufSerializer
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Mixing Avro and String may cause confusion.
- B. Correct – both key and value are plain text.
- C. ByteArray and JSON are valid, but not plain text.
- D. Integer and Protobuf are both binary formats.
```

</details>

---

## Question 9

```markdown
Why is Avro commonly used for internal messaging in Kafka?
```

**Options**

```markdown
- A. It's human-readable and easy to debug
- B. It supports schema evolution and is compact
- C. It is the only supported format by Kafka
- D. It doesn’t require a Schema Registry
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Avro is not human-readable.
- B. Correct – schema evolution + compact size = great for internal systems.
- C. Kafka supports many formats.
- D. Avro typically does use Schema Registry.
```

</details>

---

## Question 10

```markdown
Which format would be least appropriate for strongly typed microservices communicating in a high-performance environment?
```

**Options**

```markdown
- A. Protobuf
- B. JSON
- C. Avro
- D. Custom binary serializer
```

<details><summary>Response:</summary>

**Answer:** B

**Explanation:**

```markdown
- A. Protobuf is ideal in this case.
- B. JSON is less performant and loosely typed.
- C. Avro is compact and supports typing.
- D. Custom binary serializer can be highly optimized.
```

</details>

---

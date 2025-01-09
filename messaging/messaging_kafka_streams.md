# Table of Contents

1. [Kafka Streams: Stateless Transformations, Aggregations, Terminal Operations, Writing to Topics, and Joins](#kafka-streams-stateless-transformations-aggregations-terminal-operations-writing-to-topics-and-joins)
2. [Stateless Transformations](#stateless-transformations)
3. [Aggregations](#aggregations)
4. [Terminal Operations](#terminal-operations)
5. [Writing to Kafka Topics](#writing-to-kafka-topics)
6. [Kafka Streams Joins](#kafka-streams-joins)
7. [Summary](#summary)

# Kafka Streams: Stateless Transformations, Aggregations, Terminal Operations, Writing to Topics, and Joins

Kafka Streams is a powerful library for building real-time data processing pipelines. It provides mechanisms for applying **stateless transformations**, **aggregations**, **terminal operations**, **writing data to topics**, and **joining streams and tables**, enabling you to process and transform data streams efficiently. Below is a comprehensive overview of these concepts.

---

## **Stateless Transformations**

Stateless transformations are lightweight operations where each record is processed independently, without requiring state or coordination between records. These transformations are ideal for tasks like filtering, enrichment, or restructuring data.

#### Common Stateless Transformations:

1. **Map**  
   Transforms each record into a new record by modifying the key, value, or both.  
   *Example*:
    - Input: ("user1", "login").
    - Transformation: Append "processed_" to the value.
    - Output: ("user1", "processed_login").

2. **FlatMap**  
   Splits a single record into multiple records.  
   *Example*:
    - Input: A record with value "apple,banana".
    - Transformation: Split into two records.
    - Output: ("key", "apple") and ("key", "banana").

3. **Filter**  
   Removes records that do not meet a specified condition.  
   *Example*:
    - Input: A record with a value of 100.
    - Transformation: Filter out records where the value is greater than 50.
    - Output: The record is discarded.

4. **SelectKey**  
   Modifies the key of each record while keeping the value unchanged.  
   *Example*:
    - Input: ("user1", "click").
    - Transformation: Change the key to the first letter of the user ID.
    - Output: ("u", "click").

5. **Foreach**  
   Executes a side effect for each record without altering or creating a new stream.  
   *Example*:
    - Input: ("user1", "click") and ("user2", "login").
    - Action: Log each record to a monitoring system or send a notification.
    - Output: No change to the stream, but actions (e.g., logging) are performed.

**Important Note**:  
`Foreach` is a **terminal operation** and does not produce a new stream. As such, **you cannot write to a Kafka topic directly after using `foreach`**. If you need to write records to a topic, you should use transformations like `map` or `filter` to create a new stream, then write that stream using the `to()` method.

---

## **Aggregations**

Aggregations are stateful operations that group and combine records by their keys. These operations maintain state to perform summarization, counting, or custom computations.

#### Common Aggregation Operations:

1. **GroupByKey**  
   Groups records by their existing keys.  
   *Example*:
    - Input: ("user1", "click") and ("user1", "view").
    - Grouped Output: {"user1": ["click", "view"]}.

2. **Reduce**  
   Combines multiple records for the same key using a reduction function.  
   *Example*:
    - Input: ("user1", 5) and ("user1", 3).
    - Reduction: Sum the values.
    - Output: ("user1", 8).

3. **Count**  
   Counts the number of records for each key.  
   *Example*:
    - Input: ("user1", "click"), ("user1", "view"), ("user2", "click").
    - Output: {"user1": 2, "user2": 1}.

4. **Aggregate**  
   Performs custom computations to aggregate records for a key.  
   *Example*:
    - Input: ("user1", 5) and ("user1", 10).
    - Aggregation: Calculate the average for each key.
    - Output: {"user1": 7.5}.

5. **Windowed Aggregations**  
   Groups records into fixed time intervals (e.g., 5 minutes) before applying aggregation.  
   *Example*:
    - Input: Events with timestamps in a 5-minute window.
    - Aggregation: Count events in each window.
    - Output: {"window1": 50 events, "window2": 75 events}.

---

## **Terminal Operations**

Terminal operations are special operations that mark the end of a processing pipeline. They do not return a new stream for further processing and are typically used for performing side effects, materializing data, or writing results to Kafka topics.

#### Key Terminal Operations:

1. **Foreach**  
   Executes a side effect for each record in the stream (e.g., logging or sending notifications).  
   *Example*:
    - Input: ("user1", "click").
    - Action: Log the record to a monitoring system.
    - Output: The stream remains unchanged, but the action is performed.

2. **To**  
   Writes the resulting stream to a Kafka topic.  
   *Example*:
    - Input: A stream of transformed records.
    - Output: Records are written to the topic "processed_topic".

3. **ToTable**  
   Converts a `KStream` into a `KTable`.  
   *Example*:
    - Input: A stream of transactions.
    - Output: A materialized table with the latest state of each key.

4. **Print**  
   Prints the records in a stream to the console for debugging purposes.  
   *Example*:
    - Input: A stream of events.
    - Output: Events are printed to the console as they are processed.

5. **Process**  
   Allows you to write custom logic for processing records using the low-level Processor API.  
   *Example*:
    - Input: Stream of messages.
    - Action: Apply custom logic to filter and enrich records.
    - Output: Records are sent to an external system, but no new stream is returned.

---

## **Writing to Kafka Topics**

To persist processed data back to Kafka, you should use the `to()` method, which writes the output of a transformation or aggregation to a Kafka topic. This is the standard way to persist processed records while maintaining Kafka Streams' built-in guarantees (e.g., fault tolerance and scalability).

#### Why Not Use `Foreach` for Writing to Topics?
While you can technically use `foreach` with a manual Kafka producer to write records to a topic, this is discouraged because:
- It bypasses Kafka Streams' flow control and fault-tolerance mechanisms.
- It introduces inefficiencies and increases complexity.
- It is harder to manage retries and backpressure manually.

Instead, use `to()` after applying a transformation or aggregation to write to a topic declaratively.

---

## **Kafka Streams Joins**

Kafka Streams provides several types of joins that allow you to combine data from two different streams or a stream and a table based on a common key. Joins are useful for enriching data or combining related records for more complex processing.

#### Types of Joins:

1. **Stream-Stream Join**
    - Combines two streams of data by joining records based on a common key.
    - **Inner Join**: Records are joined only if they have matching keys in both streams.
    - **Left Join**: Joins records from the left stream with matching records from the right stream. If there is no match in the right stream, the left stream record is still included.
    - **Outer Join**: Joins all records from both streams, including those that don't have matching keys in the other stream.

   *Example*:
    - Input: Stream of user clicks (`("user1", "click")`) and a stream of user profile updates (`("user1", "update")`).
    - Join: Combine user activity with their profile data.
    - Output: Joined stream with enriched user data, such as `("user1", "click", "update")`.

2. **Stream-Table Join**
    - Joins a stream with a table. In this case, the table represents a snapshot of stateful data.
    - **Inner Join**: Joins the stream record with the table record based on the key, if the table has a matching value.
    - **Left Join**: Joins the stream with the table, but keeps the stream record even if there is no matching record in the table.

   *Example*:
    - Input: A stream of transaction records (`("txn1", 100)`) and a table of user balances (`("user1", 500)`).
    - Join: Enrich the transaction with the user's current balance from the table.
    - Output: Combined record with transaction and user balance, such as `("txn1", 100, 500)`.

3. **Global Table Join**
    - Similar to a stream-table join but uses a **global table** instead of a regular table, which means the table is replicated across all Kafka Streams instances.

   *Example*:
    - Input: A global table of user preferences (`("user1", "dark_mode")`) and a stream of user activity (`("user1", "click")`).
    - Join: Enrich user activity with preferences from the global table.
    - Output: Combined record with user activity and preferences, such as `("user1", "click", "dark_mode")`.

---

## **Summary**

1. **Stateless Transformations**: Lightweight operations like `map`, `filter`, and `flatMap` that process records independently.
2. **Aggregations**: Stateful operations like `reduce`, `count`, and `aggregate` that group and summarize records by key.
3. **Terminal Operations**: Endpoints of a processing pipeline, including:
    - `foreach`: Executes side effects.
    - `to`: Writes data to Kafka topics.
    - `toTable`: Materializes a stream as a table.
    - `print`: Debugging tool to inspect records.
    - `process`: Custom processing logic using the Processor API.
4. **Writing to Kafka Topics**: Use `to()` for reliable, fault-tolerant writes, and avoid manual producers within `foreach`.
5. **Kafka Streams Joins**: Combine data from two streams or a stream and a table using various types of joins, such as stream-stream, stream-table, and global table joins.

By combining these features, Kafka Streams enables the creation of efficient, reliable, and scalable real-time processing pipelines.

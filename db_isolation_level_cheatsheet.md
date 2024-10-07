# Isolation Levels in Databases: A Cheatsheet

In databases, **transaction isolation levels** define how changes made in one transaction are visible to others. They are crucial for balancing **consistency, performance, and concurrency**. Below is a summary of the standard isolation levels and the common concurrency problems they address.

---

## 1. **Read Uncommitted**
- **Description**: The lowest isolation level. Transactions can read **uncommitted changes** from other transactions.
- **Concurrency Problems**:
    - **Dirty Reads**: Reading data written by an uncommitted transaction.
    - **Non-Repeatable Reads**: Different results when reading the same data in one transaction.
    - **Phantom Reads**: New rows are added or removed by another transaction between reads.

- **Use Cases**: Not commonly used, suitable for scenarios where dirty reads are acceptable for performance.

---

## 2. **Read Committed** (Default in many databases)
- **Description**: A transaction can only read **committed data**. Uncommitted changes are not visible.
- **Concurrency Problems**:
    - **Non-Repeatable Reads**: Data can change if another transaction commits after the first read.
    - **Phantom Reads**: Another transaction can add or delete rows during a transaction.

- **Use Cases**: Common for most OLTP (Online Transaction Processing) systems.

---

## 3. **Repeatable Read**
- **Description**: Ensures that if a transaction reads a row once, subsequent reads will return the same data, even if another transaction modifies it.
- **Concurrency Problems**:
    - **Phantom Reads**: A transaction can still see new rows inserted by other transactions.

- **Use Cases**: Appropriate when it's important to ensure data consistency across multiple reads in a single transaction.

---

## 4. **Serializable**
- **Description**: The highest isolation level. Transactions are executed as if they were **serialized** (i.e., one after another), preventing all concurrency issues.
- **Concurrency Problems**:
    - **None**: Serializable isolation prevents dirty reads, non-repeatable reads, and phantom reads.

- **Use Cases**: Required for complex transactions where full consistency is needed, though it can significantly impact performance due to its strict locking and blocking mechanisms.

---

## Common Concurrency Issues Explained

- **Dirty Read**: A transaction reads data that has been modified by another uncommitted transaction.

- **Non-Repeatable Read**: A transaction reads the same row multiple times but gets different data each time because another transaction has updated the data.

- **Phantom Read**: A transaction reads a set of rows that satisfy a condition, and another transaction inserts or deletes rows, making them appear or disappear when the first transaction repeats the read.

---

## Isolation Level Comparison Table

| **Isolation Level**    | **Dirty Read** | **Non-Repeatable Read** | **Phantom Read** | **Performance**       |
|------------------------|----------------|-------------------------|------------------|-----------------------|
| **Read Uncommitted**    | ✔️             | ✔️                      | ✔️               | ⚡️ Fastest (No Locks) |
| **Read Committed**      | ❌             | ✔️                      | ✔️               | ⚡️ Fast                |
| **Repeatable Read**     | ❌             | ❌                      | ✔️               | ⚖️ Moderate            |
| **Serializable**        | ❌             | ❌                      | ❌               | 🐢 Slowest             |

---

### Notes:
- **Phantom Reads**: Only prevented at the **Serializable** level, while **Repeatable Read** ensures that individual rows remain stable.
- **Performance**: Higher isolation levels reduce concurrency but increase data consistency.
- **Implementation Variations**: Some databases implement these isolation levels differently (e.g., Oracle’s **Snapshot Isolation** for Repeatable Reads).

---

### Typical Database Defaults:
- **MySQL**: Read Committed or Repeatable Read (depends on configuration)
- **PostgreSQL**: Read Committed (supports Serializable through MVCC)
- **SQL Server**: Read Committed (with additional modes like Snapshot Isolation)

This guide provides a quick overview, but the right isolation level depends on your use case, balancing data integrity with performance.

---
layout: post
title:  "Unit 7 Blog"
date:   2025-05-25 15:30:25
categories: Blog
tags: featured
image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG


---

## Database Transactions, Concurrency Control, and Recovery



### Introduction

Before diving into Unit 7, I thought databases just stored data and let you run queries. But after going through these lessons, I’ve realized that databases are way more complicated behind the scenes! They have to keep data consistent even when multiple users are changing it at the same time—or when something goes wrong like a crash or failure. I learned about **transactions** that wrap operations into safe units of work, **concurrency control** that prevents users from interfering with each other, and **recovery mechanisms** that bring things back to normal after failure. It’s honestly like a superhero system protecting our data from chaos.

---

## Key Lessons from Unit 7

### Lesson 18: Database Transactions

#### What is a Transaction?

A transaction is a sequence of operations that acts as one single logical unit of work. For example, transferring money from account A to B should subtract from A and add to B together—not just one or the other.

#### ACID Properties

Transactions have four essential properties:

* **Atomicity**: All or nothing—either every operation completes or none do.
* **Consistency**: Keeps the database in a valid state before and after.
* **Isolation**: Each transaction runs as if it’s the only one.
* **Durability**: Once committed, the changes are permanent—even after a crash.

#### Simple Transaction Example

```sql
BEGIN;
UPDATE accounts SET balance = balance - 50 WHERE account_name = 'A';
UPDATE accounts SET balance = balance + 50 WHERE account_name = 'B';
COMMIT;
```

If anything fails between the two updates, the whole transaction rolls back.

#### Transaction States

Transactions move through states like **Active**, **Partially Committed**, **Failed**, **Aborted**, and **Committed**. Recovery systems make sure these transitions don’t cause inconsistency.

---

### Lesson 19: Concurrency Control

#### Why Concurrency Control?

When multiple transactions access the same data, things can go wrong—like one transaction reading half-updated data from another. Concurrency control avoids that.

#### Locking

There are two main lock types:

* **Shared (S)**: Allows reading.
* **Exclusive (X)**: Allows both reading and writing.

The database ensures only compatible locks are granted.

#### Two-Phase Locking (2PL)

This is a protocol that splits a transaction’s locking into two phases:

1. **Growing phase** – can only acquire locks.
2. **Shrinking phase** – can only release locks.

This ensures serializability.

#### Deadlocks

When two transactions wait for each other to release locks, you get a deadlock. There are two ways to handle this:

* **Deadlock Detection**: Use a waits-for graph to find cycles.
* **Deadlock Prevention**: Use timestamps to decide who should wait or abort.

#### Lock Granularity

Locks can be taken at levels like row, page, table, or database. Finer granularity means more concurrency but higher overhead.

#### Other Concurrency Techniques

* **Timestamp Ordering**: Transactions get timestamps to determine the order of operations.
* **Optimistic Concurrency Control**: Assume no conflict and check only at commit.
* **MVCC (Multi-Version Concurrency Control)**: Keep multiple versions of data so reads don’t block writes.

---

### Lesson 20: Database Recovery

#### Why Do We Need Recovery?

Failures happen—power outages, hardware errors, even human mistakes. Recovery ensures transactions still preserve atomicity and durability.

#### Log-Based Recovery

Every change is logged *before* it’s written to the database (Write-Ahead Logging).

A typical log looks like this:

```
<T1, X, old_value, new_value>
<T1 commit>
```

#### Undo and Redo

* **Undo**: If a transaction didn't commit, revert its changes.
* **Redo**: If it did commit, make sure its changes are applied.

#### Checkpoints

To speed up recovery, the system creates **checkpoints**—snapshots of the database state. After a crash, the system only needs to examine logs after the last checkpoint.

#### ARIES Recovery Algorithm

This advanced method has 3 passes:

1. **Analysis**: Find dirty pages and uncommitted transactions.
2. **Redo**: Repeat all operations from logs to restore state.
3. **Undo**: Roll back incomplete transactions.

ARIES uses **STEAL** and **NO-FORCE** policies to support high performance while still ensuring data safety.

#### **Fuzzy Checkpoints**

Allows new transactions to continue during a checkpoint instead of pausing everything.

#### **Remote Backup and High Availability**

For disasters, some systems keep backups at remote sites. If the main site fails, the backup takes over using log records sent in real-time.

---

## My Experience and Reflections

At first, ACID properties just felt like some abstract rules. But after trying out transactions in PostgreSQL and intentionally causing errors, I saw how these properties saved my data from becoming garbage.

The concurrency control part was *really* hard to wrap my head around. I kept confusing shared and exclusive locks, and the two-phase locking rules felt rigid. It was only when we did lab exercises with real locking conflicts that it clicked.

Deadlocks were surprisingly intuitive—like two people trying to pass each other in a narrow hallway and both refusing to move! The waits-for graph made it easier to spot these issues.

Database recovery was actually my favorite part. I didn’t expect databases to keep so many logs just to rewind and replay actions. The ARIES algorithm sounded complicated at first, but when our class simulated a crash and watched recovery kick in, it felt like watching database magic.

I still struggle with understanding timestamp ordering and the Thomas Write Rule—it feels like a bunch of edge cases that are hard to remember. But MVCC made sense to me because it's like version control for data.

---

## Conclusion

Unit 7 completely changed how I see databases. It’s not just about saving data anymore—it’s about *protecting* it no matter what. Transactions, locks, logs, and recovery mechanisms are all part of that mission.

The most useful concept I learned was probably **Write-Ahead Logging** and how it supports both undo and redo. It feels like the safety net for the whole system. I’m excited to try building a tiny banking app that uses transactions and log-based recovery just to apply this knowledge.

Some things like serializability graphs and ARIES are still challenging, but I feel a lot more confident now than when I started.

---



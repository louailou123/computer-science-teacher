# Playbook: databases

**Covers:** data models (relational, ER, document, key-value, column-family, graph), relational algebra and calculus, SQL (queries, joins, aggregation, subqueries, window functions, DDL, constraints), schema design and normalization (functional dependencies, 1NF through BCNF, 4NF), storage (pages, heap files, buffer pool), indexing (B+ trees, hash indexes, LSM trees), query processing and optimization, transactions (ACID, concurrency control, isolation levels, MVCC), recovery (WAL, ARIES), distributed databases and NoSQL.

## What a complete answer contains

- **For SQL:**
  - give a small schema, sample rows, the query, and the result table, so the student can check every row;
  - write the equivalent relational algebra (σ, π, ⋈, ∪, −, ρ, γ);
  - explain the logical evaluation order (FROM, then JOIN, WHERE, GROUP BY, HAVING, SELECT, DISTINCT, ORDER BY, LIMIT), which explains why an alias defined in SELECT can't be used in WHERE;
  - cover NULL semantics and three-valued logic.
- **For normalization:**
  - list the functional dependencies;
  - compute attribute closures to find candidate keys;
  - identify the violated normal form and why;
  - decompose step by step;
  - prove the decomposition is lossless-join and check whether it preserves dependencies;
  - show the update, insert and delete anomalies that the design prevents.
- **For indexing:**
  - draw the B+ tree node layout (keys, child pointers, leaf links);
  - compute the fanout from page size and key/pointer sizes;
  - compute the tree height as roughly log_fanout(N), and the I/Os per lookup;
  - show inserts with node splits;
  - cover clustered versus secondary indexes, covering indexes, and composite index column order (the leftmost-prefix rule);
  - explain when the optimizer ignores an index, and why.
- **For query processing:**
  - join algorithms (nested loop, block nested loop, index nested loop, sort-merge, hash join) with their I/O cost formulas in pages;
  - selectivity estimation;
  - plan enumeration (Selinger-style dynamic programming);
  - real `EXPLAIN` (or `EXPLAIN ANALYZE`) output from PostgreSQL, explained line by line.
- **For transactions:**
  - schedules written as `R1(A) W2(A)…`;
  - conflict serializability via the precedence graph;
  - two-phase locking (and why strict 2PL);
  - deadlock handling;
  - an isolation-level table showing which anomalies each level allows (dirty read, non-repeatable read, phantom, lost update, write skew), with concrete interleavings demonstrating each one;
  - MVCC as implemented in PostgreSQL (tuple versions, snapshots, VACUUM) and in MySQL InnoDB (undo logs).
- **For recovery:** the write-ahead logging rule, log records, checkpoints, and ARIES's analysis, redo and undo phases traced on an example log.
- **Real systems:** PostgreSQL, MySQL/InnoDB, SQLite, Oracle and SQL Server; MongoDB, Redis, Cassandra and DynamoDB. Say where the SQL standard and specific databases differ.

## Comparison dimensions

The data model, query capability, consistency and transaction guarantees, scalability (vertical versus horizontal), read versus write optimization (B-tree versus LSM), schema flexibility, and operational complexity.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| early 1960s | Charles Bachman (GE) | IDS, a network-model database that led to the CODASYL standard (Turing Award 1973) |
| 1966–68 | IBM | IMS, a hierarchical database built for the Apollo program |
| 1970 | Edgar F. Codd (IBM) | "A Relational Model of Data for Large Shared Data Banks" (Turing Award 1981). He defined 1NF in 1970 and 2NF and 3NF in 1971 |
| 1970–72 | Rudolf Bayer and Edward McCreight | B-trees |
| 1974 | Donald Chamberlin and Raymond Boyce (IBM) | SEQUEL, which became SQL. Boyce and Codd defined BCNF the same year |
| 1974–79 | IBM | System R, the research prototype that proved relational databases could be fast |
| 1973 onward | Michael Stonebraker and Eugene Wong (Berkeley) | Ingres, then Postgres (1986), which became PostgreSQL (Stonebraker received the Turing Award in 2014) |
| 1976 | Peter Chen | The entity-relationship model |
| 1976 | Eswaran, Gray, Lorie and Traiger | Two-phase locking and serializability |
| 1979 | Patricia Selinger et al. | Cost-based query optimization in System R |
| 1979 | Relational Software, Inc. (now Oracle) | The first commercial SQL relational database |
| 1981 | Jim Gray | "The Transaction Concept" (Turing Award 1998). The acronym ACID was coined by Härder and Reuter in 1983 |
| 1986–87 | ANSI, then ISO | The first SQL standard |
| 1992 | C. Mohan et al. (IBM) | ARIES recovery |
| 1995; 2000 | MySQL AB; D. Richard Hipp | MySQL; SQLite |
| 1996 | O'Neil et al. | The log-structured merge tree (LSM tree) |
| 2000 and 2002 | Eric Brewer; Seth Gilbert and Nancy Lynch | The CAP conjecture, then its proof |
| 2006–07 | Google; Amazon | Bigtable and Dynamo papers, which inspired the NoSQL wave (Cassandra, HBase, MongoDB in 2009) |

## Canonical sources

- Silberschatz, Korth and Sudarshan, *Database System Concepts*
- Ramakrishnan and Gehrke, *Database Management Systems*
- Garcia-Molina, Ullman and Widom, *Database Systems: The Complete Book*
- Martin Kleppmann, *Designing Data-Intensive Applications*
- Alex Petrov, *Database Internals*
- CMU 15-445/645 lectures by Andy Pavlo (free online)
- *Readings in Database Systems* (the "Red Book", free online)
- The PostgreSQL documentation, especially its chapters on MVCC and query planning

## Classic misconceptions

- "SQL runs in the order it's written." The logical order starts with FROM, and the physical plan can be completely different.
- "`NULL = NULL` is true." It evaluates to UNKNOWN. Use `IS NULL`.
- "Normalization always improves performance." It removes redundancy and anomalies, but it can add joins. Denormalization is a deliberate trade-off.
- "An index always speeds up queries." Indexes slow writes, and a low-selectivity predicate is often faster as a full scan.
- "Serializable means the transactions ran one at a time." It means the result is *equivalent to* some serial order.
- "NoSQL means no schema and no transactions." Many NoSQL systems have schemas and transactions (MongoDB has had multi-document ACID transactions since 4.0).
- "CAP means you pick two out of three." Partitions aren't optional. The real choice is between consistency and availability *during* a partition, and PACELC adds the latency trade-off when there is no partition.
- "A primary key and a clustered index are the same." They are often configured together, as in InnoDB, but they are different concepts.

## Question patterns

- Write SQL for this question, then give its relational algebra.
- Find the candidate keys from these functional dependencies, determine the normal form, and decompose to BCNF or 3NF.
- Draw the B+ tree after these inserts.
- Estimate the I/O cost of this join with each algorithm.
- Is this schedule conflict-serializable? Draw the precedence graph.
- Which anomaly does this interleaving show, and which isolation level prevents it?
- Trace ARIES recovery on this log.
- Design the schema for this application, and justify the choice of index.

## Tools and artifacts to show

`EXPLAIN ANALYZE` in PostgreSQL, the `sqlite3` shell, ER diagrams (ASCII or Mermaid), B+ tree visualizers, and two-session demos in `psql` that show isolation anomalies happening live.

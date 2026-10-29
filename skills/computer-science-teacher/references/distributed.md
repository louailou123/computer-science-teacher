# Playbook: distributed systems

**Covers:** system and failure models, time and ordering (physical clocks, NTP, Lamport clocks, vector clocks), replication (leader-based, multi-leader, leaderless), consistency models, consensus (Paxos, Raft, ZAB, Byzantine fault tolerance), impossibility results, distributed transactions (2PC, 3PC, sagas), partitioning and consistent hashing, CAP and PACELC, failure detection, membership, gossip protocols, CRDTs, MapReduce and dataflow systems, cloud-scale system design.

## What a complete answer contains

- **The system model, stated first,** because every result depends on it:
  - timing: synchronous, asynchronous or partially synchronous;
  - failures: crash-stop, crash-recovery or Byzantine;
  - the network: reliable or fair-loss links, and whether partitions can happen.
- **Message sequence diagrams** with one vertical line per node, time flowing downward, and arrows labelled with message contents, including failure cases (dropped messages, crashed nodes, partitions, delays).
- **Logical time computed by hand:** Lamport timestamps and vector clocks on an event diagram. Show why Lamport clocks can't detect concurrency and vector clocks can.
- **Consensus algorithms step by step:**
  - **Paxos:** proposers, acceptors and learners; the prepare/promise and accept/accepted phases; proposal numbers; and the safety argument for why two values can never both be chosen.
  - **Raft:** terms, leader election with randomized timeouts, log replication, commit rules, and the safety properties, traced on a five-node cluster that includes a leader crash.
- **Impossibility results with intuition and a proof sketch:** the Two Generals problem, FLP (no deterministic consensus in an asynchronous system with even one crash), and the bound of n ≥ 3f + 1 for Byzantine agreement.
- **Quorum math:** with N replicas, write quorum W and read quorum R, R + W > N guarantees that every read overlaps the latest write. Show the overlap with a concrete N = 5 example.
- **Consistency models as a ladder:** linearizable, sequential, causal, eventual. For each, give a concrete history that is allowed and one that isn't, and the cost of providing it.
- **Distributed transactions:** two-phase commit with every failure case (coordinator crashes before or after the decision, participant crashes), why 2PC blocks, and alternatives (3PC, sagas, Spanner-style commits).
- **Real systems and what they chose:** Google Spanner (TrueTime and external consistency), etcd and Consul (Raft), ZooKeeper (ZAB), Kafka (a replicated log), Cassandra and DynamoDB (leaderless, tunable consistency), CockroachDB, and MapReduce, Hadoop and Spark.

## Comparison dimensions

Consistency guarantee, availability under partition, latency, throughput, fault model tolerated, number of replicas needed (2f + 1 for crash faults, 3f + 1 for Byzantine faults), and operational complexity.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1975; 1978 | Akkoyunlu, Ekanadham and Huber; named by Jim Gray | The Two Generals problem |
| 1978 | Leslie Lamport | "Time, Clocks, and the Ordering of Events in a Distributed System": happens-before and logical clocks (Turing Award 2013) |
| 1978 | Jim Gray | Two-phase commit described in his notes on database operating systems |
| 1982 | Lamport, Shostak and Pease | "The Byzantine Generals Problem" |
| 1985 | Fischer, Lynch and Paterson | FLP impossibility |
| 1985 | K. Mani Chandy and Leslie Lamport | Distributed snapshots |
| 1988 | Colin Fidge; Friedemann Mattern | Vector clocks, independently |
| written 1989, published 1998 | Leslie Lamport | Paxos, in "The Part-Time Parliament". "Paxos Made Simple" followed in 2001 |
| 1990 | Maurice Herlihy and Jeannette Wing | Linearizability |
| 1994 | L. Peter Deutsch and others at Sun | The "fallacies of distributed computing" |
| 1997 | Karger et al. | Consistent hashing |
| 1999 | Miguel Castro and Barbara Liskov | Practical Byzantine Fault Tolerance (PBFT) |
| 2000; 2002 | Eric Brewer; Gilbert and Lynch | CAP conjecture; proof |
| 2003–06 | Google | GFS (2003), MapReduce (Dean and Ghemawat, 2004), Bigtable and Chubby (2006) |
| 2007 | Amazon | Dynamo |
| 2008 | Satoshi Nakamoto | Bitcoin: consensus by proof of work |
| 2011 | Shapiro et al. | CRDTs, formalized |
| 2012 | Google | Spanner |
| 2014 | Diego Ongaro and John Ousterhout | Raft, "In Search of an Understandable Consensus Algorithm" |

## Canonical sources

- Martin Kleppmann, *Designing Data-Intensive Applications*, plus his free Cambridge lecture notes on distributed systems
- van Steen and Tanenbaum, *Distributed Systems* (free online)
- Nancy Lynch, *Distributed Algorithms*
- Cachin, Guerraoui and Rodrigues, *Introduction to Reliable and Secure Distributed Programming*
- MIT 6.824/6.5840 lectures and labs (students implement Raft)
- The original papers listed above, which are unusually readable for this field

## Classic misconceptions

- The fallacies of distributed computing: the network is reliable, latency is zero, bandwidth is infinite, the network is secure, topology doesn't change, there is one administrator, transport cost is zero, the network is homogeneous.
- "CAP means choose any two." See the databases playbook: the choice only exists during a partition.
- "Eventual consistency means the data will be correct eventually." It means replicas converge *if writes stop*, and says nothing about which value wins without a conflict-resolution rule.
- "Clocks on different machines agree." Clock skew and drift make wall-clock timestamps unsafe for ordering (last-write-wins can lose data).
- "Exactly-once delivery is possible." Over an unreliable network you get at-most-once or at-least-once delivery. "Exactly once" in practice means at-least-once delivery plus idempotent or deduplicated processing.
- "Consensus is only for blockchains." Every leader election, configuration store and replicated database depends on it.
- "More replicas always means more availability." It depends on the quorum sizes and the failure model.

## Question patterns

- Assign Lamport and vector timestamps to this event diagram, and say which events are concurrent.
- Trace Raft through this failure scenario. Who becomes leader, and which entries are committed?
- Is this history linearizable? Is it sequentially consistent?
- For N = 5, which (R, W) choices give strong reads? What happens if two nodes fail?
- Walk through 2PC when the coordinator crashes after sending PREPARE.
- Design a distributed key-value store, a URL shortener, or a chat system, and justify each choice.

## Tools and artifacts to show

Space-time diagrams, the Raft visualization at raft.github.io, Jepsen analyses (jepsen.io) that show real databases violating their claimed guarantees, and small multi-process Python simulations.

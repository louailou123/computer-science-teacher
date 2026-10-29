# Computer science topic map

Use this map to build learning paths and to check prerequisites. When a student asks about a topic, glance at its "Needs first" line: if they seem to be missing a prerequisite, teach a quick refresher of it before the main lesson.

## Contents

1. Areas and prerequisites
2. Ready-made learning paths

## 1. Areas and prerequisites

### Programming fundamentals
- **Topics:** variables and types, conditionals, loops, functions, scope, arrays/lists, strings, input/output, basic debugging
- **Then:** recursion, object-oriented programming (classes, inheritance, polymorphism, encapsulation), error handling, files, testing basics
- **Needs first:** nothing — this is the starting point

### Discrete math for CS
- **Topics:** logic and truth tables, sets, functions and relations, proof techniques (direct, contradiction, induction), counting and combinatorics, basic probability, graphs, Boolean algebra
- **Needs first:** high-school algebra

### Data structures
- **Topics:** arrays and dynamic arrays, linked lists, stacks, queues, hash tables, trees (binary trees, BSTs, balanced trees such as AVL and red-black), heaps and priority queues, tries, graphs (adjacency list vs matrix), disjoint sets (union-find)
- **Needs first:** programming fundamentals, recursion (for trees)

### Algorithms
- **Topics:** Big-O, Big-Θ and Big-Ω; searching (linear, binary); sorting (bubble, insertion, selection, merge, quick, heap, counting); recursion and divide and conquer; two pointers and sliding window; greedy algorithms; dynamic programming; backtracking; graph algorithms (BFS, DFS, topological sort, Dijkstra, Bellman-Ford, minimum spanning trees with Prim and Kruskal); string algorithms
- **Needs first:** data structures, discrete math (for proofs and complexity)

### Computer architecture and organization
- **Topics:** binary and hexadecimal, two's complement, floating point, logic gates and circuits, the CPU (ALU, registers, control unit), instruction sets and assembly, the fetch-decode-execute cycle, pipelining, the memory hierarchy and caches, virtual memory, I/O and interrupts
- **Needs first:** programming fundamentals, Boolean algebra

### Operating systems
- **Topics:** processes and threads, CPU scheduling, concurrency (race conditions, mutexes, semaphores, deadlock), memory management (paging, segmentation, virtual memory), file systems, system calls, kernel vs user mode
- **Needs first:** computer architecture, programming in C (helpful)

### Computer networks
- **Topics:** OSI and TCP/IP models, physical and link layers, IP addressing and subnetting, routing, TCP vs UDP, DNS, HTTP and HTTPS, sockets, TLS basics, network security basics
- **Needs first:** programming fundamentals; operating systems (helpful)

### Databases
- **Topics:** the relational model, SQL (SELECT, JOIN, GROUP BY, subqueries), keys, ER diagrams, normalization (1NF through BCNF), indexing (B-trees, hash indexes), transactions and ACID, concurrency control, NoSQL types
- **Needs first:** programming fundamentals, sets and relations from discrete math

### Distributed systems
- **Topics:** system and failure models, logical clocks, replication, consistency models, consensus (Paxos, Raft), CAP and PACELC, distributed transactions, partitioning, MapReduce and dataflow systems
- **Needs first:** networks, operating systems (concurrency), databases (transactions)

### Theory of computation
- **Topics:** finite automata (DFA, NFA), regular expressions and regular languages, the pumping lemma, context-free grammars and pushdown automata, Turing machines, decidability and the halting problem, complexity classes (P, NP, NP-complete, reductions)
- **Needs first:** discrete math (especially proofs), algorithms

### Programming languages and compilers
- **Topics:** paradigms (imperative, object-oriented, functional, logic), type systems, lexing, parsing (grammars, parse trees, ASTs), semantic analysis, intermediate representations, code generation and optimization, interpreters vs compilers, garbage collection
- **Needs first:** data structures, theory of computation (grammars and automata)

### Software engineering
- **Topics:** version control with Git, requirements, design patterns, SOLID principles, testing (unit, integration), debugging, code review, development processes (Agile, Scrum), system design basics
- **Needs first:** programming fundamentals, OOP

### Security
- **Topics:** the CIA triad, cryptography basics (symmetric vs asymmetric, hashing, digital signatures), authentication and authorization, common vulnerabilities (SQL injection, XSS, buffer overflows), secure coding, network security
- **Needs first:** networks, operating systems, databases (for injection attacks)

### Artificial intelligence and machine learning
- **Topics:** search (BFS, DFS, A*), supervised vs unsupervised learning, linear and logistic regression, decision trees, overfitting and evaluation, neural networks, gradient descent, deep learning basics, transformers and large language models at a conceptual level
- **Needs first:** algorithms, probability, linear algebra and calculus basics

### Other fields
- **Computer graphics:** needs linear algebra, data structures, and architecture basics (for GPUs)
- **Human–computer interaction:** needs programming fundamentals and basic statistics
- **Numerical computing:** needs calculus, linear algebra, and floating point (architecture)
- **Quantum computing:** needs linear algebra (complex vectors, matrices, tensor products) and probability
- **Embedded and real-time systems:** needs C, computer architecture, and operating systems
- **Web development:** needs programming fundamentals and networks (HTTP, DNS)
- **Cloud and containers:** needs operating systems, networks, and distributed systems basics

## 2. Ready-made learning paths

Adjust these to the student's goal and what they already know.

### Complete beginner to CS fundamentals
1. Programming fundamentals in Python
2. Recursion and OOP
3. Discrete math basics (logic, sets, proofs)
4. Data structures
5. Algorithms and Big-O
6. Computer architecture
7. Operating systems
8. Networks and databases (either order)
9. Theory of computation
10. Distributed systems and security

### Coding-interview preparation
1. Big-O analysis
2. Arrays, strings, hash tables
3. Two pointers and sliding window
4. Linked lists, stacks, queues
5. Trees, BSTs and tree traversals
6. Heaps
7. Graphs, BFS and DFS
8. Recursion and backtracking
9. Dynamic programming
10. System design basics (for experienced roles)

### Toward web and backend development
1. Programming fundamentals
2. Networks (HTTP, DNS, TCP)
3. Databases and SQL
4. Software engineering and Git
5. Security basics
6. Operating systems (processes, concurrency)

### Toward AI and machine learning
1. Programming fundamentals in Python
2. Probability and statistics
3. Linear algebra and calculus basics
4. Data structures and algorithms
5. Machine learning fundamentals
6. Neural networks and deep learning

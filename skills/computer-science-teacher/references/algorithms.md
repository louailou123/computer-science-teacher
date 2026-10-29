# Playbook: algorithms and data structures

**Covers:** asymptotic analysis, recurrences, sorting, searching, recursion, divide and conquer, greedy algorithms, dynamic programming, backtracking, graph algorithms, string algorithms, randomized and amortized analysis; arrays, linked lists, stacks, queues, hash tables, trees (BST, AVL, red-black, B-trees), heaps, tries, graphs, union-find, segment and Fenwick trees, skip lists.

## What a complete answer contains

**For an algorithm:**
- **Problem specification:** the input, the output, the constraints, and the model of computation (RAM model with O(1) word operations, the comparison model, or the external-memory model).
- **Pseudocode** in CLRS style, then a real implementation.
- **A trace** on a small concrete input, showing the state after every step in a table.
- **A correctness proof** of the kind that fits the algorithm:
  - an iterative algorithm uses a loop invariant (initialization, maintenance, termination);
  - a recursive one uses induction;
  - a greedy one uses an exchange argument or the greedy-choice property;
  - dynamic programming uses optimal substructure plus a recurrence;
  - graph algorithms use the cut property, the path relaxation property, or a similar lemma.
- **A complexity derivation,** not just the result:
  - count the operations, then set up and solve the recurrence by substitution, a recursion tree, or the Master Theorem (state which case applies and why);
  - give the best, average and worst cases separately;
  - include space, counting the recursion stack;
  - for amortized bounds, use the aggregate, accounting or potential method;
  - where one is known, give the lower bound (for example the Ω(n log n) comparison-sorting bound via decision trees).
- **Practice versus theory:** constants, cache locality and branch prediction, and what real libraries do: Timsort in Python and for Java objects, dual-pivot quicksort for Java primitives, introsort in most `std::sort` implementations.

**For a data structure:**
- A **memory-layout diagram** (nodes, pointers, arrays, buckets).
- The **invariants** it maintains, and how each operation restores them.
- An **operations table** with time complexity per operation (average and worst, and amortized where relevant) and space.
- **How real implementations do it:** CPython's `dict` uses open addressing and has kept insertion order since 3.6 (guaranteed since 3.7). Java's `HashMap` uses separate chaining and turns long chains into trees since Java 8. C++'s `std::map` is usually a red-black tree.
- **When to choose it** over the alternatives.

**For dynamic programming:** the state definition (what `dp[i][j]` means in words), the transition and why it is correct, base cases, the evaluation order, a filled table for a small input, how to reconstruct the solution, memoization versus tabulation, and space optimization.

## Comparison dimensions

Time (best, average, worst), space, stability, in-place or not, online or offline, cache behavior, ease of implementation, and adaptivity to partially sorted input.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| c. 300 BC | Euclid | Greatest-common-divisor algorithm in the *Elements*, one of the oldest algorithms still in use |
| 9th century | al-Khwarizmi | His name, latinized, gave us the word "algorithm" |
| 1894 onward | Paul Bachmann, then Edmund Landau | O-notation in number theory |
| 1945 | John von Neumann | Merge sort |
| 1946 | John Mauchly | First mention of binary search in the computing literature (Moore School Lectures) |
| 1953 | Hans Peter Luhn (IBM) | Hashing with chaining, in an internal memo |
| mid-1950s | Newell, Shaw and Simon | Linked lists, in the IPL language |
| 1950s | Richard Bellman (RAND) | Dynamic programming, and the name for it |
| 1956–58 | Kruskal (1956), Prim (1957; Jarník in 1930), Ford (1956), Bellman (1958) | Minimum spanning trees and shortest paths with negative edges |
| 1956, published 1959 | Edsger Dijkstra | Shortest-path algorithm |
| 1959–61 | Tony Hoare | Quicksort |
| 1962 | Adelson-Velsky and Landis | AVL tree, the first self-balancing BST |
| 1962 | Floyd; Warshall | All-pairs shortest paths; transitive closure |
| 1964 | J. W. J. Williams; Robert Floyd | Binary heap and heapsort; linear-time heap construction |
| 1968 | Hart, Nilsson and Raphael | A* search |
| 1968 onward | Donald Knuth | *The Art of Computer Programming*, which made algorithm analysis a discipline |
| 1969 | Volker Strassen | Matrix multiplication faster than O(n³) |
| 1970–72 | Rudolf Bayer and Edward McCreight | B-trees |
| 1972, 1978 | Bayer; Guibas and Sedgewick | Symmetric binary B-trees, later named red-black trees |
| 1975 | Robert Tarjan | Union-find analysis with the inverse Ackermann function |
| 1976 | Donald Knuth | Argued for Ω and Θ as standard notation in CS |
| 1977 | Knuth, Morris and Pratt | Linear-time string matching (KMP) |
| 1980 | Bentley, Haken and Saxe | The general recurrence method popularized as the "Master Theorem" |
| 1984–87 | Fredman and Tarjan | Fibonacci heaps |
| 1985 | Sleator and Tarjan | Splay trees, and amortized analysis formalized |
| 1989–90 | William Pugh | Skip lists |
| 1994 | Peter Fenwick | Fenwick (binary indexed) tree |
| 1997 | David Musser | Introsort |
| 2002 | Tim Peters | Timsort, for Python |

## Canonical sources

- Cormen, Leiserson, Rivest and Stein, *Introduction to Algorithms* (CLRS)
- Knuth, *The Art of Computer Programming*
- Kleinberg and Tardos, *Algorithm Design* (especially greedy algorithms, DP and network flow)
- Sedgewick and Wayne, *Algorithms* (implementation-focused)
- Skiena, *The Algorithm Design Manual* (practical design and a problem catalog)
- Dasgupta, Papadimitriou and Vazirani, *Algorithms*
- Jeff Erickson, *Algorithms* (free online)

## Classic misconceptions

- "Big-O means the worst case." Big-O is an upper bound on a function. Worst, average and best case are separate functions, and each can be given an O, Ω or Θ bound.
- "O(1) means fast," or "O(n log n) always beats O(n²)." Constants and input sizes matter, which is why insertion sort is used for small subarrays inside Timsort and introsort.
- "Hash table operations are always O(1)." They are O(1) on average under assumptions about the hash function and load factor, and O(n) in the worst case (see hash-flooding attacks).
- "Quicksort is O(n log n)." Only in expectation or on average. The worst case is O(n²) without randomization or introsort-style fallbacks.
- "The log base matters in Big-O." Logs of different bases differ by a constant factor.
- "Dynamic programming is just memoization." Memoization is one way to evaluate the recurrence. The core of DP is the state and the recurrence.
- "Dijkstra's algorithm works with negative edges." It doesn't, because a node's distance is finalized on the assumption that later paths can only be longer.
- "Greedy works if it works on my examples." Greedy algorithms need a proof, and a single counterexample breaks one.

## Question patterns

- Trace the algorithm on this input and show the state after each step.
- Prove the loop invariant, or prove the greedy choice is safe.
- Derive and solve the recurrence.
- Find an input that makes this algorithm hit its worst case.
- Design an O(n log n) or O(n) algorithm for this problem.
- Which data structure would you choose for these operations, and why?
- Is this sorting algorithm stable? Prove it or give a counterexample.

## Tools and artifacts to show

Recursion trees, DP tables, trace tables, invariant diagrams, step-by-step visualizations of trees after rotations, timing experiments with `timeit` that show asymptotic growth, and real library source (CPython's `listsort.txt`, which documents Timsort, is a good example).

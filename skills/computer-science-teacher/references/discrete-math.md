# Playbook: discrete mathematics for CS

**Covers:** propositional and predicate logic, proof techniques, sets, relations (equivalence relations, partial orders), functions, cardinality, induction and recursion, recurrence relations, combinatorics (counting principles, permutations, combinations, pigeonhole, inclusion–exclusion), number theory (divisibility, modular arithmetic, primes, GCD, modular inverses), graph theory, discrete probability, Boolean algebra. Linear algebra for CS is covered here when it comes up outside ML.

## What a complete answer contains

- **Rigorous definitions** in standard notation, each followed by a small concrete example and a non-example.
- **Full proofs with each step justified,** and the technique named up front: direct, contrapositive, contradiction, cases, weak or strong induction, structural induction, combinatorial (double counting or bijection), pigeonhole, diagonalization.
- **For induction:** write out the predicate P(n) explicitly, the base case, the inductive hypothesis (stating whether it's weak or strong), and the inductive step, marking exactly where the hypothesis is used.
- **For counting:** say what is being counted, whether order matters and whether repetition is allowed, and verify the formula on a tiny case by listing every possibility.
- **For probability:** define the sample space and the events, check independence formally instead of assuming it, and verify the answer with a simulation in Python when that helps.
- **For number theory:** work examples with small numbers by hand (extended Euclidean algorithm tables, modular exponentiation by repeated squaring).
- **The CS connection,** because it is why the student is learning this:
  - induction is how recursive code is proven correct;
  - modular arithmetic underlies hashing, checksums and RSA;
  - graph theory underlies networks, dependency resolution, routing and compilers (register allocation is graph coloring);
  - probability underlies randomized algorithms, hashing analysis and ML;
  - Boolean algebra underlies digital circuits and query optimization;
  - relations underlie databases;
  - partial orders underlie scheduling and the happens-before relation in distributed systems.

## Comparison dimensions

For proof techniques: when each applies, what you assume, and what you must show. For counting: order matters or not, repetition allowed or not.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| c. 300 BC | Euclid | *Elements*: proof by contradiction that there are infinitely many primes, and the GCD algorithm |
| 1640 | Pierre de Fermat | Fermat's little theorem |
| 1654 | Blaise Pascal and Pierre de Fermat | Their correspondence founded probability theory |
| 1665 | Blaise Pascal | Early explicit use of mathematical induction (the term was popularized by Augustus De Morgan in 1838) |
| 1736 | Leonhard Euler | The Seven Bridges of Königsberg, the start of graph theory |
| 18th century | Leonhard Euler | Euler's theorem and the totient function, which are the basis of RSA's correctness |
| 1847 and 1854 | George Boole | *The Mathematical Analysis of Logic* and *The Laws of Thought*: Boolean algebra |
| 19th century | Augustus De Morgan | De Morgan's laws |
| 1870s–1891 | Georg Cantor | Set theory, different sizes of infinity, the diagonal argument |
| 1879 | Gottlob Frege | *Begriffsschrift*: predicate logic with quantifiers |
| 1933 | Andrey Kolmogorov | The axioms of probability |
| 1937 | Claude Shannon | Master's thesis "A Symbolic Analysis of Relay and Switching Circuits": Boolean algebra as the design language of circuits |
| 1976 | Kenneth Appel and Wolfgang Haken | Four color theorem, the first major theorem proved with essential computer help |

## Canonical sources

- Kenneth Rosen, *Discrete Mathematics and Its Applications*
- Lehman, Leighton and Meyer, *Mathematics for Computer Science* (MIT, free online)
- Graham, Knuth and Patashnik, *Concrete Mathematics*
- Daniel Velleman, *How to Prove It* (for learning to write proofs)
- Susanna Epp, *Discrete Mathematics with Applications*

## Classic misconceptions

- "If the premise is false, the implication is false." An implication with a false premise is true (vacuous truth).
- Confusing the converse (q → p) with the contrapositive (¬q → ¬p). Only the contrapositive is equivalent to p → q.
- "Induction assumes what it is trying to prove." It assumes P(k) to prove P(k + 1), which is a different statement.
- The "all horses are the same color" fallacy, where an inductive step silently fails for small n.
- Confusing permutations and combinations: whether order matters.
- "Independent events and disjoint events are the same." Disjoint events with nonzero probability are never independent.
- The gambler's fallacy: thinking past independent outcomes change future ones.
- "∀x ∃y" and "∃y ∀x" mean the same thing. They don't; the order of quantifiers matters.
- "A function and a relation are the same." A function is a relation in which each input has exactly one output.

## Question patterns

- Prove this statement and name the technique.
- Find the flaw in this proof.
- Negate this quantified statement and simplify.
- How many ways are there to…? Verify the answer on a small case.
- Solve this recurrence, or find a closed form and prove it by induction.
- Is this relation reflexive, symmetric, antisymmetric or transitive? Is it an equivalence relation or a partial order?
- Compute this inverse or power modulo n by hand.
- Prove a graph property (handshake lemma, Euler paths, bipartiteness, tree edge count).

## Tools and artifacts to show

Truth tables, Venn diagrams, proof skeletons with each line justified, extended Euclidean tables, small Python checks of identities and counting formulas, and graph drawings in ASCII.

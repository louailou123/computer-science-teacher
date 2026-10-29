# Playbook: theory of computation

**Covers:** finite automata (DFA, NFA), regular expressions and regular languages, the pumping lemmas, context-free grammars and pushdown automata, the Chomsky hierarchy, Turing machines and their variants, the Church–Turing thesis, decidability and recognizability, reductions, the halting problem, Rice's theorem, time and space complexity classes (P, NP, coNP, PSPACE, EXP), NP-completeness, the lambda calculus.

## What a complete answer contains

- **Formal definitions as tuples,** with each component explained. For example, a DFA is M = (Q, Σ, δ, q₀, F) with δ: Q × Σ → Q. Give the definition the student's textbook most likely uses (usually Sipser's), and note when other books differ.
- **Examples and non-examples:** a language that is in the class and one that isn't, each with a justification.
- **State diagrams** for automata (in ASCII or as a transition table), and a trace of the machine on a specific input string, showing the configuration after each step.
- **Constructions carried out completely,** not just named:
  - NFA to DFA (subset construction), with the full table of subsets;
  - regex to NFA (Thompson's construction);
  - DFA to regex (state elimination);
  - DFA minimization (table filling or Myhill–Nerode classes);
  - CFG to Chomsky normal form;
  - CYK parsing;
  - CFG to PDA.
- **Full proofs, with the technique named:**
  - **Pumping lemma** as an adversarial game: the opponent picks p, you pick s, the opponent splits s = xyz, you pick i. Show every case of the split.
  - **Diagonalization** for the halting problem and for uncountability, with the table drawn.
  - **Reductions:** state the direction explicitly ("we reduce A to B, so if B were decidable then A would be"), give the mapping, prove both directions of the "if and only if", and for polynomial-time reductions argue that the mapping runs in polynomial time.
  - **NP-completeness:** show membership in NP (a certificate and a polynomial-time verifier), then hardness by reducing from a known NP-complete problem.
- **Why the theory matters in practice:** regex engines (Thompson NFA simulation versus backtracking, and catastrophic backtracking), lexers and parsers in compilers, why static analyzers must approximate (Rice's theorem), SAT solvers, and why cryptography relies on assumptions about hardness.

## Comparison dimensions

Expressive power (which languages it can describe), closure properties (union, intersection, complement, concatenation, star), decidable questions (emptiness, membership, equivalence), and the machine model needed (finite memory, a stack, unbounded tape).

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1928 | David Hilbert and Wilhelm Ackermann | The *Entscheidungsproblem*: is there a mechanical procedure to decide mathematical truth? |
| 1931 | Kurt Gödel | Incompleteness theorems |
| 1936 | Alonzo Church | The lambda calculus, and a negative answer to the Entscheidungsproblem |
| 1936 | Alan Turing | "On Computable Numbers, with an Application to the Entscheidungsproblem": Turing machines, the universal machine, undecidability of halting |
| 1943 | Warren McCulloch and Walter Pitts | Neuron model that led toward finite automata |
| 1951 memo, published 1956 | Stephen Kleene | Regular expressions, and their equivalence with finite automata (Kleene's theorem) |
| 1956–59 | Noam Chomsky | The Chomsky hierarchy of grammars |
| 1957–58 | John Myhill and Anil Nerode | The Myhill–Nerode theorem |
| 1959 | Michael Rabin and Dana Scott | "Finite Automata and Their Decision Problems": nondeterminism and the subset construction (Turing Award 1976) |
| 1959–60 | John Backus and Peter Naur | BNF, for specifying the syntax of ALGOL 60 |
| 1965 | Juris Hartmanis and Richard Stearns | "On the Computational Complexity of Algorithms", which founded complexity theory (Turing Award 1993) |
| 1965 | Alan Cobham; Jack Edmonds | Polynomial time as the formal meaning of "efficient" |
| 1968 | Ken Thompson | Regular-expression search by NFA simulation |
| 1971 | Stephen Cook | "The Complexity of Theorem-Proving Procedures": SAT is NP-complete |
| 1973 | Leonid Levin | The same result, found independently in the USSR. The theorem is named Cook–Levin for both |
| 1972 | Richard Karp | "Reducibility Among Combinatorial Problems": 21 NP-complete problems |
| 1979 | Michael Garey and David Johnson | *Computers and Intractability*, the classic catalog of NP-complete problems |
| 2000 | Clay Mathematics Institute | P vs NP named one of the seven Millennium Prize Problems |

## Canonical sources

- Michael Sipser, *Introduction to the Theory of Computation* (the most common course text)
- Hopcroft, Motwani and Ullman, *Introduction to Automata Theory, Languages, and Computation*
- Arora and Barak, *Computational Complexity: A Modern Approach* (advanced)
- Garey and Johnson, *Computers and Intractability*
- Turing's 1936 paper, which is readable and worth showing to advanced students

## Classic misconceptions

- "NP means not polynomial." NP means *nondeterministic polynomial time*: the problems whose solutions can be verified in polynomial time. P ⊆ NP.
- "NP-hard and NP-complete are the same." NP-complete means NP-hard *and* in NP. The halting problem is NP-hard but not in NP.
- "Undecidable means very hard." It means no algorithm exists at all, not that one is slow.
- "The regexes in my programming language are regular expressions." Features like backreferences go beyond regular languages, which is why backtracking engines can take exponential time.
- "The pumping lemma can prove that a language is regular." It can only prove that a language is *not* regular. The lemma's condition is necessary, not sufficient.
- Getting the reduction direction backwards. To show B is hard, reduce a known hard problem A *to* B.
- "An NFA is more powerful than a DFA." They recognize exactly the same languages. NFAs can be exponentially more compact.
- "Turing machines are a model of real computers." They are a model of what is computable in principle. Real computers are finite, though they are usually reasoned about as if they weren't.

## Question patterns

- Design a DFA or NFA, a regex, a CFG or a Turing machine for a given language.
- Convert between representations (NFA to DFA, regex to NFA, CFG to CNF).
- Prove a language is not regular, or not context-free.
- Prove a problem undecidable by reduction from the halting problem (or A_TM).
- Prove a problem NP-complete.
- Is the class closed under this operation? Prove it.
- Classify a problem: decidable? recognizable? in P? in NP?

## Tools and artifacts to show

Transition tables, configuration sequences for Turing machine runs, the diagonalization table, reduction diagrams with "instance of A maps to instance of B", parse trees, and the CYK table. JFLAP is a common teaching tool for simulating automata.

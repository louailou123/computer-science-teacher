# Playbook: programming, programming languages and compilers

**Covers:** programming fundamentals (variables, control flow, functions, recursion, scope), paradigms (imperative, object-oriented, functional, logic), OOP (classes, inheritance, polymorphism, encapsulation, interfaces), type systems, generics, closures, exceptions, memory management and garbage collection, concurrency primitives in languages, interpreters, virtual machines and JIT compilation, compilers (lexing, parsing, semantic analysis, intermediate representations, optimization, code generation).

## What a complete answer contains

- **What happens under the hood** for every construct:
  - the memory model: stack frames, the heap, values versus references, object headers;
  - what the compiler or interpreter produces, shown as real output. For Python use `dis.dis(f)`. For C use the assembly from `gcc -S -O2` or Compiler Explorer (godbolt.org). For Java use `javap -c`.
- **Precise semantics:**
  - evaluation order;
  - lexical versus dynamic scoping;
  - binding time;
  - parameter passing (by value, by reference, by sharing);
  - mutability and aliasing;
  - what the language specification guarantees versus what is undefined or implementation-defined.

  Cite the specification when it settles a question: the C standard, the Java Language Specification, the Python Language Reference, the ECMAScript specification.
- **A comparison across languages** for the same concept, because seeing C, Java, Python, JavaScript, Haskell and Rust side by side shows which parts are fundamental and which are design choices.
- **Design rationale:** the problem the feature was invented to solve, and the trade-off it carries (safety versus control, expressiveness versus simplicity, compile time versus run time).
- **For OOP:** how dynamic dispatch is implemented (vtables in C++, method lookup and the MRO in Python, invokevirtual and inline caches in the JVM). Also inheritance versus composition, and the substitution principle.
- **For memory management:** manual allocation (`malloc`/`free`), reference counting (CPython, and its cycle collector), tracing GC (mark-sweep, copying, generational, and the generational hypothesis), and ownership and borrowing (Rust). Show what a memory leak, a dangling pointer or a double free looks like at the memory level.
- **For compilers, show the artifact at every stage** for one small program:
  - the token stream, the parse tree, the AST, and the symbol table;
  - type checking;
  - three-address code or another IR, then SSA form;
  - optimization passes with before and after code (constant folding, dead code elimination, inlining, loop-invariant code motion);
  - register allocation by graph coloring;
  - the final assembly.

  For parsing, build the grammar, compute FIRST and FOLLOW sets, construct the LL(1) or LR parsing table, and run the parser on an input step by step.
- **For type systems:** static versus dynamic, strong versus weak, nominal versus structural, and type inference (Hindley–Milner), shown with a worked unification example. Also soundness, and what a type error prevents at run time.

## Comparison dimensions

Paradigm, typing discipline, memory management, execution model (AOT-compiled, interpreted, bytecode VM, JIT), concurrency model, performance profile, safety guarantees, and ecosystem.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1843 | Ada Lovelace | Notes on Babbage's Analytical Engine, including a procedure to compute Bernoulli numbers, usually called the first published program |
| 1930s | Alonzo Church | The lambda calculus, the theoretical basis of functional programming |
| 1942–45 | Konrad Zuse | Plankalkül, an early high-level language design |
| 1952 | Grace Hopper | The A-0 system, an early compiler. Her later FLOW-MATIC influenced COBOL (1959) |
| 1957 | John Backus and team (IBM) | FORTRAN, the first widely used high-level language and optimizing compiler |
| 1958–60 | John McCarthy | LISP: recursion, code as data, and garbage collection invented for it |
| 1958–60 | International committee | ALGOL 58 and 60: block structure, lexical scope, recursion, BNF syntax |
| 1965 | Donald Knuth | LR parsing |
| 1965 | Tony Hoare | Null references in ALGOL W, which he later called his "billion-dollar mistake" |
| 1966 | Corrado Böhm and Giuseppe Jacopini | Any program can be written with sequence, selection and iteration |
| 1967 | Ole-Johan Dahl and Kristen Nygaard | Simula 67: classes, objects, inheritance, the first OO language (Turing Award 2001) |
| 1968 | Edsger Dijkstra | "Go To Statement Considered Harmful", which started structured programming |
| 1970s | Alan Kay and others (Xerox PARC) | Smalltalk; Kay coined "object-oriented" |
| 1972 | Dennis Ritchie (Bell Labs) | C, created for Unix (rewritten in C in 1973) |
| 1972 | Alain Colmerauer | Prolog, for logic programming |
| 1973 | Robin Milner | ML, with Hindley–Milner type inference (Hindley 1969, Milner 1978) |
| mid-1970s | Stephen Johnson; Mike Lesk and Eric Schmidt | Yacc and Lex, the parser and lexer generators |
| 1979–83 | Bjarne Stroustrup | "C with Classes", renamed C++ in 1983 |
| 1981–82 | Gregory Chaitin | Register allocation by graph coloring |
| 1986 | Aho, Sethi and Ullman | The "Dragon Book" (Aho and Ullman received the Turing Award in 2020) |
| 1990 | Committee | Haskell, a lazy, purely functional language |
| 1991 | Guido van Rossum | Python, first released (started in 1989) |
| 1991 | Cytron et al. (IBM) | SSA form, efficient construction published |
| 1995 | James Gosling (Sun); Brendan Eich (Netscape) | Java, and the "write once, run anywhere" JVM; JavaScript, written in about ten days |
| 2006–2015 | Graydon Hoare, then Mozilla | Rust: memory safety without GC, through ownership. 1.0 released in 2015 |

## Canonical sources

- Abelson and Sussman, *Structure and Interpretation of Computer Programs* (SICP)
- Aho, Lam, Sethi and Ullman, *Compilers: Principles, Techniques, and Tools* (the Dragon Book)
- Cooper and Torczon, *Engineering a Compiler*
- Robert Nystrom, *Crafting Interpreters* (free online; builds two interpreters step by step)
- Benjamin Pierce, *Types and Programming Languages*
- Michael Scott, *Programming Language Pragmatics*
- Kernighan and Ritchie, *The C Programming Language*
- Each language's official specification or reference

## Classic misconceptions

- "Python passes by reference." Python passes object references by value ("call by sharing"). Rebinding a parameter doesn't affect the caller; mutating the object does.
- "Java passes objects by reference." Java passes references by value, which is the same model as Python's.
- "Compiled versus interpreted is a property of the language." It is a property of the implementation: CPython compiles to bytecode, PyPy JIT-compiles, and Java is both compiled and JIT-compiled.
- "Static typing means strong typing." These are independent axes; C is static and weakly typed.
- "Garbage collection means no memory leaks." Objects that are still reachable but no longer used will leak.
- Confusing `==` with `is` in Python, or `==` with `.equals()` in Java: value equality versus identity.
- "0.1 + 0.2 == 0.3." Binary floating point cannot represent 0.1 exactly (see IEEE 754 in the architecture playbook).
- "Recursion is always slower than iteration." It depends on the language and on optimizations like tail-call elimination, which Scheme requires and Python deliberately does not do.
- "Inheritance is the main point of OOP." Encapsulation and polymorphism matter more, and composition is often preferred.

## Question patterns

- What does this code print? Trace the stack and heap.
- What does this compile to? Read the bytecode or assembly.
- Rewrite this in a functional style, or an object-oriented one, and compare.
- Draw the AST for this expression, or evaluate it with an environment model.
- Compute FIRST and FOLLOW sets and build the LL(1) table. Is this grammar ambiguous?
- Infer the type of this expression.
- Why is this undefined behavior in C, and what might the compiler do with it?

## Tools and artifacts to show

Python's `dis` module, Compiler Explorer (godbolt.org), `javap -c`, Python Tutor (pythontutor.com) for visualizing the stack and heap, AST dumps (`ast.dump` in Python, `clang -Xclang -ast-dump`), and LLVM IR (`clang -S -emit-llvm`).

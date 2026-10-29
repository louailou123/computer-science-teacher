# Playbook: software engineering

**Covers:** requirements, software design principles (cohesion, coupling, information hiding, SOLID, DRY), object-oriented design and UML, design patterns, software architecture (layered, client-server, MVC, microservices, event-driven, hexagonal), testing (unit, integration, system, TDD, mocking, coverage), version control and Git internals, code review, refactoring, development processes (Waterfall, Agile, Scrum, Kanban, XP), CI/CD and DevOps, system design for scale, estimation, maintenance and technical debt.

## What a complete answer contains

- **For a principle or pattern:** use the classic pattern format:
  - the **problem and forces** (what makes the problem hard);
  - the **solution structure** (a UML class diagram in ASCII or Mermaid, plus a sequence diagram when the behavior matters);
  - **before-and-after code**, where the "before" has the smell the pattern removes;
  - the **consequences** (what you gain and what it costs);
  - **when *not* to use it**;
  - where it shows up in real frameworks and libraries (Iterator in every collection library, Observer in UI event systems, Strategy in `sort` comparators, Decorator in Python's `@decorator` syntax and Java I/O streams).
- **For testing:**
  - the test pyramid;
  - what each test level catches;
  - real test code (pytest or JUnit) with arrange-act-assert;
  - when to use mocks versus fakes;
  - the TDD cycle shown over an actual small feature;
  - what coverage does and doesn't measure (statement versus branch coverage, and mutation testing as a better signal).
- **For Git:**
  - the object model (blobs, trees, commits, tags, and refs as pointers to commits);
  - the commit DAG drawn before and after merge, rebase, cherry-pick and reset;
  - what each command actually does to `.git`, shown with `git cat-file -p` and `git log --graph`;
  - why rebasing shared history causes problems.
- **For architecture and system design:**
  - functional and non-functional requirements;
  - back-of-the-envelope estimates with the arithmetic shown (QPS, storage per year, bandwidth);
  - an API sketch and a data model;
  - a component diagram;
  - scaling techniques and the trade-off each makes (caching and invalidation, replication, sharding, load balancing, queues, CDNs);
  - bottlenecks and failure modes.
- **For process:** the historical context (why Agile reacted against heavyweight processes), what each practice is meant to achieve, and how teams actually run it.
- **Case studies of failures,** to show why the discipline exists: Therac-25 (1985–87, race conditions in a radiation therapy machine), the Ariane 5 Flight 501 explosion (1996, an unhandled overflow converting a 64-bit float to a 16-bit integer in reused code), and Knight Capital (2012, a deployment error that lost about $440 million in 45 minutes).

## Comparison dimensions

Coupling and cohesion, testability, changeability, team scalability, operational cost, performance, and complexity budget. For processes: predictability versus adaptability.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1968 | NATO Software Engineering Conference, Garmisch | "Software engineering" adopted as a discipline in response to the "software crisis". Margaret Hamilton also championed the term during the Apollo program |
| 1968 | Edsger Dijkstra | "Go To Statement Considered Harmful" and structured programming |
| 1970 | Winston Royce | The paper later cited as the origin of "Waterfall", although it warned against a purely sequential process |
| 1972 | David Parnas | "On the Criteria To Be Used in Decomposing Systems into Modules": information hiding |
| 1972 | Marc Rochkind (Bell Labs) | SCCS, an early version control system |
| 1975; 1986 | Fred Brooks | *The Mythical Man-Month* ("adding people to a late project makes it later"); "No Silver Bullet" |
| 1976 | Michael Fagan (IBM) | Formal code inspections |
| 1977 | Christopher Alexander | *A Pattern Language*, about building architecture; it inspired software patterns |
| 1987 | Barbara Liskov | The substitution principle, in her keynote "Data Abstraction and Hierarchy" (formalized with Jeannette Wing in 1994; Liskov received the Turing Award in 2008) |
| 1994 | Gamma, Helm, Johnson and Vlissides (the "Gang of Four") | *Design Patterns* |
| 1995 | Ken Schwaber and Jeff Sutherland | Scrum presented |
| 1997 | Grady Booch, James Rumbaugh and Ivar Jacobson, through the OMG | UML standardized |
| late 1990s | Kent Beck | Extreme Programming; later *Test-Driven Development: By Example* (2002) |
| 1999 | Martin Fowler | *Refactoring* |
| 2000 | Roy Fielding | His dissertation defines REST |
| around 2000 and 2004 | Robert C. Martin; Michael Feathers | The design principles, then the SOLID acronym for them |
| February 2001 | 17 practitioners, Snowbird, Utah | The Agile Manifesto |
| April 2005 | Linus Torvalds | Git, written for Linux kernel development. GitHub followed in 2008 |
| around 2009 | Patrick Debois and others | The DevOps movement |

## Canonical sources

- Ian Sommerville, *Software Engineering*
- Steve McConnell, *Code Complete*
- John Ousterhout, *A Philosophy of Software Design*
- Gamma et al., *Design Patterns*, and Freeman and Robson, *Head First Design Patterns*
- Martin Fowler, *Refactoring*
- Hunt and Thomas, *The Pragmatic Programmer*
- Robert C. Martin, *Clean Code* and *Clean Architecture* (influential, though some advice is debated, so say so)
- Scott Chacon and Ben Straub, *Pro Git* (free online)
- Kleppmann, *Designing Data-Intensive Applications*, and Alex Xu, *System Design Interview*, for system design

## Classic misconceptions

- "Use design patterns wherever possible." Patterns solve specific problems; using them where those problems don't exist only adds complexity.
- "100% coverage means no bugs." Coverage shows which lines ran, not that the assertions check the right behavior.
- "Agile means no planning and no documentation." The manifesto *values* working software *more than* comprehensive documentation; it does not reject documentation.
- "Microservices are always better." They trade code complexity for distributed-systems complexity, and suit large teams more than small ones.
- "Git stores diffs." Git stores snapshots (trees of blobs) and computes diffs when you ask; packfiles add delta compression only as a storage optimization.
- "Inheritance is the best way to reuse code." It creates tight coupling; prefer composition unless there is a true "is-a" relationship that satisfies Liskov substitution.
- "Waterfall was a recommended process." Royce's paper described it as risky.

## Question patterns

- Identify the code smells here and refactor, naming the principle behind each change.
- Which pattern fits this problem? Draw its class diagram.
- Write tests for this function, including edge cases.
- Draw the commit graph after these Git commands.
- Design this system for 10 million users, with estimates.
- Which principle does this design violate, and what breaks when requirements change?

## Tools and artifacts to show

Git with `git log --graph --oneline --all` and `git cat-file`, pytest and JUnit, coverage tools, Mermaid or PlantUML diagrams, linters and static analyzers, and CI configuration (for example GitHub Actions).

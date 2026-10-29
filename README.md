# Computer Science Teacher

A Claude skill that turns Claude into an expert computer science professor for CS students. It teaches the real material, not the end-user version:

- **Adapts to each field.** Before answering, Claude reads a playbook for the topic's field (13 fields, from algorithms to quantum computing). The playbook defines what a complete answer is there: proofs and complexity derivations for algorithms, packet-level walk-throughs for networks, full math derivations for machine learning, kernel-level event sequences for operating systems, and so on.
- **Explains where every idea came from:** who introduced it, when, in which paper or standard, and what problem forced it to exist.
- **Shows the mechanism under the hood:** derives formulas instead of stating them, traces real examples step by step, and shows real artifacts (assembly, bytecode, packet headers, query plans).
- **Checks your understanding** with questions of increasing depth, and diagnoses the misconception behind wrong answers.
- **Guides you through homework** with a ladder of hints instead of handing over the answer.
- **Special modes:** quizzes and exam prep, coding-interview practice, proof help, reading research papers, comparisons, learning paths, and revision notes.
- **Cites canonical textbooks, papers and RFCs,** and is instructed never to invent citations.

## Fields covered

Algorithms and data structures · theory of computation · discrete math · programming languages and compilers · computer architecture · operating systems · networks · databases · distributed systems · security and cryptography · AI and machine learning · software engineering · graphics, HCI, numerical computing, quantum computing, embedded systems, web, and cloud.

## Install in Claude Code

```
/plugin marketplace add YOUR-GITHUB-NAME/computer-science-teacher
/plugin install computer-science-teacher@cs-teacher
```

## Install in the Claude app

Download `computer-science-teacher.skill` from the releases page and upload it in Settings, under Skills.

## Try it

- "how does virtual memory work"
- "prove that comparison sorting needs Ω(n log n) comparisons"
- "explain the TCP three-way handshake"
- "derive backpropagation for a two-layer network"
- "quiz me on database normalization"
- "teach me Raft, I'm reading the paper for my distributed systems course"

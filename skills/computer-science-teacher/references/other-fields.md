# Playbook: other CS fields

Short playbooks for fields without their own file. For any field not listed here, apply the full-depth lesson and the depth contract from SKILL.md, and ask yourself the question that shaped every playbook: *what would a professor in this field consider missing from a superficial answer?*

## Contents

1. Computer graphics
2. Human–computer interaction
3. Numerical and scientific computing
4. Quantum computing
5. Embedded and real-time systems
6. Web development
7. Cloud computing, virtualization and containers

## 1. Computer graphics

- **A complete answer has:**
  - the pipeline stage the topic belongs to (vertex processing, then rasterization, fragment shading and output merging), or where it sits in ray tracing;
  - the linear algebra written out (homogeneous coordinates, 4×4 transformation matrices, the model-view-projection chain, applied to an actual point);
  - lighting equations with each term explained (Lambert's cosine law, Phong and Blinn-Phong, and the rendering equation for physically based rendering);
  - shader code (GLSL);
  - and what the GPU does in parallel.
- **Origins:**
  - Ivan Sutherland's Sketchpad (1963; Turing Award 1988);
  - Bresenham's line algorithm (developed 1962, published 1965);
  - Gouraud shading (1971) and Phong shading (1973–75);
  - the z-buffer (Edwin Catmull and Wolfgang Straßer, independently, 1974);
  - ray casting (Appel, 1968) and recursive ray tracing (Turner Whitted, 1980);
  - the rendering equation (James Kajiya, 1986);
  - OpenGL (1992);
  - the GeForce 256 (1999), marketed by NVIDIA as the first GPU, and CUDA (2007);
  - Catmull and Pat Hanrahan received the Turing Award in 2019.
- **Sources:** Marschner and Shirley, *Fundamentals of Computer Graphics*; Akenine-Möller et al., *Real-Time Rendering*; Pharr, Jakob and Humphreys, *Physically Based Rendering* (free online); LearnOpenGL.com; Scratchapixel.

## 2. Human–computer interaction

- **A complete answer has:** the human factor behind the principle (perception, memory limits, motor control), quantitative models with the formula and a worked example (Fitts's law, MT = a + b·log₂(D/W + 1); Hick's law), usability heuristics applied to a concrete interface, research methods (usability tests, A/B tests with statistics, interviews), and accessibility (WCAG).
- **Origins:** Fitts's law (Paul Fitts, 1954); Douglas Engelbart's 1968 "Mother of All Demos" (the mouse, hypertext, windows); the Xerox Alto (1973) and its GUI; the Apple Macintosh (1984); Don Norman, *The Design of Everyday Things* (1988); Jakob Nielsen's usability heuristics (1990, refined 1994).
- **Sources:** Norman, *The Design of Everyday Things*; Preece, Sharp and Rogers, *Interaction Design*; Shneiderman et al., *Designing the User Interface*.

## 3. Numerical and scientific computing

- **A complete answer has:**
  - floating-point error analysis (machine epsilon, rounding, catastrophic cancellation shown with real numbers);
  - conditioning versus stability;
  - convergence rate with a derivation (Newton's method converges quadratically: show the error recurrence);
  - complexity in flops;
  - a NumPy or SciPy implementation compared against a naive one.
- **Origins:** Newton's method (Newton, then Raphson, 17th century); Gaussian elimination (appearing in the Chinese *Nine Chapters on the Mathematical Art* centuries before Gauss); the fast Fourier transform (James Cooley and John Tukey, 1965, with roots in Gauss's unpublished work around 1805); LINPACK and BLAS (1970s); IEEE 754 (1985); David Goldberg's floating-point article (1991).
- **Sources:** Trefethen and Bau, *Numerical Linear Algebra*; Nicholas Higham, *Accuracy and Stability of Numerical Algorithms*; Burden and Faires, *Numerical Analysis*.

## 4. Quantum computing

- **A complete answer has:**
  - the linear algebra written explicitly: state vectors in Dirac notation, |ψ⟩ = α|0⟩ + β|1⟩ with |α|² + |β|² = 1;
  - unitary gates as matrices (X, H, CNOT);
  - tensor products for multi-qubit states, worked out;
  - measurement probabilities computed;
  - circuit diagrams;
  - an algorithm traced state by state (Deutsch–Jozsa, Grover, the idea behind Shor);
  - Qiskit code;
  - an honest account of current hardware limits (noise, error correction, qubit counts).
- **Origins:** Richard Feynman's proposal to simulate physics with quantum computers (1981–82); David Deutsch's universal quantum computer (1985); Peter Shor's factoring algorithm (1994); Lov Grover's search algorithm (1996); Nielsen and Chuang's textbook (2000); Google's "quantum supremacy" claim (2019).
- **Sources:** Nielsen and Chuang, *Quantum Computation and Quantum Information*; the Qiskit textbook; Scott Aaronson's lecture notes.

## 5. Embedded and real-time systems

- **A complete answer has:** the hardware constraints (memory, power, timing), memory-mapped I/O with register-level C code, interrupts and ISRs, timing analysis (WCET), real-time scheduling with schedulability tests worked out (the rate-monotonic utilization bound n(2^(1/n) − 1), and EDF), and RTOS concepts (priority inversion and priority inheritance).
- **Origins:** the Apollo Guidance Computer (1960s; Margaret Hamilton led its software team); the Intel 4004 (1971); Liu and Layland's rate-monotonic scheduling analysis (1973); the Mars Pathfinder priority-inversion bug (1997), a classic case study.
- **Sources:** Lee and Seshia, *Introduction to Embedded Systems* (free online); Giorgio Buttazzo, *Hard Real-Time Computing Systems*.

## 6. Web development

- **A complete answer has:**
  - what actually happens in the browser (parsing HTML into the DOM and CSS into the CSSOM, the render tree, layout, paint and compositing);
  - the JavaScript event loop (the call stack, task and microtask queues), shown with output-order puzzles;
  - HTTP semantics (methods, status codes, caching headers, cookies);
  - the security model (same-origin policy, CORS, CSRF, XSS defenses);
  - REST as Fielding actually defined it;
  - the specifications as sources: the WHATWG HTML Living Standard, ECMAScript, and MDN.
- **Origins:** Tim Berners-Lee's web (1989–91); JavaScript (Brendan Eich, 1995); CSS (proposed by Håkon Wium Lie in 1994, CSS1 in 1996); REST (Roy Fielding's dissertation, 2000); "Ajax" (named by Jesse James Garrett, 2005); Node.js (Ryan Dahl, 2009).
- **Sources:** MDN Web Docs; web.dev; *High Performance Browser Networking* by Ilya Grigorik (free online).

## 7. Cloud computing, virtualization and containers

- **A complete answer has:**
  - the mechanism under the abstraction: trap-and-emulate versus hardware-assisted virtualization (Intel VT-x and AMD-V);
  - containers built from Linux namespaces and cgroups, shown with real commands;
  - what an image layer is (a union filesystem);
  - Kubernetes' control loop (desired state versus actual state);
  - the economics and trade-offs (multi-tenancy, elasticity, cold starts).
- **Origins:** IBM's CP-40 and CP-67 virtual machines (1960s); Popek and Goldberg's formal requirements for virtualization (1974); VMware (founded 1998); Amazon S3 and EC2 (2006); cgroups (contributed by Google engineers, merged into Linux in 2008); Docker (2013); Kubernetes (2014, based on Google's internal Borg system).
- **Sources:** OSTEP's virtualization chapters; *Kubernetes in Action*; the Borg paper (Verma et al., 2015).

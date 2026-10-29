# Playbook: computer architecture and organization

**Covers:** number representation (binary, hexadecimal, two's complement, IEEE 754 floating point), digital logic (gates, combinational and sequential circuits, flip-flops), the CPU (datapath, control, ALU, registers), instruction set architectures and assembly (x86-64, ARM, RISC-V, MIPS), instruction encoding, pipelining and hazards, superscalar and out-of-order execution, branch prediction, caches and the memory hierarchy, virtual memory hardware (TLB, page walks), I/O and interrupts, multicore, coherence, GPUs, performance.

## What a complete answer contains

- **Bit-level work done by hand:** conversions, two's complement negation and overflow detection, and IEEE 754 encoding and decoding with the sign, exponent (with its bias) and mantissa fields shown bit by bit. For example, show why 0.1 cannot be represented exactly.
- **Circuits:** truth tables, Boolean simplification or Karnaugh maps, the gate diagram, and timing (propagation delay, critical path, clock period).
- **Instruction encoding with real bit fields.** For example, the RISC-V R-type format is `funct7 | rs2 | rs1 | funct3 | rd | opcode` with widths 7/5/5/3/5/7. Encode a real instruction into binary and hex.
- **The mapping from C to assembly:** show the compiler output for a loop, a function call (the calling convention, prologue and epilogue, the stack frame), and an array access.
- **A cycle-by-cycle pipeline diagram** (IF, ID, EX, MEM, WB) for an instruction sequence, showing hazards (data, control, structural), stalls, forwarding paths and branch penalties.
- **Cache mechanics with concrete numbers:**
  - split an address into tag, index and offset for a given cache geometry;
  - simulate a sequence of accesses (hit or miss, and which line is evicted);
  - classify misses (compulsory, capacity, conflict);
  - compute the average memory access time, AMAT = hit time + miss rate × miss penalty, deriving it level by level for multi-level caches.
- **The performance equations, derived and applied:**
  - CPU time = instruction count × CPI × clock cycle time;
  - Amdahl's law, speedup = 1 / ((1 − f) + f/s), derived from the time split;
  - why clock rate alone is a misleading metric.
- **Virtual memory hardware:** a full translation walk with concrete numbers (virtual page number and offset, the TLB lookup, the multi-level page-table walk, physical address), and what happens on a TLB miss versus a page fault.
- **Real hardware:** how this works on actual x86-64, ARM (Apple M-series) or RISC-V chips, and where the textbook model simplifies (micro-ops, register renaming, the reorder buffer).

## Comparison dimensions

CISC versus RISC, ISA versus microarchitecture, latency versus throughput, cache organization (direct-mapped, set-associative, fully associative; write-through versus write-back), performance per watt, and cost.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1820s; 1837 | Charles Babbage | The Difference Engine; the design of the Analytical Engine, a general-purpose mechanical computer |
| 1937 | Claude Shannon | Boolean algebra applied to switching circuits |
| 1941 | Konrad Zuse | Z3, the first working programmable, fully automatic digital computer |
| 1943–45 | Tommy Flowers (Bletchley Park) | Colossus, electronic codebreaking machines |
| 1945 | J. Presper Eckert and John Mauchly | ENIAC (publicly unveiled in 1946) |
| 1945 | John von Neumann | "First Draft of a Report on the EDVAC": the stored-program architecture |
| 1947 | Bardeen, Brattain and Shockley (Bell Labs) | The transistor |
| 1948 | Manchester Baby | The first stored-program computer to run a program |
| 1949 | Maurice Wilkes (Cambridge) | EDSAC. Wilkes also proposed microprogramming in 1951 and described caches ("slave memories") in 1965 |
| 1958–59 | Jack Kilby (TI); Robert Noyce (Fairchild) | The integrated circuit |
| 1964 | Amdahl, Blaauw and Brooks (IBM) | System/360: the ISA as a contract separate from implementation, and the 8-bit byte becoming standard |
| 1965 | Gordon Moore | Moore's law (revised in 1975 to a doubling roughly every two years) |
| 1967 | Gene Amdahl | Amdahl's law |
| 1967 | Robert Tomasulo (IBM 360/91) | Tomasulo's algorithm for out-of-order execution |
| 1968 | IBM System/360 Model 85 | The first commercial machine with a cache |
| 1971 | Intel | The 4004, the first commercial microprocessor |
| 1974 | Robert Dennard | Dennard scaling. Its breakdown in the mid-2000s pushed the industry to multicore |
| 1975–81 | John Cocke (IBM 801); David Patterson (Berkeley RISC); John Hennessy (Stanford MIPS) | RISC (Hennessy and Patterson received the Turing Award in 2017) |
| 1985 | William Kahan and the IEEE committee | IEEE 754 floating point (Turing Award 1989) |
| 2010 | UC Berkeley | RISC-V, an open ISA |
| 2018 | Several research teams | Spectre and Meltdown: speculative execution leaks data through caches |

## Canonical sources

- Patterson and Hennessy, *Computer Organization and Design* (RISC-V, MIPS and ARM editions)
- Hennessy and Patterson, *Computer Architecture: A Quantitative Approach*
- Bryant and O'Hallaron, *Computer Systems: A Programmer's Perspective* (CS:APP)
- Harris and Harris, *Digital Design and Computer Architecture*
- Nisan and Schocken, *The Elements of Computing Systems* (the Nand2Tetris course, which builds a computer from NAND gates)
- David Goldberg, "What Every Computer Scientist Should Know About Floating-Point Arithmetic" (1991)

## Classic misconceptions

- "A higher clock speed means a faster CPU." Performance also depends on CPI and instruction count.
- "Twice the cores means twice the speed." Amdahl's law limits speedup by the serial fraction.
- "RISC means fewer instructions." It means simpler, regular instructions (load/store architecture, fixed encoding), designed so they can be pipelined.
- "The cache is just faster RAM." It only helps because programs have temporal and spatial locality. Access patterns decide whether it helps at all.
- "Floats store decimal numbers exactly." Most decimal fractions are rounded to the nearest representable binary fraction.
- "64-bit means twice as fast as 32-bit." It refers to register and address width.
- "Instructions execute one after another." Modern cores pipeline, execute out of order and speculate, while preserving the *appearance* of sequential execution.
- "Integer overflow throws an error." In two's complement hardware it wraps around silently. In C, signed overflow is undefined behavior.

## Question patterns

- Convert, add and detect overflow in two's complement. Encode a value in IEEE 754.
- Encode or decode this instruction.
- Draw the pipeline diagram; how many cycles, where are the stalls, and what does forwarding fix?
- For this cache geometry and access sequence, give the hit or miss for each access and the final contents.
- Compute CPI, execution time, speedup or AMAT.
- Translate this virtual address.
- Translate this C function to assembly, or explain this assembly.

## Tools and artifacts to show

Compiler Explorer (godbolt.org), RARS or Venus (RISC-V simulators), MARS (MIPS), Logisim (circuits), `perf stat` for cache-miss counters, `objdump -d`, and cache simulators.

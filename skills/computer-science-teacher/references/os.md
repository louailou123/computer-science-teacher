# Playbook: operating systems

**Covers:** the kernel and its responsibilities, system calls, user and kernel mode, processes and threads, context switching, CPU scheduling, concurrency (race conditions, critical sections, locks, semaphores, condition variables, monitors), deadlock, memory management (address spaces, paging, segmentation, page replacement), file systems, I/O and device drivers, virtualization and containers, OS security.

## What a complete answer contains

- **The exact sequence of events.** For example, a system call goes:
  1. user code calls a libc wrapper;
  2. the arguments go into registers;
  3. a trap instruction (`syscall` on x86-64) switches to kernel mode;
  4. the kernel dispatches through its syscall table to the handler;
  5. the kernel returns to user mode with the result.

  Show what is saved and restored at each step.
- **The kernel data structures involved:** the process control block (Linux `task_struct`), page tables, the file-descriptor table, the open-file table, inodes, run queues, and wait queues.
- **State diagrams** (process states: new, ready, running, blocked, terminated) and which events cause each transition.
- **Scheduling worked by hand:** Gantt charts for FCFS, SJF, SRTF, Round Robin, priority, and MLFQ, computing waiting, turnaround and response times for a given process set. Then what real kernels do: Linux used CFS from 2.6.23 (2007) and switched to EEVDF in 6.6 (2023).
- **Concurrency:**
  - show an interleaving trace in which a race corrupts data, at the level of `load`/`add`/`store` instructions;
  - fix it with a mutex, semaphore or condition variable, and show the corrected trace;
  - prove the properties needed (mutual exclusion, progress, bounded waiting) for algorithms like Peterson's;
  - explain why hardware atomic instructions (test-and-set, compare-and-swap) are needed on real machines.
- **Deadlock:** the four Coffman conditions, a resource-allocation graph, which condition each prevention strategy breaks, and the banker's algorithm worked step by step with matrices.
- **Memory:**
  - address translation with concrete numbers;
  - page-replacement simulations (FIFO, LRU, OPT, Clock) with fault counts, including Belady's anomaly;
  - thrashing and the working-set model;
  - copy-on-write after `fork()`;
  - demand paging, and what happens on a page fault.
- **File systems:**
  - inode structure, and computing the maximum file size from direct and indirect block pointers;
  - directory lookup;
  - journaling, and crash consistency scenarios.
- **Real code using the POSIX API:** `fork`, `exec`, `wait`, `pipe`, `dup2`, `mmap`, `pthread_create`, `pthread_mutex_lock`, with the output explained (including nondeterministic interleavings).
- **Real systems:** how Linux, Windows and macOS each do it, and where the textbook simplifies.

## Comparison dimensions

Processes versus threads (isolation, creation cost, sharing), user-level versus kernel-level threads, monolithic kernels versus microkernels, preemptive versus cooperative scheduling, the scheduling metrics (throughput, latency, fairness), and paging versus segmentation.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| 1956 | General Motors and North American Aviation | GM-NAA I/O for the IBM 704, often called the first OS (batch processing) |
| 1961 | Fernando Corbató (MIT) | CTSS, an early time-sharing system (Turing Award 1990) |
| 1962 | University of Manchester | The Atlas computer: the first virtual memory with paging |
| early 1960s | Theodorus Dekker, described by Dijkstra | Dekker's algorithm, the first known correct software solution to mutual exclusion for two processes |
| early to mid 1960s | Edsger Dijkstra | Semaphores, the dining philosophers (1965), the banker's algorithm |
| 1964–69 | MIT, Bell Labs and GE | Multics: hierarchical file system, protection rings, dynamic linking |
| 1966; 1969 | László Bélády | The optimal (MIN) page-replacement algorithm; Belady's anomaly |
| 1968 | Edsger Dijkstra | THE multiprogramming system, built in layers |
| 1968 | Peter Denning | The working-set model |
| 1969 | Ken Thompson and Dennis Ritchie (Bell Labs) | Unix (rewritten in C in 1973, described in CACM in 1974; Turing Award 1983) |
| 1971 | Coffman, Elphick and Shoshani | The four necessary conditions for deadlock |
| 1973–74 | Per Brinch Hansen; Tony Hoare | Monitors |
| 1974 | Leslie Lamport | The bakery algorithm |
| 1975 | Fred Brooks | *The Mythical Man-Month*, lessons from building OS/360 |
| 1977 onward | UC Berkeley | BSD Unix |
| 1981 | Gary Peterson | Peterson's algorithm |
| 1985 | Carnegie Mellon | The Mach microkernel, later part of the base of macOS |
| 1988 | IEEE | POSIX (IEEE 1003.1) |
| 1991 | Linus Torvalds | Linux, announced August 25, 1991 |
| 1993 | Dave Cutler and team (Microsoft) | Windows NT |

## Canonical sources

- Remzi and Andrea Arpaci-Dusseau, *Operating Systems: Three Easy Pieces* (OSTEP, free online)
- Silberschatz, Galvin and Gagne, *Operating System Concepts* (the "dinosaur book")
- Andrew Tanenbaum, *Modern Operating Systems*
- Robert Love, *Linux Kernel Development*
- Michael Kerrisk, *The Linux Programming Interface*
- MIT's xv6, a small teaching Unix with a book that explains its source code

## Classic misconceptions

- "A process and a program are the same thing." A program is a file; a process is a running instance with its own state and address space.
- "Threads always make programs faster." Synchronization, contention, context switches and Amdahl's law can make them slower.
- "Virtual memory means swap." Virtual memory is the address-translation abstraction. Swapping to disk is one optional use of it.
- "`fork()` copies the whole memory." Modern kernels use copy-on-write; pages are copied only when written.
- "`volatile` makes code thread-safe." In C and C++ it doesn't provide atomicity or ordering. Atomics and locks do.
- Confusing deadlock, livelock and starvation.
- "The kernel is a process that runs in the background." The kernel is code that runs in kernel mode on behalf of processes (through system calls) and in response to interrupts. It also has its own kernel threads.
- "More RAM always makes a computer faster." It only helps if the working set didn't fit before.

## Question patterns

- Draw the Gantt chart and compute the average waiting and turnaround times.
- How many times does this `fork()` program print, and in what possible orders?
- Find the race condition in this code and fix it.
- Is this state safe (banker's algorithm)? Can this resource-allocation graph deadlock?
- Count the page faults for this reference string under FIFO, LRU and OPT.
- Translate this address; what is the page-table size for this configuration?
- What is the maximum file size for this inode structure?

## Tools and artifacts to show

`strace` (system calls), `ltrace`, `ps`, `top` and `htop`, `/proc/<pid>/maps` (the address-space layout), `pmap`, `gdb`, `perf`, `lsof`, `vmstat`, and short C programs that demonstrate `fork`, pipes and races.

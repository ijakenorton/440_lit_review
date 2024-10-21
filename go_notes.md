## The benefits and costs of writing a POSIX kernel in a high-level language

Evaluation of a high-level language to implement a POSIX-style kernel

Costs and benefits of using GO vs C 





# Why C

C is the default language, it was built for making operating systems, turns out to be pretty good
for it. It allows full control of the system and memory, memory bugs cause a lot of security
vulnerabilities. Pointer arithmetic is powerful, legacy and history, direct hardware register
manipulation, (isn't that just having assembly support?)

# Why HLL

Go provides type and memory-safety at the cost of needing to have a garbage collector, which reduces
burden from the programmer but removes the fine-grained control.

People have tried building with high-level languages, though none have really stuck, people argue
that you can't have a GC in a kernel. Generally the focus for HLL kernels is safety over
performance. None have tried to do such a specific performance comparison

Current linux kernel would be difficult to implement GC

# Implementation Details

## Heap exhaustion

Made things easier, but sorting out the kernel heap memory was difficult
Having to fix the heap memory forced a new solution to kernel OOM problems, system calls must
reserve memory before they actually try to allocate. They will wait before they do so, but after
they have memory, there is no complex allocation recovery of locks/ failure. "Biscuit applications
don't see system call failures when the heap is exhausted; instead, they see delays."

# Results
The GO version was 5% to 15% slower, GC costs up to 3% of CPU, longest pause was 115 microseconds.
Other language costs were around 10%

Has enough to be able to compare fairly sophisticated things

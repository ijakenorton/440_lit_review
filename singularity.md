# Intro

Software is built off of very old paradigms, maybe its worth rebuilding from the ground up. Using
language safety features may allow for a reduction is safety tax code

Singularity is a platform for trying out novel ideas, very much a research operating system.

    - prevents memory bugs
    - Powerful compiler / verification tools to pick on errors early 
    - Runtime errors are caught at well defined boundaries
    

# Processes

## Open Processes
Multics processes include support for:
    - Dynamic code loading
    - Dynamic code generation
    - Access to cross-process shared memory
    - Universal API capable of directly modifying data in another process

Universal due to the following reasons:
    - Improved memory utilization by sharing library code
    - These days its more important that you can add plugins to existing processes

Disadvantages:
    - Need hardware protection to ensure security and process isolation
    - Hardware isolation is not free, 2.5% in compute tasks, 33% in IPC tasks due to page table
        management and cache and TLB misses
    - Extensions cause issues, no hard interface between running process and extension
    - Dynamic code can alter running program state, the program just has to assume this is fine,
        harder to analyse and have to assume the environment won't change underneath
    - Cannot rely on process security, have to rely on user level access
 
## Sealed Process Architecture


### Constraints

    - Guarantees code in a process cannot be altered once the process starts
    - No dynamic code loading
    - No self-modifying code
    - Process limited API
    - Strict extension mechanism, extensions execute in a new process, communicate through channels?

### Advantages

    - Increase static program analysis
    - Stronger security guarantees
    - Elimination of duplicatio of OS-level features in virtual execution environments
    - Encourage better software engineering
    - Forces developers to use defined interfaces
    - Enables aggressive tree shaking as there is no dynamic code that could use unused parts of the
        program

### SING SIPs
    - Assumes a sealed kernel
    - Provides isolated context for processes to run in.
    - Can have multiple threads of execution 
    - Isolates the errors so if one SIP fails it does not crash system
    - Communication between SIPs must be done through channels
    - Cannot share writable memory with other SIPS
    - Isolated with software protection instead of hardware
    - 

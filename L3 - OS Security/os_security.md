# OS Security
## OS Role
- provide ease of use and high level abstractions for resources like memory and files
- provides controlled access to hardware resources
- provides isolation between different processes
    - separates untrusted application code and trusted OS
## Trusted OS Requirements (TCB)
1. Tamper Proof
    - Need hardware support for memory protection
    - processor execution modes (system vs user mode)
    - privelaged instructions that can only be used in system mode
    - syscalls to transfer control between user/system mode
        - cost to make these calls is greater than a regular call (takes more time/computing resources)
2. Complete Mediation
    - ensure that no protected resource can be accesses without going through the TCB
    - user code cannot access OS address space without changing to system mode
        - user code cannot access physical resources, as you need to be in system mode to execute privelaged instructions
    - OS virtualizes physical resources and provides API for them
        - virtual resource (like files) must be translated into physical resource handles - only done by OS (ensures mediation)
3. Correct
    - cannot be bugs in OS code
    - smaller and simpler = better
    - must use secure coding practices 

- TCB controls access to protected resources
    - does this through authorization/access control to identify source of request
### Isolating User Processes
- OS uses hardware support for memory protection
- processes view memory as contiguous and larger than actual physical memory size (2200 - page tables and memory virtualization)
    - each process has own mapping
- OS maps virtual address/pages to physical memory frames
- OS can map pages of different processes to same physical page, but must explicitly denote that sharing is desired
- Process A cannot access process B memory - no way of knowing where process A's memory is
- page table managed by OS
- processor memory management unit uses page tables to convert virtual addresses into physical addresses

## OS Isolation
- OS/kernel resides in portial of each process's address space
    - processes can only cross fence to OS in controlled ways

## Limiting Damage of Compromised OS
- hypervisors, VMs, guest OSs
    - if 1 VM is compromised, only apps running on that VM are compromised
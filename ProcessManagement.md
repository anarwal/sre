Process Management: 
- Processes are started in user space
- Process is an abstraction of running program
- Process includes set of resources, like open files, pending signals, internal kernel data, state, address space
- Threads are units of running program, they are within processes 
- Threads do not have their own process space and other resources but use process’s. Resources
- System calls used by processes to create child and pother processes:
    - fork(): create new process by duplicating the existing process. This is used to create child process where the existing process becomes parent process
    - Exec(): it replaces the current process with new program. Here as no new process created, it uses same PID
    - vfork(): it is similar to fork, however in vfork() parent is temp suspended until child process completes which doesn’t happen in fork
    - system(): It uses fork() command’s variation. To create child process
    - clone(): they are like fork but they allow child to share execution context with parent who calls it. Like memory space, table of Giles descriptions and table of signal handlers. 
vfork() is faster the fork()

- Kernel stores all the process in a doubly linked list which stores all the data about process. Each element is called process descriptor in this list

Process state:
- Existing task calls fork() and starts new process
- Task is forked and goes in task running state where it gets ready but is not running
- Scheduler calls context switch to run task, if it can finish right away, task exits and goes in zombie state
- If task needs another event to finish, it goes in interrupt state where it waits for specific event to finish and goes back to step 2
 Kthread:
- Similar to thread but only runs in kernel space
- They do not context switch in user space like normal threads would
- kthread do not have address space as they run already in address space.

System Calls: OS needs to perform following activities:
- Process Management: start, run and stop process
- File management: create, open, close, read, write, rename files
- Memory management: Allocate and deallocate memory
- Timing, scheduling stuff and networking management
User space uses system calls to perform above operations. How system calls help:
- They provide abstraction to user space (it need not worry about intricacies of call)
- Maintain system security and scalability as kernel authenticates each. System call before requesting the service
- It provides virtualization of various process 
How are system calls implemented:
- Define the purpose of system call. It should have exactly one purpose
- Define arguments, return values and error codes. System call should have simple interface with smaller number of arguments
- Final step is to add entry to system call table, then in kernel it is compiled 
Verification done for system calls:
- All parameters are valid and legal, like access permissions
- As kernel calls can be hacked so need to make sure no invalid input is provided
- Pid and file descriptor should be checked for validity
- Pointers should be checked for validity as process might try to pass pointer to read some data from another process but it may not have access to do so.
Before Following pointe run user-space:
- Check if pointer points to memory in user spacer only, not kernel space
- Check if pointer points to memory in. Process’s address space and not other process space
- Memory is marks according to read or write, pointer should not be able to bypass that access restriction. 

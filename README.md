# sre

1. What happens when you type website name on your computer 
    - It looks for IP address in your name server (could be your router) 
    - If not available there goes to ISP which might have IP address for the DNS stored
     - If ISP doesn’t have it, ISP reaches out to root DNS server and ask for IP address, if Root server doesn’t have it , it will provide next forwarding address 
    - Till the request keeps hoping to DNS servers to find IP address and might go to actual DNS server of website which will provide IP address 
    - Once requestor receives the IP address, it goes to destination and perform Handshake 
    - Once that is done data is returned to the name server which caches the data and finally returns the website to us

2. Linux Boot Process 
    - BIOS POST: perform hardware check 
    - Initialize GRUB which is responsible for loading OS and filesystem from MBR 
    - after kernel has been given access, it uses systemd to start all the processes 
    Refer: https://leetcode.com/discuss/interview-question/125107/What-happens-when-we-turn-on-computer
    
3. Filesystems 
    - What are inodes: they store file metadata, they are created at system boot up and are limited in ext file system, whereas ifs can scale if we run out of nodes available
     - you can use inodes to delete file, by removing the inode for particular file 
    - each process stores its files in /proc where you can see all the files used/opened by that process 
    - Under system /etc/limits you can edit the limits allowed for each process
    
4. Kernel 
    - Linux operating system has two space basically:  
        —> User space: which executes user applications,  this also has GNU C library which provides access to kernel space and allows transition between user space application and kernel  
        —> Kernel Space: this further level system call interface, kernel and architecture dependent code
        
    - Basics Components of kernel Space:
       - SCI: System. Call interface this is an interface which provides means to perform system calls from user space into kernel 
       - Process Management: Focusses on execution of processes (threads), kernel provides APIs to user space via SCI to perform operations for processes
       - Memory management: Kernel includes means to manage the available memory for processes execution (which is 4KB), but also provides mechanisms to control physical and virtual mappings. It moves. Processed from memory to disk when all the available memory is exhausted.  
       - Virtual File system: VFS provides common interface abstraction for file systems. It provides a switching mechanism between different file systems. This also has Buffer cache which stores data in between file system sand physical storage. - Network Stack: This provides interaface to communicate with networking subsystem and various protocols like TCP and Internet protocol. 
       - Device Drivers: Majority of code lives here, which provides various device drivers and makes the device usable.  
       - Architecure Dependent code: though majority of code is independent if architecture but there are few things which depends on the underlying system. 
        
Linux has new implementation Kernel based Virtual Machine called KVM which allows new interface to user space and allows OS to run above KVM based kernel.
 Another use is hypervisor where we use Linus for other running other OS.

5. Troubleshooting
     - Best Practice route suggested by Netflix    
        -> Uptime: to get load average which tells what all processes are trying to run on system by CPU demand    
        -> dmseg | tail: this gives last 10 commands which were run on machine and bio can see if there was any performance hit in that timeframe     
        -> vmstat: this tells the virtual memory in use by processes , there is a newer command available dstat which combines all vmstat (virtual memory), iostat (CPU stats), ifstat. With vmstat you can look for r (which is the no of processed running on cpu and wait for their turn), free which tells you free memory available, si and so which tells swap in and swap out memory     
        -> mpstat: which tells CPU time breakdown and can help us figure out if single CPU has most load      
        -> pidstat: rolling process summary, can help us understand which process is using most CPU      
        -> iostat: I/o stats       
        -> free -m       
        -> sar      
        -> top rolling summary of all the commands which came up virtual memory, swap memory, load avg, cpu usage, process detail 
        
6. Networking:

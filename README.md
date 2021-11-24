# sre

## 1. What happens when you type website name on your computer
   
- It looks for IP address in your name server (could be your router)
- If not available in router request goes to ISP which might have IP address for the DNS stored
- If ISP doesn’t have it, ISP reaches out to root DNS server and ask for IP address, if Root server doesn’t have it , it will provide next forwarding address
- Till the request keeps hoping to DNS servers to find IP address and might go to actual DNS server of website which will provide IP address
- Once requestor receives the IP address, it goes to destination and perform Handshake
- Once that is done data is returned to the name server which caches the data and finally returns the website to us.

## 2. Linux Boot Process
- BIOS POST- hardware check
- Initialize GRUB which is responsible for loading OS and filesystem from MBR
- after kernel has been given access, it uses systemd to start all the processes
- https://leetcode.com/discuss/interview-question/125107/What-happens-when-we-turn-on-computer

## 3. Filesystems
What are inodes: 
- They store file metadata, they are created at system boot up and are limited in ext file system, whereas ifs can scale if we run out of nodes available.
- Inodes contain owner, mode, size, acl
- you can use inodes to delete file, by removing the inode for particular file
- each process stores its files in /proc where you can see all the files used/opened by that process
- Under system /etc/limits you can edit the limits allowed for each process
- If filesystem is full and you want to free up the space:  
    - see if file is open using lsof, if not you can delete the file
    - if it is used, you can using cp /dev/null which will reduce the file size to zero
    - if flisystem has reserve, you can reduce reserve space

## 4. Kernel
- Linux operating system has two space basically:  
  —> **User Space**: which executes user applications,  this also has GNU C library which provides access to kernel space and allows transition between user space application and kernel
  —> **Kernel Space**: this further level system call interface, kernel and architecture dependent code 
  Basics Components of kernel Space:
    - **SCI**: System. Call interface this is an interface which provides means to perform system calls from user space into kernel
    - **Process Management**: Focusses on execution of processes (threads), kernel provides APIs to user space via SCI to perform operations for processes
    - **Memory management**: Kernel includes means to manage the available memory for processes execution (which is 4KB), but also provides mechanisms to control physical and virtual mappings. It moves. Processed from memory to disk when all the available memory is exhausted. 
    - **Virtual File system**: VFS provides common interface abstraction for file systems. It provides a switching mechanism between different file systems. This also has Buffer cache which stores data in between file system sand physical storage.
    - **Network Stack**: This provides interaface to communicate with networking subsystem and various protocols like TCP and Internet protocol. - Device Drivers: Majority of code lives here, which provides various device drivers and makes the device usable.
    - **Architecure Dependent code**: though majority of code is independent if architecture but there are few things which depends on the underlying system. Linux has new implementation Kernel Based Virtual Machine called KVM which allows new interface to user space and allows OS to run above KVM based kernel. Another use is hypervisor where we use Linus for other running other OS 

## 5. Troubleshooting
Best Practice route suggested by Netflix:  
   -> uptime: to get load average which tells what all processes are trying to run on system by CPU demand
   -> dmseg | tail: this gives last 10 commands which were run on machine and bio can see if there was any performance hit in that timeframe
   -> vmstat: this tells the virtual memory in use by processes , there is a newer command available dstat which combines all vmstat (virtual memory), iostat (CPU stats), ifstat. With vmstat you can look for r (which is the no of processed running on cpu and wait for their turn), free which tells you free memory available, si and so which tells swap in and swap out memory
   -> mpstat: which tells CPU time breakdown and can help us figure out if single CPU has most load 
   -> pidstat: rolling process summary, can help us understand which process is using most CPU    
   -> iostat: I/o stats       
   -> free -m       
   -> sar: displays the contents of selected cumulative activity counters in the operating system. Information is reported on the paging system, i/o, CPUs, network interfaces, swap space, file system, and others.
   -> top: rolling summary of all the commands which came up virtual memory, swap memory, load avg, cpu usage, process detail 

## 6. Networking
Operating systems use load balancing to schedule tasks across physical processors, container orchestrators such as Kubernetes use load balancing to schedule tasks across a compute cluster, and network load balancers use load balancing to schedule network tasks across available backends.

#### Benefits of Load Balancing:
- **Naming abstractions**: Clients just need to know the load balancer address/ name and not every backend
- **Fault tolerance**: Using health checks and autoscaling, can handle fault in the system
- **Cost and performance benefits**: Reduces cost by distributing appropriately in the network by reducing latency

#### Load Balancing Algorithms:
- **Random**: Uses random number generator and forwards the call randomly based on that.
- **Round Robin**: Using a circular queue, load balancer walks through it. Sending one request per server
- **Weighted round robin**: New web servers are assigned higher weight whereas old one are provided lower weight, Load balancer send more traffic to the ones with higher weight
- **Dynamic Round robin**: dynamically weight is generated and if two have same then based on round robin request is forwarded
- **Fastest**: Load balancer forward based on shortest response time
- **Least connections**: Load balancer forward based on least number of connections
- **Observed**: combination of fastest and least connections
- **Predictive**: Based on observed, it predicts which one will behave better

####L4 vs L7 load balancing:
- At L4 LB has visibility to network information like application port and protocol like tcp/udp and it does load balancing based on this limited networking info by combining with round. Robin or observed
- At L7, LB has more information about application and can perform more complex LB. With help of HTTP, LB can identify client session using cookies and perform load balancing based on that

#### Reverse Proxy vs Load Balancing:
- Load balancing is type of proxy. Load balancer serves multiple instances of same application based on various algorithms and does not store cache. With proxy you don’t need multiple instances, but it serves as isolation of your backend servers and also maintains cache for your backend

#### Proxy vs Reverse Proxy:
Servers behind the proxy do not know about the client is, they just serve the response based on what proxy send them whereas in reverse proxy, client doesn’t know who the servers are and reverse proxy forwards it based on the setup. Load balancing is an example of reverse proxy.
Features of Load balancing:
- **Service discovery**: Discovers available backend using this, examples are DNS, etcd, consul
- **Health check**: determines if the backend can serve traffic or not
- **Load balancing**: Based on lb algorithm, balding is done
- **Sticky sessions**: Based on client session and cookies in someone scenarios, requests needs to go to same backend server, this is determined using sit key sessions
- **TLS termination**: l7 load balancers perform xls/ssl termination (decryption)
- **Observability**: Logging of your backend servers

#### Types of load balancer topologies: 
- **Middle Proxy**: Typical, where it is single point of failure, accepts all calls from client and forward to backend. Example ALB, NLB
- **Edge proxy**: Similar to middle proxy but uses internet thus must provide tls termination. Authentication like feature
- **Embedded client proxy**: Proxy is embedded with services this reduces latency and single point of failure but raises concern of implementing in all available language in which backend is written. Example grpc
- **Sidecar proxy**: language agnostic, becoming famous as it is concept of service mesh. Example nginx, envoy, linkerd

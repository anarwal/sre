Docker allows us to run applications in isolation using containers where container are lightweight virtualization. Docker containers run on top of host operating system sharing filesystem, OS, kernel space.  
Docker is currently the only ecosystem providing the full package:
* Image management
* Resource Isolation
* File System Isolation
* Network Isolation
* Change Management
* Sharing
* Process Management
* Service Discovery 

Build on top of:
- namespaces: they provide isolation of resources from other workspaces for a container. When container created various namespaces are created namely: pid, net, idc, mnt, uts
- Croups: this is a linux containers (lxc) technology which allows docker to limit resources for a specific application from base host 
- Union file system: docker is build on top of file systems, where each Laye is file system
- Container format: libcontainer for now 

Docker networking:
- Bridge: when you init access of containers to a specific network. i.e. containers only on the bridge network can communicate with each other 
- Host: docker uses host’s network and ports
- Overlay: sits on top of networks and allows containers to communicate securely when encryption is enabled

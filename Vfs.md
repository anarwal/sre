VFS
It is kernel’s file system which handles system calls to vary su files systems. It provides a common interface to all the file systems User space interact with VFS which knows how to talk to a specific file system and it translates the call accordingly

Unix filesystem: 
- it is a hierarchical storage of data following a particular structure. 
- It contains files, directories, associated control information. 
- It has operations like creating, deleting and mounting.
- Filesystems are mounted at a specific mount point in namespace.  
- Mounting in global namespaces allows them to look like a tree structure. 
Abstractions provided for file system:
- Mount points
- Directory entries
- Files
- Inodes

Main Object types in VFS:
- File Object: Open file associated with a process. Block of logical data for process
- Dentry Object: It maintains mapping of files to related inode. It also keeps most recently access files cached.
- Inode Object: It is metadata about file
- Superblock Object: It is file system metadata. Because it is very important, it is stored in multiple locations It helps in menial recovery. 

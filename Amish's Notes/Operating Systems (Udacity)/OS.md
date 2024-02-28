## P1L1
- Recommended Textbooks:
	1. Operating System Concepts (Silberschatz)
	2. Operating System Concepts: Essentials (Silberschatz)
	3. Modern Operating Systems (Tanenbaum)
	4. Operating Systems: Three Easy Pieces (Dusseau)
## P1L2
- An OS is a special piece of software that abstracts (to simplify what the hardware actually looks like) and arbitrates (to manage the hardware use) the use of a computer system.
- An operating system:
	- directs operational resources (control use of CPU, memory, peripheral devices)
	- enforces working policies (fair resource access, limits to resource usage)
	- mitigates difficulty of complex tasks (abstract hardware details (system calls))
- There isn't a single formal definition of OS.
- An operating system sits between applications like servers, databases, skype etc. and the physical hardware like CPU, GPU, memory etc.
- An OS:
	- hides hardware complexity
	- resource management
	- provide isolation and protection to processes
- ![[Pasted image 20240227162236.png]]
- In summary,
  An operating system is a layer of systems software that:
  - directly has privileged access to the underlying hardware
  - hides the hardware complexity
  - manages hardware on behalf of one or more applications according to some predefined policies
  - in addition, it ensures that applications are isolated and protected from one another.
- Examples of OS are:
  on Desktop
	  MS Windows
	  UNIX-based (originated from Bell Labs)
		  Mac OS (BSD or Berkeley System Distribution of UNIX)
		  Linux 
  on Embedded
	 Android
	 iOS
	 Symbian
- We'll focus more on Linux.
- OS Elements:
	- Abstractions:
		- process, thread, file, socket, memory pages
	- Mechanisms (operate on abstractions):
		- create, schedule, open, write, allocate
	- Policies (determine how the mechanisms will be used):
		- least-recently used (LRU), earliest deadline first (EDF)
- Memory management example: ![[Pasted image 20240227164124.png]]
- OS Design Principles:
	1. Separation of mechanism and policy
		- implement flexible mechanisms to support policies
		- e.g. LRU, LFU, random
	2. Optimize for the common case
		- Where will the OS be used?
		- What will the user want to execute on that machine?
		- What are the workload requirements?
- OS Protection Boundary:
	- ![[Pasted image 20240227164552.png]]
	- When the privilege bit is not set and an application tries to do something forbidden (that must only be allowed in kernel-mode), trap will occur. The hardware will interrupt the application and the control goes to OS which checks what caused the trap and whether it should allow that operation to execute or not.
	- System calls are a set of interfaces that the applications are allowed to call to perform some kernel-level action.
	- In the image, it should be mmap, not malloc (mmap is a POSIX-compliant Unix system call, malloc is a standard library function).![[Pasted image 20240227164732.png]]
	- System Call Flowchart:![[Pasted image 20240227165438.png]]![[Pasted image 20240227170231.png]]
	- Crossing the OS Boundary: User-kernel transitions are necessary but costly.
	- Because context switches will swap the data/addresses currently in **cache**, the performance of applications can benefit or suffer based on how a context switch changes what is in **cache** at the time they are accessing it.
	- A **cache** would be considered **hot** (fire) if an application is accessing the **cache** when it contains the data/addresses it needs.
	- Likewise, a **cache** would be considered **cold** (ice) if an application is accessing the **cache** when it does not contain the data/addresses it needs -- forcing it to retrieve data/addresses from main memory.![[Pasted image 20240227170403.png]]
- OS Services:
	- process management
	- file management
	- device management
	- memory management
	- storage management
	- security, etc.
	- Windows vs Linux System Calls![[Pasted image 20240227170604.png]]
- On a 64-bit Linux-based OS, some of the following system calls are used.
	- KILL is used to send a signal to a process
	- SETGID is used to set the group identity of a process
	- MOUNT is used to mount a file system
	- SYSCTL is used to read/write system parameters
- Monolithic OS: Historic, large systems, used to contain
	- memory management
	- device drivers
	- file management
	- process/thread
	- scheduling
	- file system for random i/o
	- file system for sequential access
- Advantages of Monolithic OS: everything included, inlining, compile-time optimizations
- Disadvantages of Monolithic OS: customisation, portability, manageability, memory footprint, performance
- Modular OS: Basic services are there but then extra modules can be added as required. This is possible because the OS specifies certain interfaces that the modules must implement to become part of OS. More popular today.
- Advantages of Modular OS: maintainability, smaller footprint, less resource needs
- Disadvantages of Modular OS: indirection, can impact performance, maintenance can still be an issue
- Microkernel: Require only the most basic primitives at the OS level. Everything else like DB, FS, disk driver etc. which is usually a part of OS, can run at the user level or unprivileged level. Since these processes will require to access OS, IPC (inter-process communications) are also a part of these microkernels.
- Advantages of Microkernel: size, verifiability
- Disadvantages of Microkernel: portability, complexity of software development, cost of user/kernel crossing
- Linux Architecture: ![[Pasted image 20240227172745.png]]Linux Kernel Architecture: Modular![[Pasted image 20240227172840.png]]
- Mac OS X Architecture: Mach is microkernel.![[Pasted image 20240227173011.png]]
## P2L1
- Simply, a process is an instance of an executing program. It is also called a task or a job.
- A process:
	- has state of execution
		- program counter, stack
	- requires parts and temporary holding area
		- data, register state occupies state in memory
	- may require special hardware
		- I/O devices
- OS manages hardware on behalf of applications.
- An application is a program on disk or flash memory. It is a *static entity*.
- A process is the state of a program when it is executing (when it is loaded in memory). It is an *active entity*.
- We can have multiple instances (or processes) of the same application.
- A process encapsulates all the data needed to run an instance of that application.
- Every single element of a process has to be uniquely identified by its address.
- An OS abstraction used to encapsulate all of the process state is an address space.
- An address space is a range of memory address that doesn't directly map to the physical memory address. It might also not be contiguous.
- Type of state in a process:![[Pasted image 20240228152033.png]]
- Address space is an "in memory" representation of a process. It is called virtual address because they directly represent the physical memory.
- OS maintains page tables which are mapping of virtual to physical addresses.
- 
Kernel - the heart of an operating system. 

The kernel provides the basis for programs, the tools for programs to work with hardware (interact with memory, disk space, CPU) but in an indirect way. It does so via **system calls**.
* The kernel isolates hardware from everything else.

Programs, in turn, run "on top of the kernel" (in the so-called **user space**) and could be categorized as *system* or *application*.
* The kernel isolates programs from each other.

System programs are needed for the system to work (e.g., mount, cp, mkfs).
Application programs are needed to do something useful for the user (e.g., word processor, browser).


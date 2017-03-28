# 1. Introduction to the Linux Kernel

### Handful of characteristics of Unix that are at the core of its strength.
> 1. **Unix is simple:**
>     * Whereas some operating systems implement thousands of system calls and have 
> unclear design goals, Unix systems implement only hundreds of system calls and 
> have a straightforward, even basic, design. 
> 2. **In Unix, everything is a file:**
>     * This simplifies the manipulation of data and devices into a set of core 
>     system calls: _open(), read(), write(), lseek(), and close()_.
> 3. **The Unix kernel and related system utilities are written in C:**
>     * A property that gives Unix its amazing portability to diverse hardware 
>     architectures and accessibility to a wide range of developers. 
> 4. **Unix has fast process creation time and the unique fork() system call.** 
> 5. **Unix provides simple yet robust IPC primitives** 
>     * This, when coupled with the fast process creation time, enable the 
>     creation of simple programs that _do one thing and do it well_.These 
>     single-purpose programs can be strung together to accomplish tasks of 
>     increasing complexity. 
> 
> Unix systems thus exhibit clean layering, with a strong separation between policy
> and mechanism.

## Application <-> Kernel <-> Hardware
> **Applications running on the system communicate with the kernel via system calls:** 
>  * When an application executes a system call, we say that the *kernel is
>   executing on behalf of the application.* Furthermore, the application is said 
>   to be *executing a system call in kernel-space*, and the *kernel is running in 
>   process context.* This relationship that applications call into the kernel via 
>   the system call interface is the fundamental manner in which applications 
>   get work done.
>
> **When hardware wants to communicate with the system, it issues an interrupt 
> that literally interrupts the processor, which in turn interrupts the kernel:**
> * A number identifies interrupts and the kernel uses
>   this number to execute a specific interrupt handler to process and respond 
>   to the interrupt. For example, as you type, the keyboard controller issues 
>   an interrupt to let the system know that there is new data in the keyboard 
>   buffer.The kernel notes the interrupt number of the incoming interrupt and 
>   executes the correct interrupt handler.The interrupt handler processes the 
>   keyboard data and lets the keyboard controller know it is ready for more 
>   data.To provide synchronization, the kernel can disable interrupts—either 
>   all interrupts or just one specific interrupt number. In many operating 
>   systems, including Linux, the interrupt handlers do not run in a process 
>   context. Instead, they run in a special interrupt context that is not 
>   associated with any process.This special context exists solely to let an 
>   interrupt handler quickly respond to an interrupt, and then exit.

## Linux vs Unix
Linux | Unix
----- | -----
Linux is modular design | Unix kernel is typically a monolithic static binary.
Linux historically has required an MMU, but special versions can actually run without one. | Unix systems typically require a system with a paged memory-management unit (MMU); this hardware enables the system to enforce memory protection and to provide a unique virtual address space to each process.
Supports the dynamic loading of kernel modules | Can't
Linux kernel is preemptive | Of the other commercial Unix implementations, Solaris and IRIX have preemptive kernels, but most Unix kernels are not preemptive.
Does not differentiate between threads and normal processes | May support different threads and processes
Provides an object-oriented device model with device classes, hot-pluggable events, and a user-space device filesystem (sysfs) | No idea
Linux is free in every sense of the word | Ummm...


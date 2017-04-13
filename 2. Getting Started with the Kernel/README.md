# Obtaining the Kernel Source                                                     

## Where to Install
> The kernel source is typically installed in /usr/src/linux . You should not      
> use this source tree for development because the kernel version against which 
> your C library is compiled is often linked to this tree. Moreover, you should 
> not require root in order to make changes to the kernel—instead, work out of  
> your home directory and use root only to install new kernels. Even when       
> installing a new kernel, /usr/src/linux should remain untouched.                 
                                                                                   
### Using patches                                                                  
> Instead of downloading each large tarball of the kernel source, you can simply   
> apply an incremental patch to go from one version to the next.This saves      
> everyone bandwidth and you time. To apply an incremental patch, from inside      
> your kernel source tree, simply run:                                          
```                                                                                
$ patch –p1 < ../patch-x.y.z  
```
## Directories in the Root of the Kernel Source Tree

Directory | Description
---------- | ----------
arch | Architecture-specific source
block | Block I/O layer
crypto | Crypto API
Documentation | Kernel source documentation
drivers | Device drivers
firmware | Device firmware needed to use certain drivers
fs | The VFS and the individual filesystems
include | Kernel headers
init | Kernel boot and initialization
ipc | Interprocess communication code
kernel | Core subsystems, such as the scheduler
lib | Helper routines
mm | Memory management subsystem and the VM
net | Networking subsystem
samples | Sample, demonstrative code
scripts | Scripts used to build the kernel
security | Linux Security Module
sound | Sound subsystem
usr | Early user-space code (called initramfs)
tools | Tools helpful for developing Linux
virt | Virtualization infrastructure

> The Linux Kernel Source Tree can be found in /linux directory

## Linux Kernel is different than other user space programs by:
* The kernel has access to neither the C library nor the standard C headers.
> But you can use the needed libraries implemented within the Kernel. They can
be found at /linux/include/
> e.g #include <linux/string.h>
* The kernel is coded in GNU C.
    > Kernel does not use strict ANSI C but instead uses ISO C99 and GNU C
    > extensions, which can only be compiled by gcc and Intel C compiler as these
    > are the only two that have enough extensions to ANSI C that Kernel uses for
    > compilation.

    Some difference between ANSI C and GNU C are:
    
    * Inline Function, e.g `static inline void bark(unsigned long dog)`
    
    * Inline Assembly, e.g
    ```
    unsigned int low, high;
    asm volatile("rdtsc" : "=a" (low), "=d" (high));
    /* low and high now contain the lower and upper 32-bits of the 64-bit tsc */
    ```
    
    * Branch Annotation
    ```
    /* we predict 'error' is nearly always zero ... */
    if (unlikely(error)) {
    /* ... */
    }
    ```
* The kernel lacks the memory protection afforded to user-space.
> Memory violations in the kernel result in an oops, which is a major kernel
> error. Additionally, kernel memory is not pageable.Therefore, every byte of
> memory you consume is one less byte of available physical memory. Keep that
> in mind the next time you need to add one more feature to the kernel!
* The kernel cannot easily execute floating-point operations.
> What the kernel has to do when using floating point instructions varies by
> architecture, but the kernel normally catches a trap and then initiates the
> transition from integer to floating point mode. Unlike user-space, the kernel
> does not have the luxury of seamless support for floating point because it
> cannot easily trap itself. Using a floating point inside the kernel requires
> manually saving and restoring the floating point registers, among other
> possible chores.
* The kernel has a small per-process fixed-size stack.
> The kernel stack is neither large nor dynamic; it is small and fixed in
> size.The exact size of the kernel’s stack varies by architecture. On x86, the
> stack size is configurable at compile-time and can be either 4KB or 8KB.
> Historically, the kernel stack is two pages, which generally implies that it
> is 8KB on 32-bit architectures and 16KB on 64-bit architectures—this size is
> fixed and absolute.
* Because the kernel has asynchronous interrupts, is preemptive, and supports SMP, 
synchronization and concurrency are major concerns within the kernel.
> Linux is a preemptive multitasking operating system
> Linux supports symmetrical multiprocessing (SMP).
* Portability is important.
> architecture-independent C code must correctly compile and run on a wide range of systems, and that architecture-dependent code must be properly segregated in system-specific directories in the kernel source tree.



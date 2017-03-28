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



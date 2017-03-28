# 1. Introduction to the Linux Kernel

### Handful of characteristics of Unix that are at the core of its strength.
1. **Unix is simple:**
    * Whereas some operating systems implement thousands of system calls and have 
unclear design goals, Unix systems implement only hundreds of system calls and 
have a straightforward, even basic, design. 
2. **In Unix, everything is a file:**
    * This simplifies the manipulation of data and devices into a set of core 
    system calls: _open(), read(), write(), lseek(), and close()_.
3. **The Unix kernel and related system utilities are written in C:**
    * A property that gives Unix its amazing portability to diverse hardware 
    architectures and accessibility to a wide range of developers. 
4. **Unix has fast process creation time and the unique fork() system call.** 
5. **Unix provides simple yet robust IPC primitives** 
    * This, when coupled with the fast process creation time, enable the 
    creation of simple programs that _do one thing and do it well_.These 
    single-purpose programs can be strung together to accomplish tasks of 
    increasing complexity. 

> Unix systems thus exhibit clean layering, with a strong separation between policy
> and mechanism.

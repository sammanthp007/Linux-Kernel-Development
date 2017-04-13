# Process Management

## Process
A process is a program (object code stored on some media) in the midst of
execution. Processes are, however, more than just the executing program code
(often called the text section in Unix).They also include a set of resources
such as open files and pending signals, internal kernel data, processor state,
a memory address space with one or more memory mappings, one or more threads of
execution, and a data section containing global variables.

## Thread
A process is a program (object code stored on some media) in the midst of
execution. Processes are, however, more than just the executing program code
(often called the text section in Unix).They also include a set of resources
such as open files and pending signals, internal kernel data, processor state,
a memory address space with one or more memory mappings, one or more threads of
execution, and a data section containing global variables.

> Linux has a unique implementation of threads: It does not differentiate
> between threads and processes.To Linux, a thread is just a special kind of
> process.

## Feature
On modern operating systems, processes provide two virtualizations:
* **Virtualized processor**: The virtual processor gives the process the
  illusion that it alone monopolizes the system, despite possibly sharing the
  processor among hundreds of other processes. 
* **Virtual memory**: lets the process allocate and manage memory as if it
  alone owned all the memory in the system.


## Lifecycle
A process begins its life using fork() system call, which creates a new process
by duplicating an existing one. The process that calls fork() is the parent,
whereas the new process is the child.The parent resumes execution and the child
starts execution at the same place: where the call to fork() returns.The fork()
system call returns from the kernel twice: once in the parnent process and
again in the newborn child. 

Often, immediately after a fork it is desirable to execute a new, different
program.The exec() family of function calls creates a new address space and
loads a new program into it. In contemporary Linux kernels, fork() is actually
implemented via the clone() system call 

A program exits via the exit() system call.This function terminates the process
and frees all its resources.

A parent process can inquire about the status of a terminated child via the
wait4() 1 system call, which enables a process to wait for the termination of a
specific process.When a process exits, it is placed into a special zombie state
that represents terminated processes until the parent calls wait() or
waitpid(). 



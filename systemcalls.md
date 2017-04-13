`fork()`: A process begins its life using fork() system call, which creates a new process
by duplicating an existing one. The process that calls fork() is the parent,
whereas the new process is the child.The parent resumes execution and the child
starts execution at the same place: where the call to fork() returns.The fork()
system call returns from the kernel twice: once in the parnent process and
again in the newborn child. 

`exec()`: Often, immediately after a fork it is desirable to execute a new,
different program.The exec() family of function calls creates a new address
space and loads a new program into it. 
 

`clone()`: In contemporary Linux kernels, fork() is actually implemented via
the `clone()` system call

`exit()`: A program exits via the exit() system call.This function terminates the process
and frees all its resources.

`wait4()`: A parent process can inquire about the status of a terminated child
via the wait4() 1 system call, which enables a process to wait for the
termination of a specific process.When a process exits, it is placed into a
special zombie state that represents terminated processes until the parent calls wait() or
waitpid() . 

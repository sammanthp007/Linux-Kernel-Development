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


## Process Descriptor and the Task Structure
The kernel stores the list of processes in a circular doubly linked list called
the **task list**. Each element in the task list is a process descriptor of the
type `struct task_struct` , which is defined in <linux/sched.h> .The process
descriptor contains all the information about a specific process.

### Allocating the Process Descriptor
The `task_struct` structure is allocated via the *slab allocator* to provide
object reuse and cache coloring (see Chapter 12).

With the process descriptor dynamically created via the slab allocator, a new
structure, `struct thread_info` , is created that lives at the bottom of the
stack (for stacks that grow down) and at the top of the stack (for stacks that
grow up).

> `thread_info` is defined in `<asm/thread_info.h>`

### Storing the Process Descriptor
The system identifies processes by a unique process identification value or PID.

> Because of backward compatibility with earlier Unix and Linux versions,
> however, the default maximum value is only 32,768 (that of a short int ),
> although the value optionally can be increased as high as four million (this
> is controlled in <linux/threads.h> . 

Inside the kernel, tasks are typically referenced directly by a pointer to
their `task_struct` structure. In fact, most kernel code that deals with
processes works directly with `struct task_struct` . Consequently, it is useful
to be able to quickly look up the process descriptor of the currently executing
task, which is done via the `current` macro. 

### Process State
The state field of the process descriptor describes the current condition of
the process (see Figure 3.3). Each process on the system is in exactly one of
five different states.This value is represented by one of five flags: 
* `TASK_RUNNING`
The process is runnable; it is either currently running or on a run-queue 
waiting to run (runqueues are discussed in Chapter 4).This is the only possible
state for a process executing in user-space; it can also apply to a process in
kernel-space that is actively running.
* TASK_INTERRUPTIBLE`
The process is sleeping (that is, it is blocked), waiting for some condition to
exist .When this condition exists, the kernel sets the process’s state to
TASK_RUNNING .The process also awakes prematurely and becomes runnable if it
receives a signal.
* `TASK_UNINTERRUPTIBLE`
This state is identical to TASK_INTERRUPTIBLE except that it does not wake up
and become runnable if it receives a signal.This is used in situations where
the process must wait without interruption or when the event is expected to
occur quite quickly. Because the task does not respond to signals in this
state, TASK_UNINTERRUPTIBLE is less often used than TASK_INTERRUPTIBLE .
* `__TASK_TRACED`
The process is being traced by another process, such as a debugger, via ptrace.
* `__TASK_STOPPED`
Process execution has stopped; the task is not running nor is it eligible to
run.This occurs if the task receives the `SIGSTOP` , `SIGTSTP` , `SIGTTIN` , or
`SIGTTOU` signal or if it receives any signal while it is being debugged.

### Manipulating the Current Process State

```
set_task_state(task, state);
/* set task ‘task’ to state ‘state’ */
```


